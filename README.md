# warp-wiki

Сайт документации на [Hwaro](https://github.com/hahwul/hwaro): русскоязычный интерфейс, тёмная и светлая темы с оранжевыми акцентами, адаптивная навигация, оглавление, поиск и копирование кода.

**Адрес после включения Pages:** https://eb-lan.github.io/warp-wiki.github.io/

## Включить публикацию

1. Откройте **Settings → Pages → Build and deployment**.
2. Выберите **Source: GitHub Actions**.
3. Откройте **Actions → Build and deploy warp-wiki → Run workflow**, если первый запуск не смог опубликовать сайт до включения Pages.

При каждом изменении `main` GitHub Actions собирает сайт, проверяет внутренние ссылки и публикует результат. Для pull request выполняются только сборка и проверка. Hwaro закреплён на версии **v0.22.1** полным SHA релиза.

Репозиторий `warp-wiki.github.io` принадлежит пользователю `eb-lan`, поэтому это **сайт проекта** с дополнительным путём `/warp-wiki.github.io/`. Для адреса `https://eb-lan.github.io/` нужен репозиторий `eb-lan.github.io`. После переименования обновите `base_url` в `config.toml`.

## Локальная работа

Установите Hwaro v0.22.1 из [официального релиза](https://github.com/hahwul/hwaro/releases/tag/v0.22.1), затем:

```bash
git clone https://github.com/eb-lan/warp-wiki.github.io.git
cd warp-wiki.github.io
hwaro serve
```

Для проверки production-сборки (Python 3.11+):

```bash
hwaro build
python3 scripts/check_site.py public
```

## Добавить статью

Создайте `content/guides/my-page.md`:

```markdown
+++
title = "Моя статья"
description = "Краткое описание."
weight = 4
+++

## Первый раздел

Содержимое статьи.
```

Статья автоматически появится в меню. Порядок задаёт `weight`. Оглавление наследуется от `_index.md` раздела. Внутренние ссылки: `[Другая статья](@/guides/quick-start.md)`.

Для нового раздела создайте каталог с `_index.md` и задайте `title`, `weight` и `sort_by = "weight"`. Навигация поддерживает разделы первого уровня. Стартовые статьи объясняют ведение wiki; замените или дополните их документацией своего проекта.

## Где менять оформление

- `config.toml` — название, описание, адрес, поиск и параметры Hwaro.
- `templates/` — общие HTML-шаблоны.
- `static/css/site.css` — палитра, размеры и адаптивная вёрстка.
- `static/js/site.js` — тема, мобильное меню, копирование кода и подсветка оглавления.
- `i18n/ru.toml` — локализация поиска Hwaro.

Выбор темы сохраняется в браузере; по умолчанию включена тёмная. Сайт использует системные шрифты и не загружает внешние библиотеки интерфейса.
