# 🔘 Nút Đặt Hàng Trong Chatbot

## ✅ Đã Thêm

Nút "Đặt hàng" giờ đã xuất hiện trong tin nhắn của chatbot!

## 🎯 Cách Hoạt Động

### 1. Người dùng hỏi và muốn đặt
```
User: "Tôi muốn đặt Gói Luxury"
```

### 2. Chatbot trả lời với nút đặt hàng
```
Bot: "Dạ vâng! Gói Luxury có giá 200.000.000đ..."

[Nút: 🛒 Đặt Gói Luxury]  ← NÚT MỚI!
```

### 3. Click nút → Mở form đặt hàng
- Form OrderForm tự động hiển thị
- Pre-fill thông tin sản phẩm
- Thu thập thông tin khách hàng

### 4. Submit form → Lưu database
- Gọi API `/api/app/chatbot/order`
- Lưu vào tables `orders` + `order_items`
- Hiển thị mã đơn hàng

## 🎨 UI Nút Đặt Hàng

### Design:
- **Background:** Gradient pink-500 to rose-500
- **Icon:** Shopping bag icon
- **Text:** "Đặt [Tên sản phẩm]"
- **Hover:** Darker gradient + shadow
- **Full width:** Chiếm toàn bộ chiều rộng tin nhắn

### Code:
```tsx
<button className="mt-3 w-full bg-gradient-to-r from-pink-500 to-rose-500 hover:from-pink-600 hover:to-rose-600 text-white font-medium py-2.5 px-4 rounded-lg transition-all duration-200 flex items-center justify-center gap-2 shadow-md hover:shadow-lg">
  <svg>...</svg>
  <span>Đặt {productName}</span>
</button>
```

## 📁 Files Đã Cập Nhật

### 1. `ChatMessage.tsx`
- ✅ Thêm prop `onOrderClick`
- ✅ Hiển thị nút khi có `message.action`
- ✅ Click nút → gọi callback

### 2. `ChatWindow.tsx`
- ✅ Thêm prop `onOrderClick`
- ✅ Truyền callback xuống ChatMessage
- ✅ Pass message object để lấy action

### 3. `Chatbot.tsx`
- ✅ Thêm function `handleOrderClick`
- ✅ Set orderAction khi click nút
- ✅ Truyền callback vào ChatWindow

## 🔄 Flow Hoàn Chỉnh

```
1. User: "Chốt Gói Standard"
   ↓
2. Chatbot Response:
   - Message: "Dạ vâng! Để đặt Gói Standard..."
   - Action: { type: "order", productId: "...", ... }
   ↓
3. ChatMessage Component:
   - Hiển thị tin nhắn
   - Hiển thị NÚT "Đặt Gói Standard" ✨
   ↓
4. User: Click nút
   ↓
5. handleOrderClick() được gọi
   ↓
6. setOrderAction(action)
   ↓
7. OrderForm modal hiển thị
   ↓
8. User: Điền form và submit
   ↓
9. API Call → Database
   ↓
10. Success message trong chat
```

## 🎯 Khi Nào Nút Hiển Thị?

Nút chỉ hiển thị khi:
1. ✅ Message có `action` object
2. ✅ `action.type === 'order'`
3. ✅ Message từ assistant (không phải user)
4. ✅ Có callback `onOrderClick`

## 📸 Screenshot Mô Tả

```
┌─────────────────────────────────┐
│ Chatbot                    [X]  │
├─────────────────────────────────┤
│                                 │
│  User: Tôi muốn đặt Gói Luxury │
│                                 │
│  Bot: Dạ vâng! Gói Luxury có   │
│       giá 200.000.000đ...       │
│                                 │
│  ┌───────────────────────────┐ │
│  │ 🛒 Đặt Gói Luxury         │ │ ← NÚT MỚI
│  └───────────────────────────┘ │
│                                 │
└─────────────────────────────────┘
```

## 🧪 Test Cases

### Test 1: Nút hiển thị
```
Input: "Tôi muốn đặt Gói Standard"
Expected: Nút "Đặt Gói Standard" xuất hiện
```

### Test 2: Click nút
```
Action: Click nút
Expected: OrderForm modal mở
```

### Test 3: Không có action
```
Input: "Xin chào"
Expected: Không có nút (vì không có action)
```

### Test 4: Multiple messages
```
Scenario: Nhiều tin nhắn có action
Expected: Mỗi tin nhắn có nút riêng
```

## 💡 Tips

### Styling:
- Nút có gradient đẹp mắt
- Hover effect mượt mà
- Icon shopping bag phù hợp
- Full width để dễ click

### UX:
- Nút rõ ràng, dễ nhận biết
- Text động theo tên sản phẩm
- Click → mở form ngay lập tức
- Không cần scroll để tìm nút

### Performance:
- Chỉ render nút khi cần
- Callback được memoize
- Không re-render không cần thiết

## 🎉 Kết Quả

Giờ đây người dùng có **2 CÁCH** để đặt hàng:

### Cách 1: Tự động (Mới)
1. Hỏi về sản phẩm
2. Nói muốn đặt
3. **Click nút trong chat** ✨
4. Điền form
5. Done!

### Cách 2: Thủ công (Cũ)
1. Hỏi về sản phẩm
2. Chatbot trả về action
3. Form tự động mở
4. Điền form
5. Done!

**Cách 1 trực quan và dễ dùng hơn!** 🎯
