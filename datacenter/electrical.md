---
icon: bolt
cover: ../.gitbook/assets/banner-datacenter.jpg
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

# Electrical System

เส้นทางไฟฟ้า: **Utility → RMU → หม้อแปลง → MDB → ATS → EMDB → UPS A/B → PDU → อุปกรณ์ IT (จ่ายไฟคู่)**

<figure><img src="../.gitbook/assets/electrical-en.jpg" alt="Electrical system: เส้นทางไฟฟ้าแบบ 2N (Path A / Path B)"><figcaption><p>Electrical system: เส้นทางไฟฟ้าแบบ 2N (Path A / Path B)</p></figcaption></figure>

| อุปกรณ์ | รายละเอียด |
| --- | --- |
| MEA 22 kV | สายป้อนเดี่ยว |
| RMU | LBS |
| หม้อแปลง | 500 kVA dry-type |
| MDB | ตู้ไฟหลัก |
| ATS | สลับแหล่งจ่ายอัตโนมัติ |
| Diesel generator | 60 kVA สำรองน้ำมัน 24 ชม. ต่อเข้า ATS สตาร์ทและรับโหลดเต็มใน 10–60 วินาที |
| EMDB | ตู้ไฟฉุกเฉิน |
| Mechanical DB | CRAC 1/2 ต่อเครื่องปั่นไฟ ไม่ผ่าน UPS |
| Path A / Path B | UPS 20 kVA online → แบตเตอรี่ Li-ion สำรอง 15 นาที → PDU (มีมิเตอร์) → Rack PDU (0U ทุกแร็ค) |

ทั้งสองเส้นทางอิสระต่อกันแบบ **2N** เซิร์ฟเวอร์ สตอเรจ และสวิตช์ทุกตัวมี dual power supply เสียบทั้งเส้น A และ B พร้อมกัน

## เมื่อไฟฟ้าดับ

{% stepper %}
{% step %}
### t = 0
ไฟฟ้าดับหรือแรงดันตกนอกเกณฑ์ ระบบตรวจจับได้ทันที
{% endstep %}
{% step %}
### 0–10 ms
UPS รับโหลดทันที ระบบ online double-conversion ทำให้ไม่มีการสลับแหล่งจ่าย (zero transfer time)
{% endstep %}
{% step %}
### 10–60 วินาที
ATS สั่งเครื่องปั่นไฟดีเซล 60 kVA เริ่มทำงาน และรับโหลดเต็มภายในไม่ถึง 1 นาที
{% endstep %}
{% step %}
### ไม่เกิน 15 นาที
งบเวลาของแบตเตอรี่ Li-ion เครื่องปั่นไฟต้องมาทันก่อนหมดเวลานี้
{% endstep %}
{% step %}
### เมื่อไฟกลับมา
ATS สลับกลับไปใช้ไฟการไฟฟ้าตามลำดับ เครื่องปั่นไฟทำงานต่ออีกครู่เพื่อ cool-down
{% endstep %}
{% endstepper %}

| ตัวเลข | ค่า |
| --- | --- |
| โหลด IT | 8.0 kW |
| UPS | 2 × 20 kVA (2N) |
| สำรองแบตเตอรี่ | Li-ion 15 นาที |
| เครื่องปั่นไฟ | 60 kVA · น้ำมัน 24 ชม. |
| โหลดรวมอาคาร | ~13 kW → PUE 1.6 |

เลือกแบตเตอรี่ Li-ion แทน VRLA เพราะอายุการใช้งานยาวกว่า (8–12 ปี เทียบกับ 3–5 ปี) และใช้พื้นที่ติดตั้งน้อยกว่ามาก ซึ่งสำคัญสำหรับอาคารสำนักงาน
