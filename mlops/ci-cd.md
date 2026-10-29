---
icon: code-branch
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

# CI/CD

| ส่วน | เครื่องมือ | ขั้นตอน |
| --- | --- | --- |
| แอปและ Backend | Docker + GitHub Actions | build และ test อัตโนมัติ แล้ว build image |
| Container registry | Amazon ECR | เก็บ image (เข้าผ่าน VPC Endpoint) |
| Deploy | ECS rolling deploy บน Fargate | ปล่อยทีละ task ถ้ามีปัญหา rollback กลับเป็น image เดิม |
| FAQ Classifier | GitLab CI (on-prem) | เทรน → ทดสอบ → bake โมเดลลง image |
| LLM adapter | MLflow Registry → vLLM | canary ก่อนเปิดเต็ม และสลับกลับได้ทันที |
