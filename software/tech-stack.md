---
icon: layer-group
cover: ../.gitbook/assets/banner-software.jpg
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

# Tech Stack

<figure><img src="../.gitbook/assets/tech-stack.jpg" alt="Tech Stack ของ Lukchang Move"><figcaption><p>Tech Stack ของ Lukchang Move</p></figcaption></figure>

| ส่วน | เทคโนโลยี | ใช้ทำอะไร |
| --- | --- | --- |
| Frontend | Flutter | แอปผู้ส่งและผู้ขับ (iOS / Android) จาก codebase เดียว |
| Backend | Go | บริการ Job, Matching, Payment, Location, Chat + AI และ Admin API |
| Database | PostgreSQL (Amazon Aurora) | ข้อมูลธุรกรรมหลัก |
| AI | Decision Tree + TF-IDF, Qwen บน vLLM | AI Support Chatbot แบบ Hybrid |
| Testing | flutter test, integration test, Postman, Apache JMeter | ทดสอบแอป API และ load test |
| DevOps | Docker, GitHub Actions | build image และ CI/CD |
| Cloud | AWS (ap-southeast-7 Bangkok) | รันระบบ production ทั้งหมดบน customer request path |
| Project Management & Collab | Notion, Discord | วางแผนงาน บันทึกประชุม ติดตามงานแต่ละทีม และสื่อสารภายในทีม |

{% hint style="info" %}
ใน Progress 2 ช่อง Database มี Redis ด้วย แต่สไลด์ Final เหลือเพียง PostgreSQL ส่วน ElastiCache Redis ยังใช้เป็น GEO index ใน [System Diagram](../cloud/system-diagram.md)
{% endhint %}

{% hint style="warning" %}
**[เติม]** เหตุผลที่เลือกแต่ละเทคโนโลยี เช่น ทำไมเลือก Flutter แทน native หรือทำไมเลือก Go
{% endhint %}
