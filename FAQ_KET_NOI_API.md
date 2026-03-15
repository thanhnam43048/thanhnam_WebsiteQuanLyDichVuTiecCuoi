# Câu Hỏi Thường Gặp - Kết Nối API

## 🔧 Vấn Đề CORS

### Lỗi: "Access to fetch has been blocked by CORS policy"

**Nguyên nhân:**
- Backend chưa cấu hình CORS đúng
- Frontend gọi từ domain khác với backend

**Giải pháp:**

1. **Kiểm tra file backend/.env:**
```env
CORS_ORIGIN=http://localhost:3000,http://localhost:5173
```

2. **Kiểm tra CORS middleware (backend/src/interfaces/middlewares/cors.middleware.ts):**
```typescript
app.use(cors({
  origin: process.env.CORS_ORIGIN?.split(',') || '*',
  credentials: true
}));
```

3. **Restart backend sau khi thay đổi:**
```bash
cd backend
npm run dev
```

---

## 🔐 Vấn Đề Authentication

### Lỗi: "401 Unauthorized" hoặc "Token invalid"

**Nguyên nhân:**
- Token không được gửi kèm request
- Token đã hết hạn
- Token không đúng format

**Giải pháp:**

1. **Admin Panel - Kiểm tra auth store (admin-panel/src/stores/auth.ts):**
```typescript
// Token phải được lưu và gửi kèm mỗi request
const token = localStorage.getItem('token');
```

2. **Kiểm tra HTTP client (admin-panel/src/utils/http.ts):**
```typescript
// Đảm bảo token được thêm vào header
headers: {
  'Authorization': `Bearer ${token}`
}
```

3. **Login lại để lấy token mới:**
- Vào trang login
- Đăng nhập với credentials đúng
- Token sẽ được lưu tự động

---

## 🌐 Vấn Đề Kết Nối

### Lỗi: "Network Error" hoặc "Failed to fetch"

**Nguyên nhân:**
- Backend chưa chạy
- URL API không đúng
- Port bị conflict

**Giải pháp:**

1. **Kiểm tra backend đang chạy:**
```bash
cd backend
npm run dev
# Phải thấy: Server running on port 5000
```

2. **Kiểm tra URL trong config:**

**Admin Panel (.env):**
```env
VITE_API_URL=http://localhost:5000/api
```

**Landing Page (.env.local):**
```env
NEXT_PUBLIC_API_URL=http://localhost:5000/api
```

3. **Test API trực tiếp:**
```bash
curl http://localhost:5000/api/health
```

---

## 📊 Vấn Đề Dữ Liệu

### Lỗi: "Cannot read property of undefined"

**Nguyên nhân:**
- API trả về structure khác với expected
- Dữ liệu chưa load xong
- Response không có data

**Giải pháp:**

1. **Kiểm tra response structure:**
```typescript
// Backend trả về format:
{
  success: true,
  data: [...],
  message: "Success"
}
```

2. **Thêm loading state:**
```typescript
const { data, isLoading, error } = useQuery();

if (isLoading) return <Loading />;
if (error) return <Error />;
if (!data) return null;
```

3. **Thêm optional chaining:**
```typescript
const items = response?.data?.items ?? [];
```

---

## 🔄 Vấn Đề Refresh/Update

### Dữ liệu không cập nhật sau khi thêm/sửa/xóa

**Nguyên nhân:**
- Cache không được invalidate
- Không refetch sau mutation

**Giải pháp:**

1. **Admin Panel - Refetch sau action:**
```typescript
const handleCreate = async () => {
  await createItem(data);
  await fetchItems(); // Refetch list
};
```

2. **Landing Page - Invalidate query:**
```typescript
const mutation = useMutation({
  onSuccess: () => {
    queryClient.invalidateQueries(['items']);
  }
});
```

---

## 🖼️ Vấn Đề Upload File/Image

### Lỗi: "File upload failed" hoặc ảnh không hiển thị

**Nguyên nhân:**
- FormData không đúng format
- Backend không xử lý multipart/form-data
- Path ảnh không đúng

**Giải pháp:**

1. **Kiểm tra FormData:**
```typescript
const formData = new FormData();
formData.append('image', file);
formData.append('name', name);
```

2. **Kiểm tra Content-Type:**
```typescript
// Không set Content-Type khi upload file
// Browser sẽ tự set multipart/form-data
headers: {
  'Authorization': `Bearer ${token}`
  // Không có 'Content-Type'
}
```

3. **Kiểm tra URL ảnh:**
```typescript
// Backend trả về relative path
const imageUrl = `${API_URL}${image.url}`;
```

---

## 🔍 Debug Tips

### 1. Kiểm tra Network Tab
- Mở DevTools (F12)
- Tab Network
- Xem request/response details
- Check status code, headers, payload

### 2. Kiểm tra Console
- Xem error messages
- Check API response
- Verify data structure

### 3. Test API với Postman/Thunder Client
- Import API routes
- Test từng endpoint
- Verify response format

### 4. Kiểm tra Backend Logs
```bash
cd backend
npm run dev
# Xem logs trong terminal
```

---

## 📝 Checklist Khi Gặp Lỗi API

- [ ] Backend đang chạy? (port 5000)
- [ ] URL API đúng trong .env?
- [ ] CORS được config đúng?
- [ ] Token được gửi kèm request? (nếu cần auth)
- [ ] Request payload đúng format?
- [ ] Response structure như expected?
- [ ] Network tab có lỗi gì?
- [ ] Console có error message?

---

## 🚀 Quick Fix Commands

```bash
# Restart tất cả services
cd backend && npm run dev
cd admin-panel && npm run dev
cd Laddingpage && npm run dev

# Clear cache và reinstall
rm -rf node_modules package-lock.json
npm install

# Reset database (nếu cần)
cd backend
npm run migrate:rollback
npm run migrate:latest
npm run seed:run
```

---

## 📞 Liên Hệ Support

Nếu vẫn gặp vấn đề:
1. Check file CORS_FIX_GUIDE.md
2. Check file API_DOCUMENTATION.md trong backend
3. Check file API_INTEGRATION_STATUS.md trong admin-panel
4. Tạo issue với đầy đủ thông tin: error message, screenshot, steps to reproduce
