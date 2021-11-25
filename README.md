Install instruction:
composer create-project laravel/laravel example-app </br>
composer require laravel/breeze --dev </br>
php artisan breeze:install </br>
npm install </br>
npm run dev </br>
php artisan migrate </br>
php artisan serve </br>

tạo database trong xampp, php admin vd: lap_tring_cau_truc_3, trong file .env đổi tên DB_DATABASE=lap_trinh_cau_truc_3 </br>

vào https://mailtrap.io/ để lấy các thông tin cần thiết ghi vào file env </br>
vd: </br>
MAIL_MAILER=smtp </br>
MAIL_HOST=smtp.mailtrap.io </br>
MAIL_PORT=2525 </br>
MAIL_USERNAME=5bd9c4164e097b </br>
MAIL_PASSWORD=5b851cd8e31a77 </br>
MAIL_ENCRYPTION=tls </br>
MAIL_FROM_ADDRESS=noreply@example.com </br>
MAIL_FROM_NAME="${APP_NAME}" </br>

trong models/user.php thay dòng"class User extends Authenticatable" thành "class User extends Authenticatable implements MustVerifyEmail" (để có thể bật xác thực mail) </br>
trong routes/web.php thay dòng "middleware(['auth'])->name('dashboard');" thành "middleware(['auth','verified'])->name('dashboard');" (để đổi hướng mỗi khi đăng ký sẽ chuyển sang trang yêu cầu xác thực email) </br>

API list:
