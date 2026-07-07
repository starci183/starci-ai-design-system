---
name: starci-fe-block-brainstorm
description: >
  LIGHT sibling of `starci-fe-layout-brainstorm` — design/refine ONE block (a single reusable component: card, chip,
  tooltip, meter, a form field, an interviewer-presence, …) in the MAIN StarCi Academy web app
  (`C:\Repositories\starci-academy`) at SMALL scope, much less effort than a whole flow/page. Nails the block's
  anatomy · variants · states (loading/empty/error/disabled/hover/selected) · props (WithClassNames discipline) ·
  element-compliance (which canonical primitive/HeroUI it uses — no hand-rolling). Grounded in `.claude/fe/components/`
  + `fe/{foundations,principles}` + the block's REAL source; researches the web only when the block TYPE has no ref or
  you're unsure. Optionally previews the variants. Hands off to `starci-fe-block-apply` (usually same session — it's
  small). Use this INSTEAD of the layout skill when the change lives inside ONE block, not across a page/flow. Trigger
  when the user types `/starci-fe-block-brainstorm <block>`, or asks to design/refine/tweak a single component/block.
---

# /starci-fe-block-brainstorm — Thiết kế/nắn 1 BLOCK (nhẹ, phạm vi nhỏ)

Bản NHẸ của layout-brainstorm: chỉ **1 block** (component tái dùng), **KHÔNG** cả-flow/page/prototype-luồng/hàng-đợi.
Ít effort. Dùng khi thay đổi **nằm trong 1 block**, không trải cả trang.

## Nền tra (đọc TRƯỚC, đừng tự chế)
- **`.claude/fe/components/INDEX.md`** + `components/<block>.md` (canon block đó) — có sẵn thì DÙNG/nắn, đừng đẻ trùng.
- **`fe/foundations/`** (token: màu/spacing/radius/typography) + **`fe/principles/`** (hover-theo-bản-chất · accent · a11y · interactive-needs-hover · disable-vs-lock).
- **Source THẬT** của block: `src/components/blocks/<cat>/<Block>/index.tsx` (+ README nếu có).
- **Web — CHỈ khi block-type chưa có ref HOẶC không chắc** → `WebSearch` (HeroUI/Polaris/Material component đó), neo ref. KHÔNG bịa.

## Quy trình (gọn)
1. **Khoanh 1 block** — tên + folder source + `components/<block>.md` nếu có.
2. **Anatomy + variants** — cấu trúc trong block; các biến thể (size/tone/variant-theo-nền: background→primary, surface→secondary).
3. **States** — nếu có data: loading(skeleton mirror)/empty/error; luôn: default/hover/focus/disabled/selected. Hover **theo bản chất** (go-there→underline · user→opacity · stay→fill).
4. **Props** — `*Props extends WithClassNames`; container tự đọc store/SWR, KHÔNG prop-drill data/callback thừa. 1 component = 1 folder `index.tsx`.
5. **Element-compliance** — dùng **primitive canonical** (HeroUI/block sẵn có), **KHÔNG hand-roll `<div border>`/`<button hover:bg>`**. Icon = phosphor. Element MỚI không có canon → HỎI thầy.
6. **(tuỳ) preview** — nếu đáng, `show_widget` render vài variant/state cạnh nhau cho thầy nhìn (nhẹ, không cả-flow).

→ **Thầy duyệt** → bàn giao **`starci-fe-block-apply`** (thường NGAY session này — block nhỏ). Không cần proposal-queue như layout (chỉ 1 block); nếu block lớn/đụng BE → có thể ghi 1 `fe/proposals/<block>.proposal.md` nhẹ.

## Self-verify lite (tự chấm)
- [ ] không tự chế primitive (dùng canon) · [ ] variant theo NỀN · [ ] hover theo bản chất · [ ] a11y (focus-ring, aria icon-only, contrast) · [ ] props WithClassNames, không prop-drill · [ ] data → có 4-state.

## Bàn giao / liên quan
- Build block → **`starci-fe-block-apply`** · block nằm trong 1 layout lớn → `starci-fe-layout-brainstorm` (cả flow).
- Canon: `fe/components/` · `fe/foundations/` · `fe/principles/` · `fe/README.md`.
