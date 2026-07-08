# Element — Meter / Progress bar (`ProgressMeter`, `SegmentBar`)

> Element doc cho THANH TIẾN ĐỘ (1 giá trị tới 1 mốc, hoặc N phần chia sẻ 1 tổng). Đây là API/da của component;
> QUY TẮC KHI NÀO 1 meter được phép rỗng/mặc định target đã chốt ở [[meter-tracks-out-of-box-default-target]]
> + [[progress-block-growing-quantity-headline-not-vanity-strip]] — đọc 2 file đó trước khi thiết kế 1 meter
> mới, file này chỉ tả 2 BLOCK render.

## `ProgressMeter` (`blocks/stats/ProgressMeter`) — 1 thanh, 1 giá trị/1 mốc
- `{ value, max=100, label?, showValue?, color?: "accent"|"success"|"warning"|"danger" }`. Top-row (label +
  `%` bo tròn) CHỈ render khi có `label` HOẶC `showValue` — không chèn hàng trống.
- **`color` mặc định `accent`; đổi sang `success`/`warning`/`danger` khi CHÍNH GIÁ TRỊ mang nghĩa semantic**
  (vd điểm số theo ngưỡng đạt/cận/chưa) — KHÔNG đổi color tuỳ hứng trang trí.
- `max` guard `<= 0` → fallback `1` (tránh `NaN`/`Infinity`); `%` luôn `Math.round`.
- `aria-label` = `label` khi là string, else fallback `"Progress"` — luôn truyền `label` string để a11y tốt.
- **1 THANH TẠI 1 THỜI ĐIỂM cho 1 cụm** — đừng lặp `ProgressMeter` cho MỌI item/group cùng lúc trong 1 list.
  Ref [[list]] §5d (group mở = 1 thanh, group gập = chỉ "n/m" muted).

## `SegmentBar` (`blocks/stats/SegmentBar`) — 1 thanh chia N MÀU theo tỉ lệ (GitHub-style)
- `{ segments: {key,label,value,color?}[], ariaLabel, max?, hideLegend? }`. Track `bg-default` (KHÔNG
  `bg-muted` — remainder/track phải nhạt, đúng [[progress-block-growing-quantity-headline-not-vanity-strip]]).
- **2 CHẾ ĐỘ theo `max`:** truyền `max` → width = `value/max` thật (có phần dư trống = "progress" — vd N/M
  task xong); bỏ `max` → width = share-of-each-other, LUÔN lấp đủ 100% (mix bar thuần tỉ lệ, vd phân bố ngôn
  ngữ). Chọn đúng ý nghĩa — đừng để pure-mix bar trông như progress có phần dư.
- Màu mặc định theo `PALETTE` (accent→success→warning→danger→muted) khi segment không truyền `color` riêng.
- Legend built-in (`dot + label · value`) dưới bar — tắt bằng `hideLegend` khi dùng `Legend` (`metric.md`)
  tách riêng cho nhiều bar chung 1 thang.
- `role="img"` + `aria-label` trên chính track — segment không đọc riêng lẻ cho screen reader (đọc gộp qua
  `ariaLabel` mô tả tổng).

> Block: `blocks/stats/{ProgressMeter,SegmentBar}`

## Liên quan
- [[meter-tracks-out-of-box-default-target]] (meter phải chạy out-of-box, không rỗng chờ config) ·
  [[progress-block-growing-quantity-headline-not-vanity-strip]] (track nhạt = `--default`, không `--muted`;
  1 meter có nghĩa > N số ngang hàng) · `metric.md` (số tĩnh, không progress) · [[list]] §5d (1 thanh/lúc
  trong list).
