---
title: "The Beer Drinker's Guide to Email Threats"
description: "Phishing, malware, invoice fraud, BEC and more — explained using pub analogies, with the technical detail the video couldn't fit."
date: 2026-06-19
series: "beer-drinkers-guide"
readtime: "~12 min read"
tags: ["cyber security", "email security", "phishing", "malware", "explainer", "DMARC", "ransomware", "BEC"]
youtube_id: "QiuAgMpqMec"
youtube_url: "https://www.youtube.com/watch?v=QiuAgMpqMec"
---

*Read time: ~12 minutes | Series: Tech Behind the Bar*

Your inbox is basically a dodgy pub.

A cosy, familiar place where you just want a quiet pint and maybe a packet of crisps. But instead, it's full of strangers trying to sell you things, steal your things, or convince you to do something catastrophically stupid.

The video covers the pub analogies. This post goes a layer deeper — keeping the same metaphors but pulling back the curtain on how these attacks actually work, why they're so effective, and what's happening technically when someone falls for one. Think of it as the extended cut, with footnotes.

---

## 🎣 Phishing: The Fake Free Pint

The bloke in the corner is shouting about free beer. The pint's in a bucket labelled "BEER — TRUST ME." You know the story.

What the video doesn't cover is *how he built the bucket*.

A phishing email works because it successfully impersonates a trusted sender. Attackers do this in a few ways:

**Domain spoofing** is the bluntest approach — sending an email where the visible "From" name says *Barclays Bank* but the actual sending address is something like `no-reply@barclays-secure-update.net`. Most email clients hide the full address by default, which is exactly what attackers rely on. Look past the display name and check the actual domain. If it doesn't match the organisation's real domain precisely, it's fake.

**Lookalike domains** are more sophisticated. Rather than spoofing an address, the attacker registers a real domain that's close enough to the genuine one to fool a distracted glance — `barclays-security.com`, `barcIays.com` (that's a capital i, not a lowercase L), or `barclays.co.uk.account-verify.com` (the actual domain here is `account-verify.com`; everything before it is just a subdomain). These pass basic checks because they *are* real domains sending real emails — just not from who they claim to be.

**Credential harvesting pages** are where the damage gets done. The link in the email goes to a page that looks exactly like your bank's login screen — same fonts, same layout, same logo, sometimes even the same URL structure. You type your username and password. The page either shows an error ("please try again") or silently redirects you to the real site. Either way, your credentials are already gone.

The technical defence for organisations is a trio of email authentication standards: **SPF** (Sender Policy Framework), **DKIM** (DomainKeys Identified Mail), and **DMARC** (Domain-based Message Authentication, Reporting and Conformance). Together they let receiving mail servers verify that an email claiming to be from `barclays.com` was actually sent from Barclays' infrastructure — and reject or flag it if not. If you run a domain, having all three configured correctly is non-negotiable. If you *receive* emails, these standards are what your email provider uses in the background to filter your spam folder.

**The tell:** legitimate organisations will never ask for your password via email. And if you're ever unsure about a link, go directly to the website by typing the address yourself rather than clicking through.

---

## 🎯 Spear Phishing: The Personalised Pint

The barman knows your name, your usual, and your recent LinkedIn activity. That's not magic — that's open-source intelligence (OSINT).

Before a spear phishing attack lands in your inbox, the attacker has typically spent time on reconnaissance. They might check your LinkedIn profile for your job title, your manager's name, and the tools your company uses. They'll look at your company's website for org chart clues, press releases, and supplier names. They'll scan job listings (which helpfully announce what software stack you're running). They might even scrape data from previous breaches — your email address and an old password, enough to make a message feel eerily familiar.

The resulting email references real things: a genuine project name, a colleague, an upcoming deadline. It arrives from an address that looks like your CEO's, or a supplier you actually deal with. It asks for something plausible — a file, a payment, a login.

This is why security awareness training that says "look for bad spelling and generic greetings" is only half the story. A well-crafted spear phish is grammatically perfect and disturbingly specific. The red flags are subtler: unexpected urgency, a request that bypasses normal process, or a slight mismatch in the sender's address.

**Whaling** is spear phishing aimed at senior leadership — CFOs, CEOs, board members. High-value targets because they have authority to approve large transactions and often receive less day-to-day security scrutiny than junior staff. The FBI estimates BEC and whaling attacks (which often overlap) have cost businesses globally over $50 billion since 2013.

---

## 💀 Malware: The Pint That Ruins Your Life

You accepted the drink. Here's what's actually in it.

"Malware" is a catch-all term — the interesting bit is the delivery mechanism and what it does once it's running.

**Viruses** are the oldest variety: self-replicating code that attaches itself to legitimate files and spreads when those files are shared. Less common now as delivery methods have evolved, but still present in macro-enabled Office documents (more on those shortly).

**Ransomware** has become the dominant threat to organisations over the past decade. Once executed, it typically does three things in quick succession: maps your network to find connected drives and shared storage, exfiltrates a copy of your files to the attacker's infrastructure (useful for extortion even if you restore from backups), then encrypts everything in place and drops a ransom note. Modern ransomware is often delivered as a service — criminal groups license the malware to affiliates who handle the attacks, taking a percentage of each ransom paid. The average ransom demand for businesses now runs into tens or hundreds of thousands of pounds, and that's before you factor in downtime and recovery costs.

**Spyware and keyloggers** sit silently and record. A keylogger captures every keystroke — meaning every password you type, every message you send, every search you make is forwarded to the attacker. Credential-stealing spyware often targets browser-stored passwords specifically, since most people let their browser remember logins for everything.

**Trojans** are malicious code disguised as something useful — a software update, a PDF viewer, a game crack. Unlike a virus, a Trojan doesn't replicate itself; it just sits there, waiting to be opened, at which point it executes its payload: downloading further malware, opening a backdoor, joining your machine to a botnet.

One important point the pub analogy glosses over: most malware doesn't require you to *run* anything. Modern attacks exploit **zero-day vulnerabilities** — unpatched security flaws in software — that allow code execution just from opening a document or visiting a page. Keeping your operating system and software updated isn't optional admin; it closes the holes that malware walks through.

---

## 🧾 Invoice Fraud: The Mystery Bill

The Unicorn Lager bill looks real. That's the point.

Invoice fraud works because it exploits a process — the payment workflow — rather than a technical vulnerability. There's no malware involved. Just a convincing document and a distracted human.

The most common variant targets businesses with a simple technique: the attacker identifies a genuine supplier relationship (often from publicly available information, or a compromised email account), then sends an email impersonating that supplier announcing that their bank details have changed. Please update your records. Here's the new account number. Thanks for your continued business.

The email goes to someone in finance who genuinely does process invoices from that supplier. The amount on the next invoice is exactly what they'd expect. The only difference is where the money goes.

More sophisticated versions involve **man-in-the-middle email compromise**: the attacker gains access to either the supplier's or the buyer's email account, monitors ongoing invoice threads, and intercepts at the right moment — replacing real payment details with their own, sometimes mid-conversation. The thread looks legitimate because it *is* the legitimate thread.

Defences here are procedural rather than technical: a standing policy to verify *any* change to payment details via a phone call to a known number (not a number provided in the email), and a second-signatory requirement for payments above a certain threshold. Boring, bureaucratic, and extremely effective.

---

## 🧔 Business Email Compromise (BEC): The Fake Landlord

The fake landlord doesn't need malware or a clever domain. He just needs to sound plausible and create enough urgency that you don't stop to question it.

BEC is remarkably low-tech for something so costly. The attack typically involves either a spoofed or compromised email account belonging to a senior person in the organisation — often the CEO or CFO — and a request that creates time pressure: an urgent payment, a confidential acquisition, a regulatory deadline. The message explicitly asks the recipient not to use normal channels ("don't run this through the usual process — this is sensitive") which is itself the biggest red flag.

What makes BEC particularly effective is **pretexting** — the attacker constructs a believable backstory that makes the unusual request seem logical. The CEO is travelling and can't do this through the normal system. The acquisition is confidential and finance can't know yet. The supplier is threatening to pull the contract if payment isn't received today.

There's also a growing variant using **AI-generated voice and video**. Deepfake technology has now advanced to the point where attackers have successfully impersonated executives on video calls — the employee thinks they're on a Teams call with their CFO. This is rare but not theoretical; documented cases exist of organisations losing millions this way.

The procedural defence is the same as invoice fraud: any request that bypasses normal financial controls, regardless of who it appears to come from, gets verified through a separate channel before action is taken.

---

## 📎 Attachment Malware: The Suspicious Pie

The foil wrapper is a file extension. Here's what's worth knowing about what's inside various types of pie.

**Executable files** (`.exe`, `.msi`, `.bat`, `.cmd`) are the obvious ones — most organisations now block these at the email gateway. Attackers know this, which is why they've moved on.

**Macro-enabled Office documents** (`.docm`, `.xlsm`) are more insidious. Microsoft Office documents can contain macros — essentially small programs — that run when you open the file. For years, attackers have used these to download and execute malware, which is why modern versions of Office open documents in Protected View by default and require you to explicitly "Enable Content" to run macros. That "Enable Content" button is the moment of compromise. Never click it on a document you weren't expecting.

**Archive files** (`.zip`, `.rar`, `.7z`) are used to smuggle past email filters that scan attachments for known malware signatures. The malicious payload is compressed, sometimes password-protected (the password is conveniently in the email body, so the scanner can't unzip it but you can), and extracted once you've downloaded it.

**ISO and IMG files** are a newer favourite. They're disk image files that, when opened on Windows, mount as a virtual drive — bypassing certain Windows security checks (specifically the Mark of the Web, which flags files downloaded from the internet) because the contents appear to originate from a local drive. Effective precisely because most users have never heard of them.

A broader point: email gateway filtering, antivirus, and endpoint detection tools are playing a constant catch-up game with attachment-based malware. Signature-based detection only catches *known* malware. Behaviour-based detection is better but not perfect. Human scepticism about unexpected attachments is the most reliable first line of defence.

---

## 📱 QR Code Phishing (Quishing): Scan for Free Beer

QR codes are, technically, just a way of encoding a URL in a format a camera can read. The security problem is that the URL is completely opaque until you've already scanned it.

Email security gateways are built to scan links — they inspect URLs, check them against threat databases, and follow redirects to see where a link actually goes. A QR code embedded in an email as an image bypasses all of that. The gateway sees a JPEG. It has no idea there's a URL hidden in the pattern of black and white squares.

The attacker embeds the QR code in what looks like an MFA notification, a shared document alert, or a payroll update. You scan it on your phone — which almost certainly has fewer security controls than your work laptop — and land on a credential harvesting page.

The phone dimension matters. Work devices often have mobile device management (MDM) software, secure DNS, and corporate VPN. Personal phones scanning a QR code from a work email are likely to have none of these. The attacker has neatly sidestepped your organisation's entire email security stack.

Defences: some modern email security platforms now render QR codes and inspect the underlying URL. But the more practical control is awareness — treat a QR code in an email with exactly the same suspicion you'd give an unfamiliar link, because that's all it is.

---

## 🦺 Social Engineering: "I'm From the Brewery"

Dave in a hi-vis jacket is exploiting something that no technical control fully addresses: the human instinct to be helpful, avoid conflict, and defer to apparent authority.

Social engineering as a discipline predates computers entirely. What's changed is the scale and the research tools available. An attacker preparing a vishing (voice phishing) call against your IT helpdesk will have looked up your company's ticketing system from job listings, found the names of IT staff from LinkedIn, identified recent joiners (who are more likely to have legitimate IT requests), and rehearsed a plausible scenario. The call will reference real internal details. It will create urgency. It will ask the helpdesk agent to do something they're technically permitted to do — like reset a password — for someone they can't actually verify.

This is why **identity verification procedures** matter. Not just "do you know the ticket number" but out-of-band verification — calling back on a number held in the directory, not a number the caller provided. And why **least privilege** matters in system design: if a compromised account can only access what that specific person needs for their job, the damage from a successful social engineering attack is contained.

The psychological mechanisms being exploited are well-documented — Robert Cialdini's principles of influence (authority, urgency, social proof, liking, scarcity, reciprocity) map almost exactly onto the techniques social engineers use. Understanding that these are deliberate levers being pulled is itself a meaningful defence.

---

## 📬 Spam: The Noticeboard of Nonsense

Spam is worth a slightly more technical look because understanding how spam filters work helps explain why they occasionally fail.

Modern spam filtering uses a combination of techniques. **Reputation scoring** tracks the sending IP address and domain — new domains and IPs with no sending history are automatically suspicious. **Content analysis** looks for known spam phrases, suspicious link patterns, and unusual formatting. **Bayesian filtering** uses statistical models trained on known spam and legitimate email to classify new messages. **Sender authentication** (SPF, DKIM, DMARC as above) verifies that the sender is who they claim to be.

Spammers have adapted. They use legitimate cloud platforms (SendGrid, Mailchimp, AWS SES) to inherit good sending reputations. They rotate domains constantly. They use image-based content to avoid content scanning. They slowly "warm up" new sending infrastructure by starting with low volumes of legitimate-looking email before switching to spam.

The practical upshot: spam filters are very good and occasionally wrong in both directions. A legitimate email lands in your junk folder. A carefully crafted phishing email lands in your inbox. Neither outcome is a failure of the technology so much as evidence that determined adversaries keep evolving.

---

## 🔬 Under the Hood: How Email Actually Works

One thing the video doesn't cover — and that helps make sense of all the above — is the basic mechanics of how email is sent and received, because several of the attack vectors only make sense once you understand how surprisingly trusting the email system is.

Email runs on a protocol called **SMTP** (Simple Mail Transfer Protocol), which dates to 1982. In its original design, there was essentially no authentication — any mail server could claim to be sending email from any address. The internet was a small, trusted community of academics and researchers; the idea of adversarial use wasn't on the design brief.

This is why spoofing a sender address is, technically, trivially easy. You're not hacking anything — you're using the protocol exactly as designed, just dishonestly. SPF, DKIM, and DMARC are retrofitted authentication layers built *on top of* SMTP specifically to address this gap, added decades after the protocol was designed. They work well when properly implemented, but implementation is inconsistent across the internet, and many domains still don't have all three configured correctly.

When you send an email, it travels through a chain of mail servers — your outgoing mail server hands it to the recipient's mail server, which delivers it to their mailbox. Each hop is logged in the email's **headers**, which are normally hidden but contain a detailed trail of the email's journey including originating IP addresses, timestamps, and server names. If you're ever trying to determine whether a suspicious email is genuine, viewing the full headers (available in every email client) is where you start.

---

## 🛡️ How to Stay Safe: The Pub Rules, With Reasons

The rules are simple. Here's why each one works.

**Verify before you act.** The entire BEC and invoice fraud playbook depends on the victim not picking up the phone. A 30-second call to a known number breaks the attack completely. The cost of the call is always lower than the cost of not making it.

**Check the sender's actual email address.** Display names are cosmetic. The sending domain is harder to fake convincingly at scale. Get into the habit of looking at the full address, not just the name. On mobile, this usually means tapping the name to expand it.

**Treat urgency as a red flag.** Urgency is a cognitive shortcut attacker deliberately engineer. When a message creates time pressure, that pressure is doing the work of preventing you from thinking clearly. Slow down. Verify through a different channel.

**Keep software updated.** Unpatched vulnerabilities are how malware executes without you clicking anything. Operating system and application updates are frequently security patches. The update you've been ignoring for three weeks might be the one that matters.

**Enable multi-factor authentication (MFA).** If a phishing attack does successfully harvest your credentials, MFA is the next barrier. The attacker has your password but not your phone. It's not undefeatable — real-time phishing proxies can capture MFA tokens — but it blocks the vast majority of credential-based attacks and raises the cost and complexity of the rest significantly.

**Use a password manager.** One underappreciated benefit: password managers autofill credentials based on the exact domain. If you're on a convincing lookalike of your bank's website, your password manager won't autofill — because it knows the domain doesn't match. That failed autofill is itself a warning.

---

## Last Orders

Email threats aren't mysterious. They're a combination of technical exploitation and social manipulation, and they work because email is an old, trusting protocol used by billions of people who are frequently distracted.

- **Phishing** exploits domain spoofing and lookalike infrastructure to harvest credentials — countered by sender authentication standards (SPF, DKIM, DMARC) and human scepticism
- **Spear phishing** adds OSINT-based personalisation to make attacks plausible; the tells are subtler but still present
- **Malware** exploits file handling, macro execution, and unpatched software vulnerabilities — keep everything updated and be suspicious of unexpected attachments
- **Invoice fraud and BEC** are procedural attacks that bypass technology entirely — the defence is verification policy, not a firewall
- **Quishing** routes around email security gateways by hiding URLs in images
- **Social engineering** exploits cognitive biases and human helpfulness — awareness of the techniques being used is a genuine defence
- **Spam** is mostly noise managed by increasingly sophisticated filtering, but the occasional targeted email hides within it

The email system was designed for trust. Attackers have spent forty years learning how to exploit that. The defences — technical and human — are retrofitted and imperfect. Which means the most reliable control is still a sceptical mind and a willingness to pick up the phone.

Stay sharp. Verify everything. And for the love of hops — check the sender address.

*Cheers — and see you in the next one.* 🍺

---

*Missed the previous instalment? Read [The Beer Drinker's Guide to How the Internet Works](/posts/bdg-how-the-internet-works/).*
