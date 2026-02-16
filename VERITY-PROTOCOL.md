# Verity Protocol

**"Truth through computation, not trust."**

An anonymous whistleblower disclosure platform built on Arcium's MPC network.

## Concept

Sources submit encrypted information through a web portal. No single party — not any node, not any journalist, not the platform operator — can see the raw data. The Arcium MPC cluster processes, verifies, and selectively discloses information through threshold consensus. The source is protected by math, not trust.

## Architecture

### 1. Drop Portal (Frontend)
- Minimal static site, no JavaScript required to submit (works in Tor browser with JS disabled)
- HTML form that encrypts client-side before submission
- Designed to be mirrored across multiple proxy endpoints:
  - Tor .onion hidden service
  - I2P eepsite
  - Multiple clearnet mirrors behind Cloudflare/reverse proxies
  - IPFS-hosted static frontend
- No cookies, no sessions, no fingerprinting, no analytics
- Each mirror points to the same Arcium MPC backend
- Source gets a one-time claim code (generated client-side) to check status later

### 2. Submission Pipeline (Backend)
- Lightweight relay server (Rust or Node) that receives encrypted blobs from any mirror
- Strips all metadata — IP, headers, timing — before forwarding
- Splits submission into encrypted shares using Arcium's MPC secret sharing
- Shares distributed across the cluster — no single node holds the full document
- Relay servers are also mirrored and stateless

### 3. Arcium MPC Program (On-Chain / Cluster)

**Verification (no disclosure)**
- Verify a document hash matches a known organizational signature
- Confirm timestamps fall within a claimed date range
- Check if content matches keyword patterns without reading it
- Generate a "credibility score" from encrypted metadata

**Threshold Disclosure**
- M-of-N reviewer consensus required to decrypt any portion
- Reviewers are assigned cryptographic identities — anonymous to each other
- Partial disclosure: reveal specific fields/sections while keeping the rest encrypted
- Full disclosure requires higher threshold (e.g., 5-of-7 vs 3-of-7 for partial)

**Dead Man's Switch**
- Source sets a timer at submission
- If source doesn't check in within the window, disclosure threshold automatically lowers
- Configurable: auto-release to reviewers, auto-release to public, or just alert

**Selective Queries (for journalists/reviewers)**
- "Does this submission mention [organization X]?" → yes/no
- "How many submissions reference [topic Y]?" → count only
- "Is the source internal to [sector Z]?" → boolean only
- All queries run as MPC — the question itself is also encrypted

### 4. Reviewer Dashboard
- Authenticated portal for approved reviewers
- Shows: submission count, credibility scores, pending disclosure votes
- Vote to disclose with cryptographic signature
- Audit log of all queries and votes (public, on-chain)

### 5. Public Transparency Layer
- On-chain record of: number of submissions, disclosure votes, reviewer activity
- Zero knowledge about content — only metadata about the system's activity
- Disclosed documents published to IPFS with on-chain hash verification

## Technical Stack
- Frontend: Pure HTML/CSS, progressively enhanced, <50KB total
- Relay: Rust (axum) or Node, stateless, ephemeral
- MPC Program: Arcium SDK (Rust)
- On-chain: Solana program via Anchor
- Storage: IPFS for disclosed documents, Arcium cluster for encrypted shares
- Mirrors: Tor hidden service, I2P, clearnet behind proxies, IPFS static hosting

## Phase Plan
1. Build the Arcium MPC program with verification and threshold disclosure. Test on devnet.
2. Build the drop portal and relay server. Deploy mirrors.
3. Build reviewer dashboard. Onboard test reviewers.
4. Security audit. Publish to developer-discussion on Arcium Discord.
