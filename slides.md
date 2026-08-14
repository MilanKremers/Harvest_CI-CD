---
theme: seriph
background: https://cover.sli.dev
title: Welcome to Slidev
info: |
  ## SDLC & CI/CD Deep Dive
  A team presentation on software delivery pipelines.
class: text-center
drawings:
  persist: false
transition: slide-left
mdc: true
duration: 35min
---

# 🚀 SDLC & CI/CD

### A team deep-dive into modern software delivery

<div class="pt-12">
  <span class="px-2 py-1 rounded bg-blue-500/20 text-blue-400">GitHub Actions</span>
  <span class="px-2 py-1 rounded bg-green-500/20 text-green-400">GitHub Pages</span>
  <span class="px-2 py-1 rounded bg-purple-500/20 text-purple-400">Slidev</span>
</div>

---
layout: image-right
image: https://cover.sli.dev
---

# 📖 What is SDLC?

The **Software Development Life Cycle** — the structured stages a piece of software goes through.

<v-clicks>

- 🧭 **Plan** — define scope and goals
- ✏️ **Design** — architecture and structure
- 💻 **Implement** — write the code
- 🧪 **Test** — validate it works
- 🚢 **Deploy** — ship it to users
- 🔧 **Maintain** — keep it running

</v-clicks>

---
layout: center
class: text-center
---

# 🔄 What is CI/CD?

<div class="grid grid-cols-2 gap-8 mt-8 text-left">

<div class="p-6 rounded-xl bg-blue-500/10 border border-blue-500/30">

### 🔵 CI — Continuous Integration

Merge and validate code changes frequently. Catch issues early via automated builds and tests.

</div>

<div class="p-6 rounded-xl bg-green-500/10 border border-green-500/30">

### 🟢 CD — Continuous Delivery/Deployment

Automatically ship validated changes to an environment — in our case, **GitHub Pages**.

</div>

</div>

---
layout: image-right
image: https://cover.sli.dev
---

# ⚙️ Workflow Triggers & Structure

How our pipeline decides **when** and **what** to run

<v-clicks>

- 🟣 `push` naar `main` → bouwt **en** deployt live
- 🟡 `pull_request` → bouwt alleen, ter validatie
- 🔘 `workflow_dispatch` → handmatige herstart, met reden als input

</v-clicks>

<div class="mt-8 text-sm opacity-75">
Elk moment in de levenscyclus van een wijziging heeft zijn eigen trigger.
</div>

---
layout: center
---

# 🛡️ Why separate build and deploy?

<v-clicks>

- 🚫 A PR-workflow never publishes — it only checks that the code builds
- ⛓️ `needs: build` ensures deploy only starts after a successful build
- ⏱️ Concurrency groups cancel stale runs, saving time and resources

</v-clicks>

<div class="mt-10 p-4 rounded-lg bg-gradient-to-r from-green-500/20 to-blue-500/20 text-center">
✅ Result: only valid, tested changes ever reach <code>main</code>
</div>

---
layout: image-right
image: https://cover.sli.dev
---

# 🔍 Quality in CI

Lessons learned from building this pipeline

<v-clicks>

- ⚡ **Cache correctness > raw speed** — a fast build that installs the wrong dependency versions is worse than a slow one that installs the right ones. A stale or mismatched cache can silently pass CI while breaking things locally.
- 🐛 **Lint failure we hit** — our first `markdownlint-cli2` run flagged 21 issues, mostly Slidev's own HTML/Vue syntax (`<div>`, `<v-clicks>`) being misread as invalid Markdown. This taught us: lint rules need explicit, documented exceptions for framework-specific syntax, not a blanket disable.
- 📦 **Artifacts after a failed run** — even when a build fails, the uploaded artifact (or the failure logs) let us inspect *what* was actually produced, without needing to reproduce the failure locally first.

</v-clicks>

<div class="mt-8 p-4 rounded-lg bg-purple-500/10 border border-purple-500/30 text-sm">
💡 A green checkmark only means "it ran" — correctness is a separate question we still have to actively verify.
</div>

---
layout: center
class: text-center
---

# Thank you 🎉

### Questions?

<div class="pt-8 opacity-60 text-sm">
Built with Slidev · Deployed via GitHub Actions & Pages
</div>