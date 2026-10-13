# Gợi ý nâng cấp — rà soát 2026-10-13

> Lấy từ đợt rà soát chéo 19 repo của chủ sở hữu (ma trận vệ sinh ở [seeker19110/stored, mục 23 §8.1](https://github.com/seeker19110/stored/blob/main/23-own-repos-lessons/README.md); gợi ý tích hợp ở §7b của cùng file). Số liệu đo bằng lệnh trên HEAD (đếm `uses:` ghim SHA 40 ký tự, khối `permissions:`, `dependabot.yml`, `.claude/settings.json`), không suy ra từ văn xuôi. Đây là **đề xuất**, chưa sửa code. Mỗi mục kèm bằng chứng để kiểm lại trước khi làm; mục nào đã xử lý thì đánh dấu hoặc xoá.

## Hiện trạng đo được

| HEAD đọc | Action ghim SHA | Workflow thiếu `permissions:` cấp đầu | Dependabot | LICENSE · SECURITY | File test |
|---|---|---|---|---|---|
| `b39a280` (2026-09-06) | không có workflow | – | **không có** | có · không | 86 |

## Đề xuất (🔴 cao · 🟠 trung bình · 🟢 nhẹ)

| # | Mức | Đề xuất | Bằng chứng | Kiểm xong khi |
|---|---|---|---|---|
| 1 | 🟠 | Thêm CI (`.github/workflows/test.yml`, action ghim SHA, `permissions: contents: read`) chạy các bộ test không cần Blender: `python3 -m unittest discover -s tests/execution` và `-s tests/production-gate` | Có 86 file test (README dòng 73–74) nhưng repo **không có workflow nào** | Có CI xanh trên PR |
| 2 | 🟠 | Ghim phiên bản MCP: `"args": ["blender-mcp==<phiên bản>"]` | `.agents/mcp_config.json` gọi `uvx blender-mcp` không ghim, nên mỗi lần chạy có thể kéo bản mới, mà blender-mcp lại thực thi Python bên trong Blender | Có phiên bản cố định và ghi lý do nâng |
| 3 | 🟢 | Thêm `SECURITY.md`; ghi rõ quan hệ với upstream `jangtrinh/design-os-3d-blender` (badge README đang trỏ về đó) | Không có SECURITY.md | Có file |

## Giữ nguyên (điểm mạnh)

- Sentinel AGENT_OK / FAIL, verify ladder, gate hash-bound, research 3D / marketplace.

## Gợi ý tích hợp từ catalog `stored`

- ManimGX nếu cần render toán hoặc kỹ thuật (stored mục 22 §9c).

## Ghi chú chung

- Ghim action theo SHA bằng [pinact](https://github.com/suzuki-shunsuke/pinact) hoặc [ratchet](https://github.com/sethvargo/ratchet), giữ comment tag (`# v7.0.1`), rồi để Dependabot `github-actions` tự nâng SHA. Đây là cách projects-template, xboss và Sales-Hunter đang làm.
- Chuẩn tham chiếu là `seeker19110/projects-template`: 25/25 action ghim SHA, mọi workflow có `permissions:` cấp đầu, Dependabot cho npm, github-actions và pip.
