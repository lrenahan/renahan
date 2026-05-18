---
title: "Pints, Privacy & Peach IPAs"
description: "How VPNs work — explained over a beer. What a VPN actually does, what it doesn't do, and how to cut through the marketing noise."
date: 2025-04-10
series: "beer-drinkers-guide"
readtime: "~8 min read"
tags: ["vpn", "privacy", "networking", "encryption", "explainer"]
youtube_id: "GuWrVmkcFI"
youtube_url: "https://www.youtube.com/watch?v=GuWrVmkcFI"
---

*Welcome to The Service Provider Arms — where every pint tells a story. Today's tale? How VPNs work, told through the noble art of ordering beer.*

You might already know what a VPN is — a Virtual Private Network — but if someone asked you to explain it in plain English, you'd probably wave your hand vaguely at the air and say "something to do with privacy." That's fair. The technology is genuinely useful but routinely explained like a GCSE textbook. So let's fix that.

Pull up a stool. We're going to the pub.

## The Open Bar Problem: Browsing Without a VPN

Normally, when you browse the internet, it's a bit like shouting your drink order across the bar. Your request travels through public networks — your ISP, DNS servers, various routers — and anyone with an ear to the wall can hear exactly what you're asking for.

The bartender hears it. The CCTV logs it. The bloke next to you — the one who only drinks Guinness and thinks IPAs are for cowards — hears it too. That's your internet traffic: raw, exposed, and quietly judged.

Your ISP can see every site you visit. Advertisers track your movements. On unsecured public Wi-Fi — say, your local Wetherspoons — anyone on the same network with the right tools can potentially intercept your traffic. It's not paranoia. It's just how the open internet works.

## The Private Tunnel: What a VPN Actually Does

A VPN creates a private, encrypted tunnel between your device and a server somewhere else in the world. Instead of shouting your order across the bar, you lean in close and whisper it through a soundproof tube. Nobody outside the tunnel can hear a word.

Say you want to order a Fluffy Peach IPA. Without a VPN, that request goes out in plain sight. With a VPN, it disappears into the tunnel — and before it even reaches the other end, it's been scrambled into gibberish.

> *"Fluffy Peach IPA" becomes "X7$!@#%&n" and no one's decoding that without a PhD in cryptographic linguistics and a lot of free time.*

That encryption is provided by protocols like OpenVPN, WireGuard, or IKEv2. The specifics differ, but the principle is the same: your data is scrambled in a way that only the VPN server can unscramble, using keys that are never transmitted in the open.

## The Bartender Proxy: IP Masking

Here's where it gets interesting. Once your order travels through the tunnel, it's the bartender — the VPN server — who places the actual request on your behalf. To the outside world, it looks like the bartender asked for the drink, not you.

In networking terms, this is called **IP masking**. The website or service you're connecting to only sees the VPN server's IP address, not yours. Your real location stays hidden. As far as anyone can tell, you could be ordering from London, Tokyo, or Timbuktu — depending on which server you're connected to.

This is how people use VPNs to bypass geo-blocks: connecting to a server in the US makes streaming services think you're American. Connecting via a server in Germany lets you access content locked to that region. The bartender orders on your behalf, and nobody knows where you're actually sitting.

Even your ISP — the pub's manager, if you like — can't see what you ordered. They know you entered the tunnel. They just can't see what's inside it.

## Watch the Gaps: DNS Leaks

A VPN isn't foolproof. One common vulnerability is called a **DNS leak** — and it's exactly as undignified as it sounds.

Remember DNS from last time? It's the directory that translates "www.example.com" into an IP address. If your DNS requests slip outside the encrypted tunnel — even when everything else is inside it — it's like whispering your order through the tube, then shouting the delivery address at full volume.

A good VPN routes DNS queries through the encrypted tunnel too, closing that gap entirely. When evaluating a VPN service, "DNS leak protection" is one of the things worth checking. You can also test it yourself with free tools like [dnsleaktest.com](https://dnsleaktest.com).

## Free Pints Are Never Free: Choosing a VPN

Of course, VPNs aren't magic. You still pay the tab, one way or another.

Some VPNs are free. But as the saying goes, if you're not paying for the product, you might be the product. Free VPN providers have been caught logging user activity, injecting adverts, and — in some cases — selling browsing data to third parties. That's the VPN equivalent of watering down your beer and reporting your order to the nosy Guinness bloke anyway.

Reputable paid VPNs — the kind that charge a few pounds a month — typically offer:

- A strict no-logs policy (independently audited, ideally)
- DNS leak protection built in
- A **kill switch**: if the VPN connection drops, your traffic stops entirely rather than leaking into the open
- Servers in multiple countries for geo-flexibility
- Modern encryption protocols like WireGuard

Well-reviewed options include Mullvad, ProtonVPN, and ExpressVPN — though the market moves fast, so check recent independent reviews before committing.

## Five Ways to Describe VPN Marketing (Without Crying)

The VPN industry is not exactly renowned for its restraint. Here are five sarcastic-but-accurate takes on how VPNs get sold to us:

**"Stay safe on public Wi-Fi!"** — Yes, the same public Wi-Fi that's been quietly logging your Netflix binge since 2019. A VPN helps here. The $9.99/month VPN sponsored by every podcast in existence may or may not.

**"Hackers HATE this one weird trick!"** — Hackers are largely indifferent to your VPN, actually. They've moved on to phishing your password directly. But yes, encrypting your traffic is still sensible.

**"Unlock Netflix libraries from around the world!"** — True, until Netflix patches the specific IP ranges the VPN uses. Then your provider releases a new server. Then Netflix blocks that. It's a dance.

**"Complete anonymity online!"** — A VPN hides your IP from websites. It doesn't stop you logging into your Google account and handing over your life story willingly. True anonymity is considerably harder.

**"Military-grade encryption!"** — The military uses AES-256. So does your banking app, your messaging app, and most modern websites. Using the word "military" is doing a lot of lifting for what is essentially standard practice.

## When Should You Actually Use a VPN?

A VPN is a useful tool when used for the right reasons. Here's where it genuinely earns its keep:

- **Public Wi-Fi** — airports, cafes, hotels. Encrypting your traffic on shared networks is just common sense.
- **Accessing region-restricted content** — streaming libraries, sports broadcasts, or services unavailable in your country.
- **Protecting your activity from your ISP** — in some countries, ISPs are legally permitted to sell browsing data to advertisers. A VPN prevents that.
- **Remote work** — many companies route employee traffic through a corporate VPN to keep business data inside a secure perimeter.
- **Travelling to countries with heavy internet censorship** — VPNs can provide access to services that would otherwise be blocked.

> *Where it won't save you: clicking on phishing links, using weak passwords, or logging into your personal accounts on a device you don't trust. A VPN protects the tunnel. It doesn't protect you from yourself.*

## Last Orders: What We Covered

- Browsing without a VPN is like shouting your order across a crowded bar — your ISP, DNS servers, and anyone listening can hear you.
- A VPN creates an encrypted tunnel, scrambling your data so eavesdroppers only hear gibberish.
- IP masking means websites see the VPN server's address, not yours — handy for geo-blocks and privacy alike.
- DNS leaks are the gap to watch: good VPNs route DNS through the tunnel too.
- Free VPNs can water down your beer. Paid ones with audited no-logs policies are worth the few quid.
- VPN marketing is theatrical. The tech beneath it is genuinely useful — when applied to the right problems.
- A VPN protects the tunnel. It doesn't protect you from clicking on dodgy links.

---

*Cheers to encrypted embarrassment. See you in the next one.*
