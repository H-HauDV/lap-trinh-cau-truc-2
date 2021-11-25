## Install instruction:
-Step 1: Run the following command to create application.
* Create a new app:
```
composer create-project laravel/laravel example-app
```
* Install breeze (A laravel authentication template)
```
composer require laravel/breeze --dev 
php artisan breeze:install 
```
* Install and compile npm
```
npm install 
npm run dev
```
-Step 2: Create database with xampp.
* Create database in xampp with name lap_trinh_cau_truc_2
* In file .env, rename database DB_DATABASE=lap_trinh_cau_truc_2
* Migrate database
```
php artisan migrate 
```
* Start local server
```
php artisan serve 
```

-Step 3: Config mail information to test with send confirm mail function.
* Access https://mailtrap.io/ to get fake mail information and then write to .env file
* Example: 
```
MAIL_MAILER=smtp 
MAIL_HOST=smtp.mailtrap.io 
MAIL_PORT=2525 
MAIL_USERNAME=5bd9c4164e097b 
MAIL_PASSWORD=5b851cd8e31a77 
MAIL_ENCRYPTION=tls
MAIL_FROM_ADDRESS=noreply@example.com 
MAIL_FROM_NAME="${APP_NAME}" 
```
-Step 4: Config .env file to enable mail confirmation checking.
* To enable mail verification, in models/user.php replace
```
class User extends Authenticatable
```
with
```
class User extends Authenticatable implements MustVerifyEmail
```
* To redirect every time user register, in routes/web.php replace
```
middleware(['auth'])->name('dashboard');
```
with
```
middleware(['auth','verified'])->name('dashboard')
```
-Example of .env file [.env](https://drive.google.com/file/d/14eKNtkmTM5LNaXm7y9oXdV2JeH_d_ZCp/view?usp=sharing).
-Example of database file [database](https://drive.google.com/file/d/1oZjhCX7NdZ9eLwGpCCHKcVaE7oFBy1gj/view?usp=sharing).
## API list:
1. API for register
* GET: api/register
* POST: api/register
2. API for login
* GET: api/login
* POST: api/login
3. API for forget password
* GET: api/forgot-password
* POST: api/forgot-password
4. API for reset password
* GET: api/reset-password/{token}
* POST: api/reset-password
5. API for verify email
* GET: api/verify-email
* GET: api/verify-email/{id}/{hash}
6. API for send verification noftification
* POST: api/email/verification-notification
7. API for password confirmation
* GET: api/confirm-password
* POST: api/confirm-password
8. API for logout
* GET: api/logout
