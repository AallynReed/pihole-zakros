<div align="center">

<img src="docs/icon.svg" width="128" alt="pihole-zakros icon">

# pihole-zakros

<!-- Project status -->
![GitHub Repo stars](https://img.shields.io/github/stars/AallynReed/pihole-zakros?style=for-the-badge&color=gold&cacheSeconds=21600)
![GitHub last commit](https://img.shields.io/github/last-commit/AallynReed/pihole-zakros?style=for-the-badge&color=green&cacheSeconds=21600)
![GitHub issues](https://img.shields.io/github/issues/AallynReed/pihole-zakros?style=for-the-badge&cacheSeconds=21600)

<!-- Platforms -->
![Pi-hole](https://img.shields.io/badge/Pi--hole-96060C?style=for-the-badge&logo=pihole&logoColor=white)

<!-- Project meta -->
[![Discord](https://img.shields.io/badge/Discord-Foxhearth-5865F2?style=for-the-badge&logo=discord&logoColor=white)](https://foxhearth.com/discord)
[![foxhearth.com](https://img.shields.io/badge/foxhearth.com-project_page-E8702A?style=for-the-badge)](https://foxhearth.com/projects/pihole-zakros)

</div>

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
