# pihole-zakros

A small personal Pi-hole blocklist for device telemetry that the big public lists don't cover.

Everything here was found by watching what my own devices actually query, then checking each domain
against the public lists I already run (hagezi `tif` / `pro.plus` / `ultimate`, StevenBlack, firebog,
Perflyst and friends). Only domains those lists *miss* end up here.

## Use it

Add as an adlist in Pi-hole:

```
https://raw.githubusercontent.com/AallynReed/pihole-zakros/main/aallyn-blocklist.txt
```

Then apply:

```bash
pihole -g
```

## Format

Adblock Plus syntax. `||example.com^` blocks `example.com` **and every subdomain** — Pi-hole v6 parses
this natively, so no regex rules are needed. Lines starting with `!` are comments.

Using ABP syntax rather than Pi-hole regex entries is deliberate: regex rules live only in Pi-hole's
database and are lost when you rebuild the instance, whereas an adlist is re-fetched automatically.

## What's in it

| Rule | Why |
|---|---|
| `\|\|diagnostic.networking.aws.dev^` | Amazon Echo network-diagnostics telemetry — 61 subdomains, ~61% of the device's total DNS traffic |
| `\|\|ygles.com^` | Canon printer cloud IoT backend |

The file also carries a commented-out section of IoT **control-plane** domains (TP-Link, Sonoff/eWeLink,
Canon Cloud Link). Those are deliberately disabled: blocking them doesn't stop telemetry, it severs the
device from its vendor cloud and breaks phone-app control. Uncomment per device if that's what you want.

## Adding to it

1. Find the domain in Pi-hole's query log — filter by the device's IP.
2. Confirm it isn't already blocked by an existing list.
3. Confirm it's telemetry, not the device's control plane. If unsure, block it and see what breaks.
4. Add `||domain^` with a comment explaining what it is and what you verified still works.

Pi-hole refreshes adlists on its own schedule; `pihole -g` applies changes immediately.
