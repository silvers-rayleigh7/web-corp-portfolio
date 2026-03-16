---
name: web-performance
description: Оптимизация производительности сайтов. Core Web Vitals, Lighthouse, оптимизация изображений, бандлов, шрифтов. Используется web-perf-alpha, web-perf-beta, web-coo.
disable-model-invocation: false
allowed-tools: Bash, Read, WebFetch
---

# Web Performance Skill

## Lighthouse — запуск и анализ

```bash
# CLI аудит
npx lighthouse https://site.com \
  --output=json \
  --output-path=./lighthouse-report.json \
  --chrome-flags="--headless"

# Только Core Web Vitals
npx lighthouse https://site.com \
  --only-categories=performance \
  --output=html

# Анализ отчёта
cat lighthouse-report.json | python3 -c "
import json, sys
data = json.load(sys.stdin)
cats = data['categories']
print(f'Performance: {cats[\"performance\"][\"score\"]*100:.0f}')
print(f'SEO: {cats[\"seo\"][\"score\"]*100:.0f}')
print(f'A11y: {cats[\"accessibility\"][\"score\"]*100:.0f}')
print(f'Best Practices: {cats[\"best-practices\"][\"score\"]*100:.0f}')
"
```

## Изображения — оптимизация

```bash
# WebP конвертация
for img in *.jpg *.png; do
  cwebp -q 85 "$img" -o "${img%.*}.webp"
done

# Resize + optimize
ffmpeg -i hero.jpg -vf "scale=1920:-1" -q:v 85 hero-1920.webp
ffmpeg -i hero.jpg -vf "scale=960:-1" -q:v 85 hero-960.webp
ffmpeg -i hero.jpg -vf "scale=480:-1" -q:v 85 hero-480.webp

# Responsive images HTML
<img src="hero-960.webp"
     srcset="hero-480.webp 480w, hero-960.webp 960w, hero-1920.webp 1920w"
     sizes="(max-width: 480px) 480px, (max-width: 960px) 960px, 1920px"
     alt="..." loading="lazy" decoding="async">
```

## Critical CSS — встраивание

```bash
# Генерация critical CSS
npx critical https://site.com --inline --minify > critical.css

# В HTML
<style>/* critical CSS inline */</style>
<link rel="preload" href="/styles.css" as="style" onload="this.rel='stylesheet'">
```

## Fonts — оптимизация загрузки

```html
<!-- Preconnect -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>

<!-- Preload критичного шрифта -->
<link rel="preload" href="/fonts/inter-var.woff2" as="font" type="font/woff2" crossorigin>

<!-- font-display: swap -->
@font-face {
  font-family: 'Inter';
  src: url('/fonts/inter-var.woff2') format('woff2');
  font-display: swap;
  font-weight: 100 900;
}
```

## JavaScript — оптимизация бандла

```javascript
// Lazy loading компонентов (React)
const HeavyComponent = React.lazy(() => import('./HeavyComponent'));

// Preload critical routes
<link rel="prefetch" href="/dashboard">

// Tree-shaking (импортируй конкретно)
import { debounce } from 'lodash/debounce'; // ✓
import _ from 'lodash';                      // ✗

// Code splitting (Vite/Webpack)
// vite.config.js
build: {
  rollupOptions: {
    output: {
      manualChunks: {
        vendor: ['react', 'react-dom'],
        ui: ['@radix-ui/react-*']
      }
    }
  }
}
```

## Caching стратегия

```nginx
# nginx.conf
location ~* \.(js|css|png|jpg|jpeg|gif|ico|webp|woff2)$ {
    expires 1y;
    add_header Cache-Control "public, immutable";
}

location ~* \.(html)$ {
    expires 1h;
    add_header Cache-Control "public, must-revalidate";
}
```

## Performance чеклист

- [ ] Lighthouse Performance Score ≥ 90
- [ ] LCP < 2.5s (главный элемент загружен)
- [ ] CLS < 0.1 (нет прыжков контента)
- [ ] INP < 200ms (ответ на взаимодействие)
- [ ] Все изображения — WebP/AVIF
- [ ] Hero image — preload + srcset
- [ ] Шрифты — preload + font-display: swap
- [ ] Critical CSS встроен
- [ ] JS defer/async везде кроме критичного
- [ ] Gzip/Brotli включён на сервере
- [ ] HTTP/2 или HTTP/3
- [ ] CDN для static assets
- [ ] Total page weight < 1.5MB
