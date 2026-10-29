---
icon: layer-group
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

# VLAN Design

แบ่งเครือข่ายเป็น VLAN ตามกลุ่มผู้ใช้และหน้าที่ เพื่อแยก traffic และคุมสิทธิ์ด้วย firewall policy

{% tabs %}
{% tab title="Employee Access" %}

| VLAN | ชื่อ | ใช้กับ |
| --- | --- | --- |
| 20 | STAFF | พนักงานทุกแผนก (60–100 คน) ทั้งสายและ corporate Wi-Fi สิทธิ์ควบคุมด้วย firewall policy + 802.1X role |
| 25 | COWORKING | BYOD hot-desking อุปกรณ์ที่ไม่น่าเชื่อถือ เข้าถึงได้จำกัด NAC เข้มกว่า |
| 120 | VPN_POOL | Remote access VPN สำหรับ WFH ผ่าน SSL/IPSec เข้าถึงตาม identity และ posture check |

{% endtab %}

{% tab title="Datacenter" %}

| VLAN | ชื่อ | ใช้กับ |
| --- | --- | --- |
| 30 | SERVERS | App server, AD, DNS, DHCP, RADIUS แยก L2 ออกจากผู้ใช้ |
| 35 | DEV_TEST | Prototype / staging แยกจาก production ความผิดพลาดตอนพัฒนาไม่กระทบบริการจริง |
| 40 | STORAGE | SAN/NAS: iSCSI, NFS, Jumbo Frames (MTU 9000) เส้นทางเฉพาะ storage |
| 45 | BACKUP | Backup server และ replication แยกเพื่อกัน ransomware: production เข้าถึง backup network ไม่ได้ |
| 50 | GPU_FABRIC | GPU compute: RoCE v2 lossless fabric 100 GbE แบบ non-routable สำหรับ distributed ML training |
| 100 | PCI_ZONE | Payment processing ตามขอบเขต PCI-DSS แยกขาด ไม่มี internet |

{% endtab %}

{% tab title="Security Edge" %}

| VLAN | ชื่อ | ใช้กับ |
| --- | --- | --- |
| 60 | DMZ | บริการที่หันออก public: reverse proxy, CDN origin, bastion host เป็นชั้นกั้นระหว่าง internet กับภายใน |

{% endtab %}

{% tab title="Infrastructure & Building" %}

| VLAN | ชื่อ | ใช้กับ |
| --- | --- | --- |
| 10 | MGMT | จัดการอุปกรณ์ (switch, AP, firewall, UPS ผ่าน SNMP) เป็น out-of-band control plane |
| 110 | AV_MEDIA | ห้องประชุม Chromecast/AirPlay, Karaoke จำกัด multicast ไว้ใน VLAN นี้ |

{% endtab %}

{% tab title="Guest / Public" %}

| VLAN | ชื่อ | ใช้กับ |
| --- | --- | --- |
| 80 | GUEST | Guest Wi-Fi ใช้ได้เฉพาะ internet ผ่าน captive portal + client isolation ไม่เข้าถึงระบบบริษัท |

{% endtab %}

{% tab title="Sale Office" %}

| VLAN | ชื่อ | ใช้กับ |
| --- | --- | --- |
| 200 | SALE_DATA | พนักงานสาขา (5–10 คน) ทั้งสายและ corporate Wi-Fi ผ่าน IPSec tunnel ไป HQ และ split tunnel สำหรับ internet |
| 280 | SALE_GUEST | Guest Wi-Fi ใช้ได้เฉพาะ internet, captive portal, client isolation ไม่เข้า VPN และ LAN |
| 290 | SALE_MGMT | จัดการ switch, AP, firewall ส่ง SNMP + syslog ผ่าน tunnel ไป HQ |

{% endtab %}
{% endtabs %}

{% hint style="info" %}
VLAN ออกแบบใน Progress 2 ตอนที่ระบบหลักบางส่วนยังอยู่ใน Private Datacenter หลังย้าย customer request path ขึ้น AWS แล้ว VLAN อย่าง SERVERS และ PCI_ZONE รองรับเฉพาะงานภายในของบริษัท ดู [Design Decision](../cloud/design-decision.md)
{% endhint %}
