# Three Years, Five Stacks: What I Built to Learn

## The short version

In August 2022 I started a side project to teach myself Kotlin. I kept going for three years, alongside a full-time engineering job. I was already fluent in Java and Go and comfortable in JavaScript. What I wanted was a project big enough, and real enough, to force me through unfamiliar stacks instead of tutorials.

It worked. The project grew into **16 repositories and roughly 750 commits** (Aug 2022 → Oct 2025). Along the way I wrote production code in **Kotlin, Go, Rust, TypeScript/JavaScript, and Protocol Buffers**. I built a Firefox extension, a Discord bot, a job-execution framework, a family of microservices, and a Kotlin Multiplatform desktop client.

## Why this project

My friend Ross had found a promising edge in sports markets. He had the idea and the domain insight. I had the engineering skills and a reason to learn new tools. The problem was data: his process started with gathering projections and odds by hand from many sources. That's slow, and stale data costs you the opportunity.

My goal became: **turn a manual, error-prone research routine into an automated, reliable pipeline.** That pipeline is what I'm proudest of. Fresher data meant our group of about ten people could evaluate far more opportunities, and make better-informed decisions, than manual gathering ever allowed.

This was a hobby and a learning vehicle for a small group of friends, never a substitute for my career.

## How it evolved

| When | What I built and learned |
|---|---|
| **2022** | First Kotlin backend plus a Firefox extension (my first). Data pulls from several projection and odds sources, saved with history. |
| **2023** | Moved to Firestore on GCP's free tier. Added dependency injection (Guice), a Discord bot with slash commands, hot-reloadable configuration, and **asynchronous job execution** with separate app and worker processes. Probability modelling with high-precision math. |
| **2024 (spring)** | Added a second sport. Scheduled data collection against live league schedules. Replaced most hand-built scrapers with a paid odds API. |
| **2024 (summer)** | **Broke the monolith into services.** Name matching, schedules, auth (Google JWT), a transaction ledger, and a bet-lifecycle service. Added Go for the services and Protocol Buffers for shared schemas. |
| **2024 (fall)** | A **Kotlin Multiplatform / Compose** client for desktop and Android, with DMG, MSI and Linux packaging. Wrote a simulation module to test ideas against historical data. |
| **2025** | Rewrote a fragile, embedded data source as a standalone **Rust** service (async, rustls, multi-arch Docker images). Maintained the system through a new season. |

## The architecture, simplified

```
 Data sources ──► Collectors ──► Normalization ──► Analysis engine ──► Services ──► Client apps
 (projections,    (REST services,   (name matching,   (probability       (auth, users,  (desktop,
  odds, schedules) scheduled jobs)   schedules,        models, sizing,   ledger,        Discord)
                                     shared schemas)   simulation)       bet lifecycle)
```

Every arrow was something I first did by hand and then automated.

## What I learned

**Kotlin and Kotlin Multiplatform.** Kotlin became a language I like: coroutines, expressive types, a strong ecosystem. Compose Multiplatform impressed me. One codebase can target desktop and mobile with real robustness. But I learned something about myself: I missed the distinct feel of platform-native apps, and I'm happiest working on data pipelines and the machinery behind the scenes rather than on GUIs. I tried an iOS build and stalled on integrating Google sign-in. It wasn't a priority, so I set it aside rather than sink time into it. Knowing what to stop doing is a skill too.

**(Maybe?) Buy before you build.** My biggest mistake was hand-writing bespoke scrapers for many individual sources. Sites change without notice, and I spent a lot of time on maintenance. I eventually switched to paying for an odds API and disabled nearly all the old scrapers. If I did it again, I'd evaluate a paid data source on day one and compare it to the true cost of maintenance.

**Knowing where to draw a line.** I once built a browser-based tool to import users' own bet histories. I later shut it down. I had concerns about session security and about the terms of service of the sites involved. Nothing had gone wrong. I decided to stop anyway, and replaced it with a better in-app flow where users confirm their own bets. I'd rather retire a feature early than rely on luck.

**Teaching.** Ross isn't a programmer. He built much of the client's UI components, and I taught him how: from "what is a component?" to shipping features in a real codebase. It stretched both of us. Mentoring someone that new forced me to explain my own work clearly, which sharpened my design instincts.

## What I'm open-sourcing

I'm releasing pieces that are self-contained and useful beyond this project:

- **`name-matching-service`** (Go): resolves messy player names from many sources to a single canonical ID. It handles suffixes, nicknames, misspellings, and which team a player was on at a given date. [link](https://github.com/Sectorbob/name-matching-service)
- **`schedule-service`** (Go): a small service that normalizes league schedules into a single schema. [link](TODO)

The rest stays private because it touches third-party data sources and terms I don't want to redistribute.

## A few metrics

- 16 repositories, about 750 commits, 3 years
- Tens of thousands of lines of Kotlin in the main backend
- 5 languages and formats: Kotlin, Go, Rust, TypeScript/JavaScript, Protobuf
- Targets shipped: server, Discord bot, Firefox extension, desktop app (macOS, Windows, Linux), Android build
- About 10 users

## Why this matters

I don't need an assignment to learn something. When I wanted Kotlin, I gave myself a real problem. When the problem outgrew its design, I split it apart. When a choice was costing me, I reversed it, and I stopped things I shouldn't have been doing. That's the engineer I try to be.
