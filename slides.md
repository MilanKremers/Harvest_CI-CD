---
# try also 'default' to start simple
theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://cover.sli.dev
# some information about your slides (markdown enabled)
title: Welcome to Slidev
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
# apply UnoCSS classes to the current slide
class: text-center
# https://sli.dev/features/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations.html#slide-transitions
transition: slide-left
# enable Comark Syntax: https://comark.dev/syntax/markdown
comark: true
# duration of the presentation
duration: 35min
---

# Welcome to Slidev

Presentation slides for developers

---
theme: default
title: SDLC & CI/CD
---

# SDLC & CI/CD

A team deep-dive

---

# What is SDLC?

The Software Development Life Cycle — the structured stages a piece of software goes through:

- Plan
- Design
- Implement
- Test
- Deploy
- Maintain

---

# What is CI/CD?

- **CI (Continuous Integration)** — merge and validate code changes frequently, catch issues early via automated builds/tests
- **CD (Continuous Delivery/Deployment)** — automatically ship validated changes to an environment (in our case, GitHub Pages)

---

# Workflow Triggers & Structure

How our pipeline decides *when* and *what* to run

---

# Two triggers, two purposes

- **`push` naar `main`** → bouwt én deployt de site live
- **`pull_request`** → bouwt alleen, ter validatie, deployt niets
- **`workflow_dispatch`** → handmatige herstart, met optionele reden als input

Elk moment in de levenscyclus van een wijziging heeft dus zijn eigen trigger.

---

# Waarom scheiding van build en deploy?

- Een PR-workflow mag nooit publiceren — die controleert alleen of de code bouwt
- `needs: build` zorgt dat deploy pas start als de build geslaagd is
- Concurrency groups voorkomen dat verouderde runs onnodig doorlopen

Resultaat: alleen geldige, geteste wijzigingen komen live op `main`.