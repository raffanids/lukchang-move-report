---
icon: table
cover: ../.gitbook/assets/banner-data.jpg
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

# ER Diagram

โครงสร้างฐานข้อมูลหลัก (PostgreSQL บน Amazon Aurora) ออกแบบใน Progress 2 แบ่งเป็น 5 กลุ่มตามโดเมนของระบบ ทุกตารางใช้ `uuid` เป็น primary key ยกเว้น `order_tracking_logs` ที่ใช้ `bigint` เพราะมีจำนวนแถวมาก

## ความสัมพันธ์หลัก

* `users` 1 : 1 `customer_profiles` / `driver_profiles` / `admin_profiles` ตาม `role`
* `driver_profiles` 1 : N `vehicles`
* `customer_profiles` 1 : N `orders` และ `driver_profiles` 1 : N `orders`
* `orders` 1 : N `order_parcels`, `order_tracking_logs`, `delivery_proofs`, `payments`
* `orders` 1 : 1 `driver_reviews`
* `payments` 1 : N `refunds` และ `orders` 1 : N `driver_payouts`
* `support_tickets` 1 : N `chat_messages` และ `orders` 1 : N `chat_messages` (แยกด้วย `context_type`)

## ตารางในแต่ละกลุ่ม

{% tabs %}
{% tab title="User & Authentication" %}
#### `users`

| Column | Type | หมายเหตุ |
| --- | --- | --- |
| `user_id` | uuid | PK |
| `email` | varchar | NN, unique |
| `phone_number` | varchar | NN, unique |
| `password_hash` | varchar | NN |
| `role` | user_role (enum) | NN |
| `is_active` | boolean |  |
| `created_at` / `updated_at` | timestamp |  |

#### `customer_profiles`

| Column | Type | หมายเหตุ |
| --- | --- | --- |
| `customer_id` | uuid | PK, FK → users |
| `first_name` / `last_name` | varchar |  |
| `rating_avg` | decimal(3,2) |  |

#### `driver_profiles`

| Column | Type | หมายเหตุ |
| --- | --- | --- |
| `driver_id` | uuid | PK, FK → users |
| `first_name` / `last_name` | varchar |  |
| `kyc_status` | kyc_status_enum |  |
| `kyc_verified_at` | timestamp |  |
| `is_online` | boolean |  |
| `current_latitude` / `current_longitude` | decimal(10,8) / decimal(11,8) |  |
| `rating_avg` | decimal(3,2) |  |

#### `admin_profiles`

| Column | Type | หมายเหตุ |
| --- | --- | --- |
| `admin_id` | uuid | PK, FK → users |
| `department` | department (enum) | NN |
| `corporate_sso_id` | varchar |  |

#### `vehicles`

| Column | Type | หมายเหตุ |
| --- | --- | --- |
| `vehicle_id` | uuid | PK |
| `driver_id` | uuid | NN, FK → driver_profiles |
| `vehicle_type` | vehicle_type_enum | NN |
| `license_plate` | varchar | NN |
| `is_active` | boolean |  |
{% endtab %}

{% tab title="Order & Logistics" %}
#### `orders`

| Column | Type | หมายเหตุ |
| --- | --- | --- |
| `order_id` | uuid | PK |
| `customer_id` | uuid | NN, FK → customer_profiles |
| `driver_id` | uuid | FK → driver_profiles |
| `vehicle_type_required` | vehicle_type_enum | NN |
| `estimated_price` / `final_price` | decimal(10,2) | estimated NN |
| `order_status` | order_status_enum | NN |
| `pickup_street_address` / `dropoff_street_address` | uuid / text | NN, FK → address |
| `driver_assigned_at` / `completed_at` / `cancelled_at` | timestamp |  |
| `cancellation_reason` | text |  |
| `created_at` / `updated_at` | timestamp |  |

#### `address`

| Column | Type | หมายเหตุ |
| --- | --- | --- |
| `address_id` | uuid | PK |
| `sub_district` / `district` / `province` | varchar(100) | NN |
| `postal_code` | varchar(20) | NN |
| `country` | varchar(100) | NN |
| `latitude` / `longitude` | decimal(10,8) / decimal(11,8) |  |

#### `order_parcels`

| Column | Type | หมายเหตุ |
| --- | --- | --- |
| `parcel_id` | uuid | PK |
| `order_id` | uuid | NN, FK → orders |
| `weight_kg` / `width_cm` / `height_cm` / `length_cm` | decimal(6,2) |  |
| `quantity` | int |  |

#### `order_tracking_logs`

| Column | Type | หมายเหตุ |
| --- | --- | --- |
| `log_id` | bigint | PK |
| `order_id` | uuid | NN, FK → orders |
| `status` | varchar | NN |
| `latitude` / `longitude` | decimal |  |
| `created_at` | timestamp |  |
{% endtab %}

{% tab title="Payments" %}
#### `payments`

| Column | Type | หมายเหตุ |
| --- | --- | --- |
| `payment_id` | uuid | PK |
| `order_id` | uuid | NN, FK → orders |
| `amount` | decimal(10,2) | NN |
| `payment_method` | payment_method_enum | NN |
| `payment_status` | payment_status_enum | NN |
| `transaction_ref` | varchar |  |
| `created_at` | timestamp |  |

#### `refunds`

| Column | Type | หมายเหตุ |
| --- | --- | --- |
| `refund_id` | uuid | PK |
| `payment_id` | uuid | NN, FK → payments |
| `order_id` | uuid | NN, FK → orders |
| `amount` | decimal(10,2) | NN |
| `refund_status` | refund_status_enum | NN |
| `processed_at` | timestamp |  |

#### `driver_payouts`

| Column | Type | หมายเหตุ |
| --- | --- | --- |
| `payout_id` | uuid | PK |
| `driver_id` | uuid | NN, FK → driver_profiles |
| `order_id` | uuid | NN, FK → orders |
| `amount` | decimal(10,2) | NN |
| `status` | payout_status_enum | NN |
| `transferred_at` | timestamp |  |
{% endtab %}

{% tab title="Proofs & Reviews" %}
#### `delivery_proofs`

| Column | Type | หมายเหตุ |
| --- | --- | --- |
| `proof_id` | uuid | PK |
| `order_id` | uuid | NN, FK → orders |
| `proof_stage` | proof_stage_enum | NN (รับ / ส่ง) |
| `image_url` | varchar | NN |
| `signature_url` | varchar |  |
| `captured_at` | timestamp |  |

#### `driver_reviews`

| Column | Type | หมายเหตุ |
| --- | --- | --- |
| `review_id` | uuid | PK |
| `order_id` | uuid | NN, unique, FK → orders |
| `customer_id` | uuid | NN, FK → customer_profiles |
| `driver_id` | uuid | NN, FK → driver_profiles |
| `rating` | int | NN |
| `comment` | text |  |
| `created_at` | timestamp |  |
{% endtab %}

{% tab title="Customer Support" %}
#### `support_tickets`

| Column | Type | หมายเหตุ |
| --- | --- | --- |
| `ticket_id` | uuid | PK |
| `order_id` | uuid | FK → orders |
| `reporter_id` | uuid | NN, FK → users |
| `assigned_admin_id` | uuid | FK → admin_profiles |
| `status` | ticket_status_enum | NN |
| `issue_category` | issue_category_enum |  |
| `created_at` / `updated_at` | timestamp |  |

#### `chat_messages`

| Column | Type | หมายเหตุ |
| --- | --- | --- |
| `message_id` | uuid | PK |
| `context_type` | context_type_enum | NN (แชทงาน / ticket) |
| `order_id` | uuid | FK → orders |
| `ticket_id` | uuid | FK → support_tickets |
| `sender_id` | uuid | FK → users |
| `sender_type` | sender_type_enum | NN |
| `message_text` | text | NN |
| `media_url` | varchar |  |
| `created_at` | timestamp |  |
{% endtab %}
{% endtabs %}

{% hint style="info" %}
ใน Progress 2 ข้อความแชทอยู่ในฐานข้อมูลเดียวกัน ตั้งแต่ Progress 4 แชทย้ายไปเก็บใน DynamoDB (TTL 30 วัน) ส่วน ticket ยังอยู่ใน Aurora เพราะผูกกับการคืนเงิน
{% endhint %}
