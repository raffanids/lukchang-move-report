---
icon: sitemap
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

# Software Architecture

Backend ออกแบบเป็นบริการแยกตามหน้าที่ รันเป็น container บน **Amazon ECS Fargate** ในทุก Availability Zone

| บริการ | หน้าที่ |
| --- | --- |
| Job / Order | สร้างและจัดการรายการส่ง การจอง และสถานะงาน |
| Matching + Routing | จับคู่งานกับผู้ขับ และคำนวณเส้นทาง/ราคา/ETA ผ่าน Amazon Location Service |
| Payment | รับชำระเงินผ่าน Payment Gateway (บัตร และ QR PromptPay) |
| Location ingest | รับพิกัดจากแอปผู้ขับ ส่งต่อเข้า Kinesis Data Streams |
| Chat + AI | แชทระหว่างผู้ส่งกับผู้ขับ และ AI Support Chatbot (FAQ Decision Tree) |
| Admin API | API สำหรับ KYC Management Dashboard |

## เส้นทางของ request

ลำดับตามหมายเลขใน [System Diagram](../cloud/system-diagram.md)

1. แอปถาม DNS จาก **Route 53** (มี health check)
2. request ผ่าน **CloudFront** (CDN + TLS termination) โดยมี **AWS WAF** (OWASP + rate limit) และ **Shield Standard** (DDoS) ป้องกัน
3. เข้า **API Gateway** (HTTP API + WebSocket API) และยืนยันตัวตนด้วย **Cognito** (user pool + JWT)
4. เมื่อ JWT ผ่านแล้ว API Gateway ส่งต่อผ่าน **VPC Link** ไปยัง Internal ALB
5. **Internal ALB** กระจาย request ไปยังบริการบน ECS Fargate ซึ่งอ่านเขียน Aurora ใน private subnet

งานที่ไม่ต้องรอผล (async) ใช้ **SQS + EventBridge** ส่วน push notification ใช้ **Amazon SNS** ส่งไปยัง FCM / APNs
