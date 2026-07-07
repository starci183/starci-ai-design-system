---
name: starci-fe-consolidate-components
description: >
  Scan a SCOPE of the MAIN StarCi FE app (`C:\Repositories\starci-academy`) — `all` (whole app) · a page/route · a
  feature · a file set — for DUPLICATED or near-duplicate component code (copy-pasted JSX clusters, repeated className
  blobs, parallel components that should be ONE), and CONSOLIDATE them into a single canonical block (reuse an existing
  `fe/components/` block, or extract a new one), replacing every call-site. Kills code duplication + drift. Grounded in
  `fe/components/` (reuse, don't re-invent); OPUS writes the extraction spec, SONNET applies it, verify tsc/lint +
  preview. **Records the result to MEMORY** (how many clusters found, which block created/reused, call-sites replaced)
  so next runs cross-reference + reuse instead of re-consolidating. Part of the BLOCK family (consolidates INTO blocks).
  Trigger when the user types `/starci-fe-consolidate-components <scope>`, or asks to "gom component · dedupe component ·
  tránh lặp code · gộp component trùng".
---

# /starci-fe-consolidate-components — Gom component trùng thành 1 block (tránh lặp code)

Quét 1 scope → tìm code component **lặp/gần-giống** → gom về **1 block canonical** (tái dùng hoặc trích mới), thay MỌI
call-site. Chống lặp + drift. Thuộc họ BLOCK (gom VÀO block).

## Scope (arg)
`all` (toàn app) · `page <route>` · `feature <name>` · tập file. Scope rộng → **fan-out** scan (đừng đọc 1 mạch).

## Quy trình
1. **SCAN tìm trùng** — quét scope, bắt: JSX cluster copy-paste · `className` blob lặp · component **cùng cấu trúc khác data** · 2+ chỗ tự-dựng cùng 1 primitive. Scope rộng → fan-out Sonnet reader per subtree, gom kết quả. **Ground source thật**, không đoán.
2. **ĐỐI CHIẾU `fe/components/`** — cụm trùng này **đã có block canonical chưa?** Có → **DÙNG LẠI** (thay duplicate bằng block). Chưa → đề xuất **1 block mới** (element-aware, props `WithClassNames`, 1 folder `index.tsx`). Đối chiếu memory (lần trước gom gì rồi — khỏi gom lại).
3. **CHỐT** (thầy duyệt danh sách cụm gom + block đích) → **OPUS viết spec trích** (block mới/tái dùng + LIỆT KÊ mọi call-site cần thay + thứ tự) → **SONNET apply** → verify `tsc`/`lint` + preview.
4. **GHI MEMORY (bắt buộc)** — số cụm gom · block tạo/tái dùng (tên) · số call-site thay · scope. Để **lần sau đối chiếu + tái dùng**, không gom trùng lại. Rule bộ nhớ (feedback-always-update-mindset).

## Ràng (STRICT)
- **CHỈ gom thật-sự-trùng** — đừng gộp 2 thứ **khác NGHĨA** dù trông giống (ngữ nghĩa > hình dạng). Nghi ngờ → hỏi.
- **Rule-of-three:** chỉ abstract khi **≥2-3 call-site** thật; 1 lần dùng → đừng gom sớm (over-abstraction cũng là nợ).
- KHÔNG tự chế primitive — block gom theo `fe/components/` canon; block mới → theo `starci-fe-block-brainstorm`.
- **Có sửa canon (thêm block/rule) → PUSH PRIVATE; ok/sạch → PUSH PUBLIC** (rule repo, xem `.claude/CANON.md`).

## Liên quan
- Block design → `starci-fe-block-brainstorm` · block build → `starci-fe-block-apply` · rà health sau gom → `starci-doc-audit`.
- Canon: `fe/components/` · `fe/README.md`.
