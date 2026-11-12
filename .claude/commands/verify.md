---
description: Static-site consistency check across the HTML pages (no build/test exists) — flags nav/footer drift and broken asset references.
allowed-tools: PowerShell(Get-ChildItem:*), PowerShell(Select-String:*), PowerShell(Test-Path:*), Bash(rg:*), Bash(ls:*)
---

This site has **no build, test, linter, or formatter** (per CLAUDE.md — don't invent any). Its real failure mode is the hand-duplicated header / nav / footer drifting across pages. Verify consistency:

1. Enumerate the ACTUAL page set with `Get-ChildItem *.html` — do not hardcode page names (the set changes: Origin was replaced by LaCantina, `ewd.html` was added, and the CLAUDE.md page list is slightly stale).
2. For each page, confirm it loads the shared assets it should: brand/contact pages reference `css/styles.css` and `js/main.js`. NOTE: `index.html` intentionally has its own inline `<style>` + script and does NOT load `css/styles.css` — that's by design, don't flag it.
3. Compare the `<nav>` / mobile-nav link lists and the `<footer>` blocks across pages; flag any page whose nav links or footer contact info drift from the rest. Single source of truth: phone `(843) 970-2146`, email `info@buildfcbs.com`, address `3870 Leeds Ave #101, North Charleston, SC 29405`.
4. Confirm every referenced asset path (`css/`, `js/`, `assets/...` images, hero video) exists on disk with `Test-Path`.

Report a per-check list, then a one-line verdict: **CONSISTENT** or **DRIFT FOUND** (name the page + the inconsistency). This is advisory — there's no automated gate here.
