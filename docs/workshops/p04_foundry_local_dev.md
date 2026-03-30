# Практикум p04. Foundry: локальне середовище розробки

**Мета:** Перейти від браузерного Remix IDE до професійного локального інструментарію. Навчитися створювати проєкт у Foundry, компілювати контракти, писати тести на Solidity, деплоїти через скрипти та працювати з форком реальної мережі.

**Передумови:** Базове розуміння Solidity (практикуми p00–p01), термінал (командний рядок), встановлений [Git](https://git-scm.com/).

---

## Чому Foundry, а не Remix?

| Критерій | Remix IDE | Foundry |
| :--- | :--- | :--- |
| **Середовище** | Браузер, нічого встановлювати | Локальне, потребує інсталяції |
| **Тестування** | Ручне "клацання" кнопок | Автоматичні тести на Solidity |
| **Швидкість** | Повільна компіляція великих проєктів | Блискавична (написаний на Rust) |
| **CI/CD** | Неможливо | Легко інтегрується в pipeline |
| **Форк мережі** | Ні | Так (`anvil --fork-url`) |
| **Використання** | Навчання, прототипування | Production, аудити, хакатони |

> [!IMPORTANT]
> Remix — чудовий для перших кроків. Але у реальних проєктах, на хакатонах та при проходженні технічних інтерв'ю очікується знання Foundry або Hardhat.

---

## 1. Встановлення Foundry

Foundry встановлюється через один скрипт `foundryup`:

```bash
# 1. Встановлення foundryup (менеджер версій Foundry)
curl -L https://foundry.paradigm.xyz | bash

# 2. Перезавантажте термінал (або виконайте source ~/.bashrc)
# 3. Встановлення останньої версії інструментів
foundryup
```

Після успішного встановлення у вас з'являться 4 інструменти:

| Інструмент | Призначення |
| :--- | :--- |
| `forge` | Компіляція, тестування, деплой контрактів |
| `cast` | Взаємодія з блокчейном з командного рядка (читання стану, виклик функцій) |
| `anvil` | Локальна EVM-нода (аналог Remix VM, але у терміналі) |
| `chisel` | Інтерактивний REPL для Solidity (виконання коду рядок за рядком) |

**Перевірка:**
```bash
forge --version
# forge 0.2.0 (або новіша)
```

---

## 2. Створення проєкту

```bash
# Створити новий проєкт
forge init my-first-project
cd my-first-project
```

Foundry створить таку структуру:

```
my-first-project/
├── foundry.toml       # Конфігурація проєкту (версія компілятора, оптимізації)
├── src/               # Ваші смарт-контракти (.sol)
│   └── Counter.sol    # Приклад контракту
├── test/              # Тести (теж на Solidity!)
│   └── Counter.t.sol  # Тести для Counter
├── script/            # Скрипти деплою
│   └── Counter.s.sol  # Скрипт деплою Counter
└── lib/               # Залежності (підмодулі Git)
    └── forge-std/     # Стандартна бібліотека Foundry
```

> [!NOTE]
> Зверніть увагу: тести у Foundry пишуться **на Solidity**, а не на JavaScript (як у Hardhat). Це означає, що ви тестуєте контракти тією ж мовою, якою їх написали.

---

## 3. Завдання: Компіляція та запуск тестів

### 3.1. Перегляд прикладу

Відкрийте файл `src/Counter.sol`:

```solidity
// SPDX-License-Identifier: UNLICENSED
pragma solidity ^0.8.13;

contract Counter {
    uint256 public number;

    function setNumber(uint256 newNumber) public {
        number = newNumber;
    }

    function increment() public {
        number++;
    }
}
```

Та відповідний тест `test/Counter.t.sol`:

```solidity
// SPDX-License-Identifier: UNLICENSED
pragma solidity ^0.8.13;

import {Test, console} from "forge-std/Test.sol";
import {Counter} from "../src/Counter.sol";

contract CounterTest is Test {
    Counter public counter;

    // setUp() виконується ПЕРЕД кожним тестом (аналог beforeEach)
    function setUp() public {
        counter = new Counter();
        counter.setNumber(0);
    }

    function test_Increment() public {
        counter.increment();
        assertEq(counter.number(), 1); // Перевірка: number == 1?
    }

    function testFuzz_SetNumber(uint256 x) public {
        counter.setNumber(x);
        assertEq(counter.number(), x); // Fuzz-тест: працює для БУДЬ-ЯКОГО x
    }
}
```

### 3.2. Компіляція

```bash
forge build
```

Якщо все добре, ви побачите:
```
[⠊] Compiling...
[⠊] Compiling 24 files with solc 0.8.28
[⠒] Solc 0.8.28 finished in 1.23s
Compiler run successful!
```

### 3.3. Запуск тестів

```bash
forge test
```

Результат:
```
[⠊] Compiling...
No files changed, compilation skipped

Ran 2 tests for test/Counter.t.sol:CounterTest
[PASS] testFuzz_SetNumber(uint256) (runs: 256, μ: 30803, ~: 31281)
[PASS] test_Increment() (μ: 28379, ~: 28379)
Suite result: ok. 2 passed; 0 failed; 0 skipped; finished in 8.23ms
```

> [!TIP]
> **Fuzz-тестування** (`testFuzz_SetNumber`) — це коли Foundry автоматично генерує 256 випадкових значень для параметра `x` і перевіряє, що контракт працює коректно для кожного з них. У Remix такого зробити неможливо.

---

## 4. Завдання: Написання власного контракту та тестів

### 4.1. Створіть контракт

Створіть файл `src/Greeter.sol`:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.13;

contract Greeter {
    string public greeting;
    address public owner;

    error Unauthorized();
    error EmptyGreeting();

    constructor(string memory _greeting) {
        greeting = _greeting;
        owner = msg.sender;
    }

    function setGreeting(string memory _greeting) public {
        if (msg.sender != owner) revert Unauthorized();
        if (bytes(_greeting).length == 0) revert EmptyGreeting();
        greeting = _greeting;
    }
}
```

### 4.2. Напишіть тести

Створіть файл `test/Greeter.t.sol`:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.13;

import {Test, console} from "forge-std/Test.sol";
import {Greeter} from "../src/Greeter.sol";

contract GreeterTest is Test {
    Greeter public greeter;
    address alice = makeAddr("alice"); // Створення тестової адреси

    function setUp() public {
        greeter = new Greeter("Hello, Foundry!");
    }

    function test_InitialGreeting() public view {
        assertEq(greeter.greeting(), "Hello, Foundry!");
    }

    function test_OwnerCanChange() public {
        greeter.setGreeting("New greeting");
        assertEq(greeter.greeting(), "New greeting");
    }

    function test_RevertIfNotOwner() public {
        // vm.prank — "прикинутися" іншим акаунтом для наступного виклику
        vm.prank(alice);
        vm.expectRevert(Greeter.Unauthorized.selector);
        greeter.setGreeting("Hacked!");
    }

    function test_RevertIfEmpty() public {
        vm.expectRevert(Greeter.EmptyGreeting.selector);
        greeter.setGreeting("");
    }
}
```

### 4.3. Запустіть з деталізацією

```bash
forge test -vvv
```

Прапорець `-vvv` покаже детальний трейс кожного виклику (включно з revert-повідомленнями).

**Ключові "читкоди" Foundry (cheatcodes):**

| Cheatcode | Що робить |
| :--- | :--- |
| `vm.prank(addr)` | Наступний виклик буде від імені `addr` |
| `vm.deal(addr, amount)` | Встановити баланс ETH для `addr` |
| `vm.warp(timestamp)` | "Перемотати" час (block.timestamp) |
| `vm.roll(blockNum)` | "Перемотати" номер блоку |
| `vm.expectRevert()` | Очікувати revert у наступному виклику |
| `makeAddr("name")` | Створити детерміновану тестову адресу |

---

## 5. Локальна нода: Anvil

Anvil — це локальний блокчейн-емулятор (аналог Remix VM, але запущений як окремий процес).

```bash
# Запуск локальної ноди
anvil
```

Ви побачите список з 10 тестових акаунтів (з приватними ключами) та адресу RPC:

```
Available Accounts
==================
(0) 0xf39Fd6e51...  (10000.000000000000000000 ETH)
(1) 0x70997970C...  (10000.000000000000000000 ETH)
...

Listening on 127.0.0.1:8545
```

Тепер ви можете підключити до цієї ноди MetaMask (RPC URL: `http://127.0.0.1:8545`, Chain ID: `31337`) або використовувати `cast`:

```bash
# В іншому терміналі: перевірити баланс першого акаунта
cast balance 0xf39Fd6e51aad88F6F4ce6aB8827279cffFb92266 --rpc-url http://127.0.0.1:8545
```

### Форк реальної мережі

Найпотужніша функція Anvil — можливість створити локальну копію справжньої мережі:

```bash
# Форк Ethereum mainnet (потрібен безкоштовний ключ з alchemy.com або infura.io)
anvil --fork-url https://eth-mainnet.g.alchemy.com/v2/YOUR_API_KEY
```

Тепер ваша локальна нода має повний стан реального Ethereum (всі контракти, баланси, хістори). Ви можете, наприклад, викликати функції реального контракту Uniswap або перевірити баланс USDT відомой адреси — все локально, миттєво та безкоштовно.

---

## 6. Скрипт деплою

Для автоматизації деплою використовуються Solidity-скрипти у папці `script/`.

Створіть файл `script/DeployGreeter.s.sol`:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.13;

import {Script, console} from "forge-std/Script.sol";
import {Greeter} from "../src/Greeter.sol";

contract DeployGreeter is Script {
    function run() public {
        // vm.startBroadcast() починає запис транзакцій для відправки
        vm.startBroadcast();

        Greeter greeter = new Greeter("Hello from Foundry!");
        console.log("Greeter deployed at:", address(greeter));

        vm.stopBroadcast();
    }
}
```

### Деплой у локальну ноду (Anvil)

```bash
# Переконайтесь, що anvil запущений в іншому терміналі
forge script script/DeployGreeter.s.sol --rpc-url http://127.0.0.1:8545 --broadcast --private-key 0xac0974bec39a17e36ba4a6b4d238ff944bacb478cbed5efcae784d7bf4f2ff80
```

> [!WARNING]
> Приватний ключ вище — це стандартний тестовий ключ першого акаунта Anvil. **Ніколи** не використовуйте його для реальних мереж. Для Sepolia/mainnet використовуйте змінні середовища або keystore.

### Деплой у тестнет Sepolia

```bash
# Використовуйте .env файл для зберігання секретів
forge script script/DeployGreeter.s.sol \
  --rpc-url https://eth-sepolia.g.alchemy.com/v2/YOUR_KEY \
  --broadcast \
  --verify \
  --etherscan-api-key YOUR_ETHERSCAN_KEY
```

Прапорець `--verify` автоматично верифікує код контракту на Etherscan.

---

## Питання та відповіді (екзаменаційний блок)

**П1.** Чим `forge test` принципово відрізняється від тестування у Remix?

**В1.** У Remix тестування — це ручний процес: ви натискаєте кнопки, перевіряєте результат очима. `forge test` запускає автоматичні тести, які написані на Solidity. Foundry підтримує fuzz-тестування (автогенерація сотень випадкових вхідних даних), assertion-перевірки та cheatcodes для симуляції складних сценаріїв (зміна часу, підміна відправника).

---

**П2.** Що таке `vm.prank` і навіщо він потрібен у тестах?

**В2.** `vm.prank(address)` — це cheatcode Foundry, який змушує наступний виклик функції виконуватись від імені вказаної адреси. Це дозволяє тестувати контроль доступу: наприклад, перевірити, що функція `onlyOwner` справді відхиляє виклик від стороннього акаунта.

---

**П3.** Для чого потрібен форк мережі (`anvil --fork-url`) і чому це неможливо у Remix?

**В3.** Форк створює локальну копію реальної мережі Ethereum з актуальним станом (балансами, контрактами, ліквідністю DEX). Це дозволяє тестувати інтеграцію вашого контракту з реальними протоколами (наприклад, Uniswap або Aave) без витрат газу. У Remix VM стан порожній — там немає жодних існуючих контрактів чи балансів.

---

## 🎓 Інженерний міні-кейс (на 1 бал)

Ваш колега написав контракт з модифікатором `onlyOwner`. Він стверджує, що перевірив його вручну в Remix: "Я переключив акаунт і спробував викликати — отримав revert. Все працює!"

**Питання:** Назвіть щонайменше 2 сценарії, які неможливо перевірити вручну в Remix, але легко покрити автоматичними тестами у Foundry.
