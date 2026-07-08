# Layout — Bề mặt LÀM-VIỆC full-bleed 2-pane (giải đề · phỏng vấn · thiết kế có tool)

> Archetype cho job "làm-việc-tập-trung 1 việc + cần tool" (khác canvas thuần [[fullbleed-canvas-no-chrome-and-orient-zoom]] và
> giải-đề-đọc-1-cột [[solving-surface-fullbleed-no-course-rails]]). Web ground: focus-mode (VS Code secondary side-bar,
> browser focus) **ẩn nav site** để dồn màn cho việc; CoderPad/interviewing.io = context ↔ workspace 2-pane.

## Khung (STRICT)
- **Full-bleed, BỎ rail khóa + chrome** (route bật `fullBleed`) — rail điều hướng khóa lúc này chỉ gây nhiễu. Đường lùi = **1 back-link "← Thoát"** là đủ ([[solving-surface-fullbleed-no-course-rails]] tinh thần).
- **2 pane:** TRÁI = **context/hội thoại** (đề · người phỏng vấn · câu hỏi · tiến độ · ô trả lời) · PHẢI = **workspace TOOL-TABS** (Whiteboard · Code · Ghi chú — [[tabs]]). Workspace là **pane HẠNG NHẤT**, KHÔNG toggle "+ thêm" ẩn dưới.
- Grid `lg:grid-cols-[minmax(0,1fr)_minmax(0,1fr)]`; mỗi pane cuộn riêng (`ScrollShadow`), không để cả trang cuộn.

## 2-pane CỨNG vs workspace BUNG-THEO-YÊU-CẦU (chọn theo tần suất cần tool)
- **2-pane cứng** khi việc **luôn** cần workspace: thiết kế hệ thống (vẽ suốt), giải code (gõ suốt).
- **1 cột rộng + pane bung theo yêu-cầu** khi **đa số câu KHÔNG cần tool** (vd phỏng vấn Q&A trả lời bằng lời): full-bleed 1 cột rộng, workspace mở khi câu cần (câu debug ship given-code → tự mở pane Code). Giữ quyết định sư phạm "đừng phí nửa màn cho câu không cần vẽ/code" mà vẫn full-bleed (hết cramped). → mặc định chọn cái này cho Q&A.
- **Đừng** để workspace thành 1 link "+ thêm" ẩn dưới cột hẹp (bug Mock Interview hiện tại).

## Mobile
2-pane → **xếp dọc**: context trên, workspace = 1 tab-strip/collapsible dưới ([[responsive-regions]]). 1 việc/màn, không nhồi 2 pane cạnh nhau trên màn hẹp.

## Áp đầu (2026-07-07 chốt · 2026-07-08 xác nhận ĐÃ ÁP + fix 1 bug)
Mock Interview pha `interview`: **bung-theo-yêu-cầu cho `qna`** (1 cột rộng, pane Code tự mở khi given-code, `MockInterviewSession/index.tsx`) · **2-pane cứng cho `design`** (whiteboard suốt) — 1 shell full-bleed chung, khác nhau ở lúc-mở-pane. Route bật `fullBleed` khi `phase===interview`; workspace = pane hạng nhất (nút mở/ẩn, không phải toggle "+ thêm" ẩn dưới). Prototype: `fe/prototypes/mock-interview.html`.
- **Bug đã fix (2026-07-08):** `workspaceOpen` là state CẤP-PHIÊN, tự mở đúng khi câu có `givenCode` nhưng KHÔNG tự đóng cho câu sau không cần → workspace dính mở hết phiên (phá đúng ý "bung theo yêu cầu", vi phạm §2 dòng trên "đừng phí nửa màn cho câu không cần"). Fix: `workspaceAutoOpenedRef` (ref, không phải state — bookkeeping thuần) đánh dấu open do AUTO (givenCode) hay MANUAL (user tự bấm "Thêm phác thảo"); câu sau không cần code → chỉ auto-đóng khi ref=auto, GIỮ NGUYÊN khi user tự mở (không clobber notes user đang viết).
- Ref [[surface-job-drives-layout]] §Áp đầu.

## Liên quan
[[surface-job-drives-layout]] · [[solving-surface-fullbleed-no-course-rails]] · [[fullbleed-canvas-no-chrome-and-orient-zoom]] · [[page-shell-selection]] (câu hỏi 1) · [[responsive-regions]] · [[tabs]].
