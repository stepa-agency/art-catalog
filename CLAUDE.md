# Art Catalog — контекст проекта

Сайт-каталог картин Юлии Каревой (Kareva Yulia) к персональной выставке
**«where the body fades, bitter herbs grow»** — Art Studio MUSE, 15 Galaktion Tabidze St,
Тбилиси, 12–26/09/2026, открытие 12/09 19:00.

## Что где

- `index.html` — весь сайт одним файлом (стили и скрипт inline). Данные работ — массив
  `works` внутри `<script>`, он синхронизируется с `catalog.json` вручную.
- `catalog.json` — источник правды по работам: id, title, technique, dimensions, year,
  price, `priceNote` (например «each» у серии), currency, status (`available` / `sold`),
  photos. Сейчас 20 работ. Массив `works` в `index.html` **генерируется** из него
  скриптом `tools/sync-works.py` (правим каталог, потом гоним скрипт; `--check`
  проверяет, что страница не отстала). Руками массив не трогать.
  Техника пишется в той же форме, что на этикетках: «watercolour on paper».
- `photos/` — фотографии. Работы из каталога лежат под slug-именами
  (`a-face-i-almost-remember.jpg`), свежие из телеграм-бота — под `NNNN_<file_id>.ext`.
- `decor.svg` — подписной декор, с обложки убран 12.09.2026, файл оставлен в репозитории.
- `bot.py` — телеграм-бот: принимает фото с подписями, складывает файлы в `photos/`,
  а записи в `raw_inbox.json` (оба gitignored). Токен в `bot_token.txt` (gitignored).
  Запуск: `python3 bot.py`, дальше он просто поллит getUpdates.
- `.claude/launch.json` — локальный препрокс: `python3 -m http.server 8743`.

## Прод

Живёт на **https://yuliia-kareva-catalogue.vercel.app/** (12.09.2026 переименовали проект
и добавили этот адрес; старый **art-catalog-murex.vercel.app** оставлен и продолжает
работать — оба висят на одном проекте как Production). Источник — GitHub-репозиторий
**github.com/stepa-agency/art-catalog**, Vercel-проект `art-catalog` (команда
`notstepanivanov-1419s-projects`) собирает ветку `main` автоматически, ~15 секунд.

Локальный репозиторий с ним **не связан**: `git remote` пуст, `gh`, `vercel`, `node`
на машине не установлены. Обновление прода делается через веб-интерфейс GitHub —
`github.com/stepa-agency/art-catalog/upload/main`, залить изменённые файлы и
закоммитить прямо в `main` (браузер пользователя залогинен под stepa-agency).
Из-за этого истории коммитов локально и на GitHub расходятся — хеши не совпадают.

**Каждая принятая правка катится на прод сразу** — коммит и выкладка, без отдельного
вопроса. Файлы из подпапок заливать со страницы нужной папки
(`/upload/main/photos`), иначе GitHub положит их в корень дублем.

Диплинк на работу — хеш-якорь из `slugify(title)`, например
`https://yuliia-kareva-catalogue.vercel.app/#a-face-i-almost-remember`. На этот адрес
ведут QR с этикеток.

## Правила по сайту

- Шрифт только **Geist Mono**, весь текст `text-transform: uppercase`.
- Цвета: `--bg #ffffff`, `--ink #141414`, `--muted #6b6a63`.
- Два режима: scroll (одна работа на экран, scroll-snap) и grid (4 колонки на десктопе,
  2 на мобильном), переключатель `#modeToggle` должен оставаться поверх всего и кликабельным.
- Контакт и покупка — инстаграм `@kindermilo`.

## Экспликации (печать)

Макеты в Figma: файл `IimAfmLne4yc5YUgg8P9BV` («Выставка»), страница **«Экспликации»**
(node `6:130`). Все 13 этикеток раскатаны по утверждённому варианту `16:242`.
Формат 100×60 мм при 300 dpi (1 мм = 11.811 px). Ровно два стиля текста: заголовок
Bold 13 pt (−2% трекинг, 98% интерлиньяж) и остальное Regular 7 pt (+4%, 170%).
QR — настоящий вектор (segno → `vectorPaths`, ECC L, только абсолютные `M/L/Z`:
Figma не понимает относительные `h`/`v`), не мельче 15 мм.
