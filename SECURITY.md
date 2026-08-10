# Security Policy

## Reporting a Vulnerability

Please report suspected vulnerabilities in this repository privately to:

- **Email:** [contact@ryo-currency.com](mailto:contact@ryo-currency.com)

Please do **not** open a public GitHub issue for security-sensitive reports.

## Important user notice: retired third-party domains

Historical versions of this fork used two default hostnames that are **no
longer registered to the Ryo Currency project**:

| Historical default | Where it was used | Current registrant |
| --- | --- | --- |
| `geo.ryoblocks.com` | Default mainnet remote-daemon host (`src-electron/main-process/modules/backend.js`) | Third party (Dynadot, re-registered 2024-08-27) |
| `explorer.ryoblocks.com`, `tnexp.ryoblocks.com` | Explorer URLs (`backend.js`, `pool.js`) | Same |

If DNS records are ever added for these hostnames by the current owner, users
of older builds who leave the default configuration will:

- for `geo.ryoblocks.com`: send every wallet `JSON-RPC` request to an
  attacker-controlled daemon, enabling fabricated balances / block heights,
  transaction censorship, and IP-based deanonymization;
- for `tnexp.ryoblocks.com` / `explorer.ryoblocks.com`: open
  attacker-controlled content in the user's default browser when clicking
  "Explorer" on a transaction or block.

## Recommended action for users

1. If you are running a build **older than the commit that lands this file**,
   open the wallet's preferences and either:
   - switch daemon mode to **local**, or
   - set the remote daemon to a hostname you personally trust
     (for example your own node), and
   - do **not** use the built-in "Explorer" button until you have upgraded.
2. Prefer [`ryo-currency/ryo-wallet`](https://github.com/ryo-currency/ryo-wallet)
   over this fork for ongoing use.

## Fix in this commit

- `remote_host` default cleared and `daemon.type` set to `"local"` so no
  wallet traffic goes to a third-party-owned host out of the box.
- Explorer / networkinfo URLs migrated to the project-owned
  `explorer.ryo-currency.com` and `tnexp.ryo-currency.com`.
