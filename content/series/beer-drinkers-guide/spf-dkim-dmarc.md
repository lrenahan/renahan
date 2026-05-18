---
title: "Is That Actually ABC Beer? SPF, DKIM & DMARC — Explained Over a Pint"
description: "How email authentication works — and why your inbox depends on it. Three standards, one pub analogy, zero jargon."
date: 2025-05-01
series: "beer-drinkers-guide"
readtime: "~10 min read"
tags: ["email", "spf", "dkim", "dmarc", "authentication", "explainer"]
youtube_id: "0TJm0Hw9NPw"
youtube_url: "https://www.youtube.com/watch?v=0TJm0Hw9NPw"
---

You walk into a pub and spot a discount on your favourite beer. Brilliant. But before you dive in, a nagging question: is that actually ABC Lager in the glass, or has the landlord switched the kegs? Email works exactly the same way. And billions of fraudulent messages every day are banking on the fact that you won't check.

This post is about email authentication — specifically the trio of standards that let a recipient verify that a message really did come from who it claims. Those standards are **SPF**, **DKIM**, and **DMARC**. We're going to explain all three using the oldest analogy in the world: ordering a pint.

Two fictional breweries will help us along the way: **ABC Beer**, the world's greatest lager, and **XYZ Beer**, a cheaper-than-supermarket imitation that a dodgy landlord might try to pass off as the real thing. And two technical identifiers that map onto our analogy — the **envelope sender** (RFC5321.MailFrom, the address on the outside of the letter) and the **body sender** (RFC5322.From, the name you actually see in your mail client).

> *Crucially, we're not scrutinising what's inside the glass. This is entirely about whether you can trust it came from where it says it did.*

---

## Part One: Is This Pub Allowed to Sell ABC Beer?

### The Analogy

Before you even raise the glass to your lips, there's a basic question worth asking: is this establishment authorised to sell ABC Beer at all? Reputable brewers publish a public list of every venue licensed to stock and serve their products. If the pub you're in isn't on that list, the beer almost certainly isn't genuine — full stop.

### The Email Equivalent: SPF

**SPF — Sender Policy Framework** — works exactly like that authorised venues list. It allows the owner of a domain to publish, in their DNS, a list of the mail servers they permit to send email on their behalf.

When an email arrives at your inbox, the receiving server performs a DNS lookup for the sending domain and checks whether the IP address that delivered the message appears on that approved list. If it does, SPF passes. If not, the receiving server can reject or flag the message according to the policy the domain owner set.

**Example SPF Record — abc.com**

```
v=spf1 ip4:1.1.1.1 ip4:2.2.2.2 include:thirdpartymailer.com -all
```

This tells receiving servers: only `1.1.1.1`, `2.2.2.2`, and servers listed by `thirdpartymailer.com` are authorised to send mail as abc.com. The `-all` at the end means hard fail — anything else should be blocked.

The `include:` mechanism is particularly elegant: if a third-party mailing service adds new servers to their pool, ABC's SPF record automatically reflects that, without ABC needing to update anything.

> *SPF only validates the envelope sender — the technical address used during mail delivery, not necessarily the "From" name you see in your email client. Just because the pub is authorised to sell the beer doesn't guarantee the liquid in your glass is the genuine article.*

This is also how organisations legitimately allow third parties — marketing platforms, CRM tools, ticketing systems — to send email on their behalf. The third party uses their own envelope sender, but SPF proves they're an authorised agent. And it's precisely the gap that bad actors exploit when spoofing a brand: the envelope says one thing, the visible sender says another.

---

## Part Two: Are the Kegs Genuine and Untampered?

### The Analogy

Your pub is on the approved list. The beer arrives in the right branded glassware. You can even see the ABC keg under the bar, plumbed into the correct tap. But a particularly crafty landlord could still be running XYZ through the line while the branding says otherwise. What you need is a way to verify that the beer in the keg is the exact beer ABC brewed — and that nobody has tampered with it since it left the brewery.

Fortunately, ABC designs their kegs with proprietary connectors that only fit their own taps, and applies tamper-evident seals. If anyone tries to interfere with the contents, it shows.

### The Email Equivalent: DKIM

**DKIM — DomainKeys Identified Mail** — is that tamper-evident seal. When an email leaves the sending server, DKIM generates a cryptographic hash of the message contents and signs it using a private key held by the sending organisation. That signature travels with the email in its headers.

The sending domain also publishes the corresponding *public* key in DNS. When the receiving server gets the message, it retrieves that public key and uses it to verify the signature. If the hash matches, two things are confirmed: the email was sent by a server with access to the private key, and nothing in the message has been altered in transit.

**Example DKIM DNS Record — abc.com**

```
selector1._domainkey.abc.com  TXT  "v=DKIM1; k=rsa; p=MIGfMA0GCS..."
```

The *selector* (here: `selector1`) allows an organisation to rotate keys or use multiple signing configurations simultaneously. The receiving server reads the selector from the email's DKIM header to know which DNS record to look up.

Unlike SPF, DKIM validates the *body sender* — the domain visible in the "From" field of the email. This makes it a more direct authentication of the brand the recipient actually sees.

> *If SPF proves the pub can sell the beer, DKIM proves the beer in the keg is genuine and hasn't been watered down since it left the brewery.*

---

## Part Three: Is the Beer in the Glass the One on the Tap?

### The Analogy

SPF and DKIM are both running independently. But here's the residual problem: a landlord could have an authorised ABC tap, with a genuine ABC keg, and still serve you a pint in an XYZ glass. Or pour genuine ABC beer into a generic pint glass while the menu advertises something else entirely. Each check passes in isolation, but the end-to-end story doesn't add up.

What you need is a single mechanism that ties all the checks together — and ensures the beer in the glass, the branding on the glass, and the label on the keg are all telling the same story.

### The Email Equivalent: DMARC

**DMARC — Domain-based Message Authentication, Reporting and Conformance** — is that final check. It takes the results of both SPF and DKIM, and adds one critical requirement: *alignment*.

Alignment means the domain used in the envelope sender (SPF) or the DKIM signing domain must match the visible "From" domain (the body sender). A bad actor can't pass a legitimate SPF check on one domain while displaying a completely different brand in the "From" field. Both need to tell the same story.

**Example DMARC Record — abc.com**

```
_dmarc.abc.com  TXT  "v=DMARC1; p=reject; rua=mailto:reports@abc.com; ruf=mailto:forensics@abc.com"
```

The `p=` value defines the policy. Three options are available:

| Policy | Behaviour |
|---|---|
| `none` | Monitor only — messages pass regardless. Used for initial deployment and visibility. |
| `quarantine` | Failing messages go to junk/spam. A useful stepping stone. |
| `reject` | Failing messages are blocked outright. Full enforcement. |

For DMARC to pass, at least one of the following must be true — and the domains must align:

- SPF passes *and* the envelope sender domain aligns with the From domain
- DKIM passes *and* the signing domain aligns with the From domain

> *DMARC is the check that the beer in the glass, the keg it came from, and the branding on both all agree. No more mixing genuine kegs with counterfeit glasses.*

---

## The Feedback Loop: DMARC Reporting

There's one more feature that makes DMARC genuinely powerful beyond enforcement: **reporting**.

DMARC supports two types of reports, sent to addresses defined in the DNS record. **Aggregate reports** (rua) provide regular summaries — which servers sent mail claiming to be your domain, how many messages passed or failed, and from which IP addresses. **Forensic reports** (ruf) provide message-level detail when failures occur.

Imagine every beer glass in every pub being able to send a message back to the brewery telling it what was poured into it. The brewery would quickly build a map of every venue serving their beer — authorised or not — and could take action accordingly. That's what DMARC reporting does for an email domain owner.

This feedback loop is how organisations discover shadow IT sending email in their name, identify legitimate third-party senders they hadn't configured properly, and build the confidence needed to move from a `p=none` monitoring policy to full `p=reject` enforcement.

---

## How the Three Work Together

| Standard | What it checks | Sender it validates | The pub analogy |
|---|---|---|---|
| **SPF** | Is the sending server on the authorised list? | Envelope sender (RFC5321.MailFrom) | Is this pub licensed to sell ABC Beer? |
| **DKIM** | Is the message genuine and untampered? | Body sender (RFC5322.From) | Is the keg genuine and the seal unbroken? |
| **DMARC** | Do SPF/DKIM pass, and do the domains align? | Both — alignment required | Does the glass, the keg and the tap all agree? |

Each standard addresses a different layer of trust. SPF secures the delivery path. DKIM secures the content and signs the visible brand. DMARC enforces alignment and closes the gap that would otherwise let an attacker mix and match passing components to fool a recipient.

When all three are properly configured with a `p=reject` DMARC policy, it becomes very difficult for an external attacker to send email that convincingly impersonates your domain. The beer in the glass really is ABC Beer — and you have the cryptographic receipts to prove it.

---

## Last Orders: What We Covered

- **SPF** lets a domain owner publish a list of authorised sending servers — like a brewery's list of licensed pubs. It validates the envelope sender only.
- **DKIM** uses cryptographic signing to prove a message is genuine and unaltered — like a tamper-evident seal on a keg that only fits the right tap.
- **DMARC** ties SPF and DKIM together, requiring both the checks and the domain alignment to pass — ensuring the glass, keg, and tap all tell the same story.
- DMARC offers three policies: **none** (monitor), **quarantine** (junk folder), and **reject** (block entirely).
- DMARC **reporting** sends aggregate and forensic data back to the domain owner, creating a feedback loop that enables safer enforcement over time.
- The envelope sender and body sender can be *different things* — legitimately, and maliciously. DMARC's alignment requirement is what closes that gap.

---

*Cheers — and see you in the next one.* 🍺
