# Джерела та першоджерела

Реєстр офіційних інженерних і наукових джерел курсу «Децентралізовані системи».  
У лекціях посилайтесь на джерела за номером виноски: `[1]`, `[2]` тощо.

> Короткий список для самостійного читання: [recommended_literature.md](./recommended_literature.md).  
> Декларація доброчесності: [DISCLAIMER.md](./DISCLAIMER.md).

---

## Фундаментальні основи

| № | Джерело | Теми курсу |
|:-:|---------|------------|
| [1] | [Bitcoin: A Peer-to-Peer Electronic Cash System](https://bitcoin.org/bitcoin.pdf) — Satoshi Nakamoto, 2008 | UTXO, PoW, Merkle tree, подвійна витрата |
| [2] | [Ethereum Yellow Paper](https://ethereum.github.io/yellowpaper/paper.pdf) — Gavin Wood | EVM, газ, state trie, акаунтна модель |
| [3] | [Brewer's Conjecture and the Feasibility of Consistent, Available, Partition-Tolerant Web Services](https://users.ece.cmu.edu/~adrian/731-sp04/readings/GL-cap.pdf) — Gilbert & Lynch, 2002 | CAP-теорема, компроміси CP/AP |
| [4] | [Practical Byzantine Fault Tolerance](https://pmg.csail.mit.edu/papers/osdi99.pdf) — Castro & Liskov, 1999 | pBFT, BFT-консенсус |
| [5] | [In Search of an Understandable Consensus Algorithm (Raft)](https://raft.github.io/raft.pdf) — Ongaro & Ousterhout, 2014 | Raft, CFT, лідерство |

---

## Протоколи та стандарти Bitcoin

| № | Джерело | Теми курсу |
|:-:|---------|------------|
| [6] | [Bitcoin Developer Guide — Transactions](https://developer.bitcoin.org/devguide/transactions.html) | UTXO, Script, життєвий цикл tx |
| [7] | [BIP-32: Hierarchical Deterministic Wallets](https://github.com/bitcoin/bips/blob/master/bip-0032.mediawiki) | HD-гаманці, адресація |
| [8] | [BIP-141: Segregated Witness](https://github.com/bitcoin/bips/blob/master/bip-0141.mediawiki) | Масштабування Bitcoin, witness |

---

## Ethereum, EVM та оновлення протоколу

| № | Джерело | Теми курсу |
|:-:|---------|------------|
| [9] | [Ethereum.org — Developers Documentation](https://ethereum.org/developers/docs/) | Ноди, RPC, транзакції, мережі |
| [10] | [Solidity Documentation](https://docs.soliditylang.org/) | Синтаксис, безпека, opcodes |
| [11] | [EIP-1559: Fee market change](https://eips.ethereum.org/EIPS/eip-1559) | Base fee, пріоритетна комісія |
| [12] | [EIP-6780: SELFDESTRUCT only in same transaction](https://eips.ethereum.org/EIPS/eip-6780) | selfdestruct, Cancun |
| [13] | [EIP-6110: Supply validator deposits on Execution layer](https://eips.ethereum.org/EIPS/eip-6110) | Case study Pectra |

---

## Токени та смарт-контракти (ERC/EIP)

| № | Джерело | Теми курсу |
|:-:|---------|------------|
| [14] | [EIP-20: ERC-20 Token Standard](https://eips.ethereum.org/EIPS/eip-20) | Взаємозамінні токени, approve |
| [15] | [EIP-721: ERC-721 Non-Fungible Token Standard](https://eips.ethereum.org/EIPS/eip-721) | NFT, tokenId, metadata |
| [16] | [EIP-1155: Multi Token Standard](https://eips.ethereum.org/EIPS/eip-1155) | GameFi, batch transfers |
| [17] | [EIP-1167: Minimal Proxy Contract](https://eips.ethereum.org/EIPS/eip-1167) | Proxy-патерн, clone |
| [18] | [EIP-1967: Proxy Storage Slots](https://eips.ethereum.org/EIPS/eip-1967) | Upgradeable contracts |
| [19] | [EIP-2612: Permit](https://eips.ethereum.org/EIPS/eip-2612) | Off-chain approve, безпека DeFi |
| [20] | [OpenZeppelin Contracts](https://docs.openzeppelin.com/contracts/) | Ownable, ReentrancyGuard, стандарти |

---

## Масштабування та L2

| № | Джерело | Теми курсу |
|:-:|---------|------------|
| [21] | [Ethereum.org — Layer 2 Rollups](https://ethereum.org/developers/docs/scaling/#rollups) | Optimistic / ZK rollups |
| [22] | [Optimistic Rollups Explainer](https://ethereum.org/developers/docs/scaling/optimistic-rollups/) | Fraud proofs, challenge period |
| [23] | [ZK-Rollups Explainer](https://ethereum.org/developers/docs/scaling/zk-rollups/) | ZK proofs, фінальність |

---

## Інструменти розробки

| № | Джерело | Теми курсу |
|:-:|---------|------------|
| [24] | [Foundry Book](https://book.getfoundry.sh) | forge, cast, anvil, fuzz, fork |
| [25] | [Remix IDE Documentation](https://remix-ide.readthedocs.io/) | Практикум p00 |
| [26] | [Ethers.js Documentation](https://docs.ethers.org/) | Provider, Signer, dApp-інтеграція |
| [27] | [Web3.py Documentation](https://web3py.readthedocs.io/) | RPC-скрипти (завдання 1.1) |

---

## DeFi та безпека

| № | Джерело | Теми курсу |
|:-:|---------|------------|
| [28] | [Uniswap V2 Whitepaper](https://uniswap.org/whitepaper.pdf) | AMM, constant product |
| [29] | [Consensys: Smart Contract Best Practices](https://consensys.github.io/smart-contract-best-practices/) | CEI, reentrancy, patterns |
| [30] | [SWC Registry (Smart Contract Weakness Classification)](https://swcregistry.io/) | Класифікація вразливостей |
| [31] | [Ethereum.org — Consensus Mechanisms](https://ethereum.org/developers/docs/consensus-mechanisms/) | PoS, validators, finality |

---

## Як користуватися реєстром

1. У власних роботах посилайтесь на номер виноски та URL (наприклад: «за [1]» або «EIP-20 [14]»).
2. Не цитуйте великі фрагменти PDF — наводьте власне формулювання з посиланням.
3. Якщо джерело оновилось після дати лекції — перевіряйте актуальну версію на офіційному сайті.
