---
icon: gauge-high
cover: ../.gitbook/assets/banner-data.jpg
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

# Capacity & QPS

ตัวเลขที่ใช้ออกแบบระบบ

| รายการ | ค่า |
| --- | --- |
| ผู้ส่งต่อวัน (DAU) | 40,000 คน |
| งานต่อวัน | 80,000 งาน |
| Write QPS ของธุรกรรมหลัก | 2.8 |
| คนขับที่กำลังวิ่งงานพร้อมกัน | 4,000 คน |
| ความถี่ส่งพิกัด | ทุก 5 วินาที |
| GPS write | 4,000 ÷ 5 = **800 ครั้งต่อวินาที** |
| Retention ข้อมูลหลัก | 5 ปี |

## สมมติฐาน (Chiang Mai Baseline)

| สมมติฐาน | ค่า | ที่มา |
| --- | --- | --- |
| Active Senders (DAU) | 40,000 | ~2.2% ของประชากรเขตเมือง 1.8 ล้านคน (กรมการปกครอง พ.ศ. 2568) |
| Active Drivers (DAU) | 4,000 | อัตราผู้ส่งต่อผู้ขับ 10:1 (~1 คนต่อประชากร 450 คน) |
| Daily Deliveries | 80,000 งาน/วัน | ผู้ส่งเฉลี่ย 2 งาน/คน |
| Driver GPS ping | ทุก 5 วินาที | ขณะกำลังวิ่งงาน |
| Core data retention | 5 ปี | ธุรกรรม การเงิน GPS และรูปส่งมอบ |
| Communications retention | TTL 30 วัน | ข้อความและรูปในแชท |

## QPS แยกตามฟีเจอร์

| ฟีเจอร์ | วิธีคำนวณ | ผล |
| --- | --- | --- |
| Core transactions (สร้างงาน รับงาน ชำระเงิน) | 80,000 งาน × 3 operations = 240,000 ÷ 86,400 s | **~2.8 Write QPS** |
| Driver location broadcasting | 4,000 คน ÷ 5 s | **800 Write QPS** |
| Sender live map tracking | 5% ของผู้ส่ง (2,000 คน) ดูแผนที่พร้อมกัน poll ทุก 5 s | **400 Read QPS** |
| Chat messaging | 80% ของงานมีแชท (64,000 แชท) × 10 ข้อความ = 640,000 ÷ 86,400 s | **~7.4 Write QPS** |
| In-app voice call (VoIP / WebRTC) | 10% ของแชทโทรต่อ (6,400 สาย/วัน) เฉลี่ย 2 นาที | **~80 concurrent WebSocket** ช่วงเร่งด่วน |
| Push notifications | 80,000 งาน × 4 ครั้ง (สร้าง รับ ใกล้ถึง ส่งสำเร็จ) = 320,000 ÷ 86,400 s | **~3.7 Event QPS** |

## ทำไม GPS ไม่เขียนลงฐานข้อมูลหลัก

ถ้าเขียนทุก ping ลง Aurora จะมีการเขียน 800 ครั้งต่อวินาทีตลอดวัน ทั้งที่ข้อมูลส่วนใหญ่ใช้ดูย้อนหลังเท่านั้น ทีมจึงส่ง GPS ผ่านท่อแยก

**แอปผู้ขับ → Location ingest (ECS) → Kinesis Data Streams → Firehose → S3 (Parquet) → Athena**

{% stepper %}
{% step %}
### แอปผู้ขับ
ส่งพิกัดทุก 5 วินาที
{% endstep %}
{% step %}
### Location ingest
บริการบน ECS Fargate รับพิกัดเข้าระบบ
{% endstep %}
{% step %}
### Kinesis Data Streams
1 shard เป็นบัฟเฟอร์
{% endstep %}
{% step %}
### Firehose → S3
เก็บเป็นไฟล์ Parquet
{% endstep %}
{% step %}
### Athena
ค้นประวัติเส้นทางย้อนหลังด้วย SQL
{% endstep %}
{% endstepper %}

Kinesis 1 shard รับเขียนได้สูงสุดประมาณ 1,000 records ต่อวินาทีหรือ 1 MB ต่อวินาที พิกัดหนึ่งครั้งมีขนาดประมาณ 100 byte รวมประมาณ 80 KB ต่อวินาที จึงใช้ 1 shard ได้ ถ้าชั่วโมงเร่งด่วนเกิน 1,000 ต่อวินาทีสามารถเพิ่ม shard ได้

