---
name: starci-fe-block-apply
description: >
  LIGHT sibling of `starci-fe-layout-apply` — BUILD/edit ONE block (a single reusable component's internals: its
  `<Block>/index.tsx`, variants, states, styles, testids) in the MAIN StarCi Academy web app
  (`C:\Repositories\starci-academy`) at SMALL scope, much less effort than building a whole flow/page. Reads the block
  spec (from `starci-fe-block-brainstorm` or the request) + `fe/components/<block>.md` + the real source, assembles it
  from canonical HeroUI/existing primitives (NO hand-rolling), uses design tokens + spacing scale, verifies tsc/eslint +
  previews the block in isolation, then writes any reusable ruling back to `fe/components/`. This is what
  `starci-fe-layout-apply` hands block INTERNALS to. Use INSTEAD of the layout apply when the change lives inside ONE block.
  For a big/BE-touching block it MAY use Opus-spec → Sonnet-code; small blocks build directly. Trigger when the user
  types `/starci-fe-block-apply <block>`, or asks to build/edit/fix a single component/block.
---

# /starci-fe-block-apply — Dựng/sửa 1 BLOCK (nhẹ, phạm vi nhỏ)

Bản NHẸ của layout-apply: chỉ **internals của 1 block**. Ít effort. Đây là thứ `starci-fe-layout-apply` bàn giao (layout dựng
khung → block-apply dựng chi tiết block). Dùng khi thay đổi nằm trong **1 block**.

## Trước khi build
- Đọc spec (từ `starci-fe-block-brainstorm` / yêu cầu) + **`fe/components/<block>.md`** (canon) + **source thật** `src/components/blocks/<cat>/<Block>/`.
- Nền token/heuristic: `fe/foundations/` (màu/spacing/radius/typography) + `fe/principles/` (hover · accent · a11y · disable-vs-lock).

## Build (STRUCTURE của block)
- **1 component = 1 folder `index.tsx`** (tên folder = tên component); sub nest trong cha. **Props `*Props extends WithClassNames`**; container tự đọc store/SWR, KHÔNG prop-drill data/callback thừa.
- **KHÔNG hand-roll** `<div border>`/`<button hover:bg>`/tự ghép icon+input — dùng **HeroUI + block canonical**. Element MỚI không có canon → HỎI thầy.
- **Token + spacing scale `0/2/3/4/6`** (CẤM 1.5); `rounded-xl`/`rounded-full` concentric; **variant theo NỀN** (background→primary, surface→secondary); **hover theo bản chất**; icon = **phosphor**; a11y (focus-ring, aria icon-only).
- Data → **`AsyncContent`** (skeleton mirror · empty · error). Style sống trong block, feature chỉ ghép.
- **(tuỳ) Opus-spec → Workflow:** block LỚN / đụng BE → Opus viết spec kĩ rồi **author 1 `Workflow` (sonnet)** code + Opus verify. Block nhỏ → dựng thẳng (main loop), khỏi Workflow.

## Verify
- `npx tsc --noEmit` + `npm run lint` sạch. **Preview block** (isolated hoặc trong ngữ cảnh) → soi variant/state, chụp. Đụng BE → verify runtime thật.

## Xong → feedback (nhẹ)
- Ruling block TÁI DÙNG → cập nhật/thêm **`fe/components/<block>.md`** (thin) hoặc `fe/principles/` (nếu là heuristic xuyên suốt). Chỉ ghi khi tái dùng thật, giữ ngắn. KHÔNG `drafts/`.

## Ràng / liên quan
- Bám spec block; đổi phạm vi (thành cả layout) → quay lại `starci-fe-layout-brainstorm`. KHÔNG tự chế primitive.
- Thiết kế block trước → `starci-fe-block-brainstorm` · block nằm trong flow lớn → cặp layout (`starci-fe-layout-brainstorm` → `starci-fe-layout-apply`).
- Canon: `fe/components/` · `fe/foundations/` · `fe/principles/` · `fe/README.md`.
