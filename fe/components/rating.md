# Element — Rating bar (block `RatingBar`)

> Element doc cho thang chấm SM-2 (Again→Easy). Đây là 1 trường hợp CỤ THỂ của quy tắc "hàng nút THANG"
> đã chốt ở [[button]] §7 — file này tả riêng component thật render nó.

## Khi nào dùng
- Người học chấm ĐỘ NHỚ LẠI 1 flashcard sau khi lật đáp án (spaced-repetition, SM-2 grade 0-3) → `RatingBar`,
  KHÔNG tự dựng 4 `Button` variant khác nhau ở feature.

## Quy tắc
- **1 treatment nhất quán, hue chạy ramp theo NGHĨA yếu→mạnh:** Quên=`danger` · Khó=`warning` · Được=`success`
  · Dễ=`accent` — mọi ô cùng `bg-token/10 text-token hover:bg-token/20`, KHÔNG mỗi ô 1 variant rời (đọc như 1
  thang 4 bậc, không phải 4 nút khác vai — đúng [[button]] §7).
- **Plain `<button>`, KHÔNG HeroUI `Button`** — Button bake variant nền unlayered sẽ ĐÈ tint `bg-token/10`
  tự set qua className (cùng gotcha unlayered ở [[card]] §3e/§3f).
- Equal-width lấp ô: `grid grid-cols-2 sm:grid-cols-4` (mobile 2×2, desktop 1 hàng 4).
- `{ options: {grade, label, hint?}[], onRate, isPending? }` — `hint` (preview khoảng ôn tiếp theo) render
  dưới label, `opacity-80`. `isPending` disable CẢ 4 ô khi đang gửi review (tránh double-submit).
- Labels/hint tới từ CALLER đã dịch (`t(...)`) — block không tự `useTranslations`.

> Block: `blocks/buttons/RatingBar`

## Liên quan
- [[button]] §7 (nguyên tắc chung "hàng nút thang") · [[card]] §3e/§3f (cùng gotcha unlayered-vs-tint).
