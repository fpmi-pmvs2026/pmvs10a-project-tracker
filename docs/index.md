# ExpenseTracker — Wiki

Добро пожаловать в документацию проекта **ExpenseTracker** — мобильного приложения для учёта личных финансов, разработанного на Android (Kotlin + Jetpack Compose).

---

## О проекте

**ExpenseTracker** позволяет пользователю отслеживать доходы и расходы, просматривать статистику по категориям, устанавливать бюджеты и следить за актуальными курсами валют через API Национального банка Республики Беларусь (НБРБ).

### Основные возможности

- Добавление, редактирование и удаление транзакций
- Фильтрация по периоду (день / неделя / месяц / год)
- Сводка баланса: доходы, расходы, остаток
- Статистика по категориям с прогресс-барами и дневным графиком
- Установка бюджета по категориям с уведомлениями о превышении
- Актуальные курсы валют (USD, EUR, RUB, CNY, GBP) с автообновлением каждые 6 часов
- Поддержка светлой и тёмной темы (Material 3)

---

## Экраны приложения

| Экран | Описание |
|---|---|
| **Home** | Список транзакций, сводка баланса, фильтры по периоду, FAB для добавления |
| **AddEdit** | Форма добавления/редактирования транзакции: тип, сумма, категория, дата, заметка |
| **Stats** | Статистика расходов по категориям, дневной bar-chart за последние 14 дней |
| **Settings** | Выбор валюты, бюджеты, тема, уведомления, таблица курсов НБРБ |

---

## Технологический стек

| Слой | Технологии |
|---|---|
| UI | Jetpack Compose, Material 3, Navigation Component |
| Архитектура | MVVM, Repository pattern |
| База данных | Room (SQLite), 3 таблицы: transactions, categories, budgets |
| Сеть | Retrofit, API НБРБ (`api.nbrb.by/exrates/rates`) |
| Фоновые задачи | WorkManager (обновление курсов, проверка бюджета) |
| DI | Hilt |
| Настройки | DataStore |
| CI/CD | GitHub Actions → Firebase Test Lab → Release APK |

---

## Страницы Wiki

- [Функциональные требования](https://github.com/fpmi-pmvs2026/pmvs10a-project-tracker/wiki/Functional%E2%80%90Requirements) — варианты использования и текстовые сценарии
- [Дополнительная спецификация](https://github.com/fpmi-pmvs2026/pmvs10a-project-tracker/wiki/Additional%E2%80%90Specification) — нефункциональные требования (производительность, безопасность, доступность)
- [Схема базы данных](Database-Schema) — структура таблиц Room, поля, связи
- [Структура файлов](File-Diagram) — дерево каталогов проекта

---

## Быстрый старт

```bash
git clone https://github.com/Dashuuka/expense-tracker.git
cd expense-tracker
./gradlew assembleDebug
```

Подробные инструкции по установке и запуску — в [README](https://github.com/fpmi-pmvs2026/pmvs10a-project-tracker#readme).

---

## Команда

| Роль | Зона ответственности |
|---|---|
| Person 1 — Тимлид | Data layer, Room DB, Retrofit, DI (Hilt), WorkManager |
| Person 2 | UI (Home, AddEdit), Navigation, CI/CD (GitHub Actions, Firebase Test Lab), Wiki |
| Person 3 | Stats, Settings, Unit-тесты, UI-тесты (Espresso/Compose), GitHub Pages, README |
