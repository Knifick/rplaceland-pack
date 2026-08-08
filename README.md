# RplaceLand — сборка

Файлы сборки и манифест для [лаунчера RplaceLand](https://github.com/Knifick/rplaceland-pack).

| | |
|---|---|
| Minecraft | 1.21.1 |
| Загрузчик | NeoForge 21.1.248 |
| Java | 21 (лаунчер ставит сам) |
| Модов | 30 |
| Размер | ~128 МБ |

Лаунчер читает `manifest.json` из ветки `main`, а сами файлы качает из Releases.
Игрокам этот репозиторий открывать не нужно — всё происходит автоматически.

## Что где лежит

```
manifest.json     ← лаунчер читает отсюда, адрес зашит в нём
pack/             ← исходная сборка: mods, config, resourcepacks, options.txt
upload/           ← служебное: копии файлов с плоскими именами для Releases
tools/            ← pack.config.json — настройки сборки и новости
```

Releases хранят файлы плоско, без подпапок, поэтому `mods/create-1.21.1-6.0.10.jar`
выкладывается как `mods__create-1.21.1-6.0.10.jar`. В манифесте остаётся настоящий путь —
лаунчер разложит файлы правильно.

## Обновить сборку

1. Меняете моды/конфиги в `pack/`.
2. Поднимаете `packVersion` и пишете `changelog` в `tools/pack.config.json`.
3. Одной командой (из папки лаунчера):

```bash
node tools/pack-publish.mjs --src ./pack --github Knifick/rplaceland-pack --tag pack-НОВЫЙ-ТЕГ --out ./manifest.json
```

4. Создаёте релиз с новым тегом, заливаете `upload/*`, коммитите `manifest.json`.

Подробности — в `PACK.md` репозитория лаунчера.

## Обновить только новость

Новости лежат в `manifest.json`, файлы при этом не трогаются. Правите `news`
в `tools/pack.config.json`, перегенерируете манифест с **тем же тегом** и пушите
только `manifest.json` — игроки ничего не перекачают.
