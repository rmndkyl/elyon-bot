# Elyon-Bot

Automation for the **Elyon Chain incentivised testnet** (Season 1) quest platform.

Connects a self-custody EVM wallet to `airdrop.elyon.network`, completes the on-chain quests,
and keeps the daily streak alive — no browser extension, no manual clicking.

## What it does

- **Sign-in** with an EIP-191 signature (SIWE-style message), session cookie cached per wallet
- **Faucet** claim once per campaign day
- **Transfers** 1+ ELN per day to prove the wallet can move funds
- **Badge mint** and **validator delegation** (10 ELN) as one-time quests
- Reads the quest ledger, points and rank back from the platform
- Multi-wallet config with per-wallet state

## Stack

Python 3.10+ · `eth-account` for local transaction signing · plain JSON-RPC ·
no web3.py, no Chrome, no paid captcha service.

## Design notes

- **Zero capital**: everything runs on testnet ELN from the site's own faucet.
- **Local keys**: private keys never leave `config.json`; transactions are signed locally.
- **Fleet-safe**: each wallet gets a stable device identity and its own humanised pacing so
  the fleet does not look like one script. Actions are jittered, daily caps are not always
  maxed, and wallets are staggered.
- **Idempotent**: already-claimed / already-minted / already-delegated states are detected
  before spending gas.

## Interface

Interactive Indonesian menu (`JALANKAN.bat`) plus a CLI:

```
python src/run.py --status     # points, tasks, referral
python src/run.py --daily      # claim + send
python src/run.py --onboard    # mint + delegate
python src/run.py --dry-run    # plan only, no transactions
```

## Status

Built and verified live on the Elyon testnet — daily loop confirmed crediting points from
on-chain actions. Maintenance repo: private.

---

Part of the **LYID** (Layer Airdrop ID) testnet automation collection.
Not affiliated with Elyon. Testnet only, no monetary value.
