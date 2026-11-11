# BiayaQR

BiayaQR is a mobile-friendly prototype for comparing QRIS deposit costs when buying crypto in Indonesia. It makes fee assumptions visible before a user decides what to do; it does not execute purchases or provide investment advice.

## What it does

- Compares QRIS deposit costs for Tokocrypto and INDODAX using the official help pages linked in the interface.
- Lets the user enter a deposit amount and their own trading-fee assumptions.
- Shows the deposit fee, total paid, modeled trading fee, purchase value, effective cost, and—if supplied—an estimated asset quantity using the user's own price input.
- Performs arithmetic in the browser. There is no live market-price feed.
- Can ask SERV Reasoning for a short explanation of the selected calculation, with the matching exchange source URL supplied by the backend.

## Run locally

Requires Python 3.10 or newer; the server uses only the Python standard library.

```bash
export SERV_API_KEY="YOUR_SERV_API_KEY"
python3 server.py
```

Open <http://127.0.0.1:8000>. `SERV_API_KEY` is read by the local Python server and is never placed in the page. Use your own key locally; replace the placeholder above and never commit a real key or `.env` file. The calculator works without a key; the explanation endpoint returns a configuration message until one is provided.

Optional environment variables:

- `PORT` — server port (default `8000`)
- `SERV_MODEL` — SERV model ID (default `gpt-6-luna`)

The server binds to loopback (`127.0.0.1`) for local demos. SERV API usage is metered; check the current [model catalog and pricing](https://docs.openserv.ai/serv-reasoning/models) before using a different model. See the [SERV API reference](https://docs.openserv.ai/serv-reasoning/api) for endpoint and authentication details.

## Data sources

- [Tokocrypto — QRIS deposit service and fee](https://support.tokocrypto.com/hc/id/articles/44062161904653-Tokocrypto-Hadirkan-Layanan-Deposit-Melalui-QRIS)
- [INDODAX — transaction fee details](https://help.indodax.com/hc/id/articles/4416646599705-Rincian-Biaya-Transaksi-di-INDODAX)
- The market-scale panel links the underlying [Bank Indonesia](https://www.bi.go.id/id/publikasi/ruang-media/news-release/Pages/sp_2819026.aspx) and [ASEAN](https://asean.org/wp-content/uploads/2026/04/13th-AFMGM-JS_Adopted_20260410.pdf) sources. Recheck dates, coverage, and fees before any public presentation; figures can change.

## Demo status and limitations

This is a local prototype, not a deployed service. In testing, one end-to-end SERV UI request succeeded: it returned HTTP 200, and a non-empty explanation with the official Tokocrypto source link appeared in the Tokocrypto card. This is evidence of that single test only; it does not establish production readiness, repeated reliability, or user validation. The local screenshot proof remains separate from this source package. The reviewed [demo clip](./BiayaQR-demo-with-SERV-proof.mp4) pairs the captured UI proof with calculator footage and makes no additional SERV request.

Trading fees are user-entered estimates; a blank field is treated as 0% only for the estimate. The app does not fetch prices, place orders, or verify that an exchange will apply the modeled payment flow. Always check the linked official sources and your account terms.
