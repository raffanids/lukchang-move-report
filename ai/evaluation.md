---
icon: chart-simple
cover: ../.gitbook/assets/banner-ai.jpg
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

# Evaluation

ผลทดสอบ FAQ Classifier ล่าสุด (Final Presentation)

{% columns %}
{% column %}
<h2 align="center">71.0%</h2>
<p align="center">LOOCV precision เมื่อไม่ abstain</p>
{% endcolumn %}

{% column %}
<h2 align="center">8.2%</h2>
<p align="center">Confidently-wrong rate</p>
{% endcolumn %}

{% column %}
<h2 align="center">12/18</h2>
<p align="center">Novel-phrase test (66.7%)</p>
{% endcolumn %}
{% endcolumns %}

| การทดสอบ | ผล | ความหมาย |
| --- | --- | --- |
| Training examples | 216 ตัวอย่าง | ขนาด dataset ที่ใช้เทรน |
| Novel-phrase test | 12/18 ถูก (66.7%) | ประโยคที่โมเดลไม่เคยเห็น ส่วนที่เหลือโมเดล abstain |
| LOOCV precision เมื่อไม่ abstain | 71.0% | เมื่อโมเดลเลือกตอบ ตอบถูก 71% |
| LOOCV confidently-wrong rate | 8.2% | สัดส่วนที่โมเดลมั่นใจแต่ตอบผิด |

## การตีความผล

ตัวเลขยังไม่สูงมาก เพราะ dataset มีเพียง 216 ตัวอย่าง แต่ระบบออกแบบให้ Classifier เป็นด่านแรกเท่านั้น เมื่อไม่มั่นใจ ระบบจะ **ไม่ตอบเอง (abstain)** แล้วส่งต่อให้ LLM หรือ Admin สิ่งที่สำคัญที่สุดจึงเป็นการคุม confidently-wrong rate ให้ต่ำ

ในการ deploy มีเกณฑ์ว่า novel-phrase test และ confidently-wrong ต้องไม่เกินเกณฑ์ก่อนปล่อยโมเดลใหม่ ส่วน LLM ใช้ eval set ที่วัดว่าตอบถูก route ticket ถูกทีม และ escalate ไม่พลาด

{% hint style="info" %}
ใน Progress 3 โมเดลเทรนด้วย 166 ตัวอย่าง ได้ novel-phrase test 8/18 (44.4%) หลังเพิ่มข้อมูลเป็น 216 ตัวอย่างใน Final ผลขึ้นเป็น 12/18 (66.7%) โดย precision และ confidently-wrong rate เท่าเดิม
{% endhint %}
