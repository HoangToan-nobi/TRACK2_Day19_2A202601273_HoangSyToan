# Reflection — Lab 19

**Tên:** Hoàng Sỹ Toàn
**Cohort:** 2A202601273
**Path đã chạy:** lite

---

## Câu hỏi (≤ 200 chữ)

> Trên golden set 50 queries, mode nào thắng ở loại query nào (`exact` /
> `paraphrase` / `mixed`), và tại sao? Khi nào bạn **không** dùng hybrid
> (i.e. khi nào pure BM25 hoặc pure vector là lựa chọn đúng)?

Trên corpus của tôi: `exact` BM25 và hybrid ngang nhau (96.7%), vector thấp
hơn (88.7%) — từ khoá kỹ thuật xuất hiện verbatim nên BM25 đã đủ mạnh.
`mixed` hybrid thắng rõ nhất (100% so với 97.0%/98.5%) vì RRF gộp được cả
tín hiệu từ khoá lẫn tín hiệu ngữ nghĩa của hai vế câu hỏi. Bất ngờ nhất là
`paraphrase`: lý thuyết vector phải thắng, nhưng thực đo BM25 (33.3%) lại
nhỉnh hơn cả hybrid (32.0%) và vector (24.0%) — vì embedding mặc định của
path lite (`bge-small-en`, huấn luyện tiếng Anh) yếu trên câu hỏi tiếng Việt
diễn đạt lại. Đây đúng là "bẫy" mà notebook cảnh báo trước: đổi sang
`bge-m3`/`multilingual` (path Docker) sẽ đảo ngược kết quả này.

Tôi sẽ **không** dùng hybrid khi: (1) query là tra cứu chính xác, latency
cực thấp là ưu tiên số 1 — BM25 P50 chỉ 1-2ms so với hybrid ~30-50ms vì phải
gọi thêm embedding; (2) ngân sách compute không đủ chạy model embedding
(edge device) — lúc đó pure BM25 vẫn đủ dùng cho corpus có từ khoá rõ ràng.

---

## Điều ngạc nhiên nhất khi làm lab này

BM25 thắng cả trên `paraphrase` — ngược hẳn kỳ vọng — vì embedding model
mặc định không hợp ngôn ngữ, chứ không phải vì hybrid/RRF sai.

---

## Bonus challenge

- [ ] Đã làm bonus (xem `bonus/`)
- [ ] Pair work với: _<tên đồng đội nếu có>_
