# Experiment Report: Data Quality Impact on AI Agent

**Student ID:** 2A202600119  
**Name:** Lưu Linh Ly  
**Date:** 2026-04-15

---

## 1. Kết quả thí nghiệm

Chạy `agent_simulation.py` với 2 bộ dữ liệu và ghi lại kết quả:

| Scenario | Agent Response | Accuracy (1-10) | Notes |
|----------|----------------|-----------------|-------|
| Clean Data (`processed_data.csv`) | Agent: Based on my data, the best choice is Laptop at $1200.0. | 9 | Dữ liệu đã được làm sạch, category được chuẩn hóa, không còn record âm giá hay category rỗng. Agent chọn sản phẩm điện tử hợp lý nhất trong tập dữ liệu sạch. |
| Garbage Data (`garbage_data.csv`) | Agent: Based on my data, the best choice is Nuclear Reactor at $999999. | 2 | Agent bị đánh lừa bởi outlier giá cực lớn trong category electronics. Bộ dữ liệu còn có duplicate ID, wrong type và null values, làm giảm độ tin cậy của retrieval. |

---

## 2. Phân tích & nhận xét (Phan tich & nhan xet / Analysis)

### Tại sao Agent trả lời sai khi dùng Garbage Data? (Tai sao Agent tra loi sai)

Agent trả lời sai với garbage data vì nó phụ thuộc trực tiếp vào chất lượng dữ liệu đầu vào. Trong file `garbage_data.csv`, có một record outlier là `Nuclear Reactor` với giá `999999`, nằm trong category `electronics`. Logic của agent là tìm sản phẩm electronics có giá cao nhất, nên nó bị record bất thường này chi phối ngay lập tức. Ngoài ra, bộ dữ liệu còn có duplicate ID, trường giá sai kiểu dữ liệu (`ten dollars`) và record có giá trị null. Những lỗi này không nhất thiết làm script vỡ ngay, nhưng chúng làm cho tập dữ liệu trở nên thiếu tin cậy, khó truy vấn và dễ dẫn đến kết luận sai. Bài học ở đây là prompt tốt không thể cứu được một hệ thống nếu dữ liệu nền bên dưới bị bẩn, sai hoặc không được validate trước khi đưa vào agent.

---

## 3. Kết luận

**Quality Data > Quality Prompt?** Tôi đồng ý. Prompt có thể giúp agent diễn đạt rõ hơn, nhưng nếu dữ liệu nguồn có lỗi thì agent vẫn có xu hướng đưa ra câu trả lời sai một cách rất tự tin. Trong thí nghiệm này, cùng một câu hỏi, nhưng khi dùng clean data thì agent chọn được sản phẩm hợp lý, còn khi dùng garbage data thì nó chọn một outlier phi thực tế. Điều đó cho thấy data quality là nền tảng quan trọng hơn prompt quality trong các bài toán RAG và data-driven AI.
