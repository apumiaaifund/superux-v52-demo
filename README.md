# SuperUX & APUM AI Guard v5.2

**On-premise платформа автоматического UX-аудита с ИИ.** Находит rage/dead click, chaos scroll, abandonment. Маскирует ПДн по ФЗ-152 (Luhn, СНИЛС, ИНН, ФИО). Считает **реальные** брошенные корзины из cart_value — без оценок. Калькулятор потерь с вашими данными. CEF-SIEM.

## Проблема

EU AI Act и ФЗ-152 требуют защиты ПДн в UX-логах. Зарубежные SaaS (Maze, Hotjar, UserTesting) нельзя использовать в закрытом контуре.

## Что делает

| Модуль | Что |
|---|---|
| `core/pii.py` | Маскировка: карта (Luhn), СНИЛС, ИНН 10/12, паспорт, телефон, email, мат |
| `core/behavior.py` | RAGE_CLICK, DEAD_CLICK, CHAOS_SCROLL, HESITATION, ABANDONMENT |
| `core/anomaly.py` | EWMA-детектор (variance floor, warmup 20) |
| `core/insights.py` | Бизнес-инсайт в ₽/мес (AOV × conv × uplift) |
| `core/journal.py` | HMAC-цепочка (verify через `/v1/journal/verify`) |
| `core/siem.py` | CEF over UDP (ArcSight-совместимый) |
| `core/storage.py` | SQLite (lazy init, failover recovery) |
| `core/auth.py` | JWT HS256 + multi-tenant + RBAC |
| `core/ratelimit.py` | Token bucket middleware |

## Тесты

```bash
pytest tests/ -v  # 30 тестов
```

## Ограничения (честно)

- Не сертифицирован ФСТЭК, не в Реестре Минцифры.
- Пентест не проводился, нет SLA и референс-клиента.
- YandexGPT-адаптер — **[WIP]** (требует API-ключ; сейчас только локальный шаблонный LLM).

## Цена

| Уровень | Цена | Кому |
|---|---|---|
| Пилот | 600–900 тыс ₽ / 3 мес | Маркетплейс, ритейл |
| Годовая лицензия (после ФСТЭК) | 3,5–6 млн ₽ | Tier-1 банк |
| Агентство | 120–250 тыс ₽/мес | UX-студии |

**Важно:** Tier-1 банк — только после ФСТЭК-сертификации (12–18 мес). До этого — маркетплейсы, ритейл, агентства.

Контакт: apumiaaifund@gmail.com

## Лицензия

Proprietary. См. LICENSE. Исходный код — по запросу.
