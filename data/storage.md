---
icon: database
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

# Data Storage

ทีมเลือกที่เก็บข้อมูลให้ตรงกับลักษณะของข้อมูลแต่ละประเภท

| ประเภทข้อมูล | เก็บที่ไหน | ขนาด | นโยบาย |
| --- | --- | --- | --- |
| Core transaction | Aurora PostgreSQL Multi-AZ (writer + reader) | 292 GB | เก็บ 5 ปี · PITR 35 วัน |
| Driver GPS | Kinesis → Firehose → S3 (Parquet) | 12.6 TB | ประวัติบน S3 5 ปี |
| ตำแหน่ง/เส้นทาง | Amazon Location Service | - | พิกัด เวลา รหัสผู้ใช้ ประวัติการเดินทาง |
| Chat text | DynamoDB (on-demand) | 9.6 GB | TTL 30 วัน ลบอัตโนมัติ |
| รูปส่งของ | S3 + Glacier (lifecycle) | 584 TB ใน 5 ปี | Standard → Glacier → ลบที่ 5 ปี |
| รูปในแชท | S3 | 3.84 TB | lifecycle ลบที่ 30 วัน |
| KYC documents | On-prem (Synology NAS) | 144 GB | เก็บ on-prem นอก critical path |
| CCTV | Synology NAS RAID 6 | 28 TB | rolling 30 วัน เขียนทับ |
| VM datastore | Dell PowerStore 500T | ~30 TB | snapshot รายวัน → NAS |

## ที่มาของตัวเลข

| ข้อมูล | วิธีคำนวณ | ผล |
| --- | --- | --- |
| Core transaction | 80,000 งาน × 2 KB = 160 MB/วัน × 1,825 วัน | ~292 GB |
| Driver GPS | 800 QPS × 86,400 s × 100 byte = 6.9 GB/วัน × 1,825 วัน | ~12.6 TB |
| Chat text | 640,000 ข้อความ × 500 byte = 320 MB/วัน × 30 วัน | ~9.6 GB |
| รูปส่งมอบ | 80,000 งาน × 2 รูป (รับ/ส่ง) × 2 MB = 320 GB/วัน × 5 ปี | ~584 TB |
| รูปในแชท | 1 ใน 10 ข้อความเป็นรูป 2 MB = 64,000 รูป = 128 GB/วัน × 30 วัน | ~3.84 TB |
| เอกสาร KYC | ผู้ขับสะสม ~12,000 คนใน 5 ปี × 4 เอกสาร × 3 MB (อัปโหลดครั้งเดียวตอนสมัคร) | ~144 GB |
| CCTV | 28 กล้อง × 1 TB/เดือน (1080p H.264) แบบ rolling 30 วัน | ~28 TB |

{% hint style="info" %}
Progress 2 วางแผนเก็บ GPS ใน Kafka/TimescaleDB และแชทใน MongoDB ตั้งแต่ Progress 4 เปลี่ยนเป็น Kinesis → S3 และ DynamoDB ตามตารางด้านบน
{% endhint %}

## S3 Lifecycle ของรูปส่งของ

ลดค่าเก็บเป็นขั้นตามความถี่ในการเรียกดู โดยข้อมูลยังอยู่ครบตาม retention 5 ปี

| ช่วงอายุ | Storage class |
| --- | --- |
| 0–30 วัน | S3 Standard |
| 30–90 วัน | S3 Standard-IA |
| 90 วัน–1 ปี | S3 Glacier Instant Retrieval |
| 1–5 ปี | S3 Glacier Deep Archive |
| เกิน 5 ปี | ลบทิ้ง |

## แผนสำรองข้อมูล 3-2-1

| สำเนา | ที่เก็บ |
| --- | --- |
| สำเนา 1 | Aurora Multi-AZ + PowerStore |
| สำเนา 2 | Veeam → Synology NAS (immutable snapshot) |
| สำเนา 3 | S3 Glacier Deep Archive |

ดูโครงสร้างตารางของฐานข้อมูลหลักได้ที่ [ER Diagram](er-diagram.md)
