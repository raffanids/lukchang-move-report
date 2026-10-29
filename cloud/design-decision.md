# Design Decision

ย้าย customer request path ทั้งหมดขึ้น AWS ทำให้ synchronous round trip ข้ามไปยัง Private Datacenter ลดจากประมาณ 31 ครั้งเหลือ 0 ส่วน Private DC เก็บเฉพาะ LLM, backup และงานภายใน
