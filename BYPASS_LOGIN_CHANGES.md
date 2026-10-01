# Nuojiji 6.9.89 reference-mirror access patch

This repository is a frozen static reference extracted from the official Android OTA package `6.9.89` on 2026-10-01 for UI/DOM/CSS archaeology.

The original package SHA-256 was verified before patching:

`4a1c765ff77a06f5bdff8e94aafa30451ca512ea73b1797e56d18d1561b9d47b`

Only reference-access gates are changed:

1. `assets/main-BDB-lJFa.js`: the top-level app gate is forced to the normal main-app branch (`k8L/k8H/k8t/k8b=false`, `k8P=true`) so the vendor QQ/Discord account page is not required for visual inspection.
2. `assets/main-BDB-lJFa.js`: `Xhe(hostname)` returns true so the vendor domain guard does not replace this mirror with its warning page.
3. `index.html`: before the module loads, lock-screen/password flags are disabled and `sessionStorage.unlocked=true` is seeded for reference browsing.
4. `index.html`: entry `assets/` URLs are project-relative so the build can run under a GitHub Pages repository subpath.

No application feature code is intentionally rewritten. Server-backed sync/account/payment/community functions may fail because this mirror has no vendor session; local/offline UI is the purpose of the deployment.

## GitHub Pages static-runtime patch (2026-10-01)

The vendor build was produced with a root `/` public base. GitHub Pages serves this mirror below `/doQvQ_doorkicker_6.9.89/`, so root-relative static asset references otherwise resolve to `https://mothonthe.github.io/assets/...` and trigger the vendor chunk-update recovery screen.

For this static reference mirror only:

- root `/assets/...` references are rewritten to `/doQvQ_doorkicker_6.9.89/assets/...`;
- root media/manifest references are rewritten to the repository Pages prefix;
- PWA/Service Worker registration is disabled and old registrations/caches are cleared on boot;
- stale `nuojiji_ota_pending` is cleared;
- the vendor 15-second stuck-diagnostic overlay is suppressed in reference-mirror mode.

These changes do not alter Home product behavior; they only make the frozen 6.9.89 reference bundle stable under a GitHub Pages project subpath.
