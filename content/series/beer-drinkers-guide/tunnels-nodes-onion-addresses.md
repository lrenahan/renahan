---
title: "Tunnels, Nodes & .onion Addresses: How Tor and the Dark Web Actually Work"
description: "Strip away the sensationalism and Tor is a piece of sophisticated engineering. Here's how the cryptography, circuits, and hidden services actually work — technically."
date: 2026-06-19
series: "beer-drinkers-guide"
readtime: "~12 min read"
tags: ["cyber security", "dark web", "Tor", "privacy", "anonymity", "encryption", "explainer", "onion routing"]
youtube_id: "-mimcxFlh6o"
youtube_url: "https://www.youtube.com/watch?v=-mimcxFlh6o"
---

*Read time: ~12 minutes | Series: Tech Behind the Bar*

You've heard the term dark web thrown around in news reports, crime dramas and breathless YouTube thumbnails. It's usually preceded by something ominous and followed by something sensational. But strip away the theatre and what you're actually dealing with is a piece of sophisticated engineering — one designed not for villainy, but for privacy.

In the Pints, Packets & Protocols series, we've already walked through how the standard internet works: DNS lookups, routers, TCP, HTTP, and the rest. This post goes deeper — much deeper. We're heading down into the cellar.

---

## 🗺️ First: What the 'Dark Web' Actually Is

The internet has three loosely defined layers, and they're frequently confused:

- **The Surface Web** — everything indexed by search engines like Google. If you can find it with a search, it lives here. This represents only a small fraction of what's actually online.
- **The Deep Web** — content not indexed by search engines: your online banking portal, private company intranets, academic databases behind paywalls, email inboxes. Totally mundane, totally legal. The vast majority of web content lives here.
- **The Dark Web** — a small subset of the deep web that is intentionally hidden and requires specific software to access. This is what we're talking about today.

The dark web isn't a physical place. There's no secret server room humming away somewhere underneath the internet. It's a collection of websites running on **overlay networks** — networks built on top of the standard internet infrastructure but designed to be difficult to monitor or trace. The most well-known of these overlay networks is Tor.

---

## 🧅 The Onion Router: A Technical Deep Dive

Tor stands for **The Onion Router**. It was originally developed in the mid-1990s by the United States Naval Research Laboratory as a way to protect American intelligence communications online. The concept was published in 1997 by mathematicians Paul Syverson and Michael Reed, and the first public alpha version launched in 2002. It's now maintained by the non-profit Tor Project.

The key idea is **layered encryption** — hence the onion metaphor. When you send data through the standard internet, your IP address travels with every request. Anyone monitoring network traffic — your ISP, a government agency, the website itself — can see where data is coming from and where it's going. Tor eliminates this by routing your traffic through a chain of volunteer-operated computers called **nodes** or **relays**, encrypting it at each step.

---

## 🔌 The Circuit: How a Tor Connection Is Built

Before any data is transmitted, the Tor client on your machine builds what's called a **circuit** — a pre-negotiated path through the Tor network consisting of exactly three relays.

Your Tor client first contacts a **directory authority**: a trusted server that maintains a list of all currently active Tor relays. There are nine of these authorities in total, hardcoded into the Tor software. From this list, your client selects three relays at random, biased towards nodes with higher bandwidth, better uptime, and geographically diverse locations.

Once chosen, your client performs a **key exchange** with each relay using a protocol based on **Diffie-Hellman key exchange** — the process by which two parties agree on a shared encryption key over a public channel without anyone eavesdropping being able to determine what that key is. A cornerstone of modern cryptography.

> The circuit is negotiated incrementally: your client talks to the guard node, extends the circuit to the middle node through the guard, then extends again to the exit node through the middle. At no point does any relay learn the identities of all three nodes in the circuit.

---

## 🔍 The Three Relays: What Each One Knows

Understanding the role of each relay is central to understanding why Tor provides anonymity. The model works because each relay is kept deliberately ignorant of the full picture.

### 1. The Guard Node (Entry Node)

The guard node is the first relay in your circuit — and the only node that knows your real IP address, because your traffic has to originate somewhere. However, the guard node does **not** know your destination. All it can see is that it's received encrypted traffic from you and needs to forward it to the middle node.

Your Tor client encrypts your data in three nested layers before it leaves your machine. Think of it as sealing a letter inside three envelopes, each addressed only to the next stop. The guard node peels off the outermost envelope — revealing only the address of the middle node, and an encrypted payload it cannot read.

To mitigate the risk of a malicious guard node, the Tor client uses **Guard Pinning**: instead of choosing a random guard relay every session, Tor keeps the same guard node for weeks or months. This reduces the chance of eventually being assigned a compromised node.

### 2. The Middle Node (Relay Node)

The middle relay is the node with the least information of all. It receives traffic from the guard node and forwards it to the exit node — but it doesn't know the origin of the data (your real IP was stripped by the guard), and it doesn't know the final destination (still encrypted).

The middle node is also the lowest-risk position to run as a volunteer. Because it never communicates directly with the destination website, its IP address doesn't appear in the logs of the site being visited.

### 3. The Exit Node

The exit node is where your traffic leaves the Tor network and enters the regular internet. It peels off the final layer of encryption and forwards your request to the destination server. From the destination's perspective, traffic is coming from the exit node's IP address — not yours.

This is the most sensitive position in the circuit. The exit node can, in principle, read your traffic if it isn't encrypted with HTTPS — which is why using Tor over HTTP is strongly discouraged. If you're accessing a site over HTTPS, the exit node sees only that an encrypted request was made to a particular domain, not the content of that request.

> **Guard node:** knows who you are, not where you're going. **Middle node:** knows neither. **Exit node:** knows where you're going, not who you are. No single relay holds the complete picture.

---

## 🔐 The Encryption: Three Layers, Removed in Order

When your Tor client constructs a circuit, it performs a separate key exchange with each of the three relays, giving it three distinct encryption keys — one shared with the guard, one with the middle node, one with the exit.

When you send data, your client encrypts it three times: first with the exit node's key, then the middle node's, then the guard's. This creates the nested structure that gives onion routing its name.

- The **guard node** decrypts the outermost layer, revealing the middle node's address and still-encrypted data. It forwards this on.
- The **middle node** decrypts its layer, revealing the exit node's address and still-encrypted data. It forwards this on.
- The **exit node** decrypts the final layer and sends the request — plaintext or HTTPS-encrypted — to its destination.

On the return journey, the process reverses. Each relay adds its layer of encryption as data travels back toward you; your Tor client strips each layer in reverse order.

The cryptography itself uses a combination of **asymmetric cryptography** (RSA or elliptic curve algorithms for the initial key exchange) and **symmetric cryptography** (AES-128 in counter mode for actual data transfer). Symmetric encryption handles bulk data because it's far faster; asymmetric is used only to establish the shared keys securely.

---

## 🧅 .onion Addresses: Hidden Services

So far we've described how Tor anonymises the client. But Tor also provides a mechanism for **servers** to hide their location: **Hidden Services**, accessed via .onion addresses.

A .onion address looks like this: `expyuzz4wqqyqhjn.onion` — a seemingly random string of characters followed by the .onion top-level domain. These aren't registered with any DNS authority. They're **self-certifying**: the address is mathematically derived from the server's public key. If you can connect to a .onion address, you've cryptographically verified you're talking to the server holding that private key — no certificate authority required.

Here's how a Hidden Service works technically:

1. The hidden server generates an asymmetric key pair. The public key is hashed to produce the .onion address.
2. The server picks a set of **Introduction Points** — regular Tor relays it registers with the Tor network's distributed hash table.
3. When a client wants to connect, their Tor client fetches the introduction point information, picks a **rendezvous point** (another relay), and sends a message to the hidden server via an introduction point, proposing the rendezvous relay.
4. The hidden server builds its own circuit to the rendezvous relay, completing the connection. End-to-end encryption is established, and neither party reveals their IP address to the other.

> A .onion address isn't a domain registered with anyone. It's a cryptographic fingerprint. If you reach the address, you've verified the server's identity without trusting a third party.

---

## 🆚 Version 2 vs Version 3 .onion Addresses

Older Hidden Services used **v2 addresses**: 16 characters derived from an 80-bit hash of an RSA-1024 public key. These have been officially deprecated and are no longer supported in current Tor clients, due to increasing viability of attacks against RSA-1024 and the SHA-1 hash function.

Current Hidden Services use **v3 addresses**: 56 characters derived from an **Ed25519** public key using **SHA-3** hashing. The longer address reflects the larger key and stronger cryptographic primitive. V3 addresses also include a version number and checksum within the address itself, making them self-validating.

---

## ⚠️ Tor's Limitations and Attack Vectors

Tor provides strong anonymity against a passive adversary who doesn't control a significant portion of the network. It does not provide perfect anonymity against all threat models.

**Traffic Correlation Attacks**

The most theoretically dangerous attack is traffic correlation: if an adversary controls both the network link you use to enter Tor and the exit node — or can observe both ends of a circuit simultaneously — they can potentially correlate the timing and volume of traffic to link a user to a destination, even without breaking the encryption. The Tor Project acknowledges this limitation; Tor does not protect against a sufficiently powerful global adversary capable of monitoring large portions of the internet simultaneously.

**Malicious Relays**

Anyone can run a Tor relay, which creates a supply chain trust problem. Researchers have periodically identified clusters of malicious relays designed to deanonymise traffic, inject malicious content, or harvest data through unencrypted exit node connections. Guard pinning and universal use of HTTPS significantly reduce exposure.

**Browser Fingerprinting and Operational Security**

Tor protects your IP address. It does not protect against **browser fingerprinting** — identifying users by the unique combination of browser version, installed fonts, screen resolution, time zone, and dozens of other attributes websites can query via JavaScript.

The Tor Browser addresses this by standardising as many of these attributes as possible — all Tor Browser users present the same window size, user agent string, and JavaScript settings. But if a user logs into an account, enables JavaScript on a fingerprinting site, or downloads and opens a file while Tor is running, their real identity can be compromised regardless of the network-level protection.

Law enforcement has historically been more successful at deanonymising dark web users through **operational security (OPSEC) failures** than through breaking Tor's cryptography.

**Exit Node Traffic Visibility**

Exit nodes can read unencrypted traffic. This isn't a flaw — it's an inherent consequence of the design. Tor provides anonymity, not confidentiality of content. The two are separate properties, and HTTPS provides the latter. Using Tor without HTTPS is roughly equivalent to asking your neighbours to post a letter for you without sealing the envelope.

---

## 👥 Who Uses Tor — and Why It Matters

The dark web's reputation as a marketplace for illegal activity is not without basis — there are indeed such marketplaces, and law enforcement agencies regularly investigate and dismantle them. But framing Tor through this lens alone would be like characterising all telephony as a tool for fraud because some criminals use phones.

The Tor Project's own data suggests a significant majority of Tor users are in countries with restrictive internet censorship — accessing blocked news sites, using services unavailable in their region, or communicating in ways their governments don't permit. Journalists in authoritarian states use Tor to communicate with sources. Whistleblowers use **SecureDrop** — a platform that runs as a Tor Hidden Service — to send documents to newsrooms without revealing their identity. Domestic abuse survivors use it to research their situations without leaving a browsing trail.

The cryptographic architecture doesn't distinguish between these use cases. Tor anonymises all traffic equally. Whether that's a feature or a problem depends entirely on who's asking — and from which side of which political context.

---

## Last Orders

- **The dark web** is a subset of the deep web, accessible via overlay networks like Tor — not a separate physical infrastructure
- **Tor** routes traffic through three relays — guard, middle, and exit — wrapping data in three layers of encryption that each relay peels in sequence
- **The guard node** knows your IP but not your destination; **the middle node** knows neither; **the exit node** knows the destination but not your IP
- **Key exchanges** use asymmetric cryptography (RSA or Ed25519) to establish shared keys; bulk data is encrypted with AES-128 in counter mode
- **.onion Hidden Services** allow servers to conceal their location using introduction points and rendezvous relays, with the address derived directly from the server's public key
- **V3 .onion addresses** use Ed25519 keys and SHA-3 hashing, replacing the deprecated v2 RSA-1024/SHA-1 standard
- **Tor does not protect** against traffic correlation attacks, malicious relays, browser fingerprinting, or operational security failures
- **Legitimate uses** are widespread: circumventing censorship, whistleblowing, investigative journalism, and protecting privacy in high-risk environments

The system was designed for anonymity. It achieves it — within limits. Understanding those limits is as important as understanding the mechanism.

*Cheers — and see you in the next one.* 🍺

---

*Missed the previous instalment? Read [Pints, Packets & Protocols: How the Internet Works](/posts/pints-packets-protocols/).*
