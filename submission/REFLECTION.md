# Reflection — Lab 19

**Tên:** Hoàng Sỹ Toàn
**Cohort:** 2A202601273
**Path đã chạy:** lite

---

## Câu hỏi (≤ 200 chữ)

> Trên golden set 50 queries, mode nào thắng ở loại query nào (`exact` /
> `paraphrase` / `mixed`), và tại sao? Khi nào bạn **không** dùng hybrid
> (i.e. khi nào pure BM25 hoặc pure vector là lựa chọn đúng)?

Trên 50 golden queries, Precision@10 tổng: BM25 77.8%, vector 73.2%, hybrid
78.6% — hybrid thắng nhẹ nhờ **ổn định qua mọi loại**, không áp đảo riêng
loại nào. Theo loại (n=số câu):

- **exact** (n=15): BM25 = hybrid = 96.7%, vector 88.7%. Từ khoá kỹ thuật
  xuất hiện verbatim trong doc nên BM25 đã đủ mạnh.
- **mixed** (n=20): hybrid 100% > vector 98.5% > BM25 97.0%. RRF (k=60) cộng
  rank từ hai retriever nên câu hỏi ghép hai ý được phủ đủ cả hai vế — đúng
  use-case hybrid sinh ra để giải quyết.
- **paraphrase** (n=15): BM25 33.3% > hybrid 32.0% > vector 24.0% — **ngược
  lý thuyết**. Nguyên nhân: embedding mặc định path lite (`bge-small-en`,
  huấn luyện tiếng Anh) yếu trên câu Việt diễn đạt lại. Đổi `bge-m3` (path
  Docker) sẽ đảo ngược kết quả.

Tôi **không** dùng hybrid khi: (1) cần tra cứu chính xác, latency cực thấp —
BM25 P50 chỉ 1-2ms so với hybrid ~35-50ms (đo ở NB3) vì phải gọi thêm
embedding; (2) corpus paraphrase-nặng nhưng **đã có** embedding hợp ngôn
ngữ — pure vector đủ tốt, tránh chi phí BM25 + RRF thừa.

---

## Điều ngạc nhiên nhất khi làm lab này

BM25 thắng cả trên `paraphrase` — ngược hẳn kỳ vọng — vì embedding model
mặc định không hợp ngôn ngữ, chứ không phải vì hybrid/RRF sai.

---

## Bonus challenge

- [ ] Đã làm bonus (xem `bonus/`)
- [ ] Pair work với: _<tên đồng đội nếu có>_
