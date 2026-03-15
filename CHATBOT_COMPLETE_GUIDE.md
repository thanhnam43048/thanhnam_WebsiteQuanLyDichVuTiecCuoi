# 🤖 Chatbot Hoàn Chỉnh - Hướng Dẫn Sử Dụng

## ✅ Tính Năng Đã Hoàn Thành

### 1. Backend (Node.js + TypeScript)
- ✅ Tích hợp Groq AI (Llama 3.3 70B) - Miễn phí & Nhanh
- ✅ Lấy dữ liệu từ database: Products, Services, Packages, FAQs
- ✅ Lấy ảnh từ 2 nguồn: Bảng chính + Galleries
- ✅ Trả về text + images + product info
- ✅ Personality: Linh - Tư vấn viên thân thiện
- ✅ Logs chi tiết để debug

### 2. Frontend (Next.js + React)
- ✅ Giao diện chat đẹp với gradient màu hồng
- ✅ Floating button với animation
- ✅ Hiển thị tin nhắn + ảnh sản phẩm
- ✅ Quick replies gợi ý
- ✅ Loading state
- ✅ Responsive design
- ✅ Cấu trúc features-based

## 📁 Cấu Trúc File

```
backend/
├── src/application/services/
│   └── ChatbotService.ts          # Logic chính
├── src/interfaces/controllers/
│   └── chatbot.controller.ts      # API endpoints
└── src/interfaces/routes/app/
    └── index.ts                   # Routes config

Laddingpage/
└── src/features/chat/
    ├── components/
    │   ├── ChatButton.tsx         # Nút floating
    │   ├── ChatHeader.tsx         # Header chat
    │   ├── ChatMessage.tsx        # Hiển thị tin nhắn + ảnh
    │   ├── ChatInput.tsx          # Input gửi tin
    │   ├── QuickReplies.tsx       # Gợi ý câu hỏi
    │   └── ChatWindow.tsx         # Cửa sổ chat
    ├── api.ts                     # API calls
    ├── types.ts                   # TypeScript types
    ├── constants.ts               # Constants
    ├── Chatbot.tsx               # Main component
    └── index.ts                   # Exports
```

## 🚀 API Endpoints

### POST `/api/app/chatbot/chat`
**Request:**
```json
{
  "message": "Cho xem sản phẩm thiệp cưới",
  "conversationHistory": [
    { "role": "user", "content": "Chào bạn" },
    { "role": "assistant", "content": "Chào bạn! ..." }
  ]
}
```

**Response:**
```json
{
  "success": true,
  "data": {
    "message": "Dạ có ạ! Mình có mấy mẫu thiệp cưới đẹp này...",
    "images": [
      {
        "url": "/images/thiep1.jpg",
        "alt": "Thiệp cưới cao cấp",
        "productName": "Thiệp cưới cao cấp"
      }
    ],
    "products": [
      {
        "id": "1",
        "name": "Thiệp cưới cao cấp",
        "price": 50000
      }
    ],
    "timestamp": "2024-01-01T00:00:00.000Z"
  }
}
```

### GET `/api/app/chatbot/quick-replies`
Lấy danh sách câu hỏi gợi ý

### GET `/api/app/chatbot/info`
Lấy thông tin chatbot

## 🎨 Tính Năng Nổi Bật

### 1. Hiển Thị Ảnh Thông Minh
- Tự động hiển thị ảnh khi khách hỏi về sản phẩm/dịch vụ
- Lấy ảnh từ cả bảng chính và galleries
- Hiển thị tên + giá sản phẩm kèm ảnh

### 2. Personality Tự Nhiên
- Gọi tên "Linh" - tư vấn viên thân thiện
- Dùng emoji phù hợp: 😊💕✨🥰💖
- Nói chuyện tự nhiên như bạn bè
- Không cứng nhắc, không như bot

### 3. Dữ Liệu Đầy Đủ
- Đọc HẾT products, services, packages, FAQs
- Không giới hạn 5 items
- Thông tin chi tiết: giá, mô tả, tồn kho, ảnh

## 🔧 Cách Chạy

### Backend
```bash
cd backend
npm install
npm run dev
```

### Landing Page
```bash
cd Laddingpage
npm install
npm run dev
```

### Test
1. Mở http://localhost:3000
2. Click nút chat góc phải
3. Thử các câu:
   - "Chào bạn"
   - "Có sản phẩm gì?"
   - "Cho xem ảnh thiệp cưới"
   - "Gói dịch vụ nào phù hợp?"

## 📊 Logs Debug

Server sẽ hiển thị logs:
```
🔍 Fetching ALL products...
📦 Found 50 products
✅ Product Thiệp cưới has main image: /images/thiep1.jpg
🖼️ Found 3 gallery images for Thiệp cưới
📊 Product Thiệp cưới: 4 images total
📏 System prompt length: 15000 characters
✅ Should include images
📊 Total images collected: 10
```

## ⚙️ Cấu Hình

### .env
```env
# Groq AI
USE_GROQ=true
GROQ_API_KEY=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
GROQ_MODEL=llama-3.3-70b-versatile

# Database
DB_HOST=127.0.0.1
DB_PORT=3306
DB_USER=root
DB_PASS=
DB_NAME=wedding
```

## 🎯 Từ Khóa Trigger

Chatbot sẽ lấy dữ liệu khi phát hiện:

**Products:** sản phẩm, thiệp, trang trí, product, ảnh, hình
**Services:** dịch vụ, service, chụp ảnh, quay phim, trang điểm
**Packages:** gói, package, combo, trọn gói, giá, bao nhiêu, chi phí
**FAQs:** hỏi, câu hỏi, thắc mắc, faq

## 🐛 Troubleshooting

### Không hiển thị ảnh?
1. Check logs xem có fetch được galleries không
2. Kiểm tra database có dữ liệu ảnh không
3. Verify URL ảnh có đúng không

### AI không trả lời?
1. Check API key Groq có hợp lệ không
2. Xem logs có lỗi gì không
3. Thử model khác: `llama-3.1-8b-instant`

### Prompt quá dài?
1. Giảm số lượng products/services
2. Rút gọn description
3. Tăng max_tokens

## 📝 TODO / Cải Tiến

- [ ] Thêm semantic search cho dữ liệu lớn
- [ ] Cache dữ liệu để giảm query DB
- [ ] Thêm rating/feedback cho câu trả lời
- [ ] Export chat history
- [ ] Multi-language support
- [ ] Voice input/output

## 🎉 Kết Luận

Chatbot đã hoàn chỉnh với đầy đủ tính năng:
- ✅ Tích hợp AI thông minh
- ✅ Hiển thị ảnh sản phẩm
- ✅ Giao diện đẹp, UX tốt
- ✅ Dữ liệu đầy đủ từ database
- ✅ Logs chi tiết để debug

Sẵn sàng để deploy! 🚀
