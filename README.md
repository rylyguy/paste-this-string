# Paste this string / ln-string-decode

A static, client-side Bitcoin / Lightning payment-string decoder.

**Live decoder:** https://raw.githack.com/rylyguy/paste-this-string/main/ln-string-decode.html

Same tool at the original URL: https://raw.githack.com/rylyguy/paste-this-string/main/index.html

Paste a Lightning Address, LNURL (`lnurl1…`), BOLT11 invoice (`lnbc…`), BOLT12 offer (`lno1…`), or on-chain `1` / `3` / `bc1q` / `bc1p` string. The page reports:

- **type** (LNURL / Lightning Address / BOLT11 / BOLT12 / on-chain)
- **BOLT11 expiry** (tagged `x` field, else the spec default of 3600 seconds) and whether it is already dead
- **Lightning Address LNURL reachability** via a browser GET of `https://domain/.well-known/lnurlp/name` (metadata only — no amount, no invoice mint)

Nothing is uploaded except that optional LNURL-pay metadata fetch to the receiver domain. Bech32 checksums are verified for BOLT11 and LNURL. Base58 on-chain strings are prefix-length heuristics. This is not a wallet.

(Official github.io Pages may 404 until Settings → Pages is enabled; raw.githack is the working host.)

## Optional thank-you

Skip this. The tool is free.

- Lightning (stays in Strike): `rylyguy@strike.me`
- On-chain: `3M5R7D5UwtT6NuGUH6GVunZQZQ3p9DTePg`

Lightning cannot pay the on-chain address.

## Accuracy

Prefix + bech32 decode, not a node. BOLT11 signature recovery is not performed. Some LNURL hosts omit CORS; a failed browser fetch does not prove the address is dead in a wallet.

AI assistance was used to draft the page.
