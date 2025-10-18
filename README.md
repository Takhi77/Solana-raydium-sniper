# FourMeme Trading Toolkit (BNB Chain)

A modular, CLI-driven trading toolkit tailored for the Four.meme ecosystem on BNB Chain. It includes specialized modules for sniping new launches, mirroring wallets, batching routes, and simulating/measuring volume — all powered directly on-chain with no third‑party market data services.

## Demo Video

https://github.com/user-attachments/assets/6d4bae5d-9dd1-4988-9912-faf4c4faba59

## Modules at a glance
- **Sniper**: Rapid buys on fresh listings with tunable slippage and deadlines.
- **Copy‑Trader**: Mirror specific wallets with percentage sizing, per‑trade caps, and de‑duplication.
- **Bundler**: Execute predefined swap routes (e.g., `WBNB → TOKEN`) with timing controls; designed to extend toward multicalls.
- **Volume Bot**: Programmatic buy/sell loops at a set cadence for liquidity/organic activity testing.
- **Notifications**: Optional Telegram alerts for major lifecycle events.
- **Risk Controls**: Allow/deny lists, max spend ceilings, and basic MEV‑aware settings.

## How it works

### Sniper flow
- Load targets from config → query router for expected out → apply configured slippage → perform `WBNB → TOKEN` swap → emit tx hash/receipt → optionally notify via Telegram.

### Copy‑Trader flow
- Subscribe to pending mempool transactions → filter by leader wallets → detect router swap intents → mirror with your position sizing and caps → optionally notify.

### Bundler flow
- Read a sequence of routes from config → execute each respecting slippage/deadline settings → suitable base for multicall-style extensions.

### Volume Bot flow
- Loop on an interval → small buys → approve when needed → partial or full sells → repeat with built‑in rate limiting.

## Live Example - Sniper Bot in Action

Here's a real example of the sniper bot detecting and executing trades on a new token launch:

```
[2025-10-16 15:26:37] : token create information
     token=0x7984191403e7715bf8760e74c6e56a5786df4444,
     name=test,
     symbol=kurac,
     tx_hash=Some(0x88e1c7b59d13579a59585f8a4ff7eccf923ae08dc078a3833b328e111511c0fd),
     creator=0x63f8ab9b91cc710a2fd55f20e2931b23940a4321

✅ buyTokenAMAP tx sent: 0xcb3dbf09657a224feea0a9ae53664819031ee6eecc243313955caa28943bee29
✅ buyTokenAMAP tx sent: 0x8618e38dc585c6ed992782132db8660cb437c02185559704d4baafa63dae3841
✅ buyTokenAMAP tx sent: 0x6e3d0b10d20038ef9151b8e51d7b89ea689442615ccb5becd2f0244fd51eb55b
✅ buyTokenAMAP tx sent: 0x66f106982ea5e9f42fb3695a02722e17fcefff63019c1c7a50e6d22801bbb91e
✅ buyTokenAMAP tx sent: 0xb25f2a48d23878759c051edf9e1cb2ba6532abb4b70aba33a7d85bd6a3052200
✅ buyTokenAMAP tx sent: 0xe37da78b7925ee393609d8703638d97d88382d23bf71e6eaf871c9f414f396d4
✅ buyTokenAMAP tx sent: 0x6fbcc057bc01b21c2261db45357b20ffe06eab7d5027d33183b39aa5dc22320d
✅ buyTokenAMAP tx sent: 0xdf8c61bcacce20303b5455f59d02fee2e71955d8b17d546b7c19ed241e7818b2
✅ buyTokenAMAP tx sent: 0x87d297e21de9d23162fa7571a047f3ec2a3e67d6213e36502f41f5dd5b837427
✅ buyTokenAMAP tx sent: 0xc24f2c18cceae1682edb6e7d2dc40b8c0ee46b36b147b83485bcad37dd7816b7
```

The sniper successfully detected the new token creation and executed 10 rapid buy transactions within seconds of the token going live.
There are some failed transactions, but that's because of free rpc, if you try with paid rpc, then there will be no failed transactions.

## Support
- Telegram: [Pioneer](https://t.me/@hi_3333)
