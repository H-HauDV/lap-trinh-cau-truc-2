## Install instruction:
-Step 1: Run the following command to create application.
* Create a new app:
```
composer create-project laravel/laravel example-app </br>
```
* Install breeze (A laravel authentication template)
```
composer require laravel/breeze --dev </br>
php artisan breeze:install </br>
```
* Install and compile npm
```
npm install </br>
npm run dev </br>
```
-Step 2: Create database with xampp.
* Create database in xampp with name lap_trinh_cau_truc_2
* In file .env, rename database DB_DATABASE=lap_trinh_cau_truc_2
* Migrate database
```
php artisan migrate </br>
```
* Start local server
```
php artisan serve </br>
```

-Step 3: Config mail information to test with send confirm mail function.
* Access https://mailtrap.io/ to get fake mail information and then write to .env file</br>
* Example: </br>
```
MAIL_MAILER=smtp </br>
MAIL_HOST=smtp.mailtrap.io </br>
MAIL_PORT=2525 </br>
MAIL_USERNAME=5bd9c4164e097b </br>
MAIL_PASSWORD=5b851cd8e31a77 </br>
MAIL_ENCRYPTION=tls </br>
MAIL_FROM_ADDRESS=noreply@example.com </br>
MAIL_FROM_NAME="${APP_NAME}" </br>
```
-Step 4: Config .env file to enable mail confirmation checking.
* To enable mail verification, in models/user.php replace
```
class User extends Authenticatable
```
with
```
class User extends Authenticatable implements MustVerifyEmail</br>
```
* To redirect every time user register, in routes/web.php replace
```
middleware(['auth'])->name('dashboard');
```
with
```
middleware(['auth','verified'])->name('dashboard')</br>
```
## API list:
* GET: api/register
* POST: api/register
* GET: api/login
* POST: api/login
* GET: api/forgot-password
* POST: api/forgot-password
* GET: api/reset-password/{token}
* POST: api/reset-password
* GET: api/verify-email
* GET: api/verify-email/{id}/{hash}
* POST: api/email/verification-notification
* GET: api/confirm-password
* POST: api/confirm-password
* GET: api/logout
