# `.claude/fe` — StarCi FE Design System (v3, reconciled + completed)

> **Chuyện của bộ rule này:** mọc lũy tiến từ debug (mỗi fix bake 1 rule) → `concepts/` phình thành rổ tạp 9 bản
> chất → **re-audit theo taxonomy DS chuẩn** (NN/g · Polaris · Material 3 · EightShapes) **grounded vào source thật**
> (`C:\Repositories\starci-academy`) → gom về **4 lớp design + 3 nhà tách** → **hoàn thiện** brief stub cho mọi block
> đã tồn tại trong source. Từ 58 → **90 file design**.

## Cấu trúc (7 folder)

### Design system — 5 lớp (mỗi lớp có `INDEX.md` liệt kê đủ)
| Lớp | Là gì | Khớp source | # | Index |
|---|---|---|---|---|
| **`foundations/`** | Token / raw material (màu, spacing, radius, elevation, typography, motion, z-index, breakpoint, scroll) | `app/globals.css` | 12 | [INDEX](foundations/INDEX.md) |
| **`layouts/`** | Khung/VÙNG trang: job→shell · region-model · archetype · responsive (KHÔNG GIAN trang) |  + `InnerLayout` | 15 | [INDEX](layouts/INDEX.md) |
| **`components/`** | 1 element = 1 file (button, card, tooltip, modal, avatar…) | `src/components/blocks/*` | 33 | [INDEX](components/INDEX.md) |
| **`patterns/`** | Flow/recipe TRONG khung: data-state · form · search-list · IA-behavior · overlay | `blocks/async` + hooks | 15 | [INDEX](patterns/INDEX.md) |
| **`principles/`** | Heuristic xuyên suốt (accent, hover, restraint, a11y, content-voice, **+CTA/link/psychology**) | — (governance) | 22 | [INDEX](principles/INDEX.md) |

> **Lớp `layouts/` (thêm 2026-07-07):** rút từ 1 ca thực tế — "1 page mới xây layout thế nào" = hỏi **JOB của bề mặt → chọn shell**; feature nhiều-pha ĐỔI shell theo pha. 10 archetype/shell dời từ `patterns/` sang (trước xếp nhầm) + 5 doc lõi mới (`surface-job-drives-layout` ⭐ · `region-model` · `full-bleed-work-surface` · `responsive-regions` · INDEX). Ranh: **layouts = SHAPE trang · patterns = FLOW trong shape đó**.

### Tách khỏi design (không phải design system)
| Nhà | Là gì | # |
|---|---|---|
| **`engineering/`** | FE↔BE contract + build/lint + BE/ops gotcha (envelope-nullable, opaque-id, tailwind-scan, shared-modules…) | 16 |

> **`prototypes/` (tooling):** prototype HTML flow **bấm-được** (host :8080) cho `/starci-fe-layout-brainstorm` — kit `_TEMPLATE.html` (upgrade in-place). [INDEX](prototypes/INDEX.md).

> Nhà cũ nguyên trạng (đọc-only): `../../claude-legacy/rules/`.

## Cách skill FE dùng
- **`starci-fe-layout-brainstorm`** → tra `layouts/` (`surface-job-drives-layout` → `page-shell-selection` → archetype) + `components/INDEX` (brief mỗi block 1 dòng).
- **`starci-fe-block-skill`** → tra `components/` + `foundations/` + `principles/`.
- Quyết định business → ; tránh gotcha data/build → `engineering/`.

## Taxonomy — vì sao 4 lớp (grounded)
NN/g · Polaris · Material 3 tách DS thành **Foundations (token) · Components (element) · Patterns (tổ hợp/shell/nav) ·
Principles (guideline)**. Đây KHÔNG phải áp từ ngoài — **source đã tự tổ chức đúng vậy**: `blocks/*` = components,
`globals.css` = foundations,  + `blocks/async` = patterns. 4 lớp rule map thẳng vào code.

---

## TODO finalize (refinement còn lại — chốt từng cái, agent đã để cross-link nên KHÔNG mất nội dung)

### MERGE (umbrella đã có → xoá sub sau khi thầy gật)
- ✅ **DONE (2026-07-07)** `highlight-accent-as-detail-not-block-fill` đã hợp nhất vào **`accent-system`** (xoá file + redirect 7 ref cross-doc).
- `patterns/{when-rail, solving-surface-fullbleed-no-course-rails, fullbleed-canvas-no-chrome-and-orient-zoom}` → **`page-shell-selection`** (umbrella đã viết).
- `patterns/{course-home-no-duplicate-surfaces, learn-home-surfaces-share-flat-chrome, surface-lands-on-dashboard-no-auto-forward}` (+ , `principles/resume-cta`) → **`overview-surface-ia`** (mới).

### SPLIT (1 file trộn 2 bản chất → tách)
- `principles/landing-marketing`: grounded/copy (**giữ principle** — đã có umbrella `grounded-in-data`/`content-voice`) | §7 viz-lib (**→ engineering**).
- ✅ **DỜI (2026-07-07)** `disable-vs-lock-and-perrow-autosave` → cả file về `components/` (không chẻ; nửa autosave là nuance trong file).
- `patterns/selection-anchored-entry-and-intent-state`: entry-UX (**giữ pattern**) | mount-reset state-mgmt (**→ engineering**).

### FOLD (nhét vào element doc — đã cross-link, xoá file lẻ khi gật)
- ✅ **DỜI (2026-07-07)** `modal-body-no-padding-override-heroui-idiom` · `status-icon-overrides-base` · `challenge-section-labeledcard-quiet-eyebrow-icon-once` → `components/` (giữ nguyên file; fold hẳn vào modal/icon/label.md để sau — bước đó cần viết lại chữ).
- `patterns/when-drawer` (component-half) → `components/drawer` (giữ pattern-half "khi nào drawer").

### BUG / DRIFT source FE (agent bắt khi grounding — sửa ở `C:\Repositories\starci-academy`)
- **`--font-inter`** set trong `globals.css` nhưng **chưa bao giờ define** → app thực chạy `Open_Sans` qua body; `font-sans` utility fallback OS stack. (foundations/typography.md)
- **`--brand-*`** được `components/color` §1 nhắc nhưng **không tồn tại** trong globals.
- **`ProgressMeter` README stale** — thiếu prop `color` đang dùng thật.
- **`reuseable/Dropzone`** dùng `@gravity-ui/icons` → drift khỏi Phosphor-only (components/image.md flag).

### DEAD LINKS (`[[...]]` trỏ file chưa có — cả corpus): `three-tier-page-layout` · `single-select-among-options-use-tabs` · `leaf-page-one-nav-and-combined-tab-toolbar` · `sticky-rail-overflow-wrap-scrollshadow` · `list-surface-anatomy-...` · `one-progress-bar-at-a-time` (+ vài cái). Mỗi cái: dựng file thật / rewrite ref `elements → components §y`.

### GAP còn (patterns TODO agent ttrack): `course-detail` · `feed-column` · `modal-drawer-flow` · `infinite-scroll-feed` · `breadcrumb-trail`. Components future-DS: table · badge · pagination · toast · checkbox/radio/switch · popover · spinner.
