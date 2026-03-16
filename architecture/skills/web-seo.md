---
name: web-seo
description: Полный SEO инструментарий для веб-агентов. Технический SEO, контентный SEO, schema.org, Core Web Vitals, keyword research. Используется web-seo-alpha, web-seo-beta, web-copywriter.
disable-model-invocation: false
allowed-tools: Bash, WebSearch, WebFetch, Read
---

# Web SEO Skill

## Обязательный SEO чеклист для каждой страницы

### Meta теги
```html
<title>Основной ключ — Бренд | 50-60 символов</title>
<meta name="description" content="Описание 150-160 символов с ключом и CTA">
<meta name="keywords" content="ключ1, ключ2, ключ3">
<link rel="canonical" href="https://site.com/page/">

<!-- Open Graph -->
<meta property="og:title" content="...">
<meta property="og:description" content="...">
<meta property="og:image" content="https://site.com/og-image.jpg"> <!-- 1200×630 -->
<meta property="og:url" content="...">
<meta property="og:type" content="website">

<!-- Twitter Card -->
<meta name="twitter:card" content="summary_large_image">
```

### Структура заголовков
```
H1: 1 штука, главный ключ, 40-70 символов
H2: 3-7 штук, LSI ключи, раскрывают H1
H3: подпункты H2, длинный хвост
```

### Schema.org разметка

```json
<!-- Организация -->
{
  "@context": "https://schema.org",
  "@type": "Organization",
  "name": "...",
  "url": "...",
  "logo": "...",
  "sameAs": ["https://t.me/...", "https://vk.com/..."]
}

<!-- Сайт (SiteLinks поиск) -->
{
  "@context": "https://schema.org",
  "@type": "WebSite",
  "url": "https://site.com/",
  "potentialAction": {
    "@type": "SearchAction",
    "target": "https://site.com/?s={search_term_string}",
    "query-input": "required name=search_term_string"
  }
}

<!-- Продукт (для лендингов) -->
{
  "@context": "https://schema.org",
  "@type": "Product",
  "name": "...",
  "description": "...",
  "offers": {
    "@type": "Offer",
    "price": "...",
    "priceCurrency": "USD"
  }
}
```

## Keyword Research формула

1. **Seed keywords**: 3-5 главных тем продукта
2. **Expand**: для каждого seed → `[кто|что|как|зачем|лучший|сравнение] + seed`
3. **Long-tail**: `seed + [для + аудитория] + [в + город/страна]`
4. **Intent mapping**:
   - Informational: как, что такое, зачем
   - Commercial: лучший, сравнение, отзывы
   - Transactional: купить, цена, скачать
   - Navigational: [бренд] + сайт/вход

## Core Web Vitals цели

| Метрика | Хорошо | Улучшить | Плохо |
|---------|--------|----------|-------|
| LCP (загрузка) | < 2.5s | 2.5-4s | > 4s |
| CLS (смещение) | < 0.1 | 0.1-0.25 | > 0.25 |
| INP (отклик) | < 200ms | 200-500ms | > 500ms |
| FCP | < 1.8s | 1.8-3s | > 3s |
| TTFB | < 800ms | 800ms-1.8s | > 1.8s |

## Техническое SEO

```bash
# robots.txt
User-agent: *
Allow: /
Disallow: /admin/
Sitemap: https://site.com/sitemap.xml

# .htaccess редиректы (важно для SEO)
RewriteEngine On
RewriteCond %{HTTPS} off
RewriteRule (.*) https://%{HTTP_HOST}%{REQUEST_URI} [R=301,L]

# Trailing slash consistency
RewriteCond %{REQUEST_FILENAME} !-f
RewriteRule ^(.*[^/])$ /$1/ [R=301,L]
```

## Контентный SEO для лендингов

- **Hero**: H1 с главным ключом, первые 100 слов содержат ключ 2 раза
- **Features**: alt-теги у всех картинок с ключами
- **FAQ секция**: отвечает на вопросы (PAA box в Google)
- **Social proof**: отзывы с семантикой ключей
- **Footer**: ссылки на важные страницы, хлебные крошки
