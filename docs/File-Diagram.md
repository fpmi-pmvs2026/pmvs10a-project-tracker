```
app/
├── data/
│   ├── api/          NbrbApi (Retrofit)
│   ├── db/           Room entities + DAOs + AppDatabase
│   ├── model/        Domain models (Transaction, Category, Budget, CurrencyRate)
│   └── repository/   TransactionRepository, CategoryRepository,
│                     BudgetRepository, CurrencyRepository, SettingsRepository
├── di/               Hilt AppModule
├── ui/
│   ├── home/         HomeScreen + HomeViewModel
│   ├── add/          AddEditScreen + AddEditViewModel
│   ├── stats/        StatsScreen + StatsViewModel
│   ├── settings/     SettingsScreen + SettingsViewModel
│   └── theme/        Material 3 colour scheme
└── worker/           CurrencyRefreshWorker, BudgetAlertWorker
```
