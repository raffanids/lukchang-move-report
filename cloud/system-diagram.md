# System Diagram

ระบบรันบน **AWS Bangkok (ap-southeast-7)** กระจาย 3 Availability Zone

| ส่วน | บริการ |
| --- | --- |
| API | API Gateway |
| Compute | ECS Fargate (Job, Matching, Payment, Location, Chat) |
| Database | Aurora (writer + reader), Redis |
| Chat | DynamoDB (TTL 30 วัน) |
| Storage | S3 + Glacier (Lifecycle) |
| Messaging | SQS, EventBridge |
| Push Notification | Amazon SNS → FCM / APNs |
| Location | Amazon Location Service |

> **[เติม]** System diagram (แก้เป็น 3 AZ และ SNS แล้ว)
