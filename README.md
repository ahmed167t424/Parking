<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="theme-color" content="#2E86AB">
    <meta name="description" content="تطبيق حجز مواقف السيارات">
    <title>مواقفنا - حجز مواقف</title>
    <link rel="manifest" href="manifest.json">
    <link rel="icon" href="data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'><text y='.9em' font-size='90'>🅿️</text></svg>">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background: #f5f5f5;
            color: #333;
            line-height: 1.6;
        }
        
        .app-container {
            max-width: 100%;
            min-height: 100vh;
        }
        
        /* تبقى جميع الأنماط السابقة */
        /* ... */
        
        /* أنماط الهاتف */
        @media (max-width: 768px) {
            .parking-grid {
                grid-template-columns: 1fr;
            }
            
            .hero h1 {
                font-size: 1.8rem;
            }
            
            .hero p {
                font-size: 1rem;
            }
        }
        
        /* شريط التثبيت */
        .install-prompt {
            position: fixed;
            bottom: 0;
            left: 0;
            right: 0;
            background: #2E86AB;
            color: white;
            padding: 15px;
            display: none;
            justify-content: space-between;
            align-items: center;
            box-shadow: 0 -2px 10px rgba(0,0,0,0.1);
            z-index: 1000;
        }
        
        .install-btn {
            background: white;
            color: #2E86AB;
            border: none;
            padding: 8px 15px;
            border-radius: 20px;
            font-weight: bold;
            cursor: pointer;
        }
    </style>
</head>
<body>
    <div class="app-container">
        <!-- محتوى التطبيق السابق -->
        <!-- ... -->
    </div>

    <div class="install-prompt" id="installPrompt">
        <span>تثبيت التطبيق على هاتفك</span>
        <button class="install-btn" id="installButton">تثبيت</button>
    </div>

    <script>
        // كود PWA للتثبيت
        let deferredPrompt;
        
        window.addEventListener('beforeinstallprompt', (e) => {
            e.preventDefault();
            deferredPrompt = e;
            document.getElementById('installPrompt').style.display = 'flex';
        });
        
        document.getElementById('installButton').addEventListener('click', async () => {
            if (deferredPrompt) {
                deferredPrompt.prompt();
                const { outcome } = await deferredPrompt.userChoice;
                if (outcome === 'accepted') {
                    document.getElementById('installPrompt').style.display = 'none';
                }
                deferredPrompt = null;
            }
        });
        
        // تسجيل Service Worker
        if ('serviceWorker' in navigator) {
            window.addEventListener('load', () => {
                navigator.serviceWorker.register('/sw.js')
                    .then((registration) => {
                        console.log('Service Worker registered');
                    })
                    .catch((error) => {
                        console.log('Service Worker registration failed');
                    });
            });
        }
        
    {
  "name": "مواقفنا - حجز مواقف",
  "short_name": "مواقفنا",
  "description": "تطبيق حجز مواقف السيارات",
  "start_url": "/",
  "display": "standalone",
  "background_color": "#ffffff",
  "theme_color": "#2E86AB",
  "orientation": "portrait",
  "icons": [
    {
      "src": "data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'><text y='.9em' font-size='90'>🅿️</text></svg>",
      "sizes": "192x192",
      "type": "image/svg+xml"
    }
  ]
}    // باقي الكود JavaScript السابق
        // ...
    </script>
</body>
</html>
