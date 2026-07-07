# Pattern — Dashboard hub (navbar tab-strip + centered bare-identity/panel 2-col)

> Shell/route: `Dashboard` (`src/components/features/dashboard/index.tsx`, route `/dashboard`) — "logged-in home", GitHub-style. `PublicProfile` (route `/profile/[username]`) tái dùng CÙNG layout ("rebuilt on the proven PROFILE page layout" — 1 archetype, 2 chủ thể).

## Khi nào dùng
- Nhiều KHU nội dung ngang hàng cùng 1 identity/scope (Overview · Explore · Courses · Community…), KHÔNG phải nav phân cấp (không cần rail — xem [[when-rail]]). Đổi khu = đổi TAB (single-select loại-trừ), không phải button-group.

## Region map
1. **Tab strip** = navbar BOTTOM-LAYER (`DashboardTabsBar`, đăng ký qua `useRegisterNavbarBottomLayer`) — KHÔNG sticky/border riêng; navbar root chỉ mang 1 `border-b` duy nhất, rơi dưới lớp cuối.
2. **Body** = `mx-auto max-w-6xl` 2 cột từ `md:`:
   - **Aside trái** (`w-72 shrink-0`) — identity/standing BARE (không bọc card), ĐỨNG YÊN qua mọi tab (`DashboardIdentity`).
   - **Main phải** (`min-w-0 flex-1`) — panel của tab ĐANG chọn; **chỉ panel active MOUNT** (mỗi tab tự query, lazy — tab khác không render, không fetch idle).
3. **Mobile:** aside rồi content xếp DỌC (không rail, không drawer, cùng thứ tự DOM).
- URL sync: tab hiện tại đọc/ghi `?tab=` qua store dùng chung (`useDashboardTabStore`) — không chỉ local state (share được link).

## Liên quan
[[when-rail]] (vì sao KHÔNG rail ở đây) · tabs (component canon: navbar-bottomlayer, single-select→tabs) · [[course-home-no-duplicate-surfaces]] / [[surface-lands-on-dashboard-no-auto-forward]] (IA quanh home/dashboard — không lặp surface, không auto-forward khỏi hub) · [[page-shell-selection]].
