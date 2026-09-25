Для того чтобы скрипт игнорировал конкретный репозиторий (`other`) при построении языковой статистики, мы можем использовать параметр `plugin_languages_skipped`. А для запуска GitHub Actions при каждом пуше достаточно добавить триггер `push` в блок `on`.

Вот необходимые изменения:

### [*] 1. .github\workflows\metrics.yml

```search
name: Metrics
on:
  schedule: [{cron: "0 0 * * *"}]
  workflow_dispatch:
jobs:
```

```replace
name: Metrics
on:
  schedule: [{cron: "0 0 * * *"}]
  workflow_dispatch:
  push:
jobs:
```

```search
          plugin_languages: yes
          plugin_languages_details: percentage
          output_action: commit
```

```replace
          plugin_languages: yes
          plugin_languages_details: percentage
          plugin_languages_skipped: other
          output_action: commit
```
