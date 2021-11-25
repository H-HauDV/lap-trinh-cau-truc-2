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

------------------------------+----------------------------------------------------+
| Domain | Method   | URI                             | Name                | Action
                              | Middleware                                         |
+--------+----------+---------------------------------+---------------------+-------------------------------------------------------------------------+----------------------------------------------------+
|        | GET|HEAD | /                               |                     | Closure                                                                 | web                                                |
|        | GET|HEAD | api/user                        |                     | Closure                                                                 | api                                                |
|        |          |                                 |                     |                                                                         | App\Http\Middleware\Authenticate:sanctum           |
|        | GET|HEAD | confirm-password                | password.confirm    | App\Http\Controllers\Auth\ConfirmablePasswordController@show            | web                                                |
|        |          |                                 |                     |                                                                         | App\Http\Middleware\Authenticate                   |
|        | POST     | confirm-password                |                     | App\Http\Controllers\Auth\ConfirmablePasswordController@store           | web                                                |
|        |          |                                 |                     |                                                                         | App\Http\Middleware\Authenticate                   |
|        | GET|HEAD | dashboard                       | dashboard           | Closure                                                                 | web                                                |
|        |          |                                 |                     |                                                                         | App\Http\Middleware\Authenticate                   |
|        |          |                                 |                     |                                                                         | Illuminate\Auth\Middleware\EnsureEmailIsVerified   |
|        | POST     | email/verification-notification | verification.send   | App\Http\Controllers\Auth\EmailVerificationNotificationController@store | web                                                |
|        |          |                                 |                     |
                              | App\Http\Middleware\Authenticate                   |
|        |          |                                 |                     |
                              | Illuminate\Routing\Middleware\ThrottleRequests:6,1 |
|        | GET|HEAD | forgot-password                 | password.request    | App\Http\Controllers\Auth\PasswordResetLinkController@create            | web                                                |
|        |          |                                 |                     |
                              | App\Http\Middleware\RedirectIfAuthenticated        |
|        | POST     | forgot-password                 | password.email      | App\Http\Controllers\Auth\PasswordResetLinkController@store             | web                                                |
|        |          |                                 |                     |
                              | App\Http\Middleware\RedirectIfAuthenticated        |
|        | GET|HEAD | login                           | login               | App\Http\Controllers\Auth\AuthenticatedSessionController@create         | web                                                |
|        |          |                                 |                     |
                              | App\Http\Middleware\RedirectIfAuthenticated        |
|        | POST     | login                           |                     | App\Http\Controllers\Auth\AuthenticatedSessionController@store          | web                                                |
|        |          |                                 |                     |
                              | App\Http\Middleware\RedirectIfAuthenticated        |
|        | POST     | logout                          | logout              | App\Http\Controllers\Auth\AuthenticatedSessionController@destroy        | web                                                |
|        |          |                                 |                     |
                              | App\Http\Middleware\Authenticate                   |
|        | GET|HEAD | register                        | register            | App\Http\Controllers\Auth\RegisteredUserController@create               | web                                                |
|        |          |                                 |                     |
                              | App\Http\Middleware\RedirectIfAuthenticated        |
|        | POST     | register                        |                     | App\Http\Controllers\Auth\RegisteredUserController@store                | web                                                |
|        |          |                                 |                     |
                              | App\Http\Middleware\RedirectIfAuthenticated        |
|        | POST     | reset-password                  | password.update     | App\Http\Controllers\Auth\NewPasswordController@store                   | web                                                |
|        |          |                                 |                     |
                              | App\Http\Middleware\RedirectIfAuthenticated        |
|        | GET|HEAD | reset-password/{token}          | password.reset      | App\Http\Controllers\Auth\NewPasswordController@create                  | web                                                |
|        |          |                                 |                     |
                              | App\Http\Middleware\RedirectIfAuthenticated        |
|        | GET|HEAD | sanctum/csrf-cookie             |                     | Laravel\Sanctum\Http\Controllers\CsrfCookieController@show              | web                                                |
|        | GET|HEAD | verify-email                    | verification.notice | App\Http\Controllers\Auth\EmailVerificationPromptController@__invoke    | web                                                |
|        |          |                                 |                     |
                              | App\Http\Middleware\Authenticate                   |
|        | GET|HEAD | verify-email/{id}/{hash}        | verification.verify | App\Http\Controllers\Auth\VerifyEmailController@__invoke                | web                                                |
|        |          |                                 |                     |
                              | App\Http\Middleware\Authenticate                   |
|        |          |                                 |                     |
                              | Illuminate\Routing\Middleware\ValidateSignature    |
|        |          |                                 |                     |
                              | Illuminate\Routing\Middleware\ThrottleRequests:6,1 |
+--------+----------+---------------------------------+---------------------+-------------------------------------------