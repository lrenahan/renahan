---
title: "The Bar Next Door: How Adversary-in-the-Middle Phishing Steals Your Session, Not Just Your Password"
description: "MFA doesn't stop everything. A technical breakdown of adversary-in-the-middle (AiTM) phishing, reverse-proxy toolkits like Evilginx, session cookie theft, and device code phishing — plus what actually defends against them."
date: 2026-07-26
series: "beer-drinkers-guide"
readtime: "11 minutes"
tags: ["phishing", "aitm", "session-hijacking", "mfa", "identity-security", "device-code-phishing", "cybersecurity"]
youtube_id: ""
youtube_url: ""
---

You've done everything right. Strong, unique password. MFA switched on for every account that offers it. By most advice you've read, you're covered.

There's an attack running at scale right now that walks past both of those controls without breaking either of them. It doesn't guess your password. It doesn't defeat your MFA. It just stands in the middle of the conversation, watches it happen, and takes what comes out the other end.

This is adversary-in-the-middle phishing — AiTM — and if you only know it by the older name, man-in-the-middle, it's worth updating your mental model. The mechanics have moved on.

## 🍺 The Pop-Up Bar Next Door

Picture your usual bar. Now picture someone opening an identical bar right next door this week — same signage, same till receipts, same everything. Except this one isn't actually serving you anything. Every order you place gets carried next door to the real bar, poured for real, and handed straight back. You're drinking real beer. You just don't know there's someone standing in the middle of every transaction.

That's the shape of an AiTM attack. The victim isn't interacting with a crude fake — they're interacting with a proxy that sits between them and the genuine service, passing traffic through in both directions in real time.

## 🛠️ How the Attack Actually Works

Strip away the analogy and the mechanism runs in five steps:

1. **The reverse proxy goes up.** The attacker deploys infrastructure — commonly built with toolkits like Evilginx or Modlishka — that sits between the victim and the real login page. It's not a static clone; it's a live proxy that forwards requests to the genuine site and relays the responses back.
2. **The victim authenticates against the real site.** A phishing link lands the victim on the proxy's domain, which renders the real site's login page almost pixel-for-pixel — because in large part, it *is* the real page, fetched live. The victim enters their username and password, which the proxy forwards straight to the legitimate service.
3. **The MFA challenge is relayed, not defeated.** The real site issues its normal second-factor challenge. The proxy passes this through to the victim too, and the victim completes it genuinely — because as far as their device and the identity provider are concerned, this *is* a real login attempt.
4. **The real site authenticates the session.** Having received valid credentials and a valid MFA response, the legitimate service does exactly what it's supposed to do: it issues a session token, typically delivered as a cookie in the response headers.
5. **The proxy captures the token in transit.** Because the proxy is sitting in the full path of the exchange, it sees that cookie the moment it's issued — before it ever reaches the victim's browser in a form only they control.

> Password theft gets an attacker to the front door. Session token theft gets them past every door in the building, because the session token *is* what "logged in" means to the server from that point forward.

## 🔑 Why the Session Cookie Is the Real Prize

Once authentication succeeds, most web applications don't ask you to prove who you are on every single request — that would be a miserable user experience. Instead, the server issues a session token (usually a cookie, sometimes a bearer token for APIs) and trusts any request that presents it. The login process only has to happen once; the token does the ongoing work.

That's precisely what makes it valuable to steal. With a captured session cookie, an attacker can load it into their own browser — often using an extension or simple cookie-editing tool — and be treated by the application as an already-authenticated user. No password required. No MFA prompt triggered. The identity provider already did its job; the attacker is just borrowing the receipt.

This is also why AiTM defeats MFA without ever attacking MFA directly. Multi-factor authentication verifies identity *at the point of login*. It has no visibility into, and no control over, what happens to the token that login produces afterward. If that token can be lifted in transit, MFA has done its job perfectly and the account is still compromised.

> MFA proves who you are at the door. It has no say over what happens to the pass once you're handed it.

Some session cookies carry protective flags — `HttpOnly` (inaccessible to client-side scripts), `Secure` (only sent over HTTPS), `SameSite` (restricting cross-site sending). These are useful against other attack classes, like cross-site scripting, but they don't stop AiTM: the proxy isn't reading the cookie via a script or a cross-site request, it's sitting directly in the legitimate request/response path where the cookie is issued in the first place.

## 🕵️ The Other Route In: Device Code Phishing

There's a second technique worth understanding, because it achieves the same outcome — a stolen, authenticated session — without needing any proxy infrastructure at all.

Some authentication flows are built for devices with no convenient way to type a password, like smart TVs, streaming boxes, or command-line tools. This is the OAuth 2.0 **device authorization grant**. The device displays a short code and asks the user to visit a URL on a separate device — usually their phone — and enter that code to approve the login.

Device code phishing abuses this legitimate flow directly:

1. The attacker initiates a device code login themselves, against a real service, and obtains a valid code.
2. The attacker sends that code to the target — by text, email, or a fake IT helpdesk call — framed as something routine: a verification step, a support process, a sync request.
3. The victim, believing this is a normal part of their day, visits the real login page and enters the code.
4. The identity provider completes the authorization — for the *attacker's* session, approved by the *victim's* credentials.

No fake domain. No reverse proxy. No suspicious URL to spot, because the victim never leaves the genuine site. They're simply persuaded to approve a login that isn't theirs. It's the same end state as AiTM — a valid, authenticated session in the attacker's hands — reached through a social engineering step instead of a technical proxy.

> No pop-up bar required this time. Just someone asking you to hand the wristband over directly, because it looked like part of the normal process.

## 🛡️ What Actually Defends Against This

Because both techniques route around traditional MFA rather than through it, the effective mitigations focus on the session and the authentication *method*, not just adding more factors:

- **Phishing-resistant authentication (FIDO2 / passkeys).** These bind the credential cryptographically to the legitimate origin domain. There's no code or one-time password to relay, because the authentication ceremony itself checks it's talking to the real site — a proxy on a different domain simply fails the check.
- **Token binding / continuous access evaluation.** Tying a session token to signals like device identity, IP range, or client fingerprint means a token lifted from one context doesn't work cleanly in another. Microsoft Entra's Continuous Access Evaluation and similar controls in other identity platforms are built specifically to catch this class of theft.
- **Conditional access policies that evaluate post-authentication, not just at login.** Flagging impossible travel, unfamiliar device fingerprints, or anomalous request patterns *after* a session is established closes some of the gap MFA leaves open.
- **Restricting and monitoring device code flows.** Many identity providers allow device code authentication to be disabled entirely for accounts that don't need it, removing that route as an option.
- **User habits that still matter.** Checking the actual domain before entering credentials, and treating any unexpected request to "enter this code" or "approve this sign-in" with suspicion — even when it isn't accompanied by a dodgy-looking link.

None of these are a single silver bullet, and that's the point worth taking away: AiTM and device code phishing both succeed by targeting the *session*, not the *credential*, so defenses aimed only at strengthening the credential check — however many factors deep — leave that layer untouched.

## 🍻 Last Orders

- AiTM phishing uses a live reverse proxy (Evilginx, Modlishka, and similar toolkits) to relay real login traffic between victim and legitimate site.
- Because the victim completes a genuine login, including MFA, the attacker never needs to defeat authentication — they capture the session cookie issued afterward.
- Session cookies typically aren't protected against this by `HttpOnly`, `Secure`, or `SameSite` flags, since the proxy sits in the legitimate request path rather than accessing the cookie via script or cross-site request.
- Device code phishing abuses the OAuth device authorization grant flow, tricking a victim into approving a login on the attacker's behalf — no proxy or fake domain needed.
- MFA verifies identity at login; it has no control over the session token issued after, which is exactly the gap both techniques exploit.
- Effective defenses target the session and the authentication method itself: phishing-resistant passkeys, token binding, continuous access evaluation, and restricting device code flows.

*Cheers — and see you in the next one.*

---

**Related reading:** if session security has you thinking about how your traffic gets protected in transit more broadly, the previous post in this series — [VPNs Explained](/posts/vpns-explained/) — covers how encrypted tunnels work and where they do (and don't) protect you.
