---
name: web-image-ensemble
description: Ансамблевая генерация изображений через 3 модели: Nano Banana (Gemini, основная), GPT Image 1.5, Grok Imagine. Агенты учатся друг у друга — какая модель лучше для какого типа контента.
disable-model-invocation: false
allowed-tools: Bash, Read, Write
---

# Web Image Ensemble Skill

## Три модели — три специализации

| Модель | Полза ID | Цена | Лучше всего для |
|--------|----------|------|-----------------|
| **Nano Banana** (Gemini 3.1 Flash Image) | `google/gemini-3.1-flash-image-preview` | 4.8-10.8 руб | Арт, иллюстрации, стиль, анимированные сцены |
| **GPT Image 1.5** | `openai/gpt-image-1.5` | 3-16.5 руб | Фото-реализм, текст в картинке, логотипы, UI мокапы |
| **Grok Imagine** | `x-ai/grok-imagine-image` | 2.50 руб | Массовая генерация, иконки, простые баннеры |

## Вызов через Polza API

```python
import asyncio
from pathlib import Path
import sys
sys.path.insert(0, str(Path.home() / "Documents" / "Тестовая" / "kwork"))

from agents.polza_client import PolzaClient

async def generate_image(model: str, prompt: str) -> bytes:
    client = PolzaClient()
    return await client.generate_image(model=model, prompt=prompt)

# Nano Banana (основная)
img = asyncio.run(generate_image(
    "google/gemini-3.1-flash-image-preview",
    "Modern SaaS hero illustration, isometric 3D, clean white background..."
))

# GPT Image (текст в картинке)
img = asyncio.run(generate_image(
    "openai/gpt-image-1.5",
    "Professional logo design with text 'TechCorp', minimal, blue accent..."
))

# Grok (быстро/дёшево)
img = asyncio.run(generate_image(
    "x-ai/grok-imagine-image",
    "Simple icon: gear with lightning bolt, flat design, blue color..."
))
```

## Логика выбора модели

```python
def choose_model(task_type: str, has_text: bool, budget: str) -> str:
    if has_text or task_type in ["logo", "banner_with_text", "ui_mockup"]:
        return "openai/gpt-image-1.5"  # лучший рендеринг текста

    if task_type in ["hero", "illustration", "artistic", "3d"]:
        return "google/gemini-3.1-flash-image-preview"  # Nano Banana

    if budget == "low" or task_type in ["icon", "simple_banner", "bulk"]:
        return "x-ai/grok-imagine-image"  # самый дешёвый

    return "google/gemini-3.1-flash-image-preview"  # default
```

## Промпт-формулы для веб

### Hero секция (Nano Banana)
```
"[стиль] hero section background illustration for [тип сайта].
[цвет] color palette, [настроение] atmosphere.
Abstract [элементы], modern design, no text, 16:9 ratio.
Professional commercial quality."
```

### Product/UI мокап (GPT Image)
```
"Realistic device mockup showing [описание UI].
MacBook Pro / iPhone 15 Pro screen, clean white background.
Professional product photography style, soft shadows.
UI design: [описание экрана]"
```

### Иконки/Icons (Grok)
```
"Flat design icon: [описание].
Single color: [цвет].
Simple geometric shapes, clean lines.
SVG-style, white background, 1:1 ratio."
```

## Кросс-обучение моделей

После генерации — записывай что сработало:

```python
# Обновить знания
import json, time
from pathlib import Path

kb = Path.home() / ".claude" / "knowledge" / "web-corp" / "images.json"
data = json.loads(kb.read_text()) if kb.exists() else {"patterns": []}
data["patterns"].append({
    "model": "nano_banana",
    "task_type": "hero_illustration",
    "prompt_pattern": "isometric 3D + white bg",
    "result": "excellent",
    "timestamp": time.time()
})
kb.write_text(json.dumps(data, indent=2, ensure_ascii=False))
```

## Ensemble: параллельная генерация

Для важных задач — генерируй тремя моделями, выбирай лучший результат:

```python
async def ensemble_generate(prompt: str) -> list[bytes]:
    """Генерирует одновременно тремя моделями."""
    models = [
        "google/gemini-3.1-flash-image-preview",
        "openai/gpt-image-1.5",
        "x-ai/grok-imagine-image"
    ]
    results = await asyncio.gather(*[
        generate_image(m, prompt) for m in models
    ])
    return results  # отправить все 3 на выбор
```
