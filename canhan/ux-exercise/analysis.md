# UX exercise — Vietnam Airlines NEO Chatbot  

## Sản phẩm: Vietnam Airlines — NEO Chatbot (CSKH & tra cứu chuyến bay)  

---

## 4 paths  

### 1. AI đúng  
- User hỏi “Hành lý ký gửi được bao nhiêu kg?” → NEO trả lời đúng theo từng hạng vé  
- User nhận được thông tin đầy đủ, có cấu trúc rõ ràng  
- UI: hiển thị text + link hướng dẫn, không có bước confirm  
- Hạn chế: không gợi ý hành động tiếp theo (ví dụ tra cứu chuyến bay, đặt vé)  

---

### 2. AI không chắc  
- User hỏi “Tôi muốn bay chiều nay” → NEO không hiểu intent  
- UI: không hỏi lại, không đưa option → yêu cầu nhập mã đặt chỗ hoặc số chuyến bay  
- User không có thông tin → bị kẹt flow  
- Vấn đề: không có cơ chế clarification (“bạn bay từ đâu đến đâu?”)  

---

### 3. AI sai  
- User hỏi “VN123 bay lúc 25h đúng không?” → input sai logic  
- NEO không phát hiện lỗi “25h”  
- UI: yêu cầu thêm thông tin, sau đó trả lời “không tìm thấy”  
- User nói “bạn sai rồi” → bot không sửa, chỉ lặp lại fallback  
- Sửa: user phải hỏi lại từ đầu → nhiều bước  
- Vấn đề: không có error handling và không có self-correction  

---

### 4. User mất niềm tin  
- Sau nhiều lần không hiểu hoặc trả lời lặp, user mất kiên nhẫn  
- NEO đưa fallback: hotline, email, gặp tư vấn viên  
- UI: fallback dạng text, không tích hợp trực tiếp trong chat  
- Không có chuyển tiếp seamless sang human agent  
- Vấn đề: exit có nhưng UX rời rạc, không giữ context  

---

## Path yếu nhất: Path 2 + 3  
- Không xử lý được câu hỏi mơ hồ (không hỏi lại, không gợi ý)  
- Khi sai, không có cơ chế sửa hoặc giải thích  
- User phải tự lặp lại → friction cao  
- Thiếu uncertainty handling là nguyên nhân chính  

---

## Gap marketing vs thực tế  
- Marketing: chatbot AI thông minh, hỗ trợ khách hàng nhanh chóng 24/7  
- Thực tế: hoạt động như FAQ bot, phụ thuộc vào kịch bản cố định  
- Không hiểu ngôn ngữ tự nhiên, không xử lý context  
- Gap lớn nhất: không xử lý được khi AI không chắc hoặc sai  

---

## Sketch  

- As-is:  
  user hỏi → bot không hiểu → yêu cầu mã vé → user không có → kẹt → bỏ chatbot  

- To-be:  
  user hỏi → bot nhận diện intent → hỏi lại thông tin thiếu → gợi ý lựa chọn  
  → user chọn → tiếp tục flow  

- Thay đổi:  
  + Thêm bước hỏi lại (clarification)  
  + Thêm gợi ý lựa chọn (options)  
  - Bỏ ép nhập mã vé ngay từ đầu  
  ~ Chuyển từ rule-based sang intent-based  