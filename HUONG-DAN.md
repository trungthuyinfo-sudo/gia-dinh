# Sổ Thu Chi Gia Đình — bản thử nghiệm 1.0

Đây là **mã nguồn ứng dụng web**, chưa phải ứng dụng đã xuất bản và chưa phải file cài iOS. Cần kết nối Firebase và đưa các tệp lên dịch vụ HTTPS. Không gửi mật khẩu cho người khác.

## Bước 1 — Tạo Firebase

1. Mở https://console.firebase.google.com/ và tạo project.
2. Trong Project settings → Your apps, thêm Web app (`</>`), sao chép cấu hình `firebaseConfig`.
3. Sửa **firebase-config.js**: thay `REPLACE_ME` bằng `apiKey`, `authDomain`, `projectId`, `appId` từ Firebase. Không dùng private key/service account.
4. Authentication → Sign-in method: bật **Email/Password** và **Google**.
5. Authentication → Settings → Authorized domains: thêm miền website sẽ xuất bản (ví dụ `tenban.github.io`).
6. Firestore Database → Create database. Trong mục **Rules**, dán nội dung tệp `firestore.rules` và nhấn **Publish**. **Không** dùng luật `allow read, write: if true`.

## Bước 2 — Xuất bản GitHub Pages

1. Truy cập https://github.com/ tạo tài khoản, tạo repository **public** tên `so-thu-chi-gia-dinh`.
2. Upload các tệp trong thư mục này (không upload nguyên tệp ZIP).
3. Vào repository → Settings → Pages → Build and deployment → Deploy from a branch → `main` / `(root)` → Save.
4. Đợi xuất bản, mở địa chỉ `https://TEN-TAI-KHOAN.github.io/so-thu-chi-gia-dinh/`.
5. Nếu đăng nhập Google dạng popup bị chặn trên Safari, hãy dùng đăng nhập email/mật khẩu; đăng nhập chuyển hướng qua Firebase có thể cần cấu hình bổ sung cho trình duyệt chặn third-party storage.

## Bước 3 — Dùng trên hai iPhone

1. Mỗi người đăng ký tài khoản riêng bằng email/mật khẩu hoặc Google.
2. Người thứ nhất vào **Cài đặt → Tạo sổ gia đình mới**.
3. Người thứ nhất nhấn **Sao chép mã mời của sổ**, gửi riêng cho người thứ hai.
4. Người thứ hai đăng nhập → Cài đặt → dán mã → **Tham gia sổ gia đình**.
5. Trên iPhone mở website bằng Safari → Chia sẻ → **Thêm vào Màn hình chính**.

## Cách tính

- Số dư = tiền mặt đầu kỳ + ngân hàng đầu kỳ + thu - chi + tiền gốc đi vay - tiền gốc cho vay + tiền gốc thu hồi cho vay - tiền gốc trả nợ.
- Chuyển tiền mặt ↔ ngân hàng không thay đổi tổng số dư.
- Khoản vay và trả gốc không được tính là thu nhập hoặc chi tiêu sinh hoạt.
- Chức năng trả nợ hiện chỉ ghi nhận **tiền gốc**; lãi vay chưa hỗ trợ.
- Số dư đầu kỳ là tổng tiền ở thời điểm bắt đầu ghi sổ, **không bao gồm** các giao dịch nhập lại sau đó.

## Giới hạn bản thử nghiệm

- Chưa có thông báo đẩy, Face ID, nhập khoản lãi vay, sửa giao dịch trực tiếp, sao lưu toàn bộ dữ liệu (mới xuất CSV giao dịch), lịch sử kiểm toán xóa, hoặc bảo đảm dùng ngoại tuyến.
- Chức năng **xóa** giao dịch/khoản vay không thể hoàn tác; hai người đều có quyền xóa. Nên xuất CSV định kỳ.
- Mã mời là bí mật cho phép gia nhập sổ; chỉ gửi cho người thân. Quy tắc hiện giới hạn tối đa **2 thành viên**. Không có chức năng thu hồi mã mời hoặc rời sổ trong bản này.
- Dữ liệu được lưu trên Firebase của chính người tạo dự án. Cần tự kiểm tra giới hạn miễn phí, bảo mật tài khoản và sao lưu.
- Mã nguồn public không chứa mật khẩu nhưng chứa cấu hình Firebase web (được thiết kế là cấu hình công khai); bảo mật phụ thuộc vào Authentication và Firestore Rules.
- Ứng dụng là PWA/website, **không phải ứng dụng Swift cài từ App Store**. Trên iPhone 8 Plus, Safari tương thích phụ thuộc phiên bản iOS hiện có.
