# Reflection — Lab 19

**Tên:** Hoàng Phong 
**Cohort:** AI20K-K4
**Path đã chạy:** lite (Python 3.11, BGE-small 384d, Qdrant in-memory, Feast SQLite)

---

## Câu hỏi (≤ 200 chữ)

> Trên golden set 50 queries, mode nào thắng ở loại query nào (`exact` /
> `paraphrase` / `mixed`), và tại sao? Khi nào bạn **không** dùng hybrid
> (i.e. khi nào pure BM25 hoặc pure vector là lựa chọn đúng)?

Trên 50 golden queries, Precision@10 trung bình là BM25 77,8%, semantic
73,2%, hybrid 78,6%. RRF dùng rank bắt đầu từ 1 và k=60; hybrid tăng 0,8 điểm
phần trăm so với BM25 và 5,4 điểm so với semantic.

Ở nhóm exact, BM25 và hybrid cùng đạt 96,7%, semantic đạt 88,7%: từ kỹ thuật
khớp trực tiếp nên tín hiệu lexical mạnh. Ở mixed, hybrid đạt 100%, vượt BM25
97% và semantic 98,5%, nhờ kết hợp hai thứ hạng bổ sung nhau.

Ở paraphrase, BM25 đạt 33,3%, semantic 24%, hybrid 32%. Semantic không thắng
trong môi trường lite: BGE-small thiên về tiếng Anh, còn corpus tiếng Việt.
RRF không sửa được tín hiệu semantic yếu; cần đánh giá model đa ngữ khi nâng cấp.

Tôi dùng pure BM25 cho mã định danh hoặc thuật ngữ chính xác khi cần latency
thấp; dùng pure vector khi câu hỏi chủ yếu diễn đạt lại và model đã được kiểm
chứng trên ngôn ngữ đích. Tôi không mặc định hybrid nếu cải thiện chất lượng
không bù được chi phí truy xuất của hai nhánh.

---

## Điều ngạc nhiên nhất khi làm lab này

Hybrid thắng trung bình nhưng không thắng mọi nhóm query; phải xem bảng slice,
không chỉ nhìn một điểm tổng hợp.

---

## Bonus challenge

- [ ] Đã làm bonus (xem `bonus/`)
- Không thực hiện bonus theo phạm vi yêu cầu.
