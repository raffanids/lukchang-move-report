---
icon: user-shield
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

# Admin

Admin ใช้งานผ่าน **KYC Management Dashboard** บน Web browser สำหรับตรวจสอบ แก้ปัญหา และดูข้อมูลหลังบ้าน

<figure><img src="../.gitbook/assets/admin-dashboard.jpg" alt="KYC Management Dashboard"><figcaption><p>KYC Management Dashboard</p></figcaption></figure>

| ส่วน | หน้าที่ |
| --- | --- |
| จำนวนออเดอร์ | ดูภาพรวมจำนวนออเดอร์ในระบบ |
| รายได้ | ดูสรุปรายได้ของแพลตฟอร์ม |
| ตรวจเอกสารผู้ขับ | ตรวจเอกสาร KYC ก่อนอนุมัติให้ผู้ขับรับงาน เป็นหัวใจที่ทำให้ผู้ส่งไว้ใจผู้ขับได้ |
| AI Escalation Inbox | รวมเคสที่ Chatbot ส่งต่อมา (Tier 2B และ Tier 3) ให้ Admin ตรวจตาม SLA |

## หน้าจอแต่ละส่วน

ภาพรายละเอียดด้านล่างมาจากงานออกแบบใน Progress 2

{% tabs %}
{% tab title="ภาพรวม" %}
<figure><img src="../.gitbook/assets/admin-login-overview.jpg" alt="หน้าเข้าสู่ระบบและ Analytics Hub"><figcaption><p>หน้าเข้าสู่ระบบและ Analytics Hub</p></figcaption></figure>

หน้า Analytics Hub แสดงจำนวนออเดอร์ รายได้ แนวโน้มรายได้ สัดส่วนสถานะงาน และผู้ขับยอดนิยม
{% endtab %}

{% tab title="ออเดอร์" %}
<figure><img src="../.gitbook/assets/admin-orders.jpg" alt="รายการออเดอร์และรายละเอียดออเดอร์"><figcaption><p>รายการออเดอร์และรายละเอียดออเดอร์</p></figcaption></figure>

ค้นหาและกรองออเดอร์ตามสถานะ กดเปิดดูรายละเอียด แชท และราคาของแต่ละงาน
{% endtab %}

{% tab title="AI Escalation" %}
<figure><img src="../.gitbook/assets/admin-ai-inbox.jpg" alt="AI Escalation Inbox"><figcaption><p>AI Escalation Inbox</p></figcaption></figure>

รวมเคสที่ Chatbot ส่งต่อ พร้อม AI Conversation Summary ระดับความเร่งด่วน และ SLA ให้ Admin ตอบต่อในแชทเดียวกัน
{% endtab %}

{% tab title="ตรวจ KYC" %}
<figure><img src="../.gitbook/assets/admin-kyc-list.jpg" alt="รายการผู้ขับที่รอตรวจ KYC"><figcaption><p>รายการผู้ขับที่รอตรวจ KYC</p></figcaption></figure>

<figure><img src="../.gitbook/assets/admin-kyc-review.jpg" alt="หน้าตรวจเอกสาร KYC ของผู้ขับ"><figcaption><p>หน้าตรวจเอกสาร KYC ของผู้ขับ</p></figcaption></figure>

Admin เปิดดูเอกสารแต่ละใบ ติ๊ก checklist แล้วกดอนุมัติหรือปฏิเสธ
{% endtab %}

{% tab title="ปัญหา / Ticket" %}
<figure><img src="../.gitbook/assets/admin-tickets.jpg" alt="รายการปัญหาที่ผู้ใช้แจ้ง"><figcaption><p>รายการปัญหาที่ผู้ใช้แจ้ง</p></figcaption></figure>

แยก ticket ตามสถานะและความเร่งด่วน พร้อมตัวนับ SLA
{% endtab %}

{% tab title="ผู้ขับ" %}
<figure><img src="../.gitbook/assets/admin-drivers.jpg" alt="จัดการผู้ขับ"><figcaption><p>จัดการผู้ขับ</p></figcaption></figure>

ดูรายชื่อผู้ขับ คะแนน จำนวนงาน และสถานะบัญชี
{% endtab %}
{% endtabs %}

เอกสาร KYC ของผู้ขับเก็บไว้ที่ on-prem (Synology NAS ใน Private Datacenter) นอก critical request path ดูรายละเอียดที่ [Server & Storage](../datacenter/server-storage.md)
