# Kronik v8.0

[![Version](https://img.shields.io/badge/Kronik-8.0--HyperThreaded-00A86B?style=for-the-badge&labelColor=0A0A0A&color=00A86B)](https://github.com/hypersecuritylabs/kronik)
[![Rust](https://img.shields.io/badge/Rust-2021%20Edition-FF5532?style=for-the-badge&labelColor=0A0A0A&color=FF5532)](https://www.rust-lang.org/)
[![Platform](https://img.shields.io/badge/Linux%20%7C%20Windows-F0EBE6?style=for-the-badge&labelColor=0A0A0A&color=F0EBE6)]()
[![HTTP/2](https://img.shields.io/badge/HTTP-2.0%20Multiplexed-00A86B?style=for-the-badge&labelColor=0A0A0A&color=00A86B)]()
[![AI](https://img.shields.io/badge/AI-Lyara%20Engine-FF5532?style=for-the-badge&labelColor=0A0A0A&color=FF5532)]()
[![ML](https://img.shields.io/badge/ML-linfa--bayes-F0EBE6?style=for-the-badge&labelColor=0A0A0A&color=F0EBE6)]()
[![License](https://img.shields.io/badge/License-Proprietary-FF5532?style=for-the-badge&labelColor=0A0A0A&color=FF5532)]()

**Hyper-Threaded WordPress Attack & Assessment Framework**

HTTP/2 multiplexed · AI-driven (Lyara) · ML-powered detection (linfa-bayes) · 10 DoS modules · Forensic auto-dissolution

---

[![◆](https://img.shields.io/badge/◆-Overview-00A86B?style=for-the-badge&labelColor=0A0A0A&color=00A86B)]()

Kronik is a high-performance WordPress security assessment framework engineered for professional offensive operations. Built entirely in Rust, it leverages HTTP/2 multiplexing, connection pooling, adaptive timing, and an AI attack engine (Lyara) to deliver credential testing at scale while evading WAF, CAPTCHA, and rate-limiting defenses.

| Layer | Technology |
|-------|-----------|
| **Core** | Rust · tokio async · reqwest HTTP/2 |
| **AI/ML** | Lyara engine · linfa-bayes GNb · Candle scoring |
| **Network** | Connection pooling · DNS caching · adaptive timing · token-bucket rate limiting |
| **Evasion** | UA rotation (100+ profiles) · cache busting · referer spoofing · header noise · timing jitter |
| **Stealth** | Slow mode · traffic pattern mimicry · adaptive WAF detection |
| **Filtration** | WAF detection (Cloudflare, Sucuri, Wordfence) · CAPTCHA classification · honeypot analysis |
| **DoS** | HTTP/2 flood · XML-RPC pingback · Slowloris · cache poison · WAF bypass · memory exhaust · lockout · TCP RST |
| **Dissolution** | 7 forensic cleanup strategies · stealth exit · verification |

---

[![▣](https://img.shields.io/badge/▣-Architecture-FF5532?style=for-the-badge&labelColor=0A0A0A&color=FF5532)]()

```
┌─────────────────────────────────────────────────────────────────┐
│                         main.rs                                 │
│  Orchestrator — Phase control, timing, signal handling          │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌───────────────┐    │
│  │ Discovery │  │  Recon   │  │Filtration │  │   Lyara AI  │    │
│  │  ML GNb   │  │ 30+ end- │  │WAF/CAPTCHA│  │   Engine    │    │
│  │  10-feat  │  │ points   │  │/validator │  │ 27 mutations│    │
│  └──────────┘  └──────────┘  └──────────┘  └───────────────┘    │
│                                                                 │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │                     Attack Engine                        │   │
│  │  XML-RPC · wp-login · REST API · Multi-endpoint          │   │
│  │  Token bucket · Adaptive delay · Proxy rotation          │   │
│  └──────────────────────────────────────────────────────────┘   │
│                                                                 │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌───────────────     │
│  │ Evasion  │  │  Stealth │  │  Proxy   │  │   DoS/Crash   │    │
│  │ UA/jitter│  │slow/mimic│  │SOCKS/HTTP│  │ 10 modules    │    │
│  └──────────┘  └──────────┘  └──────────┘  └───────────────┘    │
│                                                                 │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │                 Auto-Dissolution                         │   │
│  │  5 strategies · file/network/memory/process cleanup      │   │
│  └──────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────┘
```

[![⌨](https://img.shields.io/badge/⌨-Installation-00A86B?style=for-the-badge&labelColor=0A0A0A&color=00A86B)]()

```bash
# Requirements: Rust toolchain (rustc + cargo)
git clone <repo> && cd kronik

# Release build (fully optimized)
cargo build --release

# Binary located at:
./target/release/kronik

# Debian package
sudo dpkg -i kronik_8.0.0_amd64.deb
```

[![⊞](https://img.shields.io/badge/⊞-CLI%20Reference-F0EBE6?style=for-the-badge&labelColor=0A0A0A&color=F0EBE6)]()

### Target & Credentials

| Flag | Short | Description | Default |
|------|-------|-------------|---------|
| `--target` | `-U` | Target URL (required) | — |
| `--user` | `-u` | Single username | — |
| `--user-list` | | Username wordlist file | — |
| `--pass` | `-p` | Single password | — |
| `--pass-list` | `-w` | Password wordlist file | — |
| `--threads` | `-t` | Concurrent threads | 8 |
| `--duration` | | Max attack duration (seconds) | unlimited |
| `--proxy-file` | `-x` | Proxy list file | — |
| `--delay` | | Delay between requests (ms) | 100 |
| `--enum-only` | | Enumerate users only | false |
| `--output` | `-o` | Save results to file | — |
| `--verbose` | `-v` | Verbose output | false |

### Reconnaissance

| Flag | Description |
|------|-------------|
| `--active-scan` | Port scan (10 ports) + endpoint probe (34 paths) + fingerprint |
| `--plugin-scan` | Plugin vulnerability scan (requires `--active-scan`) |
| `--no-filtration` | Skip WAF/CAPTCHA/honeypot/validation checks |

### Evasion & Stealth

| Flag | Description |
|------|-------------|
| `--evasion` | Enable all evasion techniques |
| `-A` / `--random-agent` | Random UA rotation (100+ profiles) |
| `--cache-bust` | Cache busting via random query params |
| `--referer-spoof` | Spoof referer header |
| `--header-noise` | Inject noise headers (Sec-Fetch-*, X-Forwarded-*) |
| `--jitter` | Timing jitter percentage (0-100) |
| `--stealth` | Enable all stealth techniques |
| `--slow` | Slow attack mode with human pacing delays |
| `--pattern-mimic` | Human traffic pattern mimicry |
| `--detect-evade` | Adaptive WAF detection and evasion |

### AI Attack (Lyara)

| Flag | Description |
|------|-------------|
| `--ai-attack` | Enable Lyara AI attack engine |
| `--ai-skills` | Custom AI skills JSON file |

### Dissolution

| Flag | Description | Default |
|------|-------------|---------|
| `--dissolution` | Enable auto-forensic dissolution | false |
| `--dissolution-strategy` | Strategy: immediate, gradual, quantum, ghost, zero | immediate |
| `--dissolution-delay` | Delay before cleanup (seconds) | 15 |

### Advanced

| Flag | Description |
|------|-------------|
| `--no-http2` | Force HTTP/1.1 |
| `--multi-endpoint` | Hit xmlrpc + login + REST API simultaneously |
| `--auto-exploit` | Auto-exploit after successful login |
| `--stuffing` | Credential stuffing from leaked creds file |

### DoS / Crash Modules

| Flag | Description | Requires |
|------|-------------|----------|
| `--flood` | HTTP/2 adaptive flood DoS | — |
| `--xmlrpc-abuse` | XML-RPC pingback amplification | — |
| `--slowloris` | Slowloris — exhaust Apache workers | — |
| `--cache-poison` | Cache poisoning via header injection | — |
| `--waf-bypass` | WAF bypass fuzzing (12 encoding mutations) | — |
| `--plugin-exploit` | CVE-based plugin vulnerability exploitation | — |
| `--memory-exhaust` | Memory exhaustion via oversized POST bodies | — |
| `--lockout-dos` | Account lockout via rapid failed logins | users |
| `--tcp-rst` | TCP RST injection (requires root) | root |
| `--crash-duration` | Duration for crash modules (seconds) | 60 |
| `--slow-connections` | Slowloris connection count | 200 |
| `--rst-port` | Port for TCP RST injection | 443 |

---

[![▤](https://img.shields.io/badge/▤-Usage%20Examples-FF5532?style=for-the-badge&labelColor=0A0A0A&color=FF5532)]()

### Reconnaissance

```bash
# Quick WP detection + user enumeration (no attack)
kronik -U https://example.com --enum-only

# Full recon: ML detection + user enum + filtration
kronik -U https://example.com

# Active scan: 10-port scan + 34 endpoints + fingerprint
kronik -U https://example.com --active-scan --plugin-scan
```

### Credential Attacks

```bash
# Single user + wordlist, 16 threads
kronik -U https://example.com -u admin -w rockyou.txt -t 16

# Multi-user + wordlist + proxy rotation
kronik -U https://example.com --user-list users.txt -w passwords.txt -x proxies.txt

# Password spray (one password, every user)
kronik -U https://example.com --spray 'Winter2024!' -t 4

# Credential stuffing from leaked dump
kronik -U https://example.com --stuffing leaked_credentials.txt
```

### Evasion & Stealth

```bash
# Full evasion + stealth + proxy
kronik -U https://example.com -u admin -w wordlist.txt --evasion --stealth -x proxies.txt

# Custom evasion: slow + jitter 50% + cache bust
kronik -U https://example.com -u admin -w wordlist.txt --slow --jitter 50 --cache-bust

# Full stealth operation
kronik -U https://example.com -u admin -w wordlist.txt --stealth --evasion --delay 500
```

### AI Attack (Lyara)

```bash
# AI-powered attack
kronik -U https://example.com -u admin --ai-attack

# AI + evasion + dissolution
kronik -U https://example.com -u admin --ai-attack --evasion --dissolution

# AI + custom skills
kronik -U https://example.com -u admin --ai-attack --ai-skills my_skills.json
```

### Super-Lyara — Advanced AI Intelligence Set

The **Super-Lyara** stack activates when `--ai-attack` is used with full evasion and dissolution. It represents the complete AI attack pipeline:

```
┌──────────────────────────────────────────────────────────────────┐
│                      SUPER-LYARA ENGINE                          │
├──────────────────────────────────────────────────────────────────┤
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────────────┐  │
│  │  Generator   │  │  Strategist  │  │  Response Analyzer   │  │
│  │  27 mutation │  │  4 profiles  │  │  50+ patterns        │  │
│  │  rules       │  │  adaptive    │  │  waf/captcha/success │  │
│  └──────────────┘  └──────────────┘  └──────────────────────┘  │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────────────┐  │
│  │ CandleEngine │  │  Evasion     │  │  Timing Profile      │  │
│  │ ML scoring   │  │  triggers    │  │  jitter/delay        │  │
│  └──────────────┘  └──────────────┘  └──────────────────────┘  │
└──────────────────────────────────────────────────────────────────┘
```

| Strategy | Condition | Passwords | Jitter | Delay | Use Case |
|----------|-----------|-----------|--------|-------|----------|
| `smart_bruteforce` | No WAF, No CAPTCHA | 500 | — | — | Standard targets |
| `stealth_bruteforce` | WAF detected | 100 | 50% | 3x | WAF-protected sites |
| `aggressive_bruteforce` | Not rate-limited | 1000 | 0% | 0.5x | Internal/CTF/lab |
| `slow_precision` | CAPTCHA detected | 30 | 80% | 5x | CAPTCHA-protected targets |

### DoS Modules

```bash
# HTTP/2 adaptive flood
kronik -U https://example.com --flood --crash-duration 120

# XML-RPC pingback amplification
kronik -U https://example.com --xmlrpc-abuse --crash-duration 300

# Slowloris (200 connections)
kronik -U https://example.com --slowloris --slow-connections 200

# Cache poisoning + WAF bypass combo
kronik -U https://example.com --cache-poison --waf-bypass

# Memory exhaustion + account lockout
kronik -U https://example.com -u admin --memory-exhaust --lockout-dos

# TCP RST injection (requires root)
sudo kronik -U https://example.com --tcp-rst --rst-port 443

# Full chaos: flood + xmlrpc + cache poison
kronik -U https://example.com --flood --xmlrpc-abuse --cache-poison --crash-duration 120
```

### Full Pipeline

```bash
# Full assault: recon + evasion + AI + dissolution
kronik -U https://example.com -u admin -w rockyou.txt \
  --active-scan \
  --plugin-scan \
  --evasion \
  --stealth \
  --ai-attack \
  --dissolution \
  --dissolution-strategy ghost \
  --multi-endpoint

# Stealth operation: slow + proxy + evasion
kronik -U https://example.com \
  -u admin \
  -w rockyou.txt \
  --proxy-file proxies.txt \
  --stealth \
  --evasion \
  --delay 500 \
  --jitter 50
```

---

[![⊡](https://img.shields.io/badge/⊡-Module%20Reference-00A86B?style=for-the-badge&labelColor=0A0A0A&color=00A86B)]()

### Reconnaissance (`activenum/`)

| Module | File | Capability |
|--------|------|------------|
| Scanner | `activenum/scanner.rs` | Async TCP port scan — 10 ports (80, 443, 8080, 8443, 21, 22, 3306, 5432, 8888, 9090), 3s timeout |
| Probe | `activenum/probe.rs` | 34 WordPress endpoints — config backups, debug.log, xmlrpc, wp-json, .htaccess, .env, .git |
| Fingerprint | `activenum/fingerprint.rs` | Server headers · WP version · PHP version · plugins · themes · Redis · WAF detection |
| Spray | `activenum/spray.rs` | Password spray via XML-RPC across enumerated users |

### Filtration (`filtration/`)

| Module | File | Capability |
|--------|------|------------|
| WAF | `filtration/waf.rs` | Cloudflare (cf-ray, __cfuid) · Sucuri (x-sucuri-id) · Wordfence (x-wordfence) · CSP/XSS header analysis |
| CAPTCHA | `filtration/captcha.rs` | reCAPTCHA v2/v3 · hCaptcha · Cloudflare Turnstile · site key extraction |
| Honeypot | `filtration/honeypot.rs` | Timing analysis · response signatures · WP marker scoring |
| Validator | `filtration/validator.rs` | Multi-method WP verification · login form · XML-RPC · REST API |

### Attack Engine (`modules/`)

| Module | File | Capability |
|--------|------|------------|
| Engine | `modules/engine.rs` | Core attack loop — XML-RPC bruteforce, mpsc worker pool, adaptive delay, proxy rotation |
| Enum Users | `modules/enum_users.rs` | 3-method enumeration — REST API · author archive (`?author=N`) · XML-RPC probe |
| Credential Stuffing | `modules/credential_stuffing.rs` | Breach file parser · user:pass matching · candidate building |
| Auto-Exploit | `modules/auto_exploit.rs` | Post-login — nonce extraction · backdoor plugin upload · webshell deployment |
| Proxy | `modules/proxy.rs` | Thread-safe round-robin rotator · SOCKS4/5 · HTTP/HTTPS |
| Output | `modules/output.rs` | Phase headers · credential display · attack summaries · strategy breakdowns |

### DoS Modules (`modules/`)

| Module | File | Mechanism |
|--------|------|-----------|
| HTTP/2 Flood | `modules/http2_flood.rs` | Adaptive behavioural flood — 5 endpoints, GET/POST/HEAD, varies paths, RTT-based concurrency adjustment |
| XML-RPC Abuse | `modules/xmlrpc_abuse.rs` | Pingback amplification — spoofed `pingback.ping` to xmlrpc.php |
| Slowloris | `modules/slow_attack.rs` | Slow headers — trickles random headers every 5-15s, 30s idle timeout |
| Cache Poison | `modules/cache_poison.rs` | Header injection — X-Forwarded-Host/Scheme/Proto, X-Real-IP, X-Custom-Poison XSS |
| WAF Bypass | `modules/waf_bypass.rs` | 12 encoding mutations — URL encode, double encode, HTML entities, SQL comments, line feeds |
| Memory Exhaust | `modules/memory_exhaust.rs` | 1-10MB multipart POST bodies to PHP endpoints |
| Lockout DoS | `modules/lockout_dos.rs` | Rapid failed logins via wp-login + XML-RPC against enumerated users |
| TCP RST | `modules/tcp_rst.rs` | Raw packet injection via pnet — spoofed RST flags, IP/TCP checksum |
| Plugin Exploit | `modules/plugin_exploit.rs` | CVE probing — Yoast SEO (CVE-2024-24918), Really Simple SSL (CVE-2024-10924) |

### AI Engine (`ai_attacks/`)

| Module | File | Capability |
|--------|------|------------|
| Lyara Engine | `ai_attacks/mod.rs` | Skills JSON · response analysis · strategy selection · 27 mutation rules · 50+ analysis patterns |
| Candle | `ai_attacks/candle.rs` | Lightweight ML — entropy scoring · password strength · response body analysis |
| Generator | `ai_attacks/generator.rs` | Weighted mutation selection · 22 mutation types · deterministic PRNG |
| Strategist | `ai_attacks/strategist.rs` | Telemetry-driven adaptation · WAF/CAPTCHA/rate-limit detection · strategy cycling |
| Analyzer | `ai_attacks/analyzer.rs` | Colored analysis output · success/block/captcha/close-guess classification |

### Password Strategies (`strategies/`)

| Module | File | Capability |
|--------|------|------------|
| Targeted | `strategies/targeted.rs` | Domain-based generation · base word extraction · mutation pipeline |
| Mutation | `strategies/mutation.rs` | 50+ mutations — case · year suffixes · number suffixes · leet · prefixes |
| Common | `strategies/common.rs` | 55 built-in common WordPress weak passwords |
| Analyzer | `strategies/analyzer.rs` | Strategy scoring · success rate tracking · best strategy selection |

### ML Detection (`models/`)

| Module | File | Capability |
|--------|------|------------|
| Detector | `models/detector.rs` | linfa-bayes Gaussian Naive Bayes · 10-feature WP classification · 12-sample training set |

### Evasion (`evasion/`)

| Module | File | Capability |
|--------|------|------------|
| Identity | `evasion/identity.rs` | 100+ User-Agent profiles — Chrome, Firefox, Safari, Edge, mobile, bots, game consoles |
| Request | `evasion/request.rs` | Header construction — random IPs, referer spoofing, Sec-Fetch-* injection, Accept randomization |
| Cache | `evasion/cache.rs` | URL cache busting — 8 random parameter names seeded by nanosecond time |
| Timing | `evasion/timing.rs` | Jitter application — +/- jitter_pct% with 10ms floor |

### Stealth (`stealth/`)

| Module | File | Capability |
|--------|------|------------|
| Slow | `stealth/slow.rs` | Human pacing delays — 800-3000ms base, 2-6s pauses every 7th attempt |
| Pattern | `stealth/pattern.rs` | Fisher-Yates credential shuffle · traffic pattern mimicry |
| Detection | `stealth/detection.rs` | Block detection — 429/503/403, Cloudflare Ray, Sucuri headers, adaptive evasion suggestion |
| Noise | `stealth/noise.rs` | Random traceability headers — UUIDs, trace IDs, entropy markers |

### Dissolution (`dissolution/`)

| Module | File | Capability |
|--------|------|------------|
| Engine | `dissolution/engine.rs` | Auto-dissolution orchestrator · concurrent timer · emergency trigger |
| Config | `dissolution/config.rs` | 7 strategies · 4 verification levels · delay configuration |
| Phases | `dissolution/phases.rs` | File cleanup (/tmp, /var/tmp, /dev/shm) · network cleanup · memory wiping · process cleanup |
| Strategies | `dissolution/strategies.rs` | Immediate · Gradual · Conditional · Distributed · Quantum · Ghost · Zero-Knowledge |
| Verification | `dissolution/verification.rs` | Artifact scanning · connection checking · cryptographic hash comparison |
| Events | `dissolution/event.rs` | Timestamped dissolution event log · phase tracking · status reporting |

### Network Stack (`network/`)

| Module | Capability |
|--------|------------|
| `ConnPool` | 64 max idle connections · keep-alive tracking · active/total counters |
| `DnsCache` | 256 entries · 300s TTL · async resolution · capacity management |
| `AdaptiveTiming` | Sliding success window (10) · 1.5x delay on < 30% success · 0.9x delay on > 90% success · jitter 5-30% |
| `RateLimiter` | Token bucket · configurable window · wait-time calculation |
| `Client Builder` | reqwest HTTP/2 · ALPN · cookie store · browser-default headers · proxy env support |

---

[![◈](https://img.shields.io/badge/◈-Network%20Stack-F0EBE6?style=for-the-badge&labelColor=0A0A0A&color=F0EBE6)]()

| Parameter | Setting |
|-----------|---------|
| Connection pool | 64 max idle, 10s keep-alive |
| DNS cache | 256 entries, 300s TTL |
| Adaptive timing | Sliding window of 10 · 1.5x backoff · 0.9x recovery |
| Rate limiter | Token bucket — 30 tokens, 1s refill |
| HTTP version | HTTP/2 with ALPN, adaptive window, keep-alive while idle |
| Timeouts | 15s request · 30s total · 5s HTTP/2 keep-alive probe |
| Jitter | Configurable 0-100%, applied after base delay |

---

[![⌘](https://img.shields.io/badge/⌘-Attack%20Strategies-FF5532?style=for-the-badge&labelColor=0A0A0A&color=FF5532)]()

### Password Generation Pipeline

```
Domain URL
    │
    ▼
Base Words Extracted (strip protocol, www, TLD)
    │
    ├── Capitalized, uppercase, lowercase variants
    │
    ▼
Mutation Engine (50+ mutations per base word)
    │
    ├── Year suffixes: 2020-2026 (+_ ! @ variants)
    ├── Number suffixes: 1, 12, 123, 1234, 12345 (+! variants)
    ├── Symbol prefixes: ! @ # super admin wp wp_
    ├── Leet substitutions: a→@ e→3 i→1 o→0 s→$ t→7
    │
    ▼
Merge + Dedup (BTreeSet)
    │
    ▼
Optional: AI Generation (Lyara — 300 probabilistic mutations)
    │
    ▼
Attack Engine (token bucket, adaptive delay)
```

### Lyara AI Strategies

| Strategy | When | Passwords | Behaviour |
|----------|------|-----------|-----------|
| `smart_bruteforce` | No defenses detected | 500 | Standard pace, no evasion |
| `stealth_bruteforce` | WAF present | 100 | 50% jitter, 3x delay, evasion triggers |
| `aggressive_bruteforce` | No rate-limiting | 1000 | No jitter, 0.5x delay, high throughput |
| `slow_precision` | CAPTCHA blocking | 30 | 80% jitter, 5x delay, careful selection |

---

[![⚠](https://img.shields.io/badge/⚠-Legal%20Disclaimer-FF5532?style=for-the-badge&labelColor=0A0A0A&color=FF5532)]()

This tool is for **authorized security testing only**. You must have explicit written permission from the target owner before using Kronik against any system. Unauthorized access to computer systems is illegal under:

- Computer Fraud and Abuse Act (CFAA) — USA
- Computer Misuse Act 1990 — UK
- Similar laws worldwide

The DoS/crash modules (flood, slowloris, TCP RST, memory exhaustion, lockout DoS) can cause denial of service and system damage. Use only in controlled lab environments or under signed rules of engagement.

> **Name Usage Restriction:** The name "Kronik", its branding, visual identity, and any associated trademarks are the exclusive property of HyperSecurity Offensive Labs. You may not use, reproduce, or claim the Kronik name for any other project, product, or service without prior written authorization.

---

[![★](https://img.shields.io/badge/★-Credits-00A86B?style=for-the-badge&labelColor=0A0A0A&color=00A86B)]()

| Role | Name |
|------|------|
| **Operator** | KhaninKali |
| **Division** | HyperSecurity Offensive Labs |

**Engine:** Rust · tokio · reqwest · clap · linfa · linfa-bayes · ndarray · colored · indicatif · pnet · sha2


