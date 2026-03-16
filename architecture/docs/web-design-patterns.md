# Web Design — Уроки и паттерны

> Усвоено из сессий по test-websites (ai-rockets.html, the-lost-file.html)

## Главное правило (от пользователя)
**"Всегда отталкивайся от тематики сайта, который мы делаем."**
- Шрифт, размер, цвета, анимации — всё диктует жанр/тематика
- Нельзя делать "красивый универсальный дизайн" — нужно попасть в контекст

---

## Horror Game Sites

### Типографика
- **Запрещено:** крупные display fonts 80-120px, generic serif (выглядит как luxury, не horror)
- **Правильно:** IM Fell English (digitized 1593, старая рукопись), Cormorant Garamond — оба создают feel психологического ужаса
- **Размеры h1:** `clamp(40px, 6vw, 70px)` — не больше 70px для хоррора
- **Размеры h2:** `clamp(28px, 3.5vw, 48px)`

### Цвета — кровь и ужас без 18+
- `#5C0A14` — тёмная засохшая кровь / ржавчина (основной horror акцент)
- `#8B1A24` — средняя кровь
- `#B01C2E` — только для акцентных деталей
- `#060608` — void black (фон)
- `#DDD8CC` — состаренная бумага (светлый текст)
- **Запрещено:** `#C8102E` (bright fire red) — это action/danger, не horror

### Атмосферные эффекты
- **Туман (fog layer):** 3 radial-gradient blob-а, `filter: blur(50px)`, opacity 0.04-0.05, CSS keyframe дрейф
- **Капли крови на разделителях:** CSS `height` anim 0→28px, `border-radius: 0 0 50% 50%` — выглядит как потёки воды/ржавчины
- **Флуоресцентный мигач:** `@keyframes` с нерегулярными opacity drops на section `::before` — hospital feel
- **Угловые пятна ржавчины:** `radial-gradient` на hero `::before` — subtle staining
- **Виньетка:** тяжёлая, `radial-gradient(ellipse, transparent 20%, #06060A 70%, #06060A 95%)`

### Референсы
- Playdead's LIMBO site — horror через минимализм
- A24 Films — психологическая атмосфера без явного насилия
- Hideo Kojima portfolio — ambient horror

---

## Tech/SaaS/Rocket Sites (ai-rockets.html)

### Что сработало (пользователь: "прям понравилось")
- 3D card tilt: `perspective(900px) rotateX() rotateY() translateZ(10px)` на mousemove
- Dual canvas: отдельный `#stars` (z:0) + `#particles` (z:2) — изоляция render слоёв
- Floating SVG robot: `transform-box: fill-box; transform-origin: center` для SVG анимаций
- Magnetic buttons: `translate((dx*0.22)px, (dy*0.22)px)` относительно центра кнопки
- Star speed warp при запуске ракеты

### Что убрать (пользователь отклонил)
- Countdown overlay / консоль расчётов — слишком сложно, не нужно
- Robot speech bubble — убрать текстовую подсказку
- Вместо: простая мини-анимация (burst particles + rocket SVG улетает вверх за 1.5s)

### Mini launch pattern (утверждён)
```js
// Click → burst particles at rocket pos → shake + flash → star speed spike → rocket SVG translates top: -160px
// Total: 1.5s animation, no overlay, no text
```

---

## Главное правило анализа аудитории (от пользователя)

**ВСЕГДА задавать 10 вопросов о субкультуре ДО выбора цветов/шрифтов.**
Не платформа, не жанр — а живые люди: кто они, что их объединяет, что любят, что оттолкнёт.

Skill: `theme-analysis` — автоматически вызывается у stitch, web-cdo, web-figma
Агент: `design-mentor` — обучает дизайн-агентов, проверяет Theme Profile перед дизайном

10 вопросов (коротко):
1. Кто эти люди? 2. Зачем собираются? 3. Что любят вне сайта? 4. Что вдохновляет?
5. Как отличают своих? 6. Каким языком говорят? 7. Где тусуются?
8. Какой визуальный мир знают? 9. Что для них "круто"? 10. Что оттолкнёт?

## Автономное улучшение агентов (от пользователя)

**Концепция:** агенты должны улучшать друг друга постоянно, автономно, автоматизированно.
- После каждой сессии → записывать паттерны в `~/.claude/knowledge/agents/*.json`
- Stitch учится у web-figma, web-figma учится у web-frontend — цепочка передачи знаний
- Хорошее решение в одном проекте → применять во всех следующих автоматически
- Это ULP (Universal Learning Protocol) применительно к дизайну

## Определение тематики по ТЗ — главное правило

**"Дизайн сайта всегда связан с тематикой ТЗ"**

### Таблица тематик → дизайн-решений

| Тематика ТЗ | Стиль | Цвета | Шрифты | Анимации |
|-------------|-------|-------|--------|----------|
| Юридическое бюро | Серьёзный, авторитетный | Тёмно-синий, антрацит, золото | IBM Plex Serif / Playfair Display | Минимум, только subtle transitions |
| Horror игра | Атмосферный ужас | Void black, тёмная кровь #5C0A14 | IM Fell English / Cormorant | Туман, мигание, glitch |
| Tech/SaaS | Инновационный, чистый | Фиолетово-синий градиент | Inter / Plus Jakarta Sans | Aurora gradients, bento grid |
| Медицина | Доверие, чистота | Белый, голубой, светло-зелёный | Source Sans / Nunito | Плавные, мягкие |
| Ресторан/фуд | Аппетитный, тёплый | Тёплые коричневые, кремовый | Playfair + DM Sans | Parallax, hover zoom фото |
| Luxury/мода | Премиум, минимализм | Чёрный + золото/бежевый | Playfair Display + Inter | Slow reveal, editorial |
| Детский продукт | Радостный, безопасный | Яркие пастельные | Rounded fonts (Nunito, Quicksand) | Игривые bounce анимации |
| Спорт/фитнес | Энергия, сила | Чёрный + неоновый акцент | Sora / Barlow Condensed | Быстрые, динамичные |
| Финансы/банк | Надёжность | Тёмно-синий, зелёный, белый | IBM Plex Sans | Строгий minimum |
| Игровая студия (не horror) | Энергичный, fun | Яркий градиент, неон | Orbitron / Rajdhani | Particle effects, glow |

## Кавказская культура — детальная палитра (исследовано)

**Северный Кавказ (Дагестан, Чечня):**
- Металл: СЕРЕБРО, не золото. Кубачи = центр мирового серебра, техника чернь (niello)
- Цвета одежды: красный, пурпурный `#6B2D6B`, зелёный `#2D5A3D`, тёмные тона
- Паттерн: серебро `#C8C0B4` + чернь `#3A3530` + гранат `#8B1A2A` на тёмном фоне `#1A1612`

**Южный Кавказ (Грузия, Армения, Азербайджан):**
- Металл: золото + серебро оба уместны
- Армения: символ граната, 4 стихии = красный/белый/зелёный/жёлтый
- Грузия: чоха чёрная для элиты, цветные для других
- Сочетание: пергамент `#E8DCC8` + золото `#B8952A` + гранат `#8B1A2A` + бирюза `#3A8080`

**Что НЕЛЬЗЯ для кавказской тематики:**
- Пастельные тона (мятный, лаванда, baby pink) — культурно чужеродны
- Нeon/флуоресцент
- Плоский чёрный без текстуры — траурный контекст
- Карамельный/персиковый — ассоциация со Средней Азией, не Кавказом
- Скандинавский серо-голубой

**Референсы:** KavkazWear, @kubachi.ru, @geofashionlab (Тбилиси), @arisa.fashion_

---

## GameDev сообщество — правильный подход

Приоритет: **gaming culture FIRST**, underground — только стилевой слой.
- Gaming цвета: `#5865F2` (Discord purple) + `#39D353` (electric green) + `#00B4D8` (vivid blue)
- Фон: `#1a1a2e` (dark but not void) — видно что ночной стиль, не мрачный хоррор
- Ошибка: void black `#0D0D14` + нон + orange = hacker aesthetic, не gamedev
- Правило: думай Steam/Discord/Twitch, потом добавляй underground флавор

---

## Необычные стартапы (типа "Автомобили на молоке")

Когда название само по себе абсурдно-смелое:
- Эмоция: **CURIOSITY + DISRUPTION** — "это странно и поэтому я хочу узнать больше"
- НЕ делать: чистый eco-corporate дизайн — убивает уникальность названия
- Lean INTO абсурдность как дифференциатор
- Анимации: liquid morph, playful физика, что-то что визуально объясняет концепт

---

## Общие правила веб-дизайна

| Жанр | Шрифт | h1 размер | Акцент-цвет |
|------|-------|-----------|-------------|
| Horror Game | IM Fell English / Cormorant | 40-70px | #5C0A14 (тёмная кровь) |
| Tech/SaaS | Inter / Plus Jakarta Sans | 56-80px | Gradient purple-blue |
| Luxury | Playfair Display + Inter | 48-72px | #золото или #бежевый |
| E-commerce | DM Sans / Nunito | 40-60px | CTA-цвет бренда |
| Startup | Sora / Outfit | 56-90px | Яркий градиент |

## Архитектура JS для сложных интерактивных сайтов
- Canvas stars (фон) + Canvas particles (UI events) — РАЗНЫЕ canvas элементы
- SVG inline для robot/icons с CSS анимациями
- requestAnimationFrame для cursor tracking (не setInterval)
- Particle burst = 12-24 частицы с random velocity, fade out via opacity
