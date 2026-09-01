# Paste this string

A static Bitcoin / Lightning payment-string explainer. Paste `1…` / `3…` / `bc1q` / `bc1p`, a Lightning Address, a BIP-353 name, a BOLT12 offer, or a BOLT11 invoice. The page says in plain English what it looks like.

**Live page:** https://rylyguy.github.io/paste-this-string/

Client-side only. No backend, no DNS lookup, no LNURL fetch, no node, no keys. Checksums are not proven.

## Optional thank-you

Skip this. The tool is free.

- Lightning (stays in Strike): `rylyguy@strike.me`
- On-chain: `3M5R7D5UwtT6NuGUH6GVunZQZQ3p9DTePg`

Lightning cannot pay the on-chain address.

## Accuracy

Prefix heuristics, not a wallet. vbytes are conservative single-sig ballparks ([D-Central](https://d-central.tech/bitcoin-transaction-size-reference/)). BIP-353 names are not resolved here; a real wallet must DNSSEC-validate. BOLT12 support is still uneven (LND was not native as of mid-2026).

AI assistance was used to draft the page.
