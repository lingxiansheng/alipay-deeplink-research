# Alipay DeepLink + JSBridge Security Research

**17 Verified Vulnerabilities | 3 Devices | 308 Server Log Entries**

## Full Report

- **Website**: [https://innora.ai/zfb/](https://innora.ai/zfb/)
- **GitHub Mirror**: This repository

## Summary

This repository documents a comprehensive security research project that uncovered **17 security vulnerabilities** in Alipay's DeepLink URI scheme (`alipays://`) and its Nebula WebView container.

### Key Findings

| Severity | Count | Examples |
|----------|-------|---------|
| **CRITICAL** | 3 | GPS silent theft, Transfer pre-fill, Payment initiation |
| **HIGH** | 6 | Device fingerprinting, UI spoofing, Session leak |
| **MEDIUM** | 8 | Network info, Chain WebView, Scheme injection |

### Attack Chain

```
External SMS/QQ/WeChat Link
    → Browser opens alipays:// DeepLink
    → Alipay launches with attacker's URL in WebView
    → AlipayJSBridge APIs exposed to external page
    → Silent data collection (GPS, device info, session)
    → UI spoofing (title bar, toast notifications)
    → Sensitive page navigation (transaction history, transfer)
```

### Cross-Platform Verification

- Samsung Galaxy S25 Ultra (Android 15, New Zealand)
- Redmi 12 (Android 14, Malaysia)
- iPhone 16 Pro (iOS 18.3, China)

## Live PoC (Read-Only Demo)

> **No data is collected or transmitted.** All results display locally only.

- [Trigger Page](https://innora.ai/zfb/poc/trigger.html) — Simulates attacker distribution page
- [JSBridge PoC](https://innora.ai/zfb/poc/verify.html) — Demonstrates API access from external page
- [Chain WebView](https://innora.ai/zfb/poc/chain.html) — Proves chained pages retain bridge access

## Responsible Disclosure Timeline

| Date | Action |
|------|--------|
| 2026-02-25 | Initial report sent to Ant Group SRC (TLS/SSL findings) |
| 2026-03-07 | Full report V3 sent with 17 vulnerabilities + 308 log entries |
| 2026-03-08 | Ant Group response: "These are normal features" (正常功能) |
| 2026-03-11 | Public disclosure after vendor declined to acknowledge |

## Repository Structure

```
├── index.html          # Full bilingual (CN/EN) research blog
├── poc/
│   ├── trigger.html    # Attack trigger simulation page
│   ├── verify.html     # JSBridge exploitation PoC
│   └── chain.html      # Chain WebView demonstration
├── review_kimi.md      # Kimi K2 cross-validation review
├── review_sonnet.md    # Sonnet review
├── review_summary.md   # Review summary
└── README.md           # This file
```

## Evidence

- **308 server exfiltration log entries** (JSONL format, not included in public repo)
- **42 real-device screenshots** (not included in public repo)
- Full evidence available upon request: feng@innora.ai

## Legal Disclaimer

This research is conducted for **educational and security improvement purposes only**. All testing was performed on accounts owned by the researcher. No unauthorized access to third-party accounts or data occurred.

The PoC pages are **read-only demonstrations** with all data exfiltration endpoints disabled. They only display results locally in the browser.

## Mirrors & Archives

To prevent single-point deletion, this research is archived at multiple locations:

- **Website**: [https://innora.ai/zfb/](https://innora.ai/zfb/)
- **GitHub**: [https://github.com/sgInnora/alipay-deeplink-research](https://github.com/sgInnora/alipay-deeplink-research)

If any mirror is taken down, please check the other locations.

**Readers are encouraged to fork this repository as backup.**

## Contact

- **Researcher**: Innora AI Security Research Team
- **Email**: feng@innora.ai
- **Website**: [innora.ai](https://innora.ai)

---

*This research follows responsible disclosure practices. The vendor was given adequate time to respond before public disclosure.*
