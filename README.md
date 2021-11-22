composer create-project laravel/laravel example-app
composer require laravel/breeze --dev
php artisan breeze:install
npm install
npm run dev
php artisan migrate
php artisan serve

tạo database trong xampp, php admin vd: lap_tring_cau_truc_3, trong file .env đổi tên DB_DATABASE=lap_trinh_cau_truc_3 

vào https://mailtrap.io/ để lấy các thông tin cần thiết ghi vào file env
vd:
MAIL_MAILER=smtp
MAIL_HOST=smtp.mailtrap.io
MAIL_PORT=2525
MAIL_USERNAME=5bd9c4164e097b
MAIL_PASSWORD=5b851cd8e31a77
MAIL_ENCRYPTION=tls
MAIL_FROM_ADDRESS=noreply@example.com
MAIL_FROM_NAME="${APP_NAME}"

trong models/user.php thay dòng"class User extends Authenticatable" thành "class User extends Authenticatable implements MustVerifyEmail" (để có thể bật xác thực mail)
trong routes/web.php thay dòng "middleware(['auth'])->name('dashboard');" thành "middleware(['auth','verified'])->name('dashboard');" (để đổi hướng mỗi khi đăng ký sẽ chuyển sang trang yêu cầu xác thực email)

