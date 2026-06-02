# Consumer–Provider Handshake

## Thông tin chung

- Lab: FIT4110 Lab 03
- Ngày: 2026-06-02
- Provider team: team-vision
- Consumer team: team-iot
- Provider service: AI Vision Service
- Consumer service: IoT Ingestion Service

## Contract

- Contract file: `contracts/ai-vision.openapi.yaml`
- Mock base URL: `http://localhost:4011`
- Auth method: Bearer Token
- Endpoint được test: `POST /detect`

## Smoke test

### Request

```http
POST /detect
Authorization: Bearer {{authToken}}
Content-Type: application/json
```

```json
{
  "camera_id": "CAM01",
  "image_url": "https://example.com/frame.jpg"
}
```

### Expected response

```json
{
  "detection_id": "det-99128-abc",
  "camera_id": "CAM01",
  "label": "person",
  "confidence": 0.95,
  "timestamp": "2026-05-13T08:30:01+07:00"
}
```

## Kết quả

- [x] Consumer gọi mock thành công.
- [x] Consumer parse được field cần dùng (như `detection_id`, `label`, `confidence`).
- [x] Consumer hiểu lỗi 4xx/5xx provider trả về (theo chuẩn ProblemDetails).
- [x] Có Newman report hoặc screenshot (đã lưu tại `reports/newman-report.html`).

## Ghi chú thay đổi hợp đồng

| Nội dung | Trước | Sau | Người đồng ý |
|---|---|---|---|
| Khai báo confidence | min/max không rõ | Ràng buộc nằm trong đoạn [0, 1] | team-vision & team-iot |

## Xác nhận

- Provider representative: team-vision Representative (Vũ Chí Công - Mock)
- Consumer representative: team-iot Representative (Vũ Chí Công)
