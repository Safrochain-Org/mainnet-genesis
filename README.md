<div align="center">

# Safrochain Mainnet — Launch Genesis

**The canonical `genesis.json` for `safrochain-1`**

[![Chain ID](https://img.shields.io/badge/chain--id-safrochain--1-1f6feb?style=for-the-badge)](#chain-parameters)
[![Denom](https://img.shields.io/badge/denom-usaf-8957e5?style=for-the-badge)](#chain-parameters)
[![Supply](https://img.shields.io/badge/supply-1%2C000%2C000%2C000_SAF-2da44e?style=for-the-badge)](#tokenomics)
[![Validators](https://img.shields.io/badge/genesis_validators-4-fb8500?style=for-the-badge)](#genesis-validators)
[![Status](https://img.shields.io/badge/status-launch--ready-2da44e?style=for-the-badge)](#status)

</div>

---

## Status

> ✅ **LAUNCH READY** — Genesis is final and deployed to all foundation nodes. Chain wakes at **2026-06-25 10:00:00 UTC**.

| | |
| --- | --- |
| **File** | [`genesis.json`](./genesis.json) |
| **Size** | 27,596 bytes (≈ 27 KB) |
| **SHA-256** | `c05ac5aec1918df9edb257e8e0eea184d73edc51370eb4aa9f0b4f0aad615c4d` |
| **Genesis time** | `2026-06-25T10:00:00Z` |
| **Initial height** | `1` |
| **Binary** | `safrochaind v0.2.2` (Cosmos SDK 0.50.14, CometBFT 0.38.21, CosmWasm 0.51) |

---

## Chain Parameters

| Parameter | Value |
| :--- | :--- |
| **Chain ID** | `safrochain-1` |
| **Base denom** | `usaf` (1 SAF = 1 000 000 usaf) |
| **Bond denom** | `usaf` |
| **Consensus** | CometBFT, ed25519 validator keys |
| **Max validators** | 100 |
| **Min commission rate** | 5 % |
| **Unbonding period** | 14 days (`1209600s`) |
| **Voting period** | 7 days (`604800s`) — expedited 1 day (`86400s`) |
| **Min gov deposit** | 5 000 SAF · expedited 10 000 SAF |
| **Gov quorum / threshold / veto** | 33.4 % / 50 % / 33.4 % |
| **Min gas price** | `0.05 usaf` (globalfee) |
| **Inflation** | min 3 % · max 12 % · target bonded 55 % |
| **Slash — downtime** | 0.01 % · jail 10 min · window 10 000 blocks @ 50 % |
| **Slash — double-sign** | 5 % |
| **Evidence max age** | 14 days / 241 920 blocks |
| **Max block bytes** | 22 020 096 |
| **Max block gas** | 100 000 000 |
| **CosmWasm code upload** | Permissionless (`Everybody`) |
| **Feeshare (dev rev-share)** | 25 % of contract-tx fees to registered contract dev |
| **Tokenfactory denom creation fee** | 100 SAF |

### IBC stack (full)

`ibc-core`, `ibc-transfer` (ICS-20 send + receive), `interchain-accounts` host + controller, `interchain-query`, `feeibc` (ICS-29), `packet-forward-middleware`, `ibchooks` (Wasm via IBC). Light clients: `07-tendermint`, `06-solomachine`.

---

## Tokenomics

**Total supply: 1 000 000 000 SAF**

| Allocation | Amount (SAF) | % | Notes |
| :--- | ---: | ---: | :--- |
| **DAO Reserve** | 199 776 000 | 19.98 % | Governance-controlled treasury. 200M nominal less 224k pre-seeded into the 4 active validator + 2 cosigner-backup wallets. |
| **Community** | 150 000 000 | 15.00 % | Airdrops, missions, community rewards |
| **Ecosystem Dev** | 150 000 000 | 15.00 % | Grants & dApp programs (external developer pool) |
| **Liquidity** | 100 000 000 | 10.00 % | DEX liquidity & market making |
| **Treasury** | 100 000 000 | 10.00 % | Foundation operating treasury |
| **Public Sale** | 100 000 000 | 10.00 % | Sale participants |
| **Partners** | 50 000 000 | 5.00 % | Strategic partnerships |
| **Team (vesting)** | 140 000 000 | 14.00 % | 15 vesting accounts — see below |
| **Dev Reserves** | 10 000 000 | 1.00 % | Liquid dedicated wallet for grants/bounties/audits |
| **Active validator wallets** | 124 000 | 0.012 % | Ubuntu 51k + Kilimanjaro 51k + HusoNode 11k + Winnode 11k |
| **SF cosigner backups** | 100 000 | 0.010 % | 2 × 50k for Horcrux operations |
| **— Total** | **1 000 000 000** | **100 %** | |

---

## Genesis Validators

The active validator set at block 1 consists of **2 Safrochain Foundation validators + 2 community validators**, all 4 gentxs baked into `app_state.genutil.gen_txs`.

| # | Moniker | Class | Self-stake | Commission | Operator (valoper) |
| :-- | :--- | :--- | ---: | ---: | :--- |
| 1 | **Ubuntu** | Foundation | 50 000 SAF | 8 % | `addr_safrovaloper1udj3fxkjpdf6zwa9sg5x89tg2k4cgels6pu2zt` |
| 2 | **Kilimanjaro** | Foundation | 50 000 SAF | 8 % | `addr_safrovaloper1aqwk6uaw0q3xfd306fc6uuslumjdalm0x3g9tc` |
| 3 | **HusoNode** | Community | 10 000 SAF | 10 % | `addr_safrovaloper1y5axpuvmns5ksl7tv8j933gtg3trr0slnlclxx` |
| 4 | **Winnode** | Community | 10 000 SAF | 10 % | `addr_safrovaloper1jz4fmzlc9lskmxum02elvml6jms03wa77d06vk` |
| | **Total bonded at h=1** | | **120 000 SAF** | | |

Foundation validator consensus pubkeys are the **production** ed25519 keys held by 3-cosigner Horcrux clusters (2-of-3 threshold per validator). All 4 standalone signed gentxs are committed alongside this README (`gentx-fixed-*.json`).

### Community validators joining post-launch

Any community validator can join via `MsgCreateValidator` once the chain is live. Standard flow: install `safrochaind v0.2.2`, sync to tip, create a key, fund it, then submit `safrochaind tx staking create-validator …`.

---

## Verification

Reproduce the checksum and validate the file with the official binary:

```bash
# 1. Download
curl -fsSL -o genesis.json \
  https://raw.githubusercontent.com/Safrochain-Org/draft-genesis/main/genesis.json

# 2. Verify integrity
shasum -a 256 genesis.json
# Expected: c05ac5aec1918df9edb257e8e0eea184d73edc51370eb4aa9f0b4f0aad615c4d

# 3. Validate against safrochaind
mkdir -p ~/.safrochain/config
cp genesis.json ~/.safrochain/config/genesis.json
safrochaind genesis validate --home ~/.safrochain
# Expected: "File at ... is a valid genesis file"
```

Inspect the 4 bundled gentxs:

```bash
jq '.app_state.genutil.gen_txs
    | map(.body.messages[0]
          | {moniker: .description.moniker,
             valoper: .validator_address,
             self_stake_usaf: .value.amount,
             commission: .commission.rate})' genesis.json
```

Confirm supply integrity:

```bash
# Total supply (must equal 1e15 usaf = 1B SAF)
jq -r '.app_state.bank.supply[] | "\(.denom): \(.amount)"' genesis.json

# Sum of balances (must equal supply)
jq '[.app_state.bank.balances[].coins[]
     | select(.denom == "usaf") | .amount | tonumber] | add' genesis.json
```

---

## Joining the network

If you want to run a node (validator or RPC), see the operator guide:

```bash
# 1. Install safrochaind v0.2.2
git clone --depth 1 --branch v0.2.2 https://github.com/Safrochain-Org/safrochain-node ~/safrochain-node
cd ~/safrochain-node && make install

# 2. Initialize a fresh home
safrochaind init <your-moniker> --chain-id safrochain-1

# 3. Drop in this genesis
curl -fsSL -o ~/.safrochain/config/genesis.json \
  https://raw.githubusercontent.com/Safrochain-Org/draft-genesis/main/genesis.json
shasum -a 256 ~/.safrochain/config/genesis.json
# Confirm SHA matches: c05ac5aec1918df9edb257e8e0eea184d73edc51370eb4aa9f0b4f0aad615c4d

# 4. Configure seeds + persistent_peers in ~/.safrochain/config/config.toml
#    seeds = "bc772fdc9749e6dfd200a9428f07d86fe4fd34ec@seed.safrochain.network:26666,d323d296ba55e89fb6ce1a724f8da1740bd8cbb0@seed2.safrochain.network:26670"
#    persistent_peers = "131aeac8bd7fe9b678cdaa9cc3fe2d7af3ded1fe@rpc1.safrochain.network:26676,5cd69b65c08c78937b9cdf17617caaa1aa33672e@rpc2.safrochain.network:36656"
#    minimum-gas-prices = "0.05usaf"   in ~/.safrochain/config/app.toml

# 5. Start at or before 2026-06-25 10:00 UTC
safrochaind start
# The daemon will log "Genesis time is in the future. Sleeping until then..."
# and automatically commit block 1 at exactly 10:00:00 UTC.
```

Public RPC/API/gRPC endpoints (all `*.safrochain.network`): `rpc1`, `rpc2`, `api1`, `api2`, `grpc1`, `grpc2`, `grpc-web`. Load-balanced aliases: `rpc.safrochain.network`, `api.safrochain.network`, `grpc.safrochain.network`. These start serving mainnet once the chain commits block 1.

---

## Files in this folder

| File | Purpose |
| :--- | :--- |
| [`genesis.json`](./genesis.json) | The mainnet genesis (file to publish) |
| [`gentx-fixed-safro-validator-1.json`](./gentx-fixed-safro-validator-1.json) | **Ubuntu** signed gentx |
| [`gentx-fixed-safro-validator-2.json`](./gentx-fixed-safro-validator-2.json) | **Kilimanjaro** signed gentx |
| [`gentx-fixed-HusoNode.json`](./gentx-fixed-HusoNode.json) | HusoNode signed gentx |
| [`gentx-fixed-Winnode.json`](./gentx-fixed-Winnode.json) | Winnode signed gentx |
| [`_consensus_pubkeys.json`](./_consensus_pubkeys.json) | Foundation validators' public consensus keys (Horcrux-protected) |
| `README.md` | This file |

Not published (local-only / git-ignored):

| Path | Why it's private |
| :--- | :--- |
| `preprod-keys/` | SF validator **operator** mnemonics (separate from Horcrux-held consensus keys) |
| `team-mnemonic.secret` | Team root mnemonic |
| `operator-messages/` | Internal per-validator handover notes |
| `_archive/` | Historical preprod artifacts (kept for reference, not part of mainnet) |

---

## Resources

| | |
| :--- | :--- |
| 🌐 Website  | [safrochain.com](https://safrochain.com) |
| 📦 Node binary | [`safrochaind` v0.2.2](https://github.com/Safrochain-Org/safrochain-node/releases/tag/v0.2.2) |
| 📚 Docs | [docs.safrochain.com](https://docs.safrochain.com) |
| 📝 Issues | [Safrochain-Org/safrochain-node/issues](https://github.com/Safrochain-Org/safrochain-node/issues) |

---

<div align="center">

**Safrochain — Sovereign infrastructure for African on-chain finance**

🌅 Launch: **2026-06-25 10:00 UTC**

</div>
