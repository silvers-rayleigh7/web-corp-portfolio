# Web Development Corp (CORP-001)

> AI-корпорация из 36 агентов для создания сайтов любой сложности

## Живая презентация

**[Открыть презентацию архитектуры](https://silvers-rayleigh7.github.io/-------/)**

## 5 демо-проектов

| Проект | Жанр | Ссылка |
|--------|------|--------|
| The Lost File | Horror | [Открыть](https://silvers-rayleigh7.github.io/-------/test-websites/the-lost-file.html) |
| Forte Music Store | E-commerce | [Открыть](https://silvers-rayleigh7.github.io/-------/test-websites/forte-music.html) |
| Щит и Право | Legal/Corporate | [Открыть](https://silvers-rayleigh7.github.io/-------/test-websites/shield-law.html) |
| FORGE Fitness | Fitness/Industrial | [Открыть](https://silvers-rayleigh7.github.io/-------/test-websites/forge-fitness.html) |
| Зерно | Cafe/Artisan | [Открыть](https://silvers-rayleigh7.github.io/-------/test-websites/zerno-coffee.html) |

## Структура репозитория

```
/
├── index.html                    # Презентация архитектуры (главная)
├── test-websites/                # 5 демо-сайтов
│   ├── the-lost-file.html
│   ├── forte-music.html (+5 подстраниц)
│   ├── shield-law.html
│   ├── forge-fitness.html
│   └── zerno-coffee.html
└── architecture/                 # Полная архитектура корпорации
    ├── docs/
    │   ├── CORP-001-README.md    # Главная документация
    │   ├── agent-corps.md        # Реестр корпораций
    │   └── web-design-patterns.md # Паттерны дизайна по жанрам
    ├── agents/                   # 10 определений агентов (.md)
    ├── skills/                   # 7 навыков (skills)
    └── knowledge/                # 9 JSON баз знаний
```

## Архитектура

```
СОВЕТ ДИРЕКТОРОВ (пользователь)
│
└── web-ceo  [Claude Opus 4.6] — Оркестратор
    ├── web-cto  — Технический директор (Frontend, Backend, DevOps)
    ├── web-cdo  — Дизайн-директор (Figma, UX, Stitch AI)
    ├── web-cco  — Контент-директор (Copy, SEO)
    ├── web-cmo  — Маркетинг-директор (Strategy, Analytics)
    ├── web-ccro — Креативный директор (Image Trio, Video, GIF)
    └── web-coo  — Операционный директор (QA, Performance)
```

Каждый директор управляет alpha/beta парами специалистов (24 агента).

## Ключевые особенности

- **Theme-First дизайн** — 10 вопросов об аудитории перед каждым проектом
- **Image Trio** — 3 AI-модели генерируют изображения параллельно
- **Alpha/Beta обучение** — агенты учатся друг у друга
- **Quality Gate** — Lighthouse >= 90, WCAG 2.1, cross-browser
- **Knowledge Store** — 9 JSON баз знаний, накапливающих опыт

## Технологии

Frontend: Next.js, React, Tailwind CSS, Framer Motion
Backend: Node.js, Express, Prisma, PostgreSQL
AI: Gemini 3.1 Flash, GPT Image 1.5, Grok Imagine, Kimi K2.5
Hosting: Vercel, Netlify, Railway

---

*AMAI Game Studio | CORP-001 | 36 агентов | 2026*
