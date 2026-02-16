# MEMORY.md — Long-Term Memory

## Bruce
- Runs Alienware Area 51 desktop, Ubuntu 24.04, kernel 6.14.0-37-generic
- Owns **WolfPaw Data Center** — ISP in Edmonton, free colo, static IP, enterprise bandwidth
- New to Linux/self-hosting but persistent — fought through broken configs to get me running
- Wants: learning, building projects, server management, automation, good conversation
- Style: casual, direct, no corporate BS
- Telegram: @BlackberryBruce

## GitHub
- Account: bruce-burman
- Auth: HTTPS via `gh` CLI
- Git identity: Bruce Burman <bruce@sis.net>

## Me
- I'm Claude ⚡ — resident AI on Bruce's machine
- Day one: 2026-02-15

---

## Active Projects

### Arcium ARX Node — Full Reference

#### 1. Infrastructure
- **Machine:** Alienware Area 51, Ubuntu 24.04
- **Location:** WolfPaw Data Center, static IP `34.229.15.124`
- **Required ports:** 8001, 8002, 8012, 8013, 9091 (TCP & UDP)
  - 8001: MPC protocol communication
  - 8002: BLS signature aggregation
  - 8012: TD preprocessing
  - 8013: TD registration
  - 9091: Prometheus metrics

#### 2. Accounts & Addresses
- **Node authority:** `EhfvWiKGYgL2CL6YgrixYrm2ZjNKvS1Q34G2GzgHNKNc`
- **Callback authority:** `6Ye8NfEGQFhqnD15twyQ7iK4NhNjTzRufYea8BSZuST3`
- **Original devnet wallet:** `CE9FXpVyBKAnvWxrSjtsdBo6L2LoPvCzQTKC2LqHZ21E`
- **Node offset:** 5237
- **Network:** Solana devnet

#### 3. File Locations
- **Node workspace:** `~/arcium-node-setup/`
- All 5 keypairs in that directory:
  - `node-keypair.json` — Node Authority (Solana)
  - `callback-kp.json` — Callback Authority (Solana)
  - `identity.pem` — Identity (PKCS#8 Ed25519)
  - `bls-keypair.json` — BLS threshold signatures
  - `x25519-keypair.json` — Encrypted node comms
- `docker-compose.yml` and `node-config.toml` in that directory
- Support dirs: `arx-node-logs/`, `private-shares/`, `public-inputs/`
- `~/hello_world/` — validation test project (ignore)

#### 4. Tooling Versions
- Rust 1.93.1
- Solana CLI 3.0.15
- Arcium CLI 0.8.3
- Anchor 0.32.1
- Docker 28.2.2
- Node 22.x
- Yarn 1.22.22

#### 5. Phase Plan
- **Phase 1:** Testnet on Alienware (IN PROGRESS — awaiting SOL funding)
- **Phase 2:** Migrate to TEE Intel hardware at WolfPaw DC
- **Phase 3:** Mainnet operations

#### 6. Next Actions (when SOL lands)
1. Fund both addresses via faucet.solana.com
2. Run `arcium init-arx-accs` with all keypairs, offset 5237, IP `34.229.15.124`
3. Join or create cluster
4. `docker compose up -d`
5. Verify with `arx-info`, `arx-active`, health endpoint

#### 7. Key References
- **Official setup guide:** https://docs.arcium.com/developers/node-setup
- **GitHub repo:** https://github.com/bruce-burman/arcium-arx-node
- **Strategy advisor:** Claude on Poe
- **Arcium Discord** for cluster invitations
