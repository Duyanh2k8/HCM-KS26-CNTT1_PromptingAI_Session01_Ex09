# Bài 9: Kỹ thuật RAG Grounding Dập tắt Ảo giác Hợp đồng Thu mua
## Phần 1: Phân tích nguyên nhân ảo giác
Do nhân viên không cung cấp hợp đồng nên ChatGPT không biết quy định riêng của MartX. AI đã dựa vào kiến thức chung để tự đưa ra mức phạt 20% và đình chỉ nhập hàng 30 ngày.

Đây là hiện tượng ảo giác AI (Hallucination), tức là AI tự tạo ra thông tin không có căn cứ nhưng lại trả lời rất tự tin.

Muốn tránh lỗi này, nhân viên cần gửi tài liệu hợp đồng để AI dựa vào đó trả lời, thay vì để AI tự suy đoán.
## Phần 2: Cấu trúc RAG Prompt hoàn chỉnh
**Prompt sử dụng**
```text
Vai trò: Bạn là nhân viên Thu mua của MartX.

1. Văn bản hợp đồng chuẩn:

"Nhà cung cấp giao rau bị dập nát trên 10% sẽ bị phạt 5% giá trị lô hàng bị dập nát và phải đổi hàng trong vòng 24 giờ."

2. Câu hỏi nghiệp vụ:

Theo hợp đồng MartX, nếu nhà cung cấp giao rau bị dập nát trên 10% thì bị phạt bao nhiêu và phải đổi hàng trong bao lâu?

3. Negative Constraint (Khóa an toàn):

- Chỉ trả lời dựa trên nội dung hợp đồng.
- Không tự lấy thông tin bên ngoài để bổ sung.
- Nếu thông tin không có trong văn bản, tuyệt đối trả lời: "Không có dữ liệu trong tài liệu".
- Không tự suy đoán hoặc bịa ra thông tin.
```
