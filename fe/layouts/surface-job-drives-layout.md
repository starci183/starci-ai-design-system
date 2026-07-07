# Layout — CÔNG VIỆC của bề mặt CHỌN shell; feature nhiều-pha ĐỔI shell theo pha

> ⭐ Luật gốc của kệ `layouts/`. Trước khi dựng 1 trang, KHÔNG hỏi "trang này trông thế nào" mà hỏi **"bề mặt này
> đang làm CÔNG VIỆC gì?"** — job chọn shell. Web ground: adaptive layout (layout đổi theo *modality/task*, không cứng
> 1 khung — [Material](https://m2.material.io/design/layout/understanding-layout.html) · [Fluent 2](https://fluent2.microsoft.design/layout)); focus-mode (VS Code / focus browser **ẩn nav** để tập trung 1 việc).

## Job → shell (hỏi job, rẽ shell)
| Job của bề mặt | Shell | Archetype |
|---|---|---|
| **Đọc / duyệt** tài liệu phân cấp | 3-pane (rail cây + đọc + TOC) | [[docs-three-pane-reader]] |
| **Duyệt N item cùng loại** | catalog grid/line + pager | [[catalog-grid]] |
| **Quyết / nhập** 1 tác vụ (form, setup, checkout) | centered 1 cột, không rail | [[centered-form-setup]] |
| **LÀM-VIỆC-TẬP-TRUNG có tool** (giải đề · phỏng vấn · thiết kế) | **full-bleed, bỏ rail, 2-pane** | [[full-bleed-work-surface]] · [[solving-surface-fullbleed-no-course-rails]] |
| **Tổng quan** nhiều khu cùng identity | dashboard-hub (tab strip) | [[dashboard-hub]] |
| **Kết quả / debrief** | centered 1 cột | ([[centered-form-setup]] shape) |
| **Bán hàng / kể chuyện** công khai | landing stacked | [[marketing-landing]] |
- Chọn shell cụ thể → cây quyết định [[page-shell-selection]]. Từ vựng vùng → [[region-model]].

## Feature NHIỀU PHA = nhiều job trong 1 route → ĐỔI SHELL theo pha (STRICT)
- **1 route nhưng đi qua N pha có JOB KHÁC NHAU → mỗi pha dùng shell của job đó, KHÔNG khoá cứng 1 khung cho cả feature.** Ép mọi pha vào 1 shell = pha nào job khác sẽ bị bóp méo (thường pha "làm-việc" bị nhồi vào cột đọc hẹp).
- Dấu hiệu sai: 1 state-machine `phase` render mọi pha trong CÙNG `max-w-*` centered + CÙNG rail — trong khi 1 pha là solve/interview cần full-bleed.
- Chuyển shell theo pha là **adaptive-by-task** (không chỉ adaptive-by-viewport): pha đổi job → layout đổi.

## Áp đầu (2026-07-07) — Mock Interview (đang sai)
`MockInterviewSession` nhồi CẢ 4 pha vào cột `max-w-2xl` trong LearnShell **còn nguyên rail khóa** (`learn/layout.tsx` chỉ `fullBleed={isMindMap}`), lại render pha interview 2 kiểu (qna 1-cột + workspace ẩn · design 2-pane). Đúng ra theo job:
- **setup** (quyết/green-room) → centered · **interview** (làm-việc + tool) → **full-bleed 2-pane, bỏ rail** ([[full-bleed-work-surface]]) · **grading** (chờ) → centered interstitial · **scorecard** (kết quả) → centered.
- Fix layout: route bật `fullBleed` khi `phase==="interview"`; setup/grading/scorecard giữ centered. Chi tiết shape → [[full-bleed-work-surface]].

## Liên quan
