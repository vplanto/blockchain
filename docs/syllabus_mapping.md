# Відповідність матеріалів курсу робочій програмі (РП)

Відповідність зроблена за офіційною робочою програмою **«Спецкурс №2 (за вибором) Децентралізовані системи»** (ОНУ).  
4 ECTS, 120 год. (20 лекцій, 20 практичних, 80 самостійної роботи). Підсумковий контроль: залік.

Нижче — зв’язок лекцій і практикумів з темами РП.

---

## Змістовий модуль 1 (теми 1–10)

| Тема РП | Назва теми в РП | Матеріали курсу |
|--------|-----------------|-----------------|
| 1 | Базові поняття теорії розподілених систем | [Лекція 0](00_intro_distributed_systems.md), [Лекція 1](01_distributed_systems_theory.md) (CAP, BFT) |
| 2 | Побудова сучасних децентралізованих систем | [Лекція 0](00_intro_distributed_systems.md) (Web2/Web3, піраміда абстракції) |
| 3 | Блокчейн та не-блокчейн технології розподіленого реєстру | [Лекція 1](01_distributed_systems_theory.md), [Лекція 2](02_architecture_bitcoin_utxo.md), [симулятори консенсусу](index.md#інтерактивні-симуляції-simulators) |
| 4 | Децентралізовані алгоритми обробки та узгодження | [Лекція 1](01_distributed_systems_theory.md) (Paxos, Raft, VR, pBFT) |
| 5 | Протоколи консенсусу Proof of Work | [Лекція 4](04_consensus_algorithms.md), [pow.html](consensus/byzantine_algos/pow.html) |
| 6 | Протоколи консенсусу Proof of Stake | [Лекція 4](04_consensus_algorithms.md), [pos.html](consensus/byzantine_algos/pos.html) |
| 7 | Інші протоколи консенсусу | [Лекція 1](01_distributed_systems_theory.md) (pBFT, VR), [Лекція 4](04_consensus_algorithms.md) (коротко про інші) |
| 8 | Внутрішня побудова та архітектура блокчейна Bitcoin | [Лекція 2](02_architecture_bitcoin_utxo.md) (UTXO, Merkle, скрипт) |
| 9 | Внутрішня побудова та архітектура блокчейна Ethereum | [Лекція 3](03_architecture_ethereum_evm.md) (EVM, газ, state trie) |
| 10 | DAGblock та DAGchain системи | [Лекція 6](06_scaling_future.md) (коротко про DAG), масштабування |

---

## Змістовий модуль 2 (теми 11–15)

| Тема РП | Назва теми в РП | Матеріали курсу |
|--------|-----------------|-----------------|
| 11 | Мова Solidity та розробка смарт-контрактів | [Лекція 5](05_smart_contracts_solidity.md), [p00](workshops/p00_remix_solidity_basics.md) (Remix, HelloWorld, Voter) |
| 12 | Приклади та методи побудови dApps | [Лекція 5](05_smart_contracts_solidity.md), [p00](workshops/p00_remix_solidity_basics.md); приклади коду в папці [solidity](https://github.com/vplanto/blockchain/tree/main/solidity) |
| 13 | NFT, невзаємозамінні токени | Планується розширення практикумів (напр. ERC-721) |
| 14 | DeFi, осередки децентралізованих фінансів | [case_studies](case_studies.md), [p01](workshops/p01_security_checks_effects_interactions.md) (безпека) |
| 15 | DAO, децентралізовані автономні організації | [case_studies](case_studies.md) (The DAO), [p01](workshops/p01_security_checks_effects_interactions.md) (reentrancy, CEI) |

---

## Питання для поточного та періодичного контролю (з РП)

У робочій програмі (п. 11) наведено **80 питань** для поточного та періодичного контролю (блокчейн як мережа, генезис-блок, хешування, PoW/PoS, TPS, приватність, форк, DDoS тощо). Ці питання можна використовувати разом із **екзаменаційними блоками** в кінці кожної лекції та практикуму в цій документації.

Розподіл балів за РП: 10 балів за поточний контроль на лекціях (міні-кейси), 10 балів за проходження курсу з блокчейн-фінансів та криптограмотності, та 80 балів за 4 індивідуальні практичні завдання (по 20 балів кожне). Підсумок: 10 + 10 + 80 = 100 балів. Детальний опис у [individual_tasks.md](./individual_tasks.md).
