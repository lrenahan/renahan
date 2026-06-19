---
title: "Stamps, Wristbands & Single Sign-On"
subtitle: "How SAML and SSO Work — Explained at the Door of Your Favourite Bar"
description: "Show your ID once. Drink everywhere. We explain SAML and Single Sign-On using the best analogy we could think of — a night out at the pub."
date: 2025-09-11
series: "beer-drinkers-guide"
tags: ["saml", "sso", "single-sign-on", "authentication", "cybersecurity", "2fa", "identity-provider", "explainer"]
readtime: "8 min"
youtube_id: "YfXr6ht3d14"
youtube_url: "https://www.youtube.com/watch?v=YfXr6ht3d14"
---

*How SAML and SSO Work — Explained at the Door of Your Favourite Bar*

**Series: Tech Behind the Bar | Read time: ~8 minutes**

It's your birthday. You're finally old enough to walk through that door, and you've been looking forward to it for a while. But first, you've got to get past the bouncer.

You've got your ID. The bouncer checks it, nods, and stamps your hand. From that point on, no one inside the bar asks who you are — the stamp says it all.

That little moment at the door? It's a near-perfect analogy for how SAML and Single Sign-On work in the digital world. And if you stick with us through last orders, you'll never look at a login screen the same way again.

---

## The Bouncer at the Door: Authentication

Let's set the scene. You're 18 (or 21, if you're reading this from across the Atlantic), and you've arrived at a bar to celebrate. You might look young. The bouncer isn't sure. So he asks for your ID.

You hand over your driving licence or passport — a document with your name, your date of birth, your photo, and crucially, a bunch of security features: watermarks, holograms, government-issued formatting that's very hard to fake. The bouncer inspects it carefully:

- Does it look legitimate — is it from a known, trusted issuer?
- Does your face match the photo?
- Do your details meet the requirements (age, in this case)?

Only when all those checks pass does he let you in.

> In the digital world, this process is called **authentication** — confirming that you are who you claim to be.

The bar is the **service provider**: it has something you want (a cold pint). But it won't give it to you until it's satisfied you're allowed to have it. Your ID is your credentials — your username and password, or something even more secure. And the bouncer is the **Identity Provider (IdP)**: the system that does the actual checking.

---

## Something You Have, Something You Are: Two-Factor Authentication

Notice that the bouncer doesn't just check your ID — he also checks your face. The ID alone isn't enough; anyone could have stolen it. Your face alone isn't enough; you might just happen to look the right age. Together, they're much harder to fake.

This is essentially **two-factor authentication (2FA)**:

- **Something you have** — your ID card
- **Something you are** — your face (biometrics)

In the digital world, the IdP is responsible for requesting and verifying these factors — not the bar (service provider) itself. The bar just says "I need proof you're allowed in." It's the bouncer who decides how to verify that, and who carries out the checks.

If someone only has a username and password — like presenting a birth certificate with no photo — that's a single factor. It's better than nothing, but passwords can be phished, guessed, or stolen from breaches of other websites. The more factors you add, the harder it is for an attacker to impersonate you.

> A single factor is the equivalent of a birth certificate with no photo. It tells you something, but it doesn't prove you're the right person.

---

## The Stamp on Your Hand: SAML Tokens

Once the bouncer is satisfied, he stamps your hand. That stamp is your proof of authentication. Walk up to the bar, approach the dance floor, use the toilets — nobody inside is going to ask you to prove your identity again. The stamp says it all.

This is what SAML does. SAML stands for **Security Assertion Markup Language** — and yes, it's a mouthful, which is why we're sticking with the stamp analogy. Once the Identity Provider (the bouncer) has verified your credentials, it issues an **authentication token**: a digitally signed piece of data that tells any service provider "I've checked this person. They're legitimate. Let them through."

In technical terms, this token is often stored as a **cookie** in your browser — it sits quietly in the background, presented automatically whenever you visit a service that requires it. Like showing a stamped wrist at the door of each room in the venue, without having to dig your ID out of your pocket every time.

> The stamp on your hand is proof that you've already passed the checks. In digital terms, that's your authentication token — issued by the IdP and recognised by every service provider that trusts it.

Cookies have an expiry time built in. Leave the bar, come back the next day, and the stamp has faded — you'll need to verify yourself again. Same logic applies online: tokens time out for security reasons, and you'll eventually be asked to log in again.

---

## Hopping Between Bars: The Case for SSO

Here's where things get interesting. It's your birthday — you're not staying in one place. You head to the next venue down the street. And there's another bouncer. And he has no idea you were just checked at the last place.

So you dig out your ID again. And again at the next bar. And again at the one after that. After a while, it's less of a birthday and more of an admin exercise.

This is what life was like before Single Sign-On.

Companies use dozens of different software applications: email, project management tools, HR systems, cloud storage, customer databases. Each one had its own login. That meant employees needed to remember a different username and password for each system — and each set of credentials was another potential security vulnerability.

> Imagine if every room in the same venue had its own separate bouncer, and none of them accepted each other's stamps. That's what working without SSO feels like.

---

## The Magical Wristband: How SSO Works

Now imagine a different setup. Instead of a stamp that only works in one bar, you get a **wristband** — one that every bouncer in town recognises. You prove your identity once, get your wristband, and for the rest of the night you can walk into any participating venue without stopping at the door again.

That's Single Sign-On. You log in once with your primary credentials — typically your company's Microsoft or Google account — and the central Identity Provider issues a token that all your other applications recognise. Need to check your email? You're already in. Open the project management tool? Still logged in. Switch to the HR system? Seamless.

The key insight is that your actual login credentials — your password — never get shared with the individual applications. The bar staff never see your ID; they just see the wristband. The service provider trusts the Identity Provider, and the Identity Provider vouches for you.

- You don't have to remember multiple passwords
- Your credentials never touch the individual applications
- Security is centralised — one strong check, not many weak ones
- Revocation is simple — cancel the wristband at the source

---

## Why This Matters for Security

SAML and SSO aren't just about convenience — they're genuinely better for security. Here's why.

When employees have 15 different passwords, some of them are going to be weak. Some are going to be reused across personal and work accounts. Some are going to be written on sticky notes. And if an attacker manages to phish one, they might get access to several systems.

With SSO, you centralise the authentication. Apply strong multi-factor authentication at the IdP level — the bouncer stage — and you've covered every application behind it. One strong door, not fifteen weak ones.

It also simplifies **offboarding**. When an employee leaves the company, you revoke their access in one place. The wristband stops working. There's no need to go through a checklist of 20 applications, hoping you haven't missed any.

> One strong check at the door is safer than 15 weak ones scattered throughout the building. Centralise authentication, centralise control.

---

## Last Orders: What We Covered

- **Authentication** is the process of proving you are who you claim to be — like a bouncer checking your ID.
- The **Identity Provider (IdP)** carries out the checks — the bouncer — while the **Service Provider** (the bar) just wants to know you've been verified.
- **Two-factor authentication** combines something you have with something you are or know — just like showing ID and your face.
- **SAML** is the standard that allows the IdP to issue a signed token — a hand stamp — that service providers can trust.
- Tokens are stored as **cookies** and expire automatically — like a stamp that fades by morning.
- **Single Sign-On (SSO)** lets you authenticate once and access multiple applications — a wristband valid across every venue in town.
- SSO improves both usability and security: centralised authentication, centralised control, and one strong door instead of many weak ones.

*Cheers — and see you in the next one.*
