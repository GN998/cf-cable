# ☁️ cf-cable

A serverless WebSocket server for **FIDO2 / Passkey cross-device authentication** (`caBLE v2` / CTAP 2.3), running on Cloudflare Workers and Durable Objects.

When signing in with a Passkey by scanning a QR code on a computer with a phone, this service provides the standard WebSocket endpoint that allows both devices to connect and exchange end-to-end encrypted WebAuthn messages.

## ✨ Features

* **☁️ Serverless Deployment:** Runs entirely on Cloudflare Workers and Durable Objects — no VPS, Linux upgrades, or Docker containers to maintain.
* **🔑 Standard Passkey QR Flow:** Supports QR-initiated cross-device WebAuthn authentication (`/cable/new/` and `/cable/connect/`) using the `fido.cable` WebSocket subprotocol.
* **📦 Handshake Message Buffering:** Uses Durable Object SQLite storage to temporarily buffer early binary frames (up to 30 frames) if one device connects slightly before the other, delivering them in order once both sides are online.
* **🧹 Automatic Session Cleanup:** Limits each session room to two devices, automatically closes inactive sessions (121s lifetime, 30s reconnect grace period), and seals completed sessions (`410 Gone`) to prevent reuse.

## ⚠️ Compliance and Disclaimer

The code is provided 'as is', and the developers assume no liability for any misuse, damages, or legal consequences arising from its deployment.

This project is intended solely for academic research and technical exchange regarding FIDO/WebAuthn cryptographic protocols, demonstrating the implementation principles of caBLE.

Users must use this project in strict compliance with local laws and regulations. It is strictly prohibited to modify or use this code for any form of illegal activity.

## 🚀 Quick Start

Fork or clone this repository, configure your custom domain, and deploy via **Cloudflare Workers & Pages** (**Continue with GitHub**).

### Configuration (How to use your own domain)

Update `wrangler.toml` with your domain managed on Cloudflare:

~~~toml
routes = [
  { pattern = "cable.yourdomain.com", custom_domain = true }
]
~~~

## 🙏 Acknowledgments

This project is made possible thanks to the infrastructure and open standards provided by:

* **[Cloudflare](https://www.cloudflare.com/)**: For providing the Workers and Durable Objects serverless runtime.
* **[FIDO Alliance](https://fidoalliance.org/)**: For developing and maintaining the open FIDO2/WebAuthn and caBLE protocol specifications that secure the modern web.

---

GitHub and LinuxDo