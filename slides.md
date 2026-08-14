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
layout: default
---

# 🔍 Quality in CI

Lessons learned from building this pipeline

<div class="grid gap-4 mt-6">

<div class="flex items-start gap-3 p-3 rounded-lg bg-yellow-500/10 border border-yellow-500/30">
  <div class="i-carbon-flash text-2xl text-yellow-400 mt-1"></div>
  <div>
    <strong>Cache correctness > raw speed</strong> — a fast build that installs the wrong dependency versions is worse than a slow one that installs the right ones. A stale or mismatched cache can silently pass CI while breaking things locally.
  </div>
</div>

<div class="flex items-start gap-3 p-3 rounded-lg bg-red-500/10 border border-red-500/30">
  <div class="i-carbon-debug text-2xl text-red-400 mt-1"></div>
  <div>
    <strong>Lint failure we hit</strong> — our first <code>markdownlint-cli2</code> run flagged 21 issues, mostly Slidev's own HTML/Vue syntax being misread as invalid Markdown. Lint rules need explicit, documented exceptions for framework-specific syntax, not a blanket disable.
  </div>
</div>

<div class="flex items-start gap-3 p-3 rounded-lg bg-purple-500/10 border border-purple-500/30">
  <div class="i-carbon-archive text-2xl text-purple-400 mt-1"></div>
  <div>
    <strong>Artifacts after a failed run</strong> — even when a build fails, the uploaded artifact lets us inspect what was actually produced, without reproducing the failure locally first.
  </div>
</div>

</div>

---
layout: default
---

# 🔒 Security in CI/CD

Hardening the pipeline against common mistakes

<div class="grid gap-4 mt-6">

<div class="flex items-start gap-3 p-3 rounded-lg bg-blue-500/10 border border-blue-500/30">
  <div class="i-carbon-locked text-2xl text-blue-400 mt-1"></div>
  <div>
    <strong>Least privilege</strong> — every workflow's <code>GITHUB_TOKEN</code> should only have the permissions it actually uses. If a read-only validate workflow is ever compromised, the blast radius stays small.
  </div>
</div>

<div class="flex items-start gap-3 p-3 rounded-lg bg-green-500/10 border border-green-500/30">
  <div class="i-carbon-chain text-2xl text-green-400 mt-1"></div>
  <div>
    <strong>Supply-chain integrity</strong> — actions pinned to a mutable tag like <code>@v4</code> can silently change underneath you. Pinning to a full commit SHA locks in exactly the code we reviewed.
  </div>
</div>

<div class="flex items-start gap-3 p-3 rounded-lg bg-orange-500/10 border border-orange-500/30">
  <div class="i-carbon-user-avatar text-2xl text-orange-400 mt-1"></div>
  <div>
    <strong>Human gates still matter</strong> — automation catches broken builds and bad lint, but it can't judge intent. A required reviewer confirms this deploy, at this moment, is meant to go live.
  </div>
</div>

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