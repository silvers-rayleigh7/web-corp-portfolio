---
name: web-figma
description: Figma API интеграция для дизайн-агентов. Создание wireframes, экспорт assets, работа с компонентами и дизайн-системами. Используется web-figma-alpha и web-figma-beta.
disable-model-invocation: false
allowed-tools: Bash, WebFetch, Read, Write
---

# Figma Design Skill

## Figma API — базовые операции

```bash
# Получить файл
curl -H "X-Figma-Token: $FIGMA_TOKEN" \
  "https://api.figma.com/v1/files/<FILE_KEY>"

# Экспортировать assets
curl -H "X-Figma-Token: $FIGMA_TOKEN" \
  "https://api.figma.com/v1/images/<FILE_KEY>?ids=<NODE_IDS>&format=svg&scale=2"

# Получить компоненты
curl -H "X-Figma-Token: $FIGMA_TOKEN" \
  "https://api.figma.com/v1/files/<FILE_KEY>/components"
```

## Workflow: Wireframe → Макет → Экспорт

### 1. Wireframe (схема)
Описывай структуру страницы через Figma-JSON или Markdown:
```
Hero:        [Logo] [Nav: Home About Pricing CTA]
             [H1: Главный заголовок]
             [Subtitle + CTA Button]
             [Hero Image / Video]

Features:    3 колонки: [Icon + Title + Text] × 3

Pricing:     3 карточки: [Free | Pro | Enterprise]

Footer:      [Links] [Social] [Copyright]
```

### 2. Компоненты дизайн-системы

Всегда создавай компоненты атомарно:
- **Atoms**: Button, Input, Icon, Badge, Tag
- **Molecules**: Card, FormField, NavItem, PricingCard
- **Organisms**: Header, Hero, FeatureGrid, PricingTable, Footer
- **Templates**: LandingPage, ProductPage, BlogPost

### 3. Типографика (стандарт)

```
H1: 64px / 700 / -2px letter-spacing / 1.1 line-height
H2: 48px / 700 / -1px
H3: 32px / 600
H4: 24px / 600
Body: 18px / 400 / 1.6
Small: 14px / 400 / 1.4
Caption: 12px / 400 / 1.3
```

### 4. Цветовая система

```
Primary:   #[brand color]
Secondary: #[secondary]
Accent:    #[cta color]
Surface:   #FFFFFF / #F8F9FA / #1A1A2E (dark)
Text:      #1A1A1A / #6B7280 / #9CA3AF
Error:     #EF4444
Success:   #10B981
Warning:   #F59E0B
```

## Stitch AI — AI генерация UI

```bash
# Генерация через Stitch AI API
curl -X POST "https://api.stitch.design/v1/generate" \
  -H "Authorization: Bearer $STITCH_API_KEY" \
  -d '{"prompt": "...", "style": "modern-saas", "export": "code"}'
```

### Промпт-формулы для Stitch:
- Landing: `"Modern SaaS landing page, [цвет] accent, clean hero section, feature cards grid, pricing table"`
- E-commerce: `"Clean e-commerce product page, minimal white design, product gallery left, details right"`
- Dashboard: `"Dark analytics dashboard, sidebar nav, KPI cards grid, charts area"`

## Экспорт для разработки

```
SVG:  иконки, логотипы, декоративные элементы
PNG 2x: изображения с текстом, сложные иллюстрации
WebP:  все остальные изображения (сжатие +30%)
```

## Handoff чеклист (передача в CTO)

- [ ] Все компоненты именованы по BEM или atomic design
- [ ] Цвета заменены на переменные/токены
- [ ] Отступы кратны 8px
- [ ] Адаптив: mobile 375px, tablet 768px, desktop 1440px
- [ ] Состояния кнопок: default/hover/active/disabled
- [ ] Экспортированы все assets в `/assets/`
