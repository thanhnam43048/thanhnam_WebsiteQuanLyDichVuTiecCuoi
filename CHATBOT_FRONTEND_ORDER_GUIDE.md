# 🎨 Hướng Dẫn Sử Dụng Tính Năng Đặt Hàng - Frontend

## ✅ Đã Hoàn Thành

Tính năng đặt hàng qua chatbot đã được tích hợp hoàn toàn vào frontend!

## 🎯 Cách Hoạt Động

### 1. Người dùng chat với bot
```
User: "Tôi muốn đặt Gói Luxury"
```

### 2. Chatbot nhận diện và trả về action
- Backend phát hiện từ khóa: đặt, chốt, order, book, mua...
- Trả về `action` object với thông tin sản phẩm

### 3. Frontend tự động hiển thị form
- Component `OrderForm` tự động mở
- Pre-fill thông tin sản phẩm
- Thu thập thông tin khách hàng

### 4. Người dùng điền form và submit
- Validate thông tin bắt buộc
- Gọi API `POST /api/app/chatbot/order`
- Lưu vào database

### 5. Hiển thị kết quả
- Thông báo thành công với mã đơn hàng
- Hoặc hiển thị lỗi nếu có

## 📁 Files Đã Tạo/Cập Nhật

### 1. `types.ts` - Thêm types mới
```typescript
export interface OrderAction {
  type: 'order' | 'consultation';
  productId: string;
  productName: string;
  productType: 'package' | 'product' | 'service';
  price: number;
}

export interface OrderFormData {
  productId: string;
  productType: 'package' | 'product' | 'service';
  clientName: string;
  clientPhone: string;
  clientEmail?: string;
  weddingDate: string;
  venue: string;
  guestCount?: number;
  notes?: string;
}
```

### 2. `api.ts` - Thêm function createOrder
```typescript
export async function createOrder(orderData: OrderFormData): Promise<{
  success: boolean;
  orderId?: string;
  message: string;
}>
```

### 3. `OrderForm.tsx` - Component form đặt hàng
- Form đẹp với Tailwind CSS
- Validation
- Loading state
- Error handling

### 4. `Chatbot.tsx` - Tích hợp OrderForm
- Nhận `action` từ API
- Hiển thị OrderForm khi có action
- Xử lý success/error

## 🎨 UI/UX Features

### OrderForm Component
- ✅ Modal overlay với backdrop
- ✅ Header gradient đẹp mắt
- ✅ Hiển thị tên sản phẩm và giá
- ✅ Form fields với validation
- ✅ Required fields đánh dấu *
- ✅ Date picker cho ngày cưới
- ✅ Loading state khi submit
- ✅ Error messages
- ✅ Responsive design

### Form Fields
1. **Tên khách hàng** (bắt buộc)
2. **Số điện thoại** (bắt buộc)
3. **Email** (tùy chọn)
4. **Ngày cưới** (bắt buộc) - Date picker
5. **Địa điểm** (bắt buộc)
6. **Số lượng khách** (tùy chọn, default: 100)
7. **Ghi chú** (tùy chọn) - Textarea

### Buttons
- **Hủy** - Đóng form
- **Xác nhận đặt hàng** - Submit form

## 🔄 Flow Hoàn Chỉnh

```
1. User: "Chốt Gói Standard"
   ↓
2. Chatbot API Response:
   {
     message: "Dạ vâng! Để đặt Gói Standard...",
     action: {
       type: "order",
       productId: "...",
       productName: "Gói Standard",
       productType: "package",
       price: 80000000
     }
   }
   ↓
3. Frontend: setOrderAction(action)
   ↓
4. OrderForm Component: Hiển thị modal
   ↓
5. User: Điền thông tin và submit
   ↓
6. API Call: POST /api/app/chatbot/order
   ↓
7. Database: Lưu vào tables orders + order_items
   ↓
8. Response: { success: true, orderId: "...", message: "..." }
   ↓
9. Frontend: Hiển thị thông báo thành công trong chat
   ↓
10. Done! ✅
```

## 🧪 Test Cases

### Test 1: Đặt gói dịch vụ
```
User: "Tôi muốn đặt Gói Luxury"
Expected: Form hiển thị với thông tin Gói Luxury
```

### Test 2: Đặt sản phẩm
```
User: "Chốt Backdrop Hoa Tươi"
Expected: Form hiển thị với thông tin Backdrop
```

### Test 3: Validation
```
User: Submit form thiếu thông tin
Expected: Hiển thị error "Vui lòng điền đầy đủ thông tin bắt buộc"
```

### Test 4: Success
```
User: Submit form đầy đủ thông tin
Expected: 
- API call thành công
- Đơn hàng lưu vào database
- Hiển thị mã đơn hàng trong chat
- Form đóng lại
```

### Test 5: Error handling
```
Scenario: API error
Expected: Hiển thị error message trong form
```

## 📊 Database Schema

Khi submit form, data được lưu vào:

### Table: `orders`
```sql
id: UUID
client_name: string
client_email: string
client_phone: string
wedding_date: date
guest_count: number
venue: string
notes: string
payment_method: 'bank_transfer'
total_amount: number
deposit_amount: number (30% of total)
status: 'pending'
created_at: timestamp
updated_at: timestamp
```

### Table: `order_items`
```sql
id: UUID
order_id: UUID (foreign key)
package_id / product_id / service_id: UUID
item_name: string
item_type: 'package' | 'product' | 'service'
quantity: 1
unit_price: number
subtotal: number
description: 'Đặt qua chatbot'
```

## 🎯 Next Steps (Optional)

### Có thể thêm:
1. **Email confirmation** - Gửi email xác nhận đơn hàng
2. **SMS notification** - Gửi SMS cho khách hàng
3. **Order tracking** - Trang theo dõi đơn hàng
4. **Payment integration** - Tích hợp thanh toán online
5. **Admin notification** - Thông báo cho admin khi có đơn mới

## 🔧 Troubleshooting

### Lỗi: Form không hiển thị
- Check: `action` có được trả về từ API không?
- Check: Console log để xem response

### Lỗi: API call failed
- Check: Endpoint URL đúng chưa?
- Check: Request body format
- Check: Backend server đang chạy?

### Lỗi: Validation không hoạt động
- Check: Required fields có attribute `required`?
- Check: Form submit handler có validate?

## 📝 Code Example

### Sử dụng trong component khác
```typescript
import { OrderForm } from '@/features/chat/components/OrderForm';

function MyComponent() {
  const [orderAction, setOrderAction] = useState<OrderAction | null>(null);

  const handleOrder = () => {
    setOrderAction({
      type: 'order',
      productId: 'xxx',
      productName: 'Gói Standard',
      productType: 'package',
      price: 80000000,
    });
  };

  return (
    <>
      <button onClick={handleOrder}>Đặt hàng</button>
      
      {orderAction && (
        <OrderForm
          action={orderAction}
          onClose={() => setOrderAction(null)}
          onSuccess={(orderId, message) => {
            console.log('Order created:', orderId);
            alert(message);
          }}
        />
      )}
    </>
  );
}
```

## ✅ Checklist

- [x] Types định nghĩa
- [x] API function createOrder
- [x] OrderForm component
- [x] Tích hợp vào Chatbot
- [x] Validation
- [x] Error handling
- [x] Loading states
- [x] Success feedback
- [x] Responsive design
- [x] Database integration

## 🎉 Kết Luận

Tính năng đặt hàng qua chatbot đã hoàn thành 100%!

**Người dùng giờ có thể:**
1. Chat với bot về sản phẩm
2. Nói muốn đặt hàng
3. Điền form tự động hiển thị
4. Submit → Lưu vào database
5. Nhận mã đơn hàng ngay lập tức

**Admin có thể:**
- Xem đơn hàng trong admin panel
- Quản lý orders từ chatbot
- Liên hệ khách hàng theo thông tin đã lưu
