---
icon: location-dot
cover: ../.gitbook/assets/banner-cloud.jpg
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

# Location & GPS Pipeline

## Amazon Location Service

<figure><img src="../.gitbook/assets/tracking-location.jpg" alt="การติดตามตำแหน่งด้วย Amazon Location Service"><figcaption><p>การติดตามตำแหน่งด้วย Amazon Location Service</p></figcaption></figure>

* **GPS:** ระบุตำแหน่งจากดาวเทียมโดยตรง เหมาะกับการระบุตำแหน่งของอุปกรณ์
* **Amazon Location Service:** จัดการข้อมูลตำแหน่งผ่าน Cloud เหมาะกับแผนที่ การติดตาม และ Geofencing ใช้ Routes (ราคา, ETA, route matrix), Places (ค้นที่อยู่, geocode) และ Maps (tiles ในแอป)

บริการนี้ยังไม่มีใน Region Bangkok ระบบจึงเรียกไปที่ Singapore ผ่าน NAT Gateway ใช้เวลาประมาณ 30 ms

ขอบเขตข้อมูลที่เก็บ

* พิกัด Latitude / Longitude
* เวลาที่บันทึกตำแหน่ง
* รหัสอุปกรณ์/ผู้ใช้
* ประวัติการเดินทาง (Location History)
* กำหนดสิทธิ์และระยะเวลาการจัดเก็บข้อมูลให้ชัดเจน

## GPS Pipeline

| ขั้น | บริการ | หน้าที่ |
| --- | --- | --- |
| 1 | แอปผู้ขับ | ส่งพิกัดทุก 5 วินาที |
| 2 | Location ingest (ECS Fargate) | รับพิกัดเข้าระบบ |
| 3 | Kinesis Data Streams (1 shard) | เป็นบัฟเฟอร์รับข้อมูล ~800 records/s |
| 4 | Kinesis Data Firehose → S3 | รวมเป็นไฟล์ Parquet เก็บ 5 ปี (12.6 TB) |
| 5 | Athena | ค้นประวัติเส้นทางย้อนหลังด้วย SQL เมื่อต้องการ |

ข้อมูลตำแหน่งปริมาณมากจึงไม่ไปแย่งใช้ฐานข้อมูลหลัก และเก็บบน S3 ได้ในราคาถูก
