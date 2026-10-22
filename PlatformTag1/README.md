# PlatformTag

Мод для Gorilla Tag (BepInEx). Над головой каждого игрока в лобби показывает его платформу и иконку:

- **STEAM** — игроки со Steam / PC
- **OCULUS** — игроки на Quest

Мод только читает данные, которые игра и так отправляет всем в лобби (свойство игрока `platform`). Он не даёт никаких преимуществ в игре, ничего не отправляет на сервер и не меняет геймплей.

> Неофициальный проект. Не связан с Another Axiom. Файлы игры в репозитории не хранятся.

## Установка (готовый мод)

1. Установите BepInEx для Gorilla Tag (проще всего через Monke Mod Manager).
2. Скачайте `PlatformTag.dll` из раздела Releases.
3. Положите его в `Gorilla Tag/BepInEx/plugins/`.
4. Запустите игру.

## Сборка из исходников

Нужны .NET SDK и установленная игра с BepInEx.

```
dotnet build -c Release -p:GameDir="D:\SteamLibrary\steamapps\common\Gorilla Tag"
```

Готовый файл: `bin/Release/netstandard2.1/PlatformTag.dll`.

Путь к игре можно также один раз поменять в `PlatformTag.csproj` (параметр `GameDir`).

## Как это работает

Метод `DetectSteam` в `Plugin.cs` читает у каждого игрока сетевое свойство `platform`. Оно принимает значения `Steam`, `PC` или `Quest`. Игроки со значениями `Steam` и `PC` отображаются как STEAM, остальные как OCULUS. Иконки рисуются кодом, внешние картинки не нужны.

Поиск полей сделан через reflection, чтобы мод переживал небольшие обновления игры. Если после крупного обновления мод перестанет работать, проверьте названия `OwningNetPlayer`, `CustomProperties` и `platform`.

## English

PlatformTag is a BepInEx mod for Gorilla Tag that shows a platform label (STEAM or OCULUS) and an icon above every other player in the lobby. It only reads the `platform` custom property that the game already shares with everyone in the room. It is unofficial and not affiliated with Another Axiom.

Build: `dotnet build -c Release -p:GameDir="<path to Gorilla Tag>"`, then copy `PlatformTag.dll` to `BepInEx/plugins/`.

## Лицензия

MIT, см. файл `LICENSE`.
