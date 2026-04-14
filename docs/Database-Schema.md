# Схема базы данных

---

## Диаграмма взаимосвязей сущностей

```
┌──────────────────────────────┐        ┌───────────────────────────────────┐
│         categories           │        │           transactions            │
├──────────────────────────────┤        ├───────────────────────────────────┤
│ PK  id         INTEGER       │◄───┐   │ PK  id          INTEGER AUTOINCR ─│
│     name       TEXT NOT NULL │    │   │     amount      REAL    NOT NULL  │
│     icon       TEXT NOT NULL │    ├───│ FK  categoryId  INTEGER → NULL    │
│     color      INTEGER       │    │   │     date        TEXT (YYYY-MM-DD) │
│     isDefault  INTEGER 0/1   │    │   │     note        TEXT DEFAULT ''   │
└──────────────────────────────┘    │   │     isIncome    INTEGER 0/1       │
                                    │   │     createdAt   INTEGER (millis)  │
                                    │   └───────────────────────────────────┘
                                    │
┌──────────────────────────────┐    │
│           budgets            │    │
├──────────────────────────────┤    │
│ PK  categoryId INTEGER       │────┘
│ PK  month      TEXT (YYYY-MM)│
│     limitAmount REAL NOT NULL│
└──────────────────────────────
```

---

## SQL DDL

```sql
CREATE TABLE categories (
    id        INTEGER PRIMARY KEY AUTOINCREMENT,
    name      TEXT    NOT NULL,
    icon      TEXT    NOT NULL,
    color     INTEGER NOT NULL,
    isDefault INTEGER NOT NULL DEFAULT 0
);

CREATE TABLE transactions (
    id         INTEGER PRIMARY KEY AUTOINCREMENT,
    amount     REAL    NOT NULL,
    categoryId INTEGER REFERENCES categories(id) ON DELETE SET NULL,
    date       TEXT    NOT NULL,
    note       TEXT    NOT NULL DEFAULT '',
    isIncome   INTEGER NOT NULL DEFAULT 0,
    createdAt  INTEGER NOT NULL
);
CREATE INDEX idx_transactions_categoryId ON transactions(categoryId);
CREATE INDEX idx_transactions_date       ON transactions(date);

CREATE TABLE budgets (
    categoryId  INTEGER NOT NULL REFERENCES categories(id) ON DELETE CASCADE,
    month       TEXT    NOT NULL,
    limitAmount REAL    NOT NULL,
    PRIMARY KEY (categoryId, month)
);
CREATE INDEX idx_budgets_categoryId ON budgets(categoryId);
```

---

## Преобразования типов

Room использует класс `Converters` для отображения:

| Kotlin type | SQLite type | Conversion |
|---|---|---|
| `LocalDate` | `TEXT` | `toString()` / `LocalDate.parse()` |
| `Long` (color) | `INTEGER` | direct |

---

## Предварительно заполненные категории

При первом запуске через AppDatabase в базу данных добавляются 12 категорий по умолчанию `AppDatabase.Callback`:

| Name | Icon | Color |
|---|---|---|
| Food & Dining | restaurant | #E57373 |
| Transport | directions_car | #64B5F6 |
| Shopping | shopping_bag | #BA68C8 |
| Entertainment | movie | #FFB74D |
| Health | local_hospital | #81C784 |
| Utilities | bolt | #FFF176 |
| Housing | home | #4DB6AC |
| Education | school | #A1887F |
| Travel | flight | #4FC3F7 |
| Other | more_horiz | #90A4AE |
| Salary | work | #66BB6A |
| Freelance | laptop | #26C6DA |
