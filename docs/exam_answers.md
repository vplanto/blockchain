# Ключі до пулу екзаменаційних питань

> **Лише для викладача.** Студентам надається [exam.md](./exam.md) без відповідей.

| № | Джерело відповіді |
|:-:|-------------------|
| 1–4 | `00_intro_distributed_systems.md` — П1–П4 |
| 5–9 | `01_distributed_systems_theory.md` — П1–П5 |
| 10–15 | `01_distributed_systems_theory.md` + доповнення РП (нижче) |
| 16–20 | `02_architecture_bitcoin_utxo.md` — П1–П5 |
| 21 | `02_architecture_bitcoin_utxo.md` — міні-кейс (1 input, 2 outputs: 1 BTC + 3.999 change) |
| 22–24 | РП — розділ нижче |
| 25–31 | `03_architecture_ethereum_evm.md` — П1–П4 + РП |
| 32–39 | `04_consensus_algorithms.md` — П1–П4 + кейси лекції |
| 40–47 | `05_smart_contracts_solidity.md` — П1–П5 + case_studies |
| 48–53 | `05_1_modern_dapps_ecosystem.md` — П1–П4 |
| 54–58 | `case_studies.md` — П1–П4 |
| 59–64 | `06_scaling_future.md` — П1–П6 |
| 65–69 | `07_defi_financial_concepts.md` — П1–П4 |
| 70–73 | `workshops/p00_remix_solidity_basics.md` — П1–П3, міні-кейс |
| 74–76 | `workshops/p01_security_checks_effects_interactions.md` — П1–П3 |
| 77–78 | `workshops/p02_nft_erc721.md` — П1–П3 |
| 79–80 | `workshops/p04_foundry_local_dev.md` — П1–П3 |
| 81–83 | `workshops/p03_solidity_individual_tasks.md` — П1–П3 |
| 84–96 | РП — розділ нижче |

---

## Відповіді на питання РП (№ 10–15, 22–24, 31, 84–96)

**10.** Full nodes зберігають повну копію блокчейну, валідують блоки й транзакції, ретранслюють їх у P2P-мережі.

**11.** Genesis block — перший блок (висота 0), захардкоджений у клієнті; не має попереднього блоку.

**12.** Хеш забезпечує цілісність; ланцюгове посилання робить перепис історії дорогим.

**13.** Mempool — черга непідтверджених tx; до блоку tx може бути замінена — фінальності немає.

**14.** Double-spend вирішується консенсусом PoW: приймається гілка з найбільшою роботою.

**15.** DDoS на блокчейн — спам tx для заповнення block space; fee market обмежує атаку економічно.

**22.** Hard fork — несумісна зміна правил; soft fork — обмеження, сумісне зі старими вузлами.

**23.** ~7 TPS: block size ~1 МБ, block time ~10 хв.

**24.** Difficulty adjustment кожні 2016 блоків підтримує інтервал ~10 хв.

**31.** Nonce — лічильник tx акаунта; запобігає replay.

**84.** Публічний — відкритий доступ; приватний DLT — закритий периметр; консорціум — група організацій.

**85.** P2P: вузли обмінюються блоками; синхронізація через протокол і валідацію правил.

**86.** Censorship resistance: жоден вузол не цензурує валідну tx одноосібно. CEX може заморозити кошти.

**87.** SPV зберігає заголовки + Merkle proofs; не перевіряє повний стан самостійно.

**88.** 51% attack: контроль >50% хешрейту → reorg, double-spend.

**89.** Staking — блокування ETH; validator атестує блоки, slashing за порушення.

**90.** Proxy + delegatecall; старий bytecode залишається в історії.

**91.** On-chain: ownerOf; юридично NFT ≠ авторське право.

**92.** DAO — голосування токенами; on-chain виконання рішень кодом.

**93.** Oracle подає зовнішні дані on-chain; EVM ізольована від інтернету.

**94.** MEV — прибуток від впорядкування tx (арбітраж, front-running).

**95.** Testnet — безцінні токени для тестування.

**96.** Private key → ECDSA → public key → keccak256 → address.
