---
icon: map
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

# Physical Topology & Floor Plan

สำนักงานใหญ่ (HQ) มี 2 ชั้น รองรับผู้บริหารและพนักงานประมาณ 60–100 คน ผู้ใช้ระบบได้แก่ ฝ่ายบริหาร ฝ่ายบุคคล ฝ่ายการตลาด ฝ่ายการเงิน ฝ่ายสารสนเทศ และแขกภายนอก ส่วน Sale Office เป็นสาขาขนาดเล็กสำหรับพนักงานขาย 5–10 คน

แต่ละสาขามี 3 มุมมอง ได้แก่ ผังห้อง (Floor Plan), การเดินสายและวางอุปกรณ์ (Physical Topology) และ Wi-Fi Heat Map ที่จำลองความแรงสัญญาณจากตำแหน่ง Access Point จริง พื้นที่สีเขียวคือสัญญาณดี ครอบคลุมทุกห้องที่มีผู้ใช้งาน

## สำนักงานใหญ่ (HQ) ชั้น 1

{% tabs %}
{% tab title="Physical Topology" %}
<figure><img src="../.gitbook/assets/physical-hq-1f.jpg" alt="Physical Topology HQ ชั้น 1"><figcaption><p>Physical Topology HQ ชั้น 1</p></figcaption></figure>

* Access Point × 6 ที่ Financial, Marketing, canteen, Open Co-Working Space, ห้องนั่งเล่นข้าง Network Room และ Lobby
* Access Switch × 2 (stack) ใน Network Room
* Riser ขึ้นชั้น 2 ที่ปล่องบันได (Fiber OM4)
{% endtab %}

{% tab title="Wi-Fi Heat Map" %}
<figure><img src="../.gitbook/assets/heatmap-hq-1f.jpg" alt="Wi-Fi Heat Map HQ ชั้น 1 (AP 1–6)"><figcaption><p>Wi-Fi Heat Map HQ ชั้น 1 (AP 1–6)</p></figcaption></figure>

AP 6 ตัวครอบคลุมทั้งชั้น ทั้งโซนห้องทำงานด้านบน Open Co-Working Space, Lobby และโซนห้องน้ำ
{% endtab %}

{% tab title="Floor Plan" %}
<figure><img src="../.gitbook/assets/floorplan-hq-1f.jpg" alt="ผังห้อง HQ ชั้น 1"><figcaption><p>ผังห้อง HQ ชั้น 1</p></figcaption></figure>

ห้อง Financial, Marketing, HR, canteen, Open Co-Working Space, Living room, Phone Booth, Network Room, Meeting room, Multi faith spaces, Lobby และห้องน้ำ
{% endtab %}
{% endtabs %}

## สำนักงานใหญ่ (HQ) ชั้น 2

{% tabs %}
{% tab title="Physical Topology" %}
<figure><img src="../.gitbook/assets/physical-hq-2f.jpg" alt="Physical Topology HQ ชั้น 2"><figcaption><p>Physical Topology HQ ชั้น 2</p></figcaption></figure>

* Access Point × 6 ที่ CEO room, Management, หน้า Data Center, Open Co-Working Space, หน้า Meeting room และโถงข้างห้องน้ำ
* Catalyst 9800-L WLC × 1
* Access Switch × 1 (stack)
* FortiGate 200F × 2 และ Catalyst 9300-48P × 2 (Core stack) ใน Network Room
* Nexus 93180YC-FX × 2 ในห้อง Data Center
* WAN เชื่อม Internet และ Branch
{% endtab %}

{% tab title="Wi-Fi Heat Map" %}
<figure><img src="../.gitbook/assets/heatmap-hq-2f.jpg" alt="Wi-Fi Heat Map HQ ชั้น 2 (AP 7–12)"><figcaption><p>Wi-Fi Heat Map HQ ชั้น 2 (AP 7–12)</p></figcaption></figure>

เพิ่ม AP เป็น 6 ตัว (เดิม 5) เพื่อให้สัญญาณครอบคลุมโถง Open Co-Working Space ที่กว้าง รวมถึงห้อง Onsen, Meeting room และ Network Room ด้านล่าง
{% endtab %}

{% tab title="Floor Plan" %}
<figure><img src="../.gitbook/assets/floorplan-hq-2f.jpg" alt="ผังห้อง HQ ชั้น 2"><figcaption><p>ผังห้อง HQ ชั้น 2</p></figcaption></figure>

ห้อง CEO room, Management, IT, Data Center, Open Co-Working Space, Onsen, Meeting room, Network Room และห้องน้ำ
{% endtab %}
{% endtabs %}

| สาย | ใช้กับ |
| --- | --- |
| 1 Gbps UTP-CAT6 | AP และอุปกรณ์ปลายทาง |
| Fiber OM4 | riser ระหว่างชั้น และ Core → Datacenter |
| 10 Gbps Fiber Optic | ระหว่าง Core และ Firewall |

## Sale Office

{% tabs %}
{% tab title="Physical Topology" %}
<figure><img src="../.gitbook/assets/physical-sale-office.jpg" alt="Physical Topology Sale Office"><figcaption><p>Physical Topology Sale Office</p></figcaption></figure>

* Access Point × 2 ที่ CO-Working Space และโถงทางเข้า
* Access Switch × 1
* FortiGate 40F Firewall × 1 เชื่อม Internet ไปยัง Headquarter
{% endtab %}

{% tab title="Wi-Fi Heat Map" %}
<figure><img src="../.gitbook/assets/heatmap-sale-office.jpg" alt="Wi-Fi Heat Map Sale Office (AP 13–14)"><figcaption><p>Wi-Fi Heat Map Sale Office (AP 13–14)</p></figcaption></figure>

AP 2 ตัวครอบคลุมพื้นที่ 207.37 m² ทั้งหมด รวมถึงห้องประชุม ห้อง Printer & Storage และห้องน้ำ
{% endtab %}

{% tab title="Floor Plan" %}
<figure><img src="../.gitbook/assets/floorplan-sale-office.jpg" alt="ผังห้อง Sale Office"><figcaption><p>ผังห้อง Sale Office</p></figcaption></figure>

ห้อง CO-Working Space, Guest Area, Private Meeting Room, Network room, Printer & Storage, Meeting Room และห้องน้ำ
{% endtab %}
{% endtabs %}
