# Корпорации Агентов

## КРИТИЧЕСКИЕ ПРАВИЛА ПОВЕДЕНИЯ

1. **Триггер создания:** Когда пользователь говорит "давай сделаем корпорацию по [направлению]" или любую похожую фразу — это ВСЕГДА означает новую корпорацию. Понять автоматически, без уточнений.

2. **Единое хранилище:** Все корпорации хранятся в `Тестовая/КОРПОРАЦИИ АГЕНТОВ/<название>/`. Каждая новая — добавляется туда же.

3. **Универсальность:** Каждая корпорация работает на идентичные задачи по всему проекту, не только для Kwork. Но для Kwork — каждая корпорация работает на постоянке и автоматизированно.

4. **После создания:** Всегда сохранять в папку + memory + git коммит `CORP-XXX`.

---

## Концепция

Корпоративная иерархия ИИ-агентов. Пользователь = Совет директоров.
Запускает CEO → он делегирует C-Suite → специалисты alpha/beta выполняют + учатся друг у друга.

**Папка в проекте:** `Тестовая/КОРПОРАЦИИ АГЕНТОВ/`

---

## Реестр корпораций

| # | Корпорация | Папка | Статус | Агентов | Дата |
|---|-----------|-------|--------|---------|------|
| CORP-001 | Web Development Corp | `web-corp/` | ✅ Готова | 36 | 2026-03-03 |
| CORP-002 | Presentation Corp | `presentation-corp/` | ✅ Готова | 10 | 2026-03-03 |

---

## Web Development Corp ✅ (CORP-001)

**Документация:** `КОРПОРАЦИИ АГЕНТОВ/web-corp/README.md`
**Запуск:** `@web-ceo Сделай [тип сайта] для [продукт]`

### Структура: 38 агентов + 7 skills

**Super-Agents (2) — работают ACROSS ALL корпораций:**
- `stitch` — Главный дизайн-гений. Creative Direction, Brand Identity, уровень Awwwards/FWA. Использует Kimi K2.5 vision.
- `kimi-claw` — Универсальный AI помощник (Kimi K2.5, 1T params, 256K ctx). Для всех корпораций.

**C-Suite (7):**
- `web-ceo` — claude-opus-4-6, оркестратор
- `web-cto` — claude-sonnet-4-6, технический директор
- `web-cdo` — sonnet + Kimi K2.5 vision, дизайн (делегирует Stitch)
- `web-cco` — claude-sonnet-4-6, контент
- `web-cmo` — claude-sonnet-4-6, маркетинг
- `web-ccro` — sonnet + Gemini 3.1 Pro, медиа
- `web-coo` — claude-sonnet-4-6, QA и сдача

**Специалисты alpha/beta (2 на роль):**
Frontend (2025 Aurora/Bento) · Backend · DevOps · Figma (Stitch-powered) · UX · Copy · SEO · Strategy · Analytics · Video · GIF · QA · Performance

**Image Trio:** Nano Banana (PRIMARY) · GPT Image 1.5 · Grok Imagine

**Skills (8):**
`web-cross-learning` · `web-figma` · `web-seo` · `web-copywriting` · `web-performance` · `web-image-ensemble` · `kimi-universal` · `theme-analysis`

**Design Protocol:**
- `design-mentor` агент обучает всех дизайн-агентов протоколу 10 вопросов
- Перед каждым сайтом: theme-analysis → Theme Profile → Stitch brief → execution
- `web-design.md` в memory — паттерны по жанрам (horror, tech, caucasian, gamedev)

**Knowledge Stores:**
- `~/.claude/knowledge/web-corp/` (9 JSON доменов)
- `~/.claude/knowledge/stitch/design-patterns.json` ← NEW
- `~/.claude/knowledge/kimi/universal-insights.json` ← NEW (межкорпоративный)

---

## Presentation Corp ✅ (CORP-002)

**Документация:** `КОРПОРАЦИИ АГЕНТОВ/presentation-corp/README.md`
**Запуск:** `@pres-ceo Создай [тип] презентацию о [тема]`

### Структура: 10 агентов + 4 skills

**C-Suite (5):**
- `pres-ceo` — Claude Opus 4.6, оркестратор
- `pres-cro` — исследование темы, рынка
- `pres-cco` — контент, SlideContent
- `pres-cdo` — дизайн, координирует 5 дизайн-агентов
- `pres-cqo` — контроль качества

**Дизайн-агенты (5):**
- `pres-gamma-designer` — PRIMARY: Gamma API + MCP (AI-генерация)
- `pres-zoho-designer` — Zoho Office Integrator API (.pptx)
- `pres-visme-designer` — Visme (Playwright, инфографика)
- `pres-emaze-designer` — Emaze (Playwright, 3D-анимации)
- `pres-beautiful-designer` — Beautiful.ai (Playwright, Smart Slides)

**Skills (4):**
`pres-gamma-api` · `pres-gamma-mcp` · `pres-gamma-templates` · `pres-web-automation`

**MCP:** Gamma MCP сервер добавлен в `~/.claude/settings.json`

---

## Шаблон создания новой корпорации

При создании любой корпорации:

```
1. Определить: CEO prefix (например: kwork-ceo, content-ceo)
2. Создать C-Suite (минимум 4-6 директоров)
3. Специалисты alpha/beta по 2-3 на каждую роль
4. Skills специфичные для направления
5. Knowledge Store: ~/.claude/knowledge/<corp-name>/
6. Папка: КОРПОРАЦИИ АГЕНТОВ/<corp-name>/README.md
7. Git коммит: CORP-XXX
8. Обновить этот файл
```

---

## Примеры выполненных заказов Web Corp

| Проект | Файлы | Фичи |
|--------|-------|------|
| Forte Music Store | `test-websites/forte-music.html` + 5 subpages | Web Audio synth, tab carousel, cart drawer, localStorage cart |
| The Lost File | `test-websites/the-lost-file.html` | Horror design, IM Fell English, fog layers, blood drips |
| AI Rockets | `test-websites/ai-rockets.html` | 3D tilt cards, dual canvas, magnetic buttons, rocket launch |

---

## Следующие корпорации (планируются для Kwork и не только)

| Идея | Назначение |
|------|-----------|
| Content Corp | Тексты, копирайтинг, статьи, блоги |
| Design Corp | Логотипы, брендинг, UI kit, иллюстрации |
| SEO Corp | Аудиты, семантика, продвижение |
| Marketing Corp | SMM, таргет, email, воронки |
| Data Corp | Парсинг, аналитика, автоматизация |
| Video Corp | Reels, YouTube, монтаж, сценарии |
