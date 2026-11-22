# Mochi Study

Trang học tập gồm bốn công cụ: tóm tắt tài liệu bằng AI, tạo quiz tương tác, đồng hồ tập trung và đếm ngược ngày quan trọng.

## Chạy trên Windows

1. Cài Python 3.10 trở lên nếu máy chưa có Python.
2. Mở PowerShell tại thư mục dự án và cấu hình API của một nhà cung cấp tương thích OpenAI Chat Completions:

   ```powershell
   $env:AI_API_KEY = "API-key-cua-ban"
   $env:AI_MODEL = "gpt-4o-mini"
   $env:AI_BASE_URL = "https://api.openai.com/v1"
   ```

   `AI_BASE_URL` và `AI_MODEL` có thể đổi theo nhà cung cấp bạn sử dụng. Mặc định, ứng dụng dùng `https://api.openai.com/v1` và `gpt-4o-mini`.

3. Chạy ứng dụng:

   ```powershell
   python server.py
   ```

4. Mở địa chỉ `http://127.0.0.1:8000`.

Không cần cài thêm thư viện Python. Khóa API chỉ được đọc ở backend từ biến môi trường và không được gửi xuống trình duyệt. Không mở `index.html` trực tiếp bằng `file://`; trang cần backend để gọi AI.

### Nếu gặp lỗi HTTP 405

Lỗi 405 thường có nghĩa trang đang được phục vụ bởi Live Server hoặc một máy chủ tĩnh khác, không phải `server.py`. Dừng máy chủ tĩnh, chạy `python server.py` từ thư mục dự án rồi mở địa chỉ mà server in ra. Nếu cổng 8000 đã được sử dụng, chọn cổng khác:

```powershell
$env:PORT = "8001"
python server.py
```

Sau đó mở `http://127.0.0.1:8001`.

## Đọc tài liệu và riêng tư

- Hỗ trợ PDF có văn bản, DOCX, TXT, MD và ảnh PNG/JPG/WEBP. Trích xuất PDF/DOCX và OCR ảnh chạy trong trình duyệt; các thư viện và dữ liệu OCR được tải từ CDN khi cần, vì vậy cần kết nối Internet.
- Tài liệu được đọc ở máy bạn. Khi chọn tóm tắt hoặc tạo quiz, phần văn bản trích xuất được gửi qua backend đến nhà cung cấp AI đã cấu hình để tạo kết quả.
- Tài liệu tối đa 25 MB; nội dung gửi AI tối đa 100.000 ký tự.
- Ngày quan trọng được lưu trong local storage của trình duyệt.
