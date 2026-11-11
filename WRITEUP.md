# BiayaQR — QRIS costs, made legible

Buying crypto with QRIS can feel simple while the total cost is less obvious. BiayaQR is an Indonesia-first prototype that compares QRIS deposit fees at Tokocrypto and INDODAX before a user decides how much to top up.

## How it works

The user supplies a deposit amount and may add their own trading-fee assumptions, an asset label, and a price they already know. The browser calculates the deposit fee, total paid, modeled trading cost, amount left for a purchase, effective cost, and optional estimated quantity. The arithmetic stays deterministic in the app; no live price or exchange account is queried.

## Why SERV Reasoning

SERV Reasoning is used for the explanation layer—not for arithmetic or market data. The local backend sends a small, validated summary of the selected calculation and the matching official fee-source URL. Its instructions ask it to stick to supplied inputs, distinguish user-entered trading assumptions from exchange fee facts, identify the modeled payment assumptions, and avoid inventing prices or charges. The SERV key stays on the server side.

This keeps the roles clear: the application computes; SERV makes the result easier to understand. BiayaQR is intended for the Open Track of OpenServ Hackathon Edition 02.

## What the demo does not do

BiayaQR does not buy or sell assets, connect to an exchange, fetch market prices, or give financial advice. Trading fees are user inputs, and all fee/source information can change. The market-scale cards provide context, but their different periods and geographic coverage must not be added together.

## Current demo status

The page and Python backend run locally. Calculator and input/source-selection checks passed. One end-to-end SERV UI request succeeded in testing: the request returned HTTP 200, and a non-empty explanation plus the official Tokocrypto source link appeared in the Tokocrypto card. This documents one successful test, not production readiness, repeated reliability, or user validation. The captured screenshot and a short local demo clip are separate from the source archive; the clip combines that existing proof with the calculator demo without making another SERV request. The prototype has not been deployed.
