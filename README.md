# pihole-zakros

Custom Pi-hole lists for my network, kept in git so they survive rebuilding the Pi-hole instance.

## Policy

Block telemetry and pointless cloud features. **Never** block anything a device needs to work —
firmware updates, app control, time sync and local function all stay reachable.

Domains are found by filtering Pi-hole's query log by device IP, then checked against the public lists
already in use (hagezi, StevenBlack, firebog, Perflyst) so only genuine gaps end up here.

## Lists

| File | Add to Pi-hole as |
|---|---|
| `aallyn-blocklist.txt` | blocklist |
| `allowlist.txt` | **allowlist** (adlist type 1) |

```
https://raw.githubusercontent.com/AallynReed/pihole-zakros/main/aallyn-blocklist.txt
https://raw.githubusercontent.com/AallynReed/pihole-zakros/main/allowlist.txt
```

Apply with `pihole -g`. GitHub's raw CDN caches for 5 minutes, so a push takes that long to appear.

## Format

Adblock Plus syntax. `||example.com^` blocks a domain and all subdomains; `@@||example.com^` allows one.
ABP is used instead of Pi-hole regex rules on purpose — regex entries live only in the Pi-hole database
and are lost on rebuild, whereas adlists are re-fetched automatically.
