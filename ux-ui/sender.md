---
icon: box
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

# Sender

แอปผู้ส่งครอบคลุมการสั่ง หาคนขับ และติดตามพัสดุ

{% tabs %}
{% tab title="เข้าสู่ระบบ" %}
<figure><img src="../.gitbook/assets/sender-login.jpg" alt="หน้าเข้าสู่ระบบและสมัครสมาชิก (Progress 2)"><figcaption><p>หน้าเข้าสู่ระบบและสมัครสมาชิก (Progress 2)</p></figcaption></figure>

ผู้ส่งเข้าสู่ระบบด้วยอีเมลหรือเบอร์โทรศัพท์ (ยืนยันด้วย OTP) หรือใช้บัญชี Google / Apple
{% endtab %}

{% tab title="ส่งพัสดุและหาคนขับ" %}
<figure><img src="../.gitbook/assets/sender-order.jpg" alt="หน้าส่งพัสดุและหาคนขับ"><figcaption><p>หน้าส่งพัสดุและหาคนขับ</p></figcaption></figure>

ผู้ส่งเริ่มจากสร้างรายการส่ง ใส่ขนาด จำนวน และประเภทพัสดุ จากนั้นระบบช่วยหาคนขับให้ ทุกขั้นตอนอยู่ในแอปเดียว ไม่ต้องไปหาคนขนของในโซเชียลมีเดีย
{% endtab %}

{% tab title="จองส่งพัสดุล่วงหน้า" %}
<figure><img src="../.gitbook/assets/sender-booking-history.jpg" alt="จองพัสดุล่วงหน้าและประวัติการส่ง"><figcaption><p>จองพัสดุล่วงหน้าและประวัติการส่ง</p></figcaption></figure>

การจองล่วงหน้าแบ่งเป็น 6 ขั้นตอน

{% stepper %}
{% step %}
### ข้อมูลพัสดุ
กรอกขนาด กว้าง × สูง × ลึก (ซม.) และน้ำหนัก (กก.) เลือกว่าเป็นสินค้าแตกง่าย/เปราะบางหรือไม่ (ระบบจะแสดงคำเตือนให้คนขับ) และต้องถ่ายรูปหรืออัปโหลดรูปพัสดุก่อนดำเนินการต่อ
{% endstep %}
{% step %}
### ประเภทยานพาหนะ
เลือกประเภทยานพาหนะตามขนาดและน้ำหนักพัสดุของคุณ
{% endstep %}
{% step %}
### ที่อยู่
ระบุที่อยู่ต้นทางที่จะให้ไปรับพัสดุ และปลายทางที่จะให้ไปส่ง
{% endstep %}
{% step %}
### วัน-เวลา
เลือกวันที่จากปฏิทิน และเลือกเวลารับพัสดุตั้งแต่ 08:00 ถึง 18:00
{% endstep %}
{% step %}
### ข้อมูลผู้รับ
ระบุชื่อผู้รับ เบอร์โทรผู้รับ และหมายเหตุถึงคนขับ
{% endstep %}
{% step %}
### สรุปรายการ
แสดงรายละเอียดทั้งหมดที่ระบุไว้ก่อนหน้า เพื่อเตรียมไปชำระเงินต่อไป
{% endstep %}
{% endstepper %}

**การจองของฉัน:** แยกแท็บ กำลังจะมาถึง / ทั้งหมด / สำเร็จ / ยกเลิก แต่ละรายการแสดงเวลา เส้นทาง ประเภทรถ ผู้รับ และราคา พร้อมปุ่มดูรายละเอียดและยกเลิกการจอง
{% endtab %}

{% tab title="ติดตามสถานะ" %}
<figure><img src="../.gitbook/assets/tracking-location.jpg" alt="หน้าติดตามสถานะพร้อมแผนที่และ ETA"><figcaption><p>หน้าติดตามสถานะพร้อมแผนที่และ ETA</p></figcaption></figure>

เมื่อมีผู้ขับรับงาน ผู้ส่งเห็นตำแหน่งผู้ขับบนแผนที่ ETA และข้อมูลผู้ขับ (ชื่อ คะแนน ทะเบียนรถ รุ่นรถ) พร้อมปุ่มโทรและแชท สถานะแบ่งเป็นลำดับดังนี้

{% stepper %}
{% step %}
### ขั้นที่ 1
รับงานแล้ว
{% endstep %}
{% step %}
### ขั้นที่ 2
กำลังไปรับพัสดุ
{% endstep %}
{% step %}
### ขั้นที่ 3
รับพัสดุแล้ว (มีรูปถ่าย)
{% endstep %}
{% step %}
### ขั้นที่ 4
กำลังเดินทางไปส่ง
{% endstep %}
{% step %}
### ขั้นที่ 5
ส่งสำเร็จ (มีรูปถ่าย)
{% endstep %}
{% endstepper %}

ข้อมูลตำแหน่งจัดการผ่าน **Amazon Location Service** ซึ่งรองรับแผนที่ การติดตาม และ Geofencing โดยเก็บพิกัด Latitude/Longitude เวลาที่บันทึก รหัสอุปกรณ์/ผู้ใช้ และประวัติการเดินทาง พร้อมกำหนดสิทธิ์และระยะเวลาการจัดเก็บข้อมูลให้ชัดเจน

<figure><img src="../.gitbook/assets/sender-tracking.jpg" alt="หน้าติดตามสถานะพัสดุ"><figcaption><p>หน้าติดตามสถานะพัสดุ</p></figcaption></figure>
{% endtab %}

{% tab title="โปรไฟล์และการตั้งค่า" %}
<figure><img src="../.gitbook/assets/sender-profile.jpg" alt="โปรไฟล์และการตั้งค่า (Progress 2)"><figcaption><p>โปรไฟล์และการตั้งค่า (Progress 2)</p></figcaption></figure>

* ข้อมูลบัญชี: ชื่อ เบอร์โทร อีเมล และที่อยู่เริ่มต้น แก้ไขได้
* วิธีชำระเงิน: บัตร, TrueMoney Wallet, Rabbit LINE Pay และเพิ่มวิธีใหม่ได้
* การแจ้งเตือน ภาษา และการตั้งค่าอื่นๆ
{% endtab %}
{% endtabs %}
