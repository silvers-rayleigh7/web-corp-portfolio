---
name: web-cross-learning
description: Протокол кросс-обучения для всех агентов Web Corp. Агенты читают знания пиров перед задачей и записывают паттерны после. Автоматически вызывается всеми web-* агентами.
disable-model-invocation: false
allowed-tools: Bash, Read, Write
---

# Web Corp Cross-Learning Protocol

## Обязательный ритуал ПЕРЕД задачей

```bash
# Читаем знания своего домена
cat ~/.claude/knowledge/web-corp/<domain>.json 2>/dev/null || echo "{}"

# Читаем знания пиров (alpha читает beta и наоборот)
cat ~/.claude/knowledge/web-corp/<peer>.json 2>/dev/null || echo "{}"

# Читаем глобальные паттерны корпорации
cat ~/.claude/knowledge/web-corp/global.json 2>/dev/null || echo "{}"
```

## Обязательный ритуал ПОСЛЕ задачи

После выполнения — записать 1-3 инсайта в формате:

```bash
python3 << 'EOF'
import json, os, time
from pathlib import Path

knowledge_dir = Path.home() / ".claude" / "knowledge" / "web-corp"
knowledge_dir.mkdir(parents=True, exist_ok=True)

domain_file = knowledge_dir / "<domain>.json"
data = json.loads(domain_file.read_text()) if domain_file.exists() else {"patterns": [], "updated": ""}

# Добавь свои инсайты:
new_insights = [
    {"key": "pattern_name", "value": "что узнал", "timestamp": time.time()}
]
data["patterns"] = (data.get("patterns", []) + new_insights)[-50:]  # хранить последние 50
data["updated"] = time.strftime("%Y-%m-%d %H:%M")

domain_file.write_text(json.dumps(data, ensure_ascii=False, indent=2))
print(f"✓ Saved {len(new_insights)} insights to {domain_file.name}")
EOF
```

## Домены знаний

| Файл | Владелец | Читают |
|------|----------|--------|
| `frontend.json` | web-frontend-alpha/beta | web-cto, web-devops |
| `backend.json` | web-backend-alpha/beta | web-cto, web-devops |
| `design.json` | web-figma-alpha/beta | web-cdo, web-ux |
| `images.json` | web-image-nano/gpt/grok | web-cdo, web-ccro |
| `copy.json` | web-copy-alpha/beta | web-cco, web-strategy |
| `seo.json` | web-seo-alpha/beta | web-cco, web-analytics |
| `strategy.json` | web-strategy-alpha/beta | web-cmo, web-analytics |
| `qa.json` | web-qa-alpha/beta | web-coo, web-perf |
| `global.json` | web-ceo | все агенты |

## [LEARN] Маркеры

Если в тексте агента есть `[LEARN: key="value"]` — это знание автоматически парсится.
Используй для критических паттернов, которые должны знать все агенты.

Пример: `[LEARN: hero_cta="глаголы действия конвертируют на 23% лучше существительных"]`

## Правила взаимообучения

- **Alpha** специализируется на новых подходах / экспериментах
- **Beta** специализируется на проверенных паттернах / best practices
- При конфликте: beta-подход по умолчанию, alpha-подход при флаге `experimental: true`
- После 5 успешных задач alpha → паттерн переходит в beta
