---
title: "Pints, Packets & Protocols"
description: "How the internet works — explained over a beer. If you've ever wondered what actually happens when you type a web address and hit Enter, this one's for you."
date: 2025-01-15
series: "beer-drinkers-guide"
readtime: "~9 min read"
tags: ["networking", "dns", "tcp", "explainer"]
youtube_id: "WMdVQsisIQg"
youtube_url: "https://www.youtube.com/watch?v=WMdVQsisIQg"
---

You use the internet every day — but have you ever stopped to wonder what's actually happening when you type a web address and hit Enter? Routers, DNS, TCP, IP addresses... it can all sound pretty intimidating. So let's forget the jargon for a moment and head to the pub instead.

In this post we're going to walk through how the internet works, using the world's biggest bar as our guide. By the time you've finished reading, you'll understand what happens every time you visit a website — and you might even be thirsty.

## A Town Full of Connected Buildings

The word "internet" is short for interconnected network. Think of it like the streets, roads and motorways that connect people with shops, services and each other. In a town, people can send letters, pop to the shops, or grab a takeaway — all because buildings are physically connected by roads, and everyone follows shared rules: a common language, a recognised currency, and a unique address for every property.

In the digital world, we use the same ideas:

- **Buildings and homes** are called nodes — your laptop, your phone, web servers, all nodes.
- **The shared language** is called a protocol — the agreed set of rules devices use to talk to each other.
- **Every node has a unique address** — called an IP address — more on those shortly.

Services like email, online banking and multiplayer games all live on this same network of connected nodes. The most familiar example? Visiting a webpage. And that's exactly where our bar comes in.

## Every Glass Has a Serial Number: MAC Addresses

Before we even think about routing drinks around the bar, there's something worth knowing about the glassware. Every single glass — in every bar in the world — has a unique serial number etched into it at the factory. No two glasses share the same number, ever. This is its hardware identity, fixed from the moment it was made.

In networking, this is called a **MAC address** — short for Media Access Control address. Every network device (your laptop's Wi-Fi card, your phone, your smart TV) has a MAC address permanently assigned by the manufacturer. While IP addresses are like your seat in the bar tonight — they can change depending on where you are — a MAC address is more like a fingerprint. It's used for communication within your local network, rather than across the wider internet.

> *Think of an IP address as where you're sitting in the bar tonight, and a MAC address as who you are — the name on your driving licence that never changes, no matter which pub you're in.*

## Welcome to the World's Biggest Bar: DNS

The internet hosts over a billion websites, though only around 200 million are actively maintained. Our bar isn't quite that big — but let's imagine it stocks one million different types of beer.

With a million beers on tap, the barman can't memorise where every single one is located. So he keeps a directory. You order a pint of ABC Lager, he looks it up, and the directory says: Section 1, Row 3, Column 8.

On the internet, this directory is called the **Domain Name System**, or DNS.

> *DNS translates a human-readable web address — like www.example.com — into a machine-readable IP address, like 93.184.216.34. That number is the actual location of the website on the internet.*

## The Bar Manager and the Floor Staff: Routers and Switches

Now the barman knows which beer to pour and roughly where to deliver it — but in a bar this size, getting drinks to the right place is a job in itself. This is where the bar manager and the floor staff come in.

The floor staff — **switches** — operate within a defined section. A switch knows every table in its zone, and if a drink is destined for table 14 in Zone B, it gets it there directly and efficiently.

The bar manager — the **router** — has a bigger picture view. When a drink needs to travel between zones, or leave the building entirely for delivery elsewhere in town, that's the router's job.

> *Switches connect devices within the same network. Routers connect different networks together — and decide the smartest route for your data to take.*

## On the Door: Firewalls

Our bar is popular. And like any popular venue, it needs a bouncer.

The bouncer stands at the entrance and checks everyone coming in — and sometimes controls who's allowed to leave too. He works from a list of rules: regulars are waved through, troublemakers are turned away, and anyone acting suspiciously gets a closer look.

A **firewall** works in exactly the same way. It sits at the boundary of a network and inspects incoming and outgoing traffic based on a defined set of rules.

> *A firewall doesn't read the contents of your data — it checks who's sending it, where it's going, and whether that matches the house rules.*

## One Tab for the Whole Table: NAT

Here's something that might surprise you: most devices in your home don't have their own public IP address. They share one — the address assigned to your router by your internet provider.

Imagine a group of friends running a single tab. From the bar's perspective there's one account — one name, one address. But the person running the tab knows internally who ordered what, and makes sure each drink reaches the right person. This system is called **NAT** — Network Address Translation.

> *NAT allows dozens of devices in your home to share a single public IP address, with your router acting as the translator between the outside world and your internal network.*

## Pulling the Pint: How a Webpage is Delivered

When you visit a site, your browser sends an **HTTP GET request** to the server holding the website files. Those files were assembled using a mix of ingredients:

- **HTML** — the structure of the page, like the glass that holds everything together.
- **CSS** — the styling: fonts, colours, layout.
- **Images and scripts** — the flavour and character of the page.

If the website is secure — which it should be — it uses **HTTPS** instead of HTTP. The 'S' stands for Secure, and it means data is encrypted in transit using Transport Layer Security (TLS). Think of it as a sealed, tamper-proof container for your pint.

> *Rather than arriving all at once, websites are delivered in packets — tiny chunks of data sent one at a time, like delivering your beer teaspoon by teaspoon until the glass is full.*

## The Satellite Bar: Caching and CDNs

Our world's biggest bar has a problem: it's in one location, and some customers are a very long way away. The solution? Open satellite bars in every city, pre-stocked with the most popular drinks.

This is exactly how a **Content Delivery Network** — or CDN — works. Instead of every request travelling to one central server, CDNs store copies of popular content on servers dotted around the globe.

**Caching** takes this idea further. Your browser can remember drinks it's already fetched — storing local copies of images, scripts and stylesheets so it doesn't have to request them on your next visit.

> *CDNs reduce the distance data has to travel. Caching reduces how often it needs to travel at all. Together, they're why popular websites load almost instantly, wherever you are in the world.*

## Rush Hour at the Bar: Load Balancing

Friday night. The bar is heaving. One barman simply can't keep up. The solution is obvious: bring in more bar staff and share the work between them.

**Load balancing** works on exactly the same principle. When a popular website receives millions of simultaneous requests, a single server would buckle. Instead, a load balancer sits in front of a pool of servers and distributes incoming requests across them.

## Finding Your Table: IP Addresses and Binary

An IPv4 address consists of four numbers between 0 and 255, separated by dots — something like `192.168.1.1`. Each number is called an octet, defined by 8 binary digits.

To show how it works, imagine our mixologist has lined up 8 spirits — each one is either in your cocktail or it isn't. The spirits have values ascending from right to left: 1, 2, 4, 8, 16, 32, 64, 128. Their combinations produce any number from 0 to 255. With four octets and just 32 binary digits, you can represent over 4.2 billion unique addresses.

> *With 8 billion people on the planet, that pool is running dry. The industry is moving to IPv6, which uses 128 binary digits and an almost incomprehensibly large number of addresses. A story for another video.*

## Speed vs. Capacity: Latency and Bandwidth

Two things determine how quickly your beer arrives:

**Latency** is the delay — the time it takes for a single request to travel from your device to a server and back. It's measured in milliseconds and is heavily influenced by physical distance.

**Bandwidth** is about capacity — how much data can flow through a connection simultaneously. A high-bandwidth connection is like a barman with a huge tray: he might take the same time to walk over, but he's bringing you twelve drinks in one go.

> *Latency is how fast. Bandwidth is how much. For a great internet experience, you want both to be good.*

## No Spillages: TCP Keeps Things Intact

On the internet, **TCP** — Transmission Control Protocol — works alongside HTTP to ensure every packet of data making up a webpage arrives safely and in the right order. If any packet goes missing, TCP has built-in mechanisms to request a resend. No lost data, no broken pages, no half-poured pints.

---

*Cheers — and see you in the next one.*
