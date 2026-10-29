---
icon: ethernet
cover: ../.gitbook/assets/banner-network.jpg
coverY: 0
layout:
  cover:
    visible: true
    size: hero
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Network Devices & Cost

## HQ (รวม ฿3.315M)

| อุปกรณ์ | จำนวน | หน้าที่ | ราคา (บาท) |
| --- | --- | --- | --- |
| FortiGate 200F | 2 | Firewall (HA) | 500,000 |
| Catalyst 9300-48P | 2 | Core stack | 560,000 |
| Catalyst 9300-48P | 3 | Access ชั้น 1 และ 2 | 735,000 |
| Nexus 93180YC-FX | 2 | DC fabric | 700,000 |
| Catalyst 9166 | 11 | Access Point | 605,000 |
| Catalyst 9800-L | 1 | WLAN Controller | 215,000 |
| **รวม** | | | **3,315,000** |

## Sale Office (รวม ฿162,000)

| อุปกรณ์ | จำนวน | หน้าที่ | Key ports & power | ราคา (บาท) |
| --- | --- | --- | --- | --- |
| Fortinet FortiGate 40F | 1 | Branch NGFW/VPN | 5 × 1G RJ45, ~800 Mbps FW | 27,000 |
| Catalyst 1200-24P-4G | 1 | Access Switch | 24 × 1G PoE+ (195W) + 4 × 1G SFP | 25,000 |
| Catalyst 9166 | 2 | Access Point | PoE+ | 110,000 |
| **รวม** | | | | **162,000** |

## Speed Ladder

| Device / Segment | Speed | Medium |
| --- | --- | --- |
| Staff desks | Wi-Fi 6E (11 APs) | RF |
| AP Catalyst 9166 | 1 Gbps (PoE+) | Cat6A |
| Access switch (IDF-1F / MDF) | 2 × 10G LAG | OM4 fiber (riser) |
| Core stack → Nexus × 2 (vPC) | 2 × 10G LAG each (40G total) | OM4 + SFP+ |
| Nexus → Servers | 2 × 25G | DAC ≤ 5 m |
| Nexus → GPU / peer-link | 100G | DAC/AOC |
