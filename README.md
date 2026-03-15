# Wedding Paradise - Full Stack Application

Hệ thống quản lý và đặt dịch vụ tổ chức đám cưới chuyên nghiệp, bao gồm **Landing Page** (Next.js 15) và **Backend API** (Node.js + TypeScript).

## 🎯 Tổng Quan Dự Án

Wedding Paradise là một nền tảng full-stack cho phép:
- ✅ Khách hàng xem và đặt dịch vụ tổ chức đám cưới
- ✅ Quản lý gói dịch vụ, sản phẩm, và đơn hàng
- ✅ Hệ thống mã giảm giá và voucher
- ✅ Thư viện ảnh và testimonials
- ✅ API RESTful với Clean Architecture

---

## 📦 Cấu Trúc Dự Án

```
wedding-paradise/
├── 📁 Laddingpage/          # Frontend - Next.js 15
│   ├── app/                 # Next.js App Router
│   ├── src/                 # Source code
│   │   ├── features/        # Feature modules
│   │   │   ├── api/         # API integration
│   │   │   ├── packages/    # Wedding packages
│   │   │   ├── services/    # Services
│   │   │   ├── products/    # Products
│   │   │   ├── order/       # Order & cart
│   │   │   ├── gallery/     # Photo gallery
│   │   │   └── testimonials/# Customer reviews
│   │   └── components/      # Shared components
│   └── public/              # Static assets
│
└── 📁 backend/              # Backend - Node.js + TypeScript
    ├── src/
    │   ├── application/     # Business logic
    │   │   ├── services/    # Application services
    │   │   ├── dto/         # Data transfer objects
    │   │   └── interfaces/  # Service interfaces
    │   ├── domain/          # Domain entities
    │   │   ├── entities/    # Business entities
    │   │   └── repositories/# Repository interfaces
    │   ├── infrastructure/  # External concerns
    │   │   ├── database/    # Database setup
    │   │   │   ├── migrations/
    │   │   │   └── seeds/
    │   │   └── repositories/# Repository implementations
    │   └── interfaces/      # API layer
    │       ├── controllers/ # HTTP controllers
    │       ├── routes/      # Route definitions
    │       └── middlewares/ # Express middlewares
    └── knexfile.ts          # Database configuration
```

---

## 🚀 Frontend - Landing Page

### **Công Nghệ**
- **Next.js 15** - App Router, SSR/SSG
- **React 19** - Latest features
- **TypeScript** - Type safety
- **Tailwind CSS v4** - Styling
- **Zustand** - State management
- **Axios** - HTTP client

### **Tính Năng Chính**

#### 🏠 Hero Section
- Hero banner với gradient background
- Call-to-action buttons
- Responsive animations

#### 💍 Wedding Packages
- Hiển thị gói dịch vụ từ API
- Pricing cards với features
- Mã giảm giá tích hợp
- Chi tiết gói với images

#### 🛍️ Services & Products
- Danh sách dịch vụ
- Chi tiết sản phẩm
- Thêm vào giỏ hàng
- Áp dụng voucher

#### � Shopping Cart & Checkout
- Giỏ hàng với Zustand
- Nhập mã giảm giá
- Form đặt hàng
- Validation & error handling

#### 📸 Gallery & Testimonials
- Thư viện ảnh từ API
- Đánh giá khách hàng
- Rating stars

#### ❓ FAQ Section
- Câu hỏi thường gặp
- Accordion design

### **Cài Đặt Frontend**

```bash
cd Laddingpage
npm install
npm run dev
```

**Chạy tại:** http://localhost:3000

### **Environment Variables**

Tạo file `Laddingpage/.env.local`:

```env
NEXT_PUBLIC_API_URL=http://localhost:4000
```

---

## 🔧 Backend - API Server

### **Công Nghệ**
- **Node.js** + **TypeScript**
- **Express.js** - Web framework
- **Knex.js** - Query builder
- **MySQL** - Database
- **Clean Architecture** - Design pattern
- **JWT** - Authentication (future)

### **Architecture Pattern**

```
Clean Architecture (Layered)
├── Domain Layer (Entities, Business Rules)
├── Application Layer (Use Cases, Services)
├── Infrastructure Layer (Database, External Services)
└── Interface Layer (Controllers, Routes, Middlewares)
```

### **API Endpoints**

#### **User/Public Endpoints**

**Services**
- `GET /api/user/services` - Danh sách dịch vụ
- `GET /api/user/services/:id` - Chi tiết dịch vụ
- `GET /api/user/services/slug/:slug` - Dịch vụ theo slug

**Packages**
- `GET /api/user/packages` - Danh sách gói
- `GET /api/user/packages/:id` - Chi tiết gói
- `GET /api/user/packages/slug/:slug` - Gói theo slug

**Products**
- `GET /api/user/products` - Danh sách sản phẩm
- `GET /api/user/products/:id` - Chi tiết sản phẩm
- `GET /api/user/products/slug/:slug` - Sản phẩm theo slug

**Gallery**
- `GET /api/user/galleries` - Thư viện ảnh
- `GET /api/user/galleries/:id` - Chi tiết ảnh

**Testimonials**
- `GET /api/user/testimonials` - Đánh giá khách hàng

**FAQ**
- `GET /api/user/faqs` - Câu hỏi thường gặp

**Vouchers**
- `POST /api/user/vouchers/validate` - Validate mã giảm giá
- `GET /api/user/vouchers/active` - Voucher đang hoạt động
- `GET /api/user/vouchers/:code` - Voucher theo code

**Orders**
- `POST /api/user/orders` - Tạo đơn hàng
- `GET /api/user/orders/:id` - Chi tiết đơn hàng
- `GET /api/user/orders/email/:email` - Đơn hàng theo email

**Consultations**
- `POST /api/user/consultations` - Đặt lịch tư vấn

#### **Admin Endpoints**

**Services Management**
- `GET /api/admin/services` - Quản lý dịch vụ
- `POST /api/admin/services` - Tạo dịch vụ
- `PUT /api/admin/services/:id` - Cập nhật dịch vụ
- `DELETE /api/admin/services/:id` - Xóa dịch vụ

**Packages Management**
- `GET /api/admin/packages` - Quản lý gói
- `POST /api/admin/packages` - Tạo gói
- `PUT /api/admin/packages/:id` - Cập nhật gói
- `DELETE /api/admin/packages/:id` - Xóa gói

**Products Management**
- `GET /api/admin/products` - Quản lý sản phẩm
- `POST /api/admin/products` - Tạo sản phẩm
- `PUT /api/admin/products/:id` - Cập nhật sản phẩm
- `DELETE /api/admin/products/:id` - Xóa sản phẩm

**Orders Management**
- `GET /api/admin/orders` - Quản lý đơn hàng
- `PUT /api/admin/orders/:id` - Cập nhật trạng thái
- `DELETE /api/admin/orders/:id` - Xóa đơn hàng

**Vouchers Management**
- `GET /api/admin/vouchers` - Quản lý voucher
- `POST /api/admin/vouchers` - Tạo voucher
- `PUT /api/admin/vouchers/:id` - Cập nhật voucher
- `DELETE /api/admin/vouchers/:id` - Xóa voucher

### **Database Schema**

**Core Tables:**
- `services` - Dịch vụ cưới
- `packages` - Gói dịch vụ
- `products` - Sản phẩm
- `orders` - Đơn hàng
- `order_items` - Chi tiết đơn hàng
- `vouchers` - Mã giảm giá
- `promotions` - Khuyến mãi
- `galleries` - Thư viện ảnh
- `testimonials` - Đánh giá
- `faqs` - Câu hỏi thường gặp
- `consultations` - Lịch tư vấn

**Shared Tables:**
- `features` - Features cho services/packages/products
- `images` - Images cho các entities

### **Cài Đặt Backend**

```bash
cd backend
npm install
```

### **Database Setup**

1. **Tạo database MySQL:**
```sql
CREATE DATABASE wedding CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
```

2. **Cấu hình environment:**

Tạo file `backend/.env`:

```env
# Server
PORT=4000
NODE_ENV=development

# Database
DB_HOST=localhost
DB_PORT=3306
DB_USER=root
DB_PASSWORD=your_password
DB_NAME=wedding

# JWT (future)
JWT_SECRET=your_jwt_secret_key
JWT_EXPIRES_IN=7d

# CORS
CORS_ORIGIN=http://localhost:3000
```

3. **Chạy migrations:**
```bash
npm run migrate:latest
```

4. **Seed data:**
```bash
npm run seed:run
```

5. **Start server:**
```bash
npm run dev
```

**API chạy tại:** http://localhost:4000

### **Available Scripts**

```bash
# Development
npm run dev              # Start dev server with nodemon

# Database
npm run migrate:latest   # Run migrations
npm run migrate:rollback # Rollback migrations
npm run seed:run         # Seed database
npm run db:setup         # Migrate + Seed

# Production
npm run build            # Compile TypeScript
npm start                # Start production server
```

---

## 🎨 Design System

### **Color Palette**
```css
/* Primary - Rose/Pink Theme */
--rose-500: #f43f5e
--rose-600: #e11d48
--pink-500: #ec4899
--pink-600: #db2777

/* Gradients */
bg-gradient-to-r from-rose-500 to-pink-600
bg-gradient-to-b from-white via-pink-50/30 to-white
```

### **Typography**
```tsx
// Hero Text
text-5xl sm:text-6xl lg:text-7xl font-bold

// Section Headings
text-3xl sm:text-4xl lg:text-5xl font-bold

// Body Text
text-lg leading-relaxed text-gray-600
```

---

## 🔄 API Integration Flow

### **1. Fetch Services/Packages/Products**
```typescript
// Frontend
import { servicesApi, packagesApi, productsApi } from '@/src/features/api';

const services = await servicesApi.getAll();
const packages = await packagesApi.getAll();
const products = await productsApi.getAll();
```

### **2. Apply Voucher**
```typescript
const result = await vouchersApi.validate({
  code: 'FREESHIP',
  orderAmount: 50000000
});

if (result.data.valid) {
  // Apply discount
  const discount = result.data.discountAmount;
}
```

### **3. Create Order**
```typescript
const order = await ordersApi.create({
  clientName: 'Nguyễn Văn A',
  clientEmail: 'email@example.com',
  clientPhone: '0123456789',
  items: cartItems,
  weddingDate: '2025-12-25',
  guestCount: 100,
  venue: 'Khách sạn ABC',
  notes: 'Ghi chú',
  paymentMethod: 'bank_transfer',
  promotionCode: 'FREESHIP',
  discountAmount: 5000000
});
```

---

## 📊 Data Flow

```
User Action (Frontend)
    ↓
API Call (Axios)
    ↓
Backend Route
    ↓
Controller
    ↓
Service (Business Logic)
    ↓
Repository (Data Access)
    ↓
Database (MySQL)
    ↓
Response back to Frontend
```

---

## 🔒 Security Features

- ✅ CORS configuration
- ✅ Input validation
- ✅ SQL injection prevention (Knex.js)
- ✅ Error handling
- ✅ Environment variables
- 🔜 JWT authentication
- 🔜 Rate limiting
- 🔜 Request sanitization

---

## 🚀 Deployment

### **Frontend (Vercel)**
```bash
cd Laddingpage
vercel deploy
```

### **Backend (Railway/Heroku)**
```bash
cd backend
# Set environment variables
# Deploy using platform CLI
```

### **Database (PlanetScale/AWS RDS)**
- Setup MySQL database
- Run migrations
- Update connection string

---

## 📝 API Response Format

### **Success Response**
```json
{
  "success": true,
  "data": { ... },
  "message": "Operation successful"
}
```

### **Error Response**
```json
{
  "success": false,
  "message": "Error message",
  "errors": [
    {
      "field": "email",
      "message": "Invalid email format"
    }
  ]
}
```

---

## 🐛 Troubleshooting

### **Frontend Issues**
- Port 3000 đã được sử dụng: `npx kill-port 3000`
- API connection failed: Kiểm tra `NEXT_PUBLIC_API_URL`
- Build errors: `rm -rf .next && npm run build`

### **Backend Issues**
- Port 4000 đã được sử dụng: `npx kill-port 4000`
- Database connection failed: Kiểm tra `.env` credentials
- Migration errors: `npm run migrate:rollback` rồi `npm run migrate:latest`

---

## 📚 Documentation

- [Frontend README](./Laddingpage/README.md)
- [Backend API Routes](./backend/API_ROUTES.md)
- [Backend Architecture](./backend/ARCHITECTURE.md)
- [API Integration Guide](./Laddingpage/API_INTEGRATION_GUIDE.md)

---

## 🤝 Contributing

1. Fork the project
2. Create feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit changes (`git commit -m 'Add AmazingFeature'`)
4. Push to branch (`git push origin feature/AmazingFeature`)
5. Open Pull Request

---

## 📄 License

This project is licensed under the MIT License.

---

## 👥 Team

**Wedding Paradise Development Team**
- Frontend: Next.js + TypeScript
- Backend: Node.js + Clean Architecture
- Database: MySQL + Knex.js

---

**Wedding Paradise** - Tạo nên những khoảnh khắc đáng nhớ nhất! 💒✨
