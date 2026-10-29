---
icon: house
description: แพลตฟอร์มส่งพัสดุที่ทำให้ผู้ส่งกับผู้ขับเจอกันได้อย่างมั่นใจ โดย Soog Free Me Company
cover: .gitbook/assets/banner-home.jpg
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

# Lukchang Move

**Lukchang Move** คือแพลตฟอร์มบริการส่งพัสดุที่ช่วยให้ผู้ส่งระบุขนาดและประเภทของพัสดุได้ชัดเจน หาผู้ขับที่ผ่านการตรวจสอบตัวตน (KYC) และติดตามพัสดุได้ตั้งแต่ต้นจนจบ โดยมี **AI Support Chatbot** คอยตอบคำถามและส่งต่อเคสให้ Admin เมื่อจำเป็น

โครงงานนี้เป็นส่วนหนึ่งของรายวิชา Advanced Computer Engineering พัฒนาโดยทีม **Soog Free Me Company** ซึ่งแบ่งงานเป็น 3 ทีม คือ Software, Systems และ Network

<a href="overview/about-us.md" class="button primary">เริ่มอ่านรายงาน</a> <a href="ai/overview.md" class="button secondary">ดู AI Chatbot</a> <a href="https://github.com/raffanids/lukchang-move-report" class="button secondary">GitHub</a>

## ตัวเลขสำคัญ

{% columns %}
{% column %}
<h2 align="center">40,000</h2>
<p align="center">ผู้ส่งต่อวัน (DAU)</p>
{% endcolumn %}

{% column %}
<h2 align="center">80,000</h2>
<p align="center">งานต่อวัน</p>
{% endcolumn %}

{% column %}
<h2 align="center">3 AZ</h2>
<p align="center">AWS Bangkok ไม่มี Single Point of Failure</p>
{% endcolumn %}

{% column %}
<h2 align="center">31 → 0</h2>
<p align="center">Round trip ข้ามระบบบน critical path</p>
{% endcolumn %}
{% endcolumns %}

## สิ่งที่อยู่ในรายงานนี้

<table data-view="cards"><thead><tr><th></th><th></th><th data-hidden data-card-cover data-type="files"></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody>
<tr><td><strong>Overview</strong></td><td>ปัญหา โซลูชัน กลุ่มผู้ใช้ และทีมงาน</td><td><a href=".gitbook/assets/banner-overview.jpg">banner-overview.jpg</a></td><td><a href="overview/about-us.md">overview/about-us.md</a></td></tr>
<tr><td><strong>UX/UI Design</strong></td><td>หน้าจอแอปผู้ส่ง ผู้ขับ Admin และ User Flow</td><td><a href=".gitbook/assets/banner-ux-ui.jpg">banner-ux-ui.jpg</a></td><td><a href="ux-ui/sender.md">ux-ui/sender.md</a></td></tr>
<tr><td><strong>Software Architecture</strong></td><td>Tech Stack, สถาปัตยกรรมซอฟต์แวร์ และการทดสอบ</td><td><a href=".gitbook/assets/banner-software.jpg">banner-software.jpg</a></td><td><a href="software/tech-stack.md">software/tech-stack.md</a></td></tr>
<tr><td><strong>Data & Storage</strong></td><td>Capacity, QPS และการออกแบบที่เก็บข้อมูล</td><td><a href=".gitbook/assets/banner-data.jpg">banner-data.jpg</a></td><td><a href="data/capacity-qps.md">data/capacity-qps.md</a></td></tr>
<tr><td><strong>AI Support Chatbot</strong></td><td>Hybrid Classifier + LLM, Support Tiers และผลการทดสอบ</td><td><a href=".gitbook/assets/banner-ai.jpg">banner-ai.jpg</a></td><td><a href="ai/overview.md">ai/overview.md</a></td></tr>
<tr><td><strong>Cloud Deployment</strong></td><td>System Diagram บน AWS Bangkok และเหตุผลการออกแบบ</td><td><a href=".gitbook/assets/banner-cloud.jpg">banner-cloud.jpg</a></td><td><a href="cloud/system-diagram.md">cloud/system-diagram.md</a></td></tr>
<tr><td><strong>MLOps</strong></td><td>ML Deployment, MLOps Pipeline และ ML Monitoring</td><td><a href=".gitbook/assets/banner-mlops.jpg">banner-mlops.jpg</a></td><td><a href="mlops/ml-deployment.md">mlops/ml-deployment.md</a></td></tr>
<tr><td><strong>Private Datacenter</strong></td><td>Rack, Server & Storage, ระบบไฟฟ้า, ระบบทำความเย็น และงบประมาณ</td><td><a href=".gitbook/assets/banner-datacenter.jpg">banner-datacenter.jpg</a></td><td><a href="datacenter/rack-design.md">datacenter/rack-design.md</a></td></tr>
<tr><td><strong>Network Design</strong></td><td>Topology, อุปกรณ์, Redundancy และ Network Services</td><td><a href=".gitbook/assets/banner-network.jpg">banner-network.jpg</a></td><td><a href="network/logical-topology.md">network/logical-topology.md</a></td></tr>
<tr><td><strong>Project</strong></td><td>การบริหารโครงการ ทีมงาน และบทสรุป</td><td><a href=".gitbook/assets/banner-project.jpg">banner-project.jpg</a></td><td><a href="project/management.md">project/management.md</a></td></tr>
</tbody></table>
