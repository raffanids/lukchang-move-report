---
icon: diagram-project
cover: ../.gitbook/assets/banner-ux-ui.jpg
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

# User Flow

แต่ละบทบาทมีขั้นตอนการใช้งานต่างกัน เลือกแท็บเพื่อดู flow ของผู้ใช้แต่ละกลุ่ม

{% tabs %}
{% tab title="Sender" %}
<figure><img src="../.gitbook/assets/userflow-sender.jpg" alt="User Flow ของผู้ส่ง"><figcaption><p>User Flow ของผู้ส่ง</p></figcaption></figure>

{% stepper %}
{% step %}
### ขั้นที่ 1
เปิดแอป แล้วระบุประเภทพัสดุ
{% endstep %}
{% step %}
### ขั้นที่ 2
ถ้ารู้ขนาดพัสดุ ให้กรอกขนาด จำนวน และปลายทาง แล้วเลือกขนาดรถ
{% endstep %}
{% step %}
### ขั้นที่ 3
ถ้าไม่รู้ขนาด ให้ถ่ายรูปพัสดุและระบุปลายทาง (Proposal วางแผนให้ AI ประเมินขนาดและแนะนำขนาดรถ)
{% endstep %}
{% step %}
### ขั้นที่ 4
ระบบแสดงราคาประเมิน ผู้ส่งยืนยันและชำระเงิน
{% endstep %}
{% step %}
### ขั้นที่ 5
รอคนขับมารับ แล้วติดตามสถานะแบบ real-time
{% endstep %}
{% step %}
### ขั้นที่ 6
พัสดุถึงปลายทาง จบขั้นตอน
{% endstep %}
{% endstepper %}
{% endtab %}

{% tab title="Driver" %}
<figure><img src="../.gitbook/assets/userflow-driver.jpg" alt="User Flow ของผู้ขับ"><figcaption><p>User Flow ของผู้ขับ</p></figcaption></figure>

{% stepper %}
{% step %}
### ขั้นที่ 1
เปิดแอป แล้วรับแจ้งเตือนงานที่ระบบจับคู่ให้
{% endstep %}
{% step %}
### ขั้นที่ 2
ถ้าไม่รับงาน จะกลับไปรองานใหม่
{% endstep %}
{% step %}
### ขั้นที่ 3
ถ้ารับงาน กดยอมรับ แล้วนำทางไปจุดรับพัสดุ
{% endstep %}
{% step %}
### ขั้นที่ 4
ถ่ายรูปพัสดุก่อนส่ง แล้วนำทางไปปลายทาง
{% endstep %}
{% step %}
### ขั้นที่ 5
ยืนยันการส่งมอบด้วยลายเซ็นหรือรูปถ่ายของผู้รับ
{% endstep %}
{% step %}
### ขั้นที่ 6
รับเงิน จบขั้นตอน
{% endstep %}
{% endstepper %}
{% endtab %}

{% tab title="Admin" %}
<figure><img src="../.gitbook/assets/userflow-admin.jpg" alt="User Flow ของ Admin"><figcaption><p>User Flow ของ Admin</p></figcaption></figure>

{% stepper %}
{% step %}
### ขั้นที่ 1
ล็อกอินผ่านเครือข่ายบริษัท
{% endstep %}
{% step %}
### ขั้นที่ 2
เข้า Dashboard แล้วดูสถานะการจัดส่งทั้งหมด
{% endstep %}
{% step %}
### ขั้นที่ 3
ตรวจข้อมูล KYC ของผู้ขับ
{% endstep %}
{% step %}
### ขั้นที่ 4
จัดการคำร้องเรียนและปัญหา
{% endstep %}
{% step %}
### ขั้นที่ 5
จบขั้นตอน
{% endstep %}
{% endstepper %}
{% endtab %}
{% endtabs %}
