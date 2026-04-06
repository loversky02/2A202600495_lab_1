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
Kết quả:
gpt4o_latency: 3.0901737213134766
mini_latency: 2.3788180351257324
gpt4o_cost_estimate: 0.0006533333333333332
---

## Phần 2 — Bài Tập Mở Rộng (1:00–1:30)

### Bài tập 2.1 — Độ Nhạy Của Temperature
Gọi `call_openai` với các giá trị temperature 0.0, 0.5, 1.0 và 1.5 sử dụng prompt **"Hãy kể cho tôi một sự thật thú vị về Việt Nam."**

**Bạn nhận thấy quy luật gì qua bốn phản hồi?** (2–3 câu)
> Khi temperature tăng từ 0.0 đến 1.5, các phản hồi trở nên đa dạng và sáng tạo hơn. Ở temperature 0.0 và 0.5, model tập trung vào chủ đề hang Sơn Đoòng với nội dung tương tự nhau. Ở temperature 1.5, model chuyển sang chủ đề hoàn toàn khác (rùa Hồ Gươm), cho thấy sự ngẫu nhiên và khả năng khám phá các chủ đề mới tăng lên đáng kể.

**Bạn sẽ đặt temperature bao nhiêu cho chatbot hỗ trợ khách hàng, và tại sao?**
> Tôi sẽ đặt temperature từ 0.0 đến 0.3 cho chatbot hỗ trợ khách hàng. Lý do là chatbot cần cung cấp thông tin chính xác, nhất quán và đáng tin cậy. Temperature thấp giúp model đưa ra câu trả lời có xác suất cao nhất, giảm thiểu rủi ro đưa ra thông tin sai lệch hoặc không liên quan, đảm bảo trải nghiệm khách hàng tốt nhất.

---

### Bài tập 2.2 — Đánh Đổi Chi Phí
Xem xét kịch bản: 10.000 người dùng hoạt động mỗi ngày, mỗi người thực hiện 3 lần gọi API, mỗi lần trung bình ~350 token.

**Ước tính xem GPT-4o đắt hơn GPT-4o-mini bao nhiêu lần cho workload này:**
> GPT-4o đắt hơn GPT-4o-mini **16.7 lần**. Cụ thể: GPT-4o chi phí $105/ngày ($38,325/năm) trong khi GPT-4o-mini chỉ $6.30/ngày ($2,299.50/năm). Sử dụng GPT-4o-mini sẽ tiết kiệm được $36,025.50/năm cho workload này.

**Mô tả một trường hợp mà chi phí cao hơn của GPT-4o là xứng đáng, và một trường hợp GPT-4o-mini là lựa chọn tốt hơn:**
> **GPT-4o xứng đáng:** Hệ thống tư vấn pháp lý hoặc y tế, nơi độ chính xác và khả năng reasoning phức tạp là tối quan trọng. Một sai sót có thể dẫn đến hậu quả nghiêm trọng về pháp lý hoặc sức khỏe, do đó chi phí cao hơn là đáng giá để đảm bảo chất lượng đầu ra tốt nhất.
> 
> **GPT-4o-mini tốt hơn:** Chatbot hỗ trợ khách hàng cơ bản (FAQ, tra cứu đơn hàng, hướng dẫn sử dụng sản phẩm). Các tác vụ này không yêu cầu reasoning phức tạp, chỉ cần trả lời nhanh và chính xác các câu hỏi đơn giản. GPT-4o-mini đủ khả năng xử lý với chi phí thấp hơn 16.7 lần, giúp tiết kiệm đáng kể cho doanh nghiệp.

---

### Bài tập 2.3 — Trải Nghiệm Người Dùng với Streaming
**Streaming quan trọng nhất trong trường hợp nào, và khi nào thì non-streaming lại phù hợp hơn?** (1 đoạn văn)
> Streaming quan trọng nhất trong các ứng dụng tương tác trực tiếp với người dùng như chatbot, trợ lý ảo, hoặc công cụ viết nội dung, nơi người dùng cần thấy phản hồi ngay lập tức để cảm thấy hệ thống đang hoạt động và giảm thời gian chờ đợi cảm nhận. Khi response dài (hơn vài giây), streaming giúp cải thiện trải nghiệm người dùng đáng kể bằng cách hiển thị từng phần kết quả ngay khi có sẵn. Ngược lại, non-streaming phù hợp hơn cho các tác vụ xử lý batch, API backend không có giao diện người dùng, hoặc khi cần xử lý toàn bộ response trước khi hiển thị (ví dụ: phân tích sentiment, trích xuất dữ liệu có cấu trúc JSON). Non-streaming cũng đơn giản hơn để implement và debug, phù hợp với các use case không yêu cầu tương tác real-time.


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
