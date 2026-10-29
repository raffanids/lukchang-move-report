# Location & GPS Pipeline

* ตำแหน่งคนขับจัดการผ่าน **Amazon Location Service** (Singapore ผ่าน NAT ประมาณ 30 ms)
* ประวัติพิกัด: Kinesis Data Streams (1 shard) → Firehose → S3 (Parquet) → Athena
* 1 shard รับได้ประมาณ 1,000 records/วินาที เพียงพอสำหรับ 800 ครั้ง/วินาที และเพิ่ม shard ได้เมื่อโหลดสูงขึ้น
