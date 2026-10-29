---
icon: rocket
cover: ../.gitbook/assets/banner-mlops.jpg
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

# ML Deployment

<figure><img src="../.gitbook/assets/ml-deployment.jpg" alt="ML deployment"><figcaption><p>ML deployment</p></figcaption></figure>

| ส่วน | อยู่ที่ | รายละเอียด |
| --- | --- | --- |
| FAQ Classifier (Tier 1) | AWS · Chat + AI service บน ECS Fargate | Decision Tree + TF-IDF ตอบคำถามสำเร็จรูปทันที ไม่เรียก LLM |
| GPU 0 · vLLM serve 24/7 | Private DC (HQ) | Qwen3.8-27B-FP8 vision-language แยก Tier 2A / 2B / 3 ตาม System Prompt, L40S 48 GB (weight ~27 GB + KV cache) |
| Vector index (RAG) | Private DC | ค้นคู่มือ/FAQ ของบริษัทก่อนให้ LLM ตอบ |
| LoRA adapter | Private DC | โหลดเวอร์ชันที่ใช้งานจาก MLflow Registry สลับกลับได้ทันที |
| GPU 1 · train / batch | Private DC | fine-tune, embedding, ประเมินผล ไม่อยู่ในเส้นทางของผู้ใช้ และเป็น backup ให้ GPU 0 |
| DynamoDB · ประวัติแชท | AWS | เก็บ 30 วัน แล้ว ETL เป็น dataset สำหรับเทรน |
| Aurora · ตาราง ticket | AWS | ACID เพราะผูกกับการคืนเงิน |

การเชื่อมระหว่าง AWS กับ GPU on-prem ใช้ Transit Gateway → Direct Connect ใช้เวลาประมาณ 3 ms

## เมื่อ GPU 0 หรือ Direct Connect ล่ม

* Decision Tree รันบน cloud คำถาม Tier 1 ยังตอบได้ตามปกติ
* คำถามที่ต้องใช้ LLM จะเปิด ticket ทั่วไปให้ Admin (ยังไม่แยก tier)
* ถ้า GPU 0 ไม่ตอบ ระบบหยุด batch แล้วโหลดโมเดลบน GPU 1 แทน
