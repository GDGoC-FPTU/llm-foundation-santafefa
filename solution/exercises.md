# Ngày 1 — Bài Tập & Phản Ánh
## Nền Tảng LLM API | Phiếu Thực Hành

**Thời lượng:** 1:30 giờ  
**Cấu trúc:** Lập trình cốt lõi (60 phút) → Bài tập mở rộng (30 phút)

---

## Phần 1 — Lập Trình Cốt Lõi (0:00–1:00)

Chạy các ví dụ trong Google Colab tại: https://colab.research.google.com/drive/172zCiXpLr1FEXMRCAbmZoqTrKiSkUERm?usp=sharing

Triển khai tất cả TODO trong `template.py`. Chạy `pytest tests/` để kiểm tra tiến độ.

**Điểm kiểm tra:** Sau khi hoàn thành 4 nhiệm vụ, chạy:
```bash
python template.py
```
Bạn sẽ thấy output so sánh phản hồi của GPT-4o và GPT-4o-mini.

---

## Phần 2 — Bài Tập Mở Rộng (1:00–1:30)

### Bài tập 2.1 — Độ Nhạy Của Temperature
Gọi `call_openai` với các giá trị temperature 0.0, 0.5, 1.0 và 1.5 sử dụng prompt *
*0.0: Việt Nam là quốc gia xuất khẩu hạt điều và hạt tiêu đen lớn nhất trên thế giới.

0.5: Một sự thật thú vị là Hang Sơn Đoòng ở Quảng Bình, Việt Nam, là hang động tự nhiên lớn nhất thế giới. Nó rộng lớn đến mức có cả một hệ sinh thái, rừng cây và mây mù hình thành ngay bên trong hang.

1.0: Bạn có biết về "Cà phê trứng" không? Đây là một thức uống đặc sản của Hà Nội, được làm từ lòng đỏ trứng gà đánh bông mịn cùng sữa đặc, tạo ra một lớp kem béo ngậy phủ lên trên lớp cà phê đen đậm đà. Nó có vị giống như món tráng miệng tiramisu dạng lỏng vậy!

1.5: Ồ, nón lá không chỉ che nắng đâu! Những dòng sông xe máy cuồn cuộn như bầy ong kim loại dệt mộng qua Hà Nội. Gạo lúa nhảy múa tung tăng trong chảo phở bốc khói nghi ngút, và bạn sẽ thấy những dải đất hình chữ S lấp lánh phép thuật nhiệt đới ở mọi góc phố!**

**Bạn nhận thấy quy luật gì qua bốn phản hồi?** (2–3 câu)
> *Tăng dần từ 0.0 lên 1.5 câu trả lời trở câu trả lời của bạn chuyển từ trạng thái an toàn, súc tích và mang tính tất định sang trạng thái đa dạng, sáng tạo và ngẫu hứng hơn rất dễ xuất hiện hiện tượng "ảo giác"*

**Bạn sẽ đặt temperature bao nhiêu cho chatbot hỗ trợ khách hàng, và tại sao?**
> *khoảng 0.0 đến 0.2.Lý do là vì chatbot hỗ trợ khách hàng ưu tiên độ chính xác, tính nhất quán và sự rõ ràng tuyệt đối. Khi khách hàng hỏi về quy định đổi trả, giá sản phẩm hay khắc phục sự cố, họ cần thông tin chuẩn xác và đáng tin cậy giống nhau trong mọi lần hỏi, chứ không cần một AI sáng tạo, nói đùa hay có rủi ro cung cấp sai lệch thông tin chính sách của công ty*

---

### Bài tập 2.2 — Đánh Đổi Chi Phí
Xem xét kịch bản: 10.000 người dùng hoạt động mỗi ngày, mỗi người thực hiện 3 lần gọi API, mỗi lần trung bình ~350 token.

**Ước tính xem GPT-4o đắt hơn GPT-4o-mini bao nhiêu lần cho workload này:**
> *khoảng 33 lần*

**Mô tả một trường hợp mà chi phí cao hơn của GPT-4o là xứng đáng, và một trường hợp GPT-4o-mini là lựa chọn tốt hơn:**
> *Trường hợp GPT-4o xứng đáng (Ưu tiên chất lượng & Trí tuệ): Khi ứng dụng của bạn giải quyết các tác vụ có rủi ro cao, đòi hỏi khả năng suy luận logic sâu, hiểu ngữ cảnh phức tạp hoặc phân tích dữ liệu đa phương tiện.Trường hợp GPT-4o-mini tốt hơn (Ưu tiên quy mô & Chi phí): Khi ứng dụng phục vụ số lượng lớn người dùng với các tác vụ đơn giản, lặp đi lặp lại và mang tính phân loại/trích xuất thông tin cơ bản.*

---

### Bài tập 2.3 — Trải Nghiệm Người Dùng với Streaming
**Streaming quan trọng nhất trong trường hợp nào, và khi nào thì non-streaming lại phù hợp hơn?** (1 đoạn văn)
> *Streaming quan trọng nhất trong các ứng dụng tương tác trực tiếp với người dùng, chẳng hạn như chatbot hoặc trợ lý ảo, nơi việc chờ đợi một phản hồi dài có thể gây ức chế; việc hiển thị từng từ (token) ngay khi được tạo ra giúp giảm thiểu thời gian chờ phản hồi đầu tiên (Time To First Token), tạo cảm giác mượt mà và giữ chân sự chú ý của người dùng. Ngược lại, non-streaming (chờ nhận toàn bộ kết quả rồi mới trả về) lại phù hợp và tối ưu hơn đối với các tác vụ xử lý ngầm (background processing), phân tích hàng loạt (batch jobs), hoặc trích xuất dữ liệu có cấu trúc (như trả về chuỗi JSON), bởi vì trong những trường hợp này, các hệ thống phần mềm cần một khối dữ liệu hoàn chỉnh và chính xác để xử lý bước tiếp theo chứ không quan tâm đến hiệu ứng hiển thị thời gian thực.*


## Danh Sách Kiểm Tra Nộp Bài
- [ ] Tất cả tests pass: `pytest tests/ -v`
- [ ] `call_openai` đã triển khai và kiểm thử
- [ ] `call_openai_mini` đã triển khai và kiểm thử
- [ ] `compare_models` đã triển khai và kiểm thử
- [ ] `streaming_chatbot` đã triển khai và kiểm thử
- [ ] `retry_with_backoff` đã triển khai và kiểm thử
- [ ] `batch_compare` đã triển khai và kiểm thử
- [ ] `format_comparison_table` đã triển khai và kiểm thử
- [ ] `exercises.md` đã điền đầy đủ
- [ ] Sao chép bài làm vào folder `solution` và đặt tên theo quy định 
