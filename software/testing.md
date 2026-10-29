# Testing

| ประเภท | เครื่องมือ | ทดสอบอะไร |
| --- | --- | --- |
| Unit / Widget test | flutter test | logic และหน้าจอของแอป Flutter |
| Integration test | Flutter integration test | flow การใช้งานต่อเนื่องในแอป |
| API test | Postman | endpoint ของ Backend |
| Load test | Apache JMeter | ความสามารถรองรับโหลดของ API |
| AI test | LOOCV, novel-phrase test | ความแม่นยำของ FAQ Classifier (ดู [Evaluation](../ai/evaluation.md)) |

{% hint style="warning" %}
**[เติม]** ผลการทดสอบจริง เช่น จำนวน test case ที่ผ่าน และผล load test จาก JMeter (requests/s, latency)
{% endhint %}
