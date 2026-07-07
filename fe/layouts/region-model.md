# Layout — Mô hình VÙNG (region model): shell + từ vựng vùng của StarCi

> Đặt 1 component/feature mới = **gọi tên VÙNG nó thuộc về TRƯỚC**, rồi mới style. Vùng = building-block của layout,
> mỗi vùng tự sở hữu padding/sticky/width ([Calcite Shell](https://developers.arcgis.com/calcite-design-system/foundations/layouts/) · [Fluent 2 layout](https://fluent2.microsoft.design/layout)).

## Shell thật (grounded)
| Shell | Vùng | Nguồn |
|---|---|---|
| **InnerLayout** (global, bọc MỌI trang) | navbar `h-16` (sticky) · ambient bg · content · footer (CHỈ landing) · overlay containers (modal/drawer) · TopLoader | `src/app/InnerLayout.tsx` |
| **LearnShell** (docs 4-cột) | icon-rail (`LearnSidebar`) · content-rail trái (`leftRail`, ResizableRail) · reading-col (`p-6`, owns measure) · on-this-page phải (`rightRail`, TOC) · `fullBleed` opt-out |  + `learn/layout.tsx` |
| **SettingsLayout** (2-pane manage) | collapsible-rail (`CollapsibleSidebar`, sticky) · content-col centered |  |
| **PageContainer** | 1 cột centered `max-w-*` gutter | `blocks/layout/PageContainer` |

## Từ vựng vùng (đặt component vào đúng vùng)
- **navbar** (trên, `h-16`) + **navbar-bottom-layer** (tab-strip dính dưới navbar — dashboard/profile, `useRegisterNavbarBottomLayer`).
- **icon-rail** (điều hướng surface, mảnh, `lg+`) · **content-rail** (cây/list nội dung, trái) · **reading-col** (nội dung chính, sở hữu measure `max-w-3xl`) · **on-this-page** (TOC phải).
- **CTA-anchor** (primary action — hero/sticky) · **bottom-bar** (`StickyBottomBar`, mobile enroll) · **workspace-pane** (full-bleed 2-pane, [[full-bleed-work-surface]]).

## Quy tắc
- **1 component mới → hỏi "vùng nào?"**: nav toàn cục → navbar/bottom-layer · duyệt list → content-rail · nội dung chính → reading-col · phụ theo ngữ cảnh → on-this-page · hành động chính → CTA-anchor · tool khi solve → workspace-pane.
- **Vùng sở hữu chrome của nó**: reading-col owns `p-6` + measure ([[three-tier-page-layout]] — cột đọc narrow `max-w-3xl mx-auto`); rail owns sticky + width; feature KHÔNG tự khai padding cột (LearnShell lo — xem `components/sidebar`).
- **Đo bằng cột, không nhét max-width vào renderer** (measure là việc của reading-col, không của MarkdownContent).

## Liên quan
[[page-shell-selection]] · [[surface-job-drives-layout]] · [[responsive-regions]] · `components/sidebar` (rail/shell blocks) · `components/header` (PageHeader vùng) · `foundations/gap` · `foundations/sticky` · `foundations/breakpoints`.
