# Login API bo'yicha qilingan ishlar

Loyihaga login va current user uchun API qo'shdim. Token uchun Simple JWT ishlatdim.

## Endpointlar

POST /api/auth/login/ - username va password yuboriladi, to'g'ri bo'lsa access, refresh token va user ma'lumotlari qaytadi.

GET /api/auth/me/ - login qilgan userning id, username va email'ini qaytaradi. Header'da `Authorization: Bearer <access>` bo'lishi kerak, bo'lmasa 401 qaytadi.

POST /api/auth/token/refresh/ - access token muddati tugaganda refresh token orqali yangisini olish uchun qo'shib qo'ydim.

## Qaysi fayllar o'zgardi

accounts/ - yangi app ochdim, auth bilan bog'liq hamma narsa shu yerda.

- serializers.py - LoginSerializer username va password'ni tekshiradi.
- views.py - LoginView token yaratib beradi, CurrentUserView esa faqat token bilan kirgan userga ishlaydi.
- urls.py - yuqoridagi uchta endpoint.

config/settings.py - rest_framework, simplejwt va accounts'ni INSTALLED_APPS'ga qoshdim, default authentication qilib JWT'ni qo'ydim. Access token 30 daqiqa, refresh token 7 kun ishlaydi. Baza PostgreSQL, parol va secret key `.env` fayldan olinadi.

config/urls.py - `api/auth/` ni accounts.urls'ga ulab qoydim

requirements.txt - djangorestframework-simplejwt qo'shildi.

.env.example - qaysi o'zgaruvchilar kerakligi ko'rsatilgan. Haqiqiy `.env` gitga qo'shilmagan.

User modeli o'zgarmadi, Django'ning tayyor User modelidan foydalandim. Shuning uchun yangi migratsiya ham yo'q.

## Xatoliklar

- Username yoki password bo'sh bo'lsa 400 qaytadi va qaysi maydon bo'shligi yoziladi.
- Password noto'g'ri bo'lsa yoki bunday username bo'lmasa 401 qaytadi. Ikkala holatda ham xabar bir xil: "Invalid username or password." Buni ataylab shunday qildim, aks holda bazada qaysi username borligini bilib olish mumkin bo'lardi.
- Tokensiz yoki noto'g'ri token bilan /me/ ga kirilsa 401 qaytadi.

## Tekshirish

Postman orqali tekshirdim:

1. To'g'ri login va password - 200
2. Noto'g'ri password - 401
3. Mavjud bo'lmagan username - 401
4. Bo'sh maydonlar - 400
5. Tokensiz /me/ - 401
6. Token bilan /me/ - 200

Screenshotlar Pull Request'da.

## Ishga tushirish

README.md da yozilgan. Qisqasi: `.env.example` dan `.env` yaratib DB parolini yozish, `bookstore` bazasini ochish, keyin `migrate` va `runserver`.
