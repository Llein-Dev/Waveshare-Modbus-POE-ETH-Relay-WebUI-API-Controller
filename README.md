Relay Control Server
1. Purpose

Service provides REST API to control 8 relays via Modbus TCP. Configuration stored in JSON file for persistence.

2. Architecture

Express server: REST endpoints + serve static UI.

ModbusRTU client: TCP connection to device (default 192.168.1.200:502, unit ID = 1).

Config storage: relayConfig.json, loaded at startup and updated on config changes.

Safe write: after writing coil, server reads back to verify requested state.

3. Workflow

On startup: load relay config.

On each request: ensure Modbus connection alive.

Status API: return coils + config.

Relay action API: execute action based on config (hold/pulse).

Config API: update mode/ms/type and persist to JSON.

4. Relay Modes

Hold: coil toggles and stays until next command.

Pulse: coil switches temporarily. Parameters:

ms: 50–10000 (duration).

type: on (OFF→ON→OFF) or off (ON→OFF→ON).

5. API Summary

GET /api/status → snapshot coils + config.

POST /api/relay/:id/action → perform relay action.

POST /api/config/:id → update relay configuration.

6. Constraints

Relay ID: 0–7.

Mode: hold | pulse.

Pulse ms: 50–10000.

Pulse type: on | off.

7. Frontend

public/ folder served as static UI for relay operations.
------------------------------------------------------------------------------------
Tiếng Việt – Relay Control Server
1. Mục đích

Service cung cấp REST API để điều khiển 8 relay qua Modbus TCP. Cấu hình lưu trong file JSON để giữ trạng thái bền vững.

2. Kiến trúc

Express server: cung cấp REST API và phục vụ giao diện tĩnh.

ModbusRTU client: kết nối TCP tới thiết bị (mặc định 192.168.1.200:502, unit ID = 1).

Lưu trữ config: file relayConfig.json, load khi khởi động, update khi có thay đổi.

Safe write: sau khi ghi coil, server đọc lại để xác minh trạng thái đúng với yêu cầu.

3. Luồng xử lý

Khi start: load config relay.

Mỗi request: đảm bảo kết nối Modbus đang mở.

API Status: trả về coils + config.

API Relay Action: chạy theo mode config (hold/pulse).

API Config: cập nhật mode/ms/type và ghi lại vào JSON.

4. Chế độ relay

Hold: relay bật/tắt và giữ trạng thái cho đến khi có lệnh mới.

Pulse: relay chỉ nháy tạm thời. Tham số:

ms: 50–10000 (thời gian).

type: on (OFF→ON→OFF) hoặc off (ON→OFF→ON).

5. API chính

GET /api/status → snapshot coils + config.

POST /api/relay/:id/action → thực thi hành động relay.

POST /api/config/:id → update config cho relay.

6. Ràng buộc

Relay ID: 0–7.

Mode: hold | pulse.

Pulse ms: 50–10000.

Pulse type: on | off.

7. Frontend

Thư mục public/ được serve để người dùng thao tác relay qua giao diện web.
