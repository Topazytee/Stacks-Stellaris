
# Stacks-Stellaris Token Smart Contract

## Overview

The **Stacks-Stellaris Token (STLR)** is a highly secure, feature-rich, and extensible fungible token implementation on the Stacks blockchain using the Clarity smart contract language. This token goes beyond standard token behavior by incorporating governance, security restrictions, minting roles, token locking, and pausing capabilities — making it ideal for regulated or enterprise-grade applications.

---

## Features

✅ **Fungible Token (FT)** compliant
✅ **Governance token integration** with voting power tracking
✅ **Token locking** by block height
✅ **Advanced allowance management** with expiry support
✅ **Contract pausing/unpausing** by owner
✅ **Role-based minting** system
✅ **Blacklist and restriction management**
✅ **Supply cap enforcement** (1 trillion max supply)
✅ **Safe arithmetic operations** with overflow checks
✅ **On-chain event emissions** for mint, burn, and transfer
✅ **Initialization enforcement** for token metadata

---

## Constants

| Name         | Description                            |
| ------------ | -------------------------------------- |
| `MAX-SUPPLY` | 1 trillion (1,000,000,000,000,000)     |
| `PRECISION`  | 6 decimal places (1 token = 10⁶ units) |

---

## Data Variables

| Variable                                       | Description                                       |
| ---------------------------------------------- | ------------------------------------------------- |
| `contract-owner`                               | Current owner of the contract                     |
| `token-name`, `token-symbol`, `token-decimals` | Token metadata                                    |
| `total-supply`                                 | Current circulating supply                        |
| `paused`                                       | Global pause flag                                 |
| `initialized`                                  | Ensures contract initialization only happens once |
| `last-event-id`                                | ID for tracking emitted events                    |

---

## Data Maps

| Map                    | Description                                               |
| ---------------------- | --------------------------------------------------------- |
| `allowances`           | Token allowances with expiration timestamps               |
| `locked-tokens`        | Locks tokens per address until a specific block           |
| `governance-tokens`    | Tracks voting power and last vote block                   |
| `restricted-addresses` | Blacklist for preventing actions from certain addresses   |
| `minter-roles`         | Controls minting rights and quotas for specific addresses |

---

## Key Errors

| Code   | Meaning                   |
| ------ | ------------------------- |
| `u100` | Not authorized            |
| `u101` | Insufficient balance      |
| `u102` | Invalid amount            |
| `u103` | Invalid recipient         |
| `u104` | Invalid spender           |
| `u105` | Overflow error            |
| `u106` | Contract is paused        |
| `u107` | Already initialized       |
| `u108` | Not initialized           |
| `u109` | Blacklisted address       |
| `u110` | Max supply reached        |
| `u111` | Zero address not allowed  |
| `u112` | Self-transfer not allowed |
| `u113` | Expired allowance         |

---

## Core Public Functions

### `initialize(name, symbol, decimals)`

Sets token metadata. Can only be called once by the contract owner.

### `mint(amount, recipient)`

Mints new tokens to a recipient. Restricted to contract owner and respects max supply.

### `transfer(amount, recipient)`

Transfers tokens to another principal. Fails if paused, sender is locked, or recipient is invalid.

### `approve(amount, spender, expiry)`

Grants a time-bound allowance to a spender.

### `set-contract-owner(new-owner)`

Transfers ownership to a new principal.

### `pause()` / `unpause()`

Pauses or unpauses contract-level operations.

---

## Read-Only Functions

* `get-name()` – Returns token name
* `get-symbol()` – Returns token symbol
* `get-decimals()` – Returns token decimal precision
* `get-total-supply()` – Returns current supply
* `get-balance(account)` – Returns token balance of account
* `get-allowance(owner, spender)` – Gets allowance with expiration check
* `is-locked(address)` – Checks if an address’s tokens are locked

---

## Security Highlights

* Immutable supply cap
* Allowance expiration to reduce risk of stale approvals
* Locked addresses cannot transfer
* Blacklisted/restricted accounts blocked from interaction
* Overflow-safe arithmetic via `safe-add`
* Events for mint, burn, and transfer aid in off-chain tracking

---

## Use Cases

* DAO token with built-in governance power tracking
* Regulated utility token with blacklist/whitelist capabilities
* Staged release token using `locked-tokens`
* Pausable token system for emergency halts
* Custom mint roles for multi-party token issuance control

---

## Future Expansion

* Role-based burning
* Snapshot voting logic
* Staking integration
* Cross-chain wrapping support

---

## Deployment

To deploy this contract:

1. Ensure Clarity is installed and integrated with the Stacks CLI.
2. Replace `"Stacks-Stellaris"` with your desired token name if needed.
3. Deploy to your testnet or mainnet environment using:
