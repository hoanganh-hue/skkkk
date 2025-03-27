# BÁO CÁO PHÂN TÍCH VÀ ĐỀ XUẤT CẤU TRÚC
# DỰ ÁN NỀN TẢNG THƯƠNG MẠI ĐIỆN TỬ TIKTOK SHOP

**Ngày báo cáo:** 27/03/2025  
**Phiên bản:** 2.0  
**Trạng thái:** Đề xuất điều chỉnh

## 1. TỔNG QUAN ĐỀ XUẤT CẤP NHẬT

Báo cáo này xác nhận và đề xuất bổ sung yêu cầu mới vào cấu trúc 4 hạng mục đã được đề xuất trước đó cho dự án TikTok Shop. Các điều chỉnh tập trung vào các tính năng thiết yếu như quản lý tiền tệ (USD), hệ thống xét duyệt sản phẩm, quản lý tài chính cho người bán, và phân loại danh mục hàng hóa chi tiết. Đồng thời, loại bỏ các tính năng livestream và feed video theo yêu cầu.

Kiến trúc microservices và công nghệ cốt lõi vẫn được giữ nguyên, tuy nhiên các dịch vụ được điều chỉnh để đáp ứng các yêu cầu nghiệp vụ mới.

## 2. XÁC NHẬN VÀ BỔ SUNG YÊU CẦU

### 2.1. Trạng thái các yêu cầu trong hệ thống

| Yêu cầu | Trạng thái | Vị trí trong hệ thống |
|---------|------------|------------------------|
| Đơn vị tiền USD | ✅ Đã có | Admin Panel > Settings > Currencies |
| Xét duyệt sản phẩm cho người bán | ✅ Đã có | Admin Panel > Products > Approvals |
| Hiển thị ví và số dư người bán | ✅ Đã có | Seller Portal > Wallet |
| Liên kết ngân hàng & rút tiền | ✅ Đã có | Seller Portal > Wallet > Bank Accounts |
| Nạp tiền vào ví | ✅ Đã bổ sung | Seller Portal > Wallet > Deposit |
| Xét duyệt rút tiền | ✅ Đã có | Admin Panel > Finance > Withdrawals |
| Danh mục hàng hóa | ✅ Đã bổ sung | Các danh mục đã được cập nhật |
| Loại bỏ livestream & feed video | ✅ Đã thực hiện | Các tính năng này đã được loại bỏ |

### 2.2. Cấu hình tiền tệ USD

Hệ thống được thiết lập mặc định sử dụng USD làm đơn vị tiền tệ chính, với khả năng:
- Quản trị viên có thể thay đổi đơn vị tiền tệ mặc định trong Admin Panel
- Hệ thống lưu trữ tỷ giá chuyển đổi giữa USD và các đơn vị tiền tệ khác
- Người dùng có thể chọn xem giá sản phẩm theo đơn vị tiền tệ khác nhau
- Các báo cáo tài chính có thể hiển thị theo USD hoặc tiền tệ địa phương

## 3. CẤU TRÚC 4 HẠNG MỤC ĐIỀU CHỈNH

### 3.1. KHÁCH HÀNG - GIAO DIỆN NGƯỜI DÙNG

#### 3.1.1. Giao diện màn hình chính
- **Danh mục sản phẩm**: Hiển thị theo cấu trúc danh mục đã cập nhật
- **Tìm kiếm**: Tìm theo tên, mô tả, danh mục, thương hiệu
- **Sản phẩm nổi bật**: Các sản phẩm khuyến mãi, bán chạy

#### 3.1.2. Danh mục hàng hóa chính
1. **Điện tử tiêu dùng**
   - Điện thoại thông minh và phụ kiện
   - Thiết bị đeo thông minh
   - Tai nghe và âm thanh
   - Laptop và máy tính bảng
   - Phụ kiện máy tính
   - Thiết bị gia dụng thông minh

2. **Thời trang và Phụ kiện**
   - Quần áo nữ
   - Quần áo nam
   - Giày dép
   - Túi xách và ví
   - Phụ kiện thời trang
   - Thời trang trẻ em

3. **Sức khỏe và Sắc đẹp**
   - Chăm sóc da mặt
   - Trang điểm
   - Chăm sóc tóc
   - Sản phẩm chăm sóc cơ thể
   - Thực phẩm chức năng
   - Nước hoa

4. **Nhà cửa và Đời sống**
   - Đồ dùng nhà bếp
   - Đồ trang trí nhà
   - Nội thất
   - Thiết bị gia dụng
   - Đồ dùng làm vườn

5. **Mẹ và Bé / Thú cưng**
   - Đồ dùng cho trẻ sơ sinh
   - Đồ chơi các loại
   - Thức ăn và phụ kiện thú cưng

6. **Thể thao, Giải trí và Sách**
   - Đồ dùng thể thao
   - Phụ kiện ô tô và xe máy
   - Sách và văn phòng phẩm

#### 3.1.3. Đăng ký và đăng nhập
- **Đăng ký tài khoản**: Form đăng ký, xác minh email/số điện thoại
- **Đăng nhập**: Username/password, social login, bảo mật hai lớp
- **Mã giới thiệu**: Nhập mã giới thiệu khi đăng ký (nếu có)

#### 3.1.4. Giỏ hàng và thanh toán
- **Quản lý giỏ hàng**: Thêm/xóa sản phẩm, cập nhật số lượng
- **Thanh toán**: Chọn phương thức thanh toán, địa chỉ giao hàng
- **Hiển thị giá**: Theo đơn vị tiền tệ USD mặc định hoặc tiền tệ người dùng chọn

#### 3.1.5. Trang thông tin cá nhân
- **Hồ sơ người dùng**: Thông tin cá nhân, quản lý địa chỉ
- **Lịch sử đơn hàng**: Xem đơn hàng, theo dõi trạng thái
- **Sản phẩm yêu thích**: Danh sách đã lưu/thích
- **Đánh giá sản phẩm**: Quản lý đánh giá đã viết

### 3.2. NHÀ BÁN HÀNG - CỔNG THÔNG TIN NGƯỜI BÁN

#### 3.2.1. Đăng nhập và quản lý thông tin
- **Đăng nhập**: Xác thực riêng cho người bán
- **Thiết lập hồ sơ**: Thông tin cửa hàng, logo, banner
- **Xác minh tài khoản**: Quy trình KYC, xác minh danh tính

#### 3.2.2. Quản lý sản phẩm
- **Tạo sản phẩm mới**: Form nhập thông tin chi tiết, tải ảnh
- **Chọn danh mục**: Danh mục và phân loại theo cấu trúc đã cập nhật
- **Quản lý tồn kho**: Cập nhật số lượng, biến thể
- **Trạng thái phê duyệt**: Xem trạng thái duyệt sản phẩm, nhận thông báo
- **Nhận thông báo**: Khi sản phẩm được phê duyệt hoặc từ chối kèm lý do

#### 3.2.3. Quản lý đơn hàng
- **Danh sách đơn hàng**: Lọc theo trạng thái, thời gian
- **Xử lý đơn**: Xác nhận, đóng gói, giao hàng
- **Trả hàng/hoàn tiền**: Quy trình xử lý
- **In vận đơn**: Tạo và in vận đơn giao hàng

#### 3.2.4. Ví điện tử và tài chính
- **Xem số dư và giao dịch**: Hiển thị bằng USD và tiền tệ địa phương nếu cần
- **Liên kết tài khoản ngân hàng**: Thêm, xóa, cập nhật tài khoản ngân hàng
- **Yêu cầu rút tiền**: Chọn tài khoản, nhập số tiền, theo dõi trạng thái duyệt
- **Nạp tiền**: Nạp tiền vào ví từ thẻ tín dụng, chuyển khoản ngân hàng
- **Báo cáo tài chính**: Doanh số, xu hướng, phân tích theo thời gian

#### 3.2.5. Báo cáo và phân tích
- **Báo cáo bán hàng**: Doanh số theo sản phẩm, danh mục
- **Hiệu quả kinh doanh**: Tỷ lệ chuyển đổi, giá trị đơn hàng trung bình
- **Phân tích khách hàng**: Địa lý, độ tuổi, hành vi mua

### 3.3. HẬU ĐÀI QUẢN TRỊ - DÀNH CHO NGƯỜI SÁNG LẬP & ĐỘI NGŨ VẬN HÀNH

#### 3.3.1. Quản lý người dùng và nhà bán hàng
- **Danh sách người dùng**: Tìm kiếm, lọc, xem chi tiết
- **Danh sách người bán**: Tìm kiếm, lọc, xem chi tiết
- **Hành động quản trị**: Khóa/mở tài khoản, cảnh báo

#### 3.3.2. Xét duyệt sản phẩm
- **Danh sách chờ duyệt**: Sắp xếp theo thời gian, người bán
- **Quy trình xét duyệt**: Xem chi tiết sản phẩm, phê duyệt/từ chối
- **Lý do từ chối**: Template phản hồi, ghi chú
- **Kiểm tra nội dung**: Đảm bảo tuân thủ quy định nền tảng
- **Lưu trữ lịch sử**: Ghi nhận ai duyệt/từ chối và thời gian

#### 3.3.3. Quản lý danh mục
- **Cấu trúc danh mục**: Quản lý cây danh mục sản phẩm đã cập nhật
- **Thuộc tính danh mục**: Thiết lập thuộc tính bắt buộc cho từng danh mục
- **Quy tắc danh mục**: Thiết lập quy tắc xét duyệt theo từng danh mục

#### 3.3.4. Quản lý tài chính
- **Xét duyệt rút tiền**: Danh sách yêu cầu, xem chi tiết tài khoản
- **Điều chỉnh số dư**: Thêm/trừ tiền trong ví người bán
- **Báo cáo tài chính**: Doanh thu nền tảng, phí giao dịch
- **Xét duyệt nạp tiền**: Xác nhận các giao dịch nạp tiền thủ công
- **Quản lý tỷ giá hối đoái**: Cập nhật tỷ giá giữa USD và các tiền tệ khác

#### 3.3.5. Hệ thống mã giới thiệu
- **Tạo mã giới thiệu**: Gán cho nhân viên, cộng tác viên
- **Thiết lập hoa hồng**: Tỷ lệ % trên đơn hàng
- **Báo cáo hiệu quả**: Số lượng đăng ký, đơn hàng, doanh thu qua mã

#### 3.3.6. Cài đặt hệ thống
- **Quản lý tiền tệ**: USD là tiền tệ mặc định, cấu hình các đơn vị khác
- **Phân quyền**: Vai trò, quyền hạn cho nhân viên vận hành
- **Cấu hình chung**: Giao diện, thông báo, nội dung tĩnh

### 3.4. HẠ TẦNG VÀ KIẾN TRÚC KỸ THUẬT

#### 3.4.1. Kiến trúc tổng thể
- **Tổng quan microservices**: Mô hình các dịch vụ đã điều chỉnh
- **Luồng dữ liệu**: Cách các dịch vụ giao tiếp, xử lý dữ liệu
- **Công nghệ sử dụng**: NestJS, Next.js, Flutter, gRPC, Kafka

#### 3.4.2. Cơ sở dữ liệu và tích hợp
- **Schema database**: Cấu trúc DB cho từng dịch vụ
- **Phân vùng dữ liệu**: Chiến lược database-per-service
- **Cache và hiệu năng**: Redis, distributed caching

#### 3.4.3. Triển khai và vận hành
- **Môi trường phát triển**: Docker Compose, local setup
- **CI/CD**: Pipeline xây dựng và triển khai
- **Kubernetes**: Helm charts, deployment patterns

#### 3.4.4. Bảo mật và hiệu năng
- **Xác thực và phân quyền**: JWT, RBAC
- **Monitoring và logging**: Tracing, metrics
- **Storage và backup**: Quản lý dữ liệu và sao lưu

## 4. CẤU TRÚC THƯ MỤC ĐỀ XUẤT CẬP NHẬT

```plaintext
tiktoksshopp.com/
├── frontend/
│   ├── customer-web/           # Next.js - Giao diện khách hàng
│   │   ├── pages/
│   │   │   ├── index.tsx       # Trang chủ (hiển thị danh mục)
│   │   │   ├── product/
│   │   │   ├── category/       # Trang danh mục sản phẩm
│   │   │   ├── auth/
│   │   │   ├── cart/
│   │   │   └── profile/
│   │   └── ...
│   ├── seller-portal/          # Next.js - Cổng thông tin người bán
│   │   ├── pages/
│   │   │   ├── index.tsx       # Dashboard người bán
│   │   │   ├── products/
│   │   │   │   ├── index.tsx   # Danh sách sản phẩm
│   │   │   │   ├── new.tsx     # Tạo sản phẩm mới
│   │   │   │   └── [id]/       # Chi tiết sản phẩm
│   │   │   ├── orders/
│   │   │   └── wallet/
│   │   │       ├── index.tsx   # Tổng quan ví
│   │   │       ├── bank-accounts.tsx # Quản lý tài khoản ngân hàng
│   │   │       ├── withdraw.tsx # Rút tiền
│   │   │       └── deposit.tsx  # Nạp tiền
│   │   └── ...
│   ├── admin-panel/            # Next.js - Hậu đài quản trị
│   │   ├── pages/
│   │   │   ├── index.tsx       # Dashboard quản trị
│   │   │   ├── users/
│   │   │   ├── sellers/
│   │   │   ├── products/
│   │   │   │   ├── index.tsx   # Quản lý sản phẩm
│   │   │   │   └── approvals/  # Xét duyệt sản phẩm
│   │   │   ├── categories/     # Quản lý danh mục
│   │   │   ├── finance/
│   │   │   │   ├── index.tsx   # Tổng quan tài chính
│   │   │   │   ├── withdrawals/ # Xét duyệt rút tiền
│   │   │   │   └── deposits/    # Xét duyệt nạp tiền
│   │   │   ├── referrals/      # Quản lý mã giới thiệu
│   │   │   └── settings/
│   │   │       └── currencies.tsx # Cài đặt tiền tệ (USD mặc định)
│   │   └── ...
│   └── mobile-app/             # Flutter - Ứng dụng di động
├── backend/
│   ├── apps/                   # NestJS Monorepo
│   │   ├── api-gateway/
│   │   ├── admin-gateway/
│   │   ├── user-service/
│   │   ├── product-service/    # Đã cập nhật với trạng thái duyệt
│   │   ├── category-service/   # Dịch vụ quản lý danh mục mới
│   │   ├── cart-service/
│   │   ├── order-service/
│   │   ├── payment-service/
│   │   ├── admin-service/
│   │   ├── approval-service/   # Dịch vụ xét duyệt sản phẩm
│   │   ├── finance-service/    # Dịch vụ tài chính (ví, rút tiền, nạp tiền)
│   │   └── referral-service/
│   └── ...
└── deployment/
    ├── docker-compose.yml
    └── kubernetes/
```

## 5. CÁC ĐIỂM ĐIỀU CHỈNH CHỦ YẾU

### 5.1. Điều chỉnh về nội dung

1. **Loại bỏ livestream và feed video**:
   - Đã loại bỏ dịch vụ `livestream-service` và `feed-service`
   - Đã loại bỏ các component UI liên quan đến livestream và feed video
   - Tập trung vào trải nghiệm mua sắm thương mại điện tử truyền thống

2. **Bổ sung quản lý danh mục chi tiết**:
   - Thêm `category-service` với cấu trúc danh mục đa cấp
   - Cấu trúc danh mục được phân loại theo 6 nhóm chính với các danh mục con
   - Hỗ trợ thuộc tính đặc thù cho từng danh mục

3. **Tăng cường tính năng tài chính**:
   - Bổ sung chi tiết về nạp tiền vào ví
   - Chi tiết hơn về quy trình xét duyệt rút tiền
   - Xác nhận USD là đơn vị tiền tệ mặc định

### 5.2. Điều chỉnh về kỹ thuật

1. **Cập nhật product-service**:
   - Thêm trường cho trạng thái duyệt: isApproved, approvedBy, approvedAt
   - Thêm trường lý do từ chối: rejectionReason, rejectedBy, rejectedAt

2. **Cập nhật finance-service**:
   - Bổ sung endpoint cho nạp tiền: /deposit
   - Bổ sung luồng xử lý nạp tiền tự động và thủ công
   - Tích hợp với hệ thống thanh toán để nạp tiền tự động

3. **Cập nhật schemas database**:
   - Thêm bảng danh mục chi tiết
   - Thêm bảng giao dịch nạp tiền
   - Cập nhật quan hệ giữa sản phẩm và danh mục

## 6. KẾT LUẬN

Với các điều chỉnh này, hệ thống TikTok Shop sẽ tập trung vào mô hình thương mại điện tử truyền thống thay vì kết hợp với nền tảng video. Các tính năng tài chính, đặc biệt là quản lý ví điện tử (hiển thị số dư, nạp tiền, rút tiền) cùng với hệ thống xét duyệt sản phẩm đã được thiết kế chi tiết để đáp ứng yêu cầu.

Hệ thống sử dụng USD làm đơn vị tiền tệ mặc định và cung cấp khả năng quản lý danh mục sản phẩm chi tiết theo cấu trúc đã được đề xuất. Tất cả các thay đổi này đã được tích hợp vào cấu trúc 4 hạng mục chính, giúp dễ dàng tiếp cận và triển khai dự án.

Các microservices cốt lõi và công nghệ nền tảng vẫn được giữ nguyên, chỉ điều chỉnh và bổ sung các dịch vụ cần thiết để hỗ trợ các tính năng mới. Dự án có thể được triển khai theo từng giai đoạn, bắt đầu với các chức năng cơ bản và mở rộng dần theo nhu cầu kinh doanh.