---
icon: flag-checkered
cover: ../.gitbook/assets/banner-project.jpg
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

# Conclusion

Lukchang Move ทำให้การส่งพัสดุชัดเจน ปลอดภัย และมี AI ช่วยดูแลลูกค้า

## สรุปผลงาน

* **ผลิตภัณฑ์:** แอปผู้ส่งและผู้ขับบน Flutter พร้อม KYC Management Dashboard ครอบคลุมการสั่ง จองล่วงหน้า ติดตาม แชท และยืนยันการส่งมอบ
* **AI:** Support Chatbot แบบ Hybrid ตอบคำถามพบบ่อยทันทีด้วย Decision Tree และส่งต่อเคสซับซ้อนให้ LLM ที่รันบน GPU ของบริษัท โดยแบ่งระดับ Tier 1 ถึง 3 ตามความเสี่ยง
* **Cloud:** ย้ายทุกอย่างบน customer request path ขึ้น AWS Bangkok แบบ Multi-AZ ลด round trip ข้ามระบบจาก ~31 เหลือ 0 ถ้าการเชื่อมต่อกับ Private Datacenter มีปัญหา ลูกค้าก็ไม่รู้สึก
* **Datacenter:** ห้อง DC ขนาดเล็ก 8 kW ไฟฟ้าแบบ 2N และระบบทำความเย็นสำรองแบบ Double รองรับ LLM, งานภายใน และ backup งบประมาณ ฿12.285M
* **Network:** HQ 2 ชั้นและ Sale Office เชื่อมด้วย IPSec VPN ไม่มี Single Point of Failure ในจุดสำคัญ งบประมาณรวม ฿3.532M

## ข้อจำกัด

* FAQ Classifier ยังมี dataset เพียง 216 ตัวอย่าง ตอบประโยคใหม่ถูก 12/18 (66.7%) ยังต้องเพิ่มข้อมูลอีก
* Private Datacenter ยังไม่ถึงมาตรฐาน TIA-942 Rated-3
* Amazon Location Service ยังไม่มีใน Region Bangkok ต้องเรียกไป Singapore (~30 ms)
