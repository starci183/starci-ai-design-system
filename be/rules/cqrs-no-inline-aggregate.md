# Rule — Read nặng (aggregate/join/GROUP BY/COUNT) PHẢI qua CQRS projection + CDC, không SQL inline ở resolver

**Bất kỳ query cần aggregate/join nhiều bảng/GROUP BY/COUNT/SUM/DISTINCT PHẢI làm 1 projection (entity + service + CDC listener), KHÔNG viết SQL/logic thẳng trong resolver/handler — chấp nhận boilerplate đổi lấy nhất quán, kể cả scale nhỏ.**

- Recipe 1 projection (5 file + đăng ký 4 chỗ): `entities/<name>-projection.entity.ts` extends `AbstractProjectionEntity` (jsonb `value` + `updatedAt`) · `types/index.ts` · `<name>-projection.service.ts` (`recompute()` = 1 UPSERT heavy SQL + `getX()` đọc kèm stale-check) · `<name>-projection.listener.ts` extends `AbstractProjectionListener` (CDC topic → `deriveTargets` → `recomputeTarget`) · module 3-file.
- ⚠️ Đăng ký DataSource `entities:[...]` trong `primary.module.ts` liệt kê **TAY 3 CHỖ** — quên 1 chỗ → bảng không tạo, query trả `null` im lặng (không throw rõ).
- Ngoại lệ KHÔNG cần projection: list/filter đơn giản (find/order/limit), feed ledger append-only cursor-paginated, per-viewer single-row edge check, write-path/cron tính fresh.

> Đã áp: `src/modules/bussiness/projections/{content-engagement,contribution,course-stats,league-cohort-points}` (mẫu chuẩn 5-file); `codingLeaderboard`/`trendingContents`/`league.rankCohortMembers` đã chuyển hết sang đọc projection (2026-06-15).
> Nguồn: memory `feedback-cqrs-no-inline-aggregate.md` (HOUSE PATTERN, thầy chốt 2026-06-15).

[[log-errors-typed-exception]]
