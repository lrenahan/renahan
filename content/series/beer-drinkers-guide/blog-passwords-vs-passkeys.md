---
title: "Passwords vs Passkeys: Which is actually more secure when ordering a beer?"
description: "For decades, the password has been the gatekeeper of your digital life. And it's rubbish."
date: 2026-06-10
series: "beer-drinkers-guide"
readtime: "~10 min read"
tags: ["cyber security", "email security", "phishing", "malware", "explainer", "DMARC", "ransomware", "BEC"]
youtube_id: "Rvsxdt4UeB0"
youtube_url: "https://www.youtube.com/watch?v=Rvsxdt4UeB0"
---

# Passwords vs Passkeys
## Why the System You've Used for 30 Years Is Fundamentally Broken — and What's Replacing It

*Series: The Beer Drinker's Guide to Not Getting Hacked | Read time: ~10 minutes*

You've been whispering secrets to strangers for most of your digital life. That's essentially what a password is. And while "The-badger-flies-at-midnight" might *feel* secure, the problem isn't the password itself — it's the entire model behind it.

Let's talk about why, and what passkeys actually do differently under the bonnet.

---

## The Password Problem Is Architectural, Not Behavioural

Before we get to passkeys, it's worth understanding exactly *where* the password system breaks down — because it's not just that people choose bad ones.

**The shared-secret model** is the fundamental issue. When you create a password, you and the server both need to know it. That means the server has to store something derived from your password (usually a hashed version), and you have to *transmit* it during login. That transmission and that stored hash are both attack surfaces.

Here's what can go wrong at each stage:

**At rest (server-side):** Servers store passwords as hashes — typically bcrypt, Argon2, or scrypt. If the database is breached, attackers get those hashes. For weak passwords, they can crack them with rainbow tables or brute force. Good hashing buys time; it doesn't eliminate the risk.

**In transit:** Even over HTTPS, your password moves from your device to the server. If you're on a compromised network, or if a bug in TLS implementation exists, that transmission is potentially visible.

**At the human layer:** You. You reuse passwords. You write them down. You fall for phishing. This isn't a character flaw — it's the inevitable result of asking a human brain to manage dozens of unique 20-character random strings. It's like designing a car that only works safely if the driver is also a Formula 1 pilot.

---

## Enter Phishing — the Attack That Still Works on Everyone

Phishing remains the most successful attack vector in the world, and the password model is almost perfectly suited to it.

The attack is simple: build a website that looks like your bank, send someone a convincing email, and wait for them to type their password into your fake form. Your server receives the credential. You now own that account.

No amount of password complexity helps here. A 50-character random password typed into a fake site is just as useful to an attacker as "password123". The issue isn't strength — it's that passwords are *knowledge-based credentials*, and knowledge can be shared, copied, or stolen from anyone.

---

## How Passkeys Actually Work

Passkeys solve this at a cryptographic level, not a behavioural one. They're built on a standard called **FIDO2** (Fast Identity Online), developed by the FIDO Alliance — a consortium including Google, Apple, Microsoft, and others.

The mechanism is **asymmetric (public-key) cryptography**. Here's the technical walkthrough:

### Registration

When you set up a passkey on a site:

1. Your device generates a **key pair** — a mathematically linked pair of numbers:
   - A **public key**, which is sent to and stored by the website.
   - A **private key**, which never leaves your device. Ever.

2. The private key is stored in a **Trusted Platform Module (TPM)** or **Secure Enclave** — dedicated hardware chips (like Apple's T2/M-series chips or Android's StrongBox) specifically designed so the key can be *used* but never *extracted*.

3. The public key is useless on its own. Think of it as an open padlock — anyone can see it, but only your private key can close and open it.

### Authentication

When you log in:

1. The website sends a **cryptographic challenge** — a random nonce (a one-time-use random number).
2. Your device uses the private key to **digitally sign** that challenge. This produces a signature that can *only* have been created by your specific private key.
3. The website verifies the signature using your stored public key.

You never transmit your secret. The website never receives anything sensitive. The private key never moves.

### Why This Eliminates Phishing

Here's the elegant part: the signing process is **origin-bound**. Your device only uses the passkey if the domain matches the one it was registered for.

A fake `bаrcIays.com` (with a Cyrillic 'а') gets nothing — your authenticator checks the actual domain and simply refuses to sign for an impersonator. The credential is cryptographically bound to the real site. Phishing Phil is unemployed.

---

## Biometrics: The Gatekeeper, Not the Key

There's a common misconception worth clearing up: when you use Face ID or a fingerprint to authenticate with a passkey, your biometric data is **not sent to the website**. At all.

What's happening is a *local unlock*:

1. You present your face or fingerprint to your device.
2. The device checks you are *you* — locally, on-chip.
3. Having confirmed your identity, it unlocks the private key and performs the signing operation.

The website only ever sees a cryptographic signature. Your fingerprint never leaves your phone. The FIDO2 standard explicitly separates *device unlock* (biometric or PIN) from *authentication* (the public-key challenge-response). These are two different operations.

---

## Synced vs Device-Bound Passkeys

There are two flavours of passkeys, and the distinction matters:

**Synced passkeys** (what Apple Keychain, Google Password Manager, and 1Password implement) are encrypted and synced across your devices via the cloud. This trades a small theoretical security reduction for massive usability gains — you don't lose access if you lose your phone. The private key is encrypted before it leaves your device, so the cloud provider can't read it.

**Device-bound passkeys** (used in high-security contexts, hardware security keys like YubiKey) never leave the physical hardware. Losing the device means losing the passkey. Used for things like privileged access management, government systems, and where the security-usability tradeoff tilts firmly toward security.

For most people, synced passkeys are the right choice — they eliminate the primary risk (phishing, credential stuffing) while remaining practical.

---

## What About Credential Stuffing?

One of the most damaging attacks today is **credential stuffing**: attackers take a leaked database of email/password pairs (billions are freely available on the dark web) and try them against every major website, because most people reuse passwords.

Passkeys eliminate this entirely. There's nothing to stuff. Every passkey is a unique cryptographic key pair generated per site. Breaching one site's database exposes only public keys — which are, by design, public. They're useless to an attacker.

---

## Why Hasn't This Happened Sooner?

FIDO2 and WebAuthn (its web API) have been around since 2018. The slow adoption comes down to a few factors:

**Ecosystem fragmentation** — until Apple, Google, and Microsoft all implemented synced passkeys (which happened between 2022 and 2023), you'd lose access to all your passkeys if you switched platforms. That's now largely solved.

**Account recovery complexity** — the password reset flow (forgot password → email link → new password) doesn't map onto passkeys. Sites need to rebuild their recovery flows, which is engineering work.

**Inertia** — passwords are deeply embedded in identity systems, auditing requirements, and enterprise tooling. Replacing them is a multi-year infrastructure project for most organisations.

---

## The Pub Analogy, Properly Technical

Since we started in the pub: the password model is like every customer whispering a secret phrase to the barman, who writes them all down in a ledger. If the ledger is stolen, every customer is compromised. If Phil builds a fake bar and asks for your phrase, you'll probably give it to him.

Passkeys are like giving every customer a personal stamp — a unique signet ring. The bar knows what your stamp impression looks like (public key), but not the ring itself (private key). To verify you, they hand you a lump of wax (the challenge) and ask you to stamp it. They check the impression against their records. Phil can build a perfect replica of the bar, but when he hands you the wax, your ring refuses to stamp it — it knows he's not the real bar.

The ring never leaves your pocket. Phil never gets an impression he can copy. The ledger, if stolen, is useless — it only contains stamp impressions, not the rings themselves.

---

## Last Orders: What to Actually Do

If your device supports passkeys (iOS 16+, Android 9+, Windows 10+, macOS Ventura+), most major sites now support them — Google, Apple, Microsoft, GitHub, PayPal, Shopify, and many others.

**To enable passkeys:** look for a "Security" or "Sign-in methods" section in your account settings on any supported site. Add a passkey. Your device will handle the rest.

For sites that still require passwords, use a password manager. Unique, random passwords for everything — let the software do the remembering.

The password had a good run. It's time to let it retire.

*Cheers — and see you in the next one.*

---

*The Beer Drinker's Guide to Not Getting Hacked is a video series explaining digital security without the jargon.*
