<div class="" align="center">
    <p> Progressive web app </p>
    <h1>DJANGO PWA</h1>
    <span>✨⭐⭐⭐✨</span>
    <hr>
    <img src="gambar/gambar (1).png"/>
    <br>
</div>

## INSTALASI and Setup

- 📁&nbsp;&nbsp;buat project django
```bash
django-admin startproject tutorial
```

- 📁&nbsp;&nbsp;buat app django
```bash
django-admin startapp djangopwa
```

- 📁&nbsp;&nbsp;register app dan pwa
```bash
pip install django_pwa
```
<img src="gambar/gambar (2).png"/>
- setup template
<img src="gambar/gambar (3).png"/>
-setup static
<img src="gambar/gambar 3 (1).png"/>
<img src="gambar/gambar 3 (2).png"/>


- 📁&nbsp;&nbsp;register url pwa di urls project
```bash
path('', include('pwa.urls'))
```
<img src="gambar/gambar (4).png"/>


- 📁&nbsp;&nbsp;buat folder js didalam static kemudian didalm folder js tersebut buat file serviceworker.js
```bash
var staticCacheName = 'djangopwa-v1';

self.addEventListener('install', function(event) {
event.waitUntil(
	caches.open(staticCacheName).then(function(cache) {
	return cache.addAll([
		'',
	]);
	})
);
});

self.addEventListener('fetch', function(event) {
var requestUrl = new URL(event.request.url);
	if (requestUrl.origin === location.origin) {
	if ((requestUrl.pathname === '/')) {
		event.respondWith(caches.match(''));
		return;
	}
	}
	event.respondWith(
	caches.match(event.request).then(function(response) {
		return response || fetch(event.request);
	})
	);
});
```
<img src="gambar/gambar (5).png"/>


- 📁&nbsp;&nbsp;tambahkan kode berikut di settings.py
```bash
PWA_SERVICE_WORKER_PATH = os.path.join(BASE_DIR, 'static/js', 'serviceworker.js')
```
<img src="gambar/gambar (6).png"/>


- 📁&nbsp;&nbsp;tambahkan kode berikut di settings.py nanti secara otomtis ketika menjalankan kode akan dibuatkan file manifest.json
```bash

PWA_APP_NAME = 'djangoPWA'
PWA_APP_DESCRIPTION = "GeeksForGeeks PWA"
PWA_APP_THEME_COLOR = '#000000'
PWA_APP_BACKGROUND_COLOR = '#ffffff'
PWA_APP_DISPLAY = 'standalone'
PWA_APP_SCOPE = '/'
PWA_APP_ORIENTATION = 'any'
PWA_APP_START_URL = '/'
PWA_APP_STATUS_BAR_COLOR = 'default'
PWA_APP_ICONS = [
	{
		'src': 'static/images/logo.png', #ganti dengan alamat icon/logo/gambar yang ada di folder static
		'sizes': '160x160'
	}
]
PWA_APP_ICONS_APPLE = [
	{
		'src': 'static/images/logo.png', #ganti dengan alamat icon/logo/gambar yang ada di folder static
		'sizes': '160x160'
	}
]
PWA_APP_SPLASH_SCREEN = [
	{
		'src': 'static/images/logo.png', #ganti dengan alamat icon/logo/gambar yang ada di folder static
		'media': '(device-width: 320px) and (device-height: 568px) and (-webkit-device-pixel-ratio: 2)'
	}
]
PWA_APP_DIR = 'ltr'
PWA_APP_LANG = 'en-US'

```
<img src="gambar/gambar (7).png"/>


- 📁&nbsp;&nbsp;tambahakan kode bberikut dibawah tag pembuka html
```bash
{% load pwa %}
{% progressive_web_app_meta %}
```
<img src="gambar/gambar (8).png"/>



- 📁&nbsp;&nbsp;Run Server
```bash
python manage.py runserver
```