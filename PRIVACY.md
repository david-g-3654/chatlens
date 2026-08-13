# Privacy & local-only verification

chatlens is designed so your conversation data never leaves your device. This
document records how that is enforced and, more importantly, **how you can verify
it yourself in about two minutes** — you should not have to take anyone's word for it.

## What the code does

- **No backend.** The app is a single `index.html`. There is no server component.
- **No network calls in the app.** `index.html` contains no `fetch()`,
  `XMLHttpRequest`, `WebSocket`, `EventSource`, `sendBeacon`, `RTCPeerConnection`,
  dynamic `import()`, or any `http(s)://` / `ws(s)://` URL. (The word "fetch"
  appears once — as English prose inside sample text.)
- **The only browser storage used is `localStorage['cl_theme']`**, which stores your
  light/dark preference. No conversation content is written to `localStorage`,
  `sessionStorage`, `indexedDB`, or cookies.
- **Your export is held in memory only.** Parsing and indexing happen in a Web Worker
  (loaded from an in-page `Blob`, not the network). Reload the tab and all data is gone.
- **The README badges (shields.io) load only on GitHub's rendered README**, not in the app.

## Verify it yourself (2 minutes)

1. **Offline test.** Turn off Wi‑Fi / disconnect from the network, open `index.html`,
   load an export (or the sample data), search, browse. Everything still works —
   because nothing is sent anywhere.
2. **Network tab.** Open DevTools → Network, then load your export and run searches.
   You will see **zero** requests triggered by the app.
3. **Reload = gone.** Load data, then reload the page. You start from the empty
   drop screen; nothing was persisted.
4. **Read the source.** It is one file. Search it for `fetch`, `http`, `WebSocket`,
   `localStorage` — the only storage key is `cl_theme` (your theme).

## Honest limitations

- This describes the **app code**. If you host the file somewhere, your **host's**
  server logs will still see the page request for `index.html` itself (as with any
  web page). The safest mode is opening the local file directly, or self-hosting.
- Browser extensions you have installed can read page content regardless of any app.
  That is outside this app's control.
- This document reflects the code at the time of writing; re-verify after any change.
  The checks above are exactly how to do that.

*This is the author's own verification, not a third‑party certification. The value is
that every claim here is reproducible by you with the steps above.*
