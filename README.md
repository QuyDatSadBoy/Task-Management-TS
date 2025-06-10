# 📝 Task Management TypeScript

Ứng dụng quản lý công việc được xây dựng bằng TypeScript, Node.js, Express và MongoDB.

## 🌟 Demo

🔗 **Live Demo:** [https://task-management-ts-lilac.vercel.app](https://task-management-ts-lilac.vercel.app)

## 📋 Mô tả

Task Management TS là một ứng dụng API RESTful được thiết kế để quản lý công việc hiệu quả. Ứng dụng cung cấp các tính năng đầy đủ cho việc tạo, chỉnh sửa, theo dõi và quản lý trạng thái công việc với hệ thống xác thực người dùng an toàn.

## ✨ Tính năng chính

### 🔐 Xác thực người dùng
- **Đăng ký tài khoản**: Tạo tài khoản mới với email và mật khẩu
- **Đăng nhập**: Xác thực và nhận token truy cập
- **Bảo mật**: Mã hóa mật khẩu bằng MD5 và xác thực token

### 📋 Quản lý công việc
- **Tạo công việc mới**: Thêm công việc với tiêu đề, nội dung, thời gian
- **Xem danh sách công việc**: Hiển thị tất cả công việc với phân trang
- **Xem chi tiết công việc**: Thông tin đầy đủ của từng công việc
- **Chỉnh sửa công việc**: Cập nhật thông tin công việc
- **Xóa công việc**: Xóa mềm công việc (soft delete)

### 🔄 Quản lý trạng thái
- **initial**: Khởi tạo
- **doing**: Đang thực hiện
- **finish**: Hoàn thành
- **pending**: Tạm hoãn
- **notFinish**: Chưa hoàn thành

### 🔍 Tính năng nâng cao
- **Tìm kiếm**: Tìm kiếm công việc theo tiêu đề
- **Lọc**: Lọc công việc theo trạng thái
- **Sắp xếp**: Sắp xếp công việc theo các tiêu chí
- **Phân trang**: Hiển thị công việc theo trang
- **Thao tác hàng loạt**: Thay đổi trạng thái hoặc xóa nhiều công việc cùng lúc

## 🛠️ Công nghệ sử dụng

| Công nghệ | Phiên bản | Mục đích |
|-----------|-----------|----------|
| **TypeScript** | Latest | Ngôn ngữ lập trình chính |
| **Node.js** | 16+ | Runtime JavaScript |
| **Express.js** | Latest | Framework web backend |
| **MongoDB** | Latest | Cơ sở dữ liệu NoSQL |
| **Mongoose** | Latest | ODM cho MongoDB |
| **MD5** | Latest | Mã hóa mật khẩu |
| **CORS** | Latest | Xử lý Cross-Origin |
| **Body-parser** | Latest | Parse request body |
| **Dotenv** | Latest | Quản lý biến môi trường |

## 📁 Cấu trúc dự án

```
Task-Management-TS/
├── api/
│   └── v1/
│       ├── controllers/        # Controllers xử lý logic
│       │   ├── task.controller.ts
│       │   └── user.controller.ts
│       ├── middlewares/        # Middleware xác thực
│       │   └── auth.middleware.ts
│       ├── models/            # Models MongoDB
│       │   ├── task.model.ts
│       │   └── user.model.ts
│       └── routes/            # Định tuyến API
│           ├── index.route.ts
│           ├── task.route.ts
│           └── user.route.ts
├── config/
│   └── database.ts           # Cấu hình database
├── helpers/                  # Các hàm tiện ích
│   ├── generate.ts
│   ├── pagination.ts
│   └── search.ts
├── index.ts                  # File chính của ứng dụng
└── package.json
```

## 🚀 Cài đặt và chạy

### Yêu cầu hệ thống
- Node.js phiên bản 16 trở lên
- MongoDB
- npm hoặc yarn

### Các bước cài đặt

1. **Clone repository**
```bash
git clone https://github.com/QuyDatSadBoy/Task-Management-TS.git
cd Task-Management-TS
```

2. **Cài đặt dependencies**
```bash
npm install
```

3. **Tạo file môi trường**
```bash
cp .env.example .env
```

4. **Cấu hình biến môi trường**
```env
PORT=3000
MONGO_URL=mongodb://localhost:27017/task-management
```

5. **Chạy ứng dụng**
```bash
# Môi trường development
npm run dev

# Môi trường production
npm start
```

Ứng dụng sẽ chạy tại: `http://localhost:3000`

## 📚 API Documentation

### 🔐 Authentication

#### Đăng ký tài khoản
```http
POST /api/v1/users/register
Content-Type: application/json

{
  "fullName": "Nguyễn Văn A",
  "email": "user@example.com",
  "password": "123456"
}
```

#### Đăng nhập
```http
POST /api/v1/users/login
Content-Type: application/json

{
  "email": "user@example.com",
  "password": "123456"
}
```

#### Thông tin người dùng
```http
GET /api/v1/users/detail
Authorization: Bearer YOUR_TOKEN
```

### 📋 Tasks Management

#### Lấy danh sách công việc
```http
GET /api/v1/tasks?page=1&limit=10&status=doing&keyword=search
Authorization: Bearer YOUR_TOKEN
```

**Query Parameters:**
- `page`: Số trang (mặc định: 1)
- `limit`: Số lượng công việc mỗi trang (mặc định: 2)
- `status`: Lọc theo trạng thái (initial, doing, finish, pending, notFinish)
- `keyword`: Tìm kiếm theo tiêu đề
- `sortKey`: Trường sắp xếp
- `sortValue`: Chiều sắp xếp (asc, desc)

#### Tạo công việc mới
```http
POST /api/v1/tasks/create
Authorization: Bearer YOUR_TOKEN
Content-Type: application/json

{
  "title": "Hoàn thành báo cáo",
  "content": "Hoàn thành báo cáo tháng 12",
  "status": "initial",
  "timeStart": "2023-12-01T00:00:00.000Z",
  "timeFinish": "2023-12-31T23:59:59.000Z",
  "createdBy": "user_id",
  "listUsers": ["user1_id", "user2_id"]
}
```

#### Xem chi tiết công việc
```http
GET /api/v1/tasks/detail/:id
Authorization: Bearer YOUR_TOKEN
```

#### Cập nhật công việc
```http
PATCH /api/v1/tasks/edit/:id
Authorization: Bearer YOUR_TOKEN
Content-Type: application/json

{
  "title": "Tiêu đề mới",
  "content": "Nội dung mới",
  "status": "doing"
}
```

#### Thay đổi trạng thái công việc
```http
PATCH /api/v1/tasks/change-status/:id
Authorization: Bearer YOUR_TOKEN
Content-Type: application/json

{
  "status": "finish"
}
```

#### Thao tác hàng loạt
```http
PATCH /api/v1/tasks/change-multi
Authorization: Bearer YOUR_TOKEN
Content-Type: application/json

{
  "ids": ["task1_id", "task2_id"],
  "key": "status",
  "value": "finish"
}
```

#### Xóa công việc
```http
DELETE /api/v1/tasks/delete/:id
Authorization: Bearer YOUR_TOKEN
```

## 🗃️ Cấu trúc dữ liệu

### User Schema
```typescript
{
  fullName: String,      // Họ tên đầy đủ
  email: String,         // Email (unique)
  password: String,      // Mật khẩu đã mã hóa
  token: String,         // Token xác thực
  deleted: Boolean,      // Trạng thái xóa
  deletedAt: Date,       // Thời gian xóa
  createdAt: Date,       // Thời gian tạo
  updatedAt: Date        // Thời gian cập nhật
}
```

### Task Schema
```typescript
{
  title: String,         // Tiêu đề công việc
  status: String,        // Trạng thái công việc
  content: String,       // Nội dung mô tả
  timeStart: Date,       // Thời gian bắt đầu
  timeFinish: Date,      // Thời gian kết thúc
  createdBy: String,     // ID người tạo
  listUsers: Array,      // Danh sách người được giao
  taskParentId: String,  // ID công việc cha
  deleted: Boolean,      // Trạng thái xóa
  deletedAt: Date,       // Thời gian xóa
  createdAt: Date,       // Thời gian tạo
  updatedAt: Date        // Thời gian cập nhật
}
```

## 🔒 Bảo mật

- **Mã hóa mật khẩu**: Sử dụng MD5 để mã hóa mật khẩu
- **Token Authentication**: Xác thực bằng token cho các API
- **CORS**: Cấu hình CORS để bảo mật cross-origin requests
- **Middleware Authentication**: Kiểm tra quyền truy cập cho các route protected

## 🧪 Testing

```bash
# Chạy tests
npm test

# Chạy tests với coverage
npm run test:coverage
```

## 📝 Scripts

```bash
npm run dev      # Chạy môi trường development với nodemon
npm start        # Chạy môi trường production
npm run build    # Build TypeScript sang JavaScript
npm test         # Chạy unit tests
npm run lint     # Kiểm tra code style
```

## 🚀 Deployment

### Vercel (Production)
Ứng dụng hiện tại được deploy trên Vercel: [https://task-management-ts-lilac.vercel.app](https://task-management-ts-lilac.vercel.app)

### Manual Deployment
1. Build ứng dụng: `npm run build`
2. Upload lên server
3. Cài đặt dependencies: `npm install --production`
4. Cấu hình biến môi trường
5. Chạy: `npm start`

## 🤝 Đóng góp

1. Fork repository
2. Tạo feature branch: `git checkout -b feature/AmazingFeature`
3. Commit changes: `git commit -m 'Add some AmazingFeature'`
4. Push to branch: `git push origin feature/AmazingFeature`
5. Tạo Pull Request

## 📄 License

Dự án này được phân phối dưới giấy phép MIT. Xem file `LICENSE` để biết thêm chi tiết.

## 👨‍💻 Tác giả

**QuyDatSadBoy**
- GitHub: [@QuyDatSadBoy](https://github.com/QuyDatSadBoy)
- Project Link: [https://github.com/QuyDatSadBoy/Task-Management-TS](https://github.com/QuyDatSadBoy/Task-Management-TS)

## 📞 Liên hệ

Nếu bạn có câu hỏi hoặc đề xuất, vui lòng tạo issue trên GitHub hoặc liên hệ trực tiếp.

---

⭐ **Nếu dự án này hữu ích, hãy cho một star để ủng hộ!** ⭐
