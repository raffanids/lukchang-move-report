---
icon: snowflake
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

# Cooling

พื้นที่ Data Hall 30 ตร.ม. แถวเดียว ใช้ Cold aisle containment และไม่มีพื้นยก (raised floor)

## ทำไมเลือกทำความเย็นด้วยอากาศ ไม่ใช่ของเหลว

* ความหนาแน่นต่อแร็คอยู่ที่ 1.8 kW ระบบอากาศรองรับได้ถึง 20–30 kW/แร็ค
* ระบบของเหลว (D2C / immersion) จะคุ้มค่าตั้งแต่ ~40 kW/แร็คขึ้นไปเท่านั้น
* เครื่องปรับอากาศ precision แบบ DX ไม่ต้องมี chiller plant จนกว่าโหลดจะเกิน ~100 kW
* Containment และแผงปิดช่องว่างช่วยลดลมร้อนไหลย้อนกลับเข้าฝั่งเย็น
* แผนการเติบโต: หากแร็ค GPU มีโหลดเกิน 10 kW/แร็ค จะย้ายไปใช้ in-row cooling + RDHx

## การคำนวณโหลดความร้อน

```
Q = m × Cp × dT
ความร้อนรวม = IT 8.0 + UPS loss 0.4 + แสงสว่าง 0.5 + envelope 0.8 = 9.7 kW = 2.76 TR
m = 9.7 / (1.005 × 12 K) = 0.80 kg/s
V = 0.80 / 1.2 = 0.67 m³/s ≈ 1,420 CFM
```

**เลือกใช้:** เครื่องปรับอากาศ precision 12 kW DX จำนวน 2 เครื่อง แบบ N+1 เครื่องใดเครื่องหนึ่งรองรับโหลดทั้งหมดได้ 100% ถ้าเครื่องหนึ่งหยุดหรือเข้าซ่อมบำรุง อีกเครื่องยังทำความเย็นได้ตามปกติ

## สภาพแวดล้อมที่ควบคุม

| รายการ | ค่า |
| --- | --- |
| อุณหภูมิลมจ่าย | 22 °C |
| ความชื้นสัมพัทธ์ | 50 % |
| มาตรฐาน | ASHRAE Class A1 |
| Cold aisle | กว้าง 1.2 ม. ปิดสนิท |
