# Web Development Corp

> Корпорация для создания сайтов любых форматов: лендинги, многостраничники, интернет-магазины.

## Быстрый запуск

```
@web-ceo Сделай [тип сайта] для [продукт/бизнес]
```

CEO запустит всю корпорацию автоматически.

---

## Иерархия

```
СОВЕТ ДИРЕКТОРОВ (ты)
│
└── web-ceo  [Claude Opus 4.6]
    Принимает задачу → декомпозирует → делегирует → собирает результат
    │
    ├── web-cto  [Claude Sonnet 4.6]  — Архитектура и код
    │   ├── web-frontend-alpha   React/Next.js, Framer Motion
    │   ├── web-frontend-beta    HTML/CSS, accessibility
    │   ├── web-backend-alpha    API, Stripe, Resend
    │   ├── web-backend-beta     DB, auth, security
    │   ├── web-devops-alpha     Vercel + Railway деплой
    │   └── web-devops-beta      CI/CD GitHub Actions
    │
    ├── web-cdo  [Sonnet + Gemini 3.1 Pro]  — Дизайн
    │   ├── web-figma-alpha      Wireframes, GPT-5 Vision анализ
    │   ├── web-figma-beta       Дизайн-система, Stitch AI
    │   ├── web-ux-alpha         User flow, психология
    │   └── web-ux-beta          Accessibility, mobile-first
    │
    ├── web-cco  [Claude Sonnet 4.6]  — Контент
    │   ├── web-copy-alpha       Hero, CTA, UVP
    │   ├── web-copy-beta        Features, FAQ, About
    │   ├── web-seo-alpha        Технический SEO (Gemini 2.5 Pro)
    │   └── web-seo-beta         Контентный SEO (DeepSeek V3.2)
    │
    ├── web-cmo  [Claude Sonnet 4.6]  — Маркетинг
    │   ├── web-strategy-alpha   CRO, воронка, конверсия
    │   ├── web-strategy-beta    A/B тесты, конкуренты
    │   ├── web-analytics-alpha  GA4, GTM (Qwen3 235B)
    │   └── web-analytics-beta   Инсайты (DeepSeek V3.2)
    │
    ├── web-ccro  [Sonnet + Gemini 3.1 Pro]  — Медиа
    │   ├── web-image-nano       Nano Banana (Gemini Flash) — PRIMARY
    │   ├── web-image-gpt        GPT Image 1.5 — мокапы, текст
    │   ├── web-image-grok       Grok Imagine — bulk, 2.50 руб
    │   ├── web-video-alpha      Kling AI 2.0 — AI видео
    │   ├── web-video-beta       ffmpeg — обработка
    │   ├── web-gif-alpha        Animated content (Grok + Nano)
    │   └── web-gif-beta         CSS/JS анимации (0 зависимостей)
    │
    └── web-coo  [Claude Sonnet 4.6]  — QA и сдача
        ├── web-qa-alpha         Playwright автотесты
        ├── web-qa-beta          Lighthouse + axe accessibility
        ├── web-perf-alpha       Core Web Vitals LCP/CLS/INP
        └── web-perf-beta        Bundle + Assets оптимизация
```

---

## Модели по ролям

| Агент / Тип | Модель | Через |
|-------------|--------|-------|
| CEO | claude-opus-4-6 | Claude Code |
| C-Suite | claude-sonnet-4-6 | Claude Code |
| Специалисты | claude-sonnet-4-6 | Claude Code |
| CDO анализ дизайна | gemini-3.1-pro-preview | Polza.ai |
| SEO анализ | gemini-2.5-pro | Polza.ai |
| Figma анализ | openai/gpt-5 (vision) | Polza.ai |
| Конт. SEO / Research | deepseek/deepseek-v3.2 | Polza.ai |
| Analytics данные | qwen/qwen3-235b-a22b | Polza.ai |
| Image PRIMARY | google/gemini-3.1-flash-image-preview | Polza.ai |
| Image мокапы/текст | openai/gpt-image-1.5 | Polza.ai |
| Image bulk/дёшево | x-ai/grok-imagine-image | Polza.ai |
| AI видео | Kling AI 2.0 | API |
| Видео обработка | ffmpeg | local |

---

## Skills (навыки агентов)

| Skill | Файл | Используют |
|-------|------|-----------|
| Кросс-обучение | `web-cross-learning` | все web-* |
| Figma API | `web-figma` | figma-alpha/beta, cdo |
| SEO инструменты | `web-seo` | seo-alpha/beta, copy, cco |
| Продающие тексты | `web-copywriting` | copy-alpha/beta, cco |
| Производительность | `web-performance` | perf-alpha/beta, coo, frontend |
| Image Trio | `web-image-ensemble` | image-nano/gpt/grok, ccro |

---

## Knowledge Store

Путь: `~/.claude/knowledge/web-corp/`

| Файл | Владелец | Содержит |
|------|----------|---------|
| `global.json` | web-ceo | Глобальные паттерны корпорации |
| `frontend.json` | frontend-alpha/beta | Компоненты, анимации, стек |
| `backend.json` | backend-alpha/beta | API паттерны, интеграции |
| `design.json` | figma-alpha/beta, ux | Layout, UX паттерны |
| `images.json` | image-nano/gpt/grok | Модель → тип контента |
| `copy.json` | copy-alpha/beta | Заголовки, CTA формулы |
| `seo.json` | seo-alpha/beta | Schema, ключи, структура |
| `strategy.json` | strategy-alpha/beta | CRO, A/B паттерны |
| `qa.json` | qa-alpha/beta, perf | Баги, тесты, метрики |

---

## Протокол кросс-обучения

Каждый специалист:
1. **ДО задачи:** читает `knowledge/web-corp/<domain>.json`
2. **ПОСЛЕ задачи:** записывает 1-3 инсайта через `[LEARN: key="value"]`
3. **Пир-обучение:** alpha читает паттерны beta и наоборот

Через 5+ выполненных задач база знаний накапливает специфику твоего бизнеса.

---

## Типы сайтов

| Тип | Стек | Время |
|-----|------|-------|
| Лендинг (статик) | HTML/CSS/JS + Vercel | быстро |
| Лендинг SaaS | Next.js + Tailwind + Vercel | средне |
| Многостраничник | Next.js + CMS (Sanity) + Vercel | средне |
| Интернет-магазин | Next.js + Stripe + Railway | долго |
| Корпоративный | Next.js + Postgres + Railway | долго |

---

*Создано: 2026-03-03 | Агентов: 36 | Skills: 6 | Knowledge domains: 9*
