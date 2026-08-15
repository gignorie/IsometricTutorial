
# IsometricTutorial — LibGDX Isometric Game Tutorial Series

Кодовая база для серии учебных примеров по созданию изометрической игры с использованием LibGDX. Проект поставляется мультиплатформенным: общая игровая логика в модуле `core`, с платформенными лаунчерами/проектами для Desktop, Android, HTML и iOS.

## Стек
- Язык: Java (основной)
- Фреймворк/рантайм: LibGDX (gdx 1.9.8 в конфигурации)
- Основные зависимости: LibGDX, Box2D, Ashley (ECS), RoboVM (iOS), GWT (HTML)

## Быстрый запуск

Требования:
- JDK (совместимость исходников указана как 1.6; используйте JDK 8+ для сборки)
- Gradle wrapper включён в репозиторий — сборка через `./gradlew`
- Для Android: Android SDK и файл `local.properties` с `sdk.dir` (или переменная окружения ANDROID_HOME)
- Для iOS: Xcode + поддержка RoboVM (плагин robovm указан в сборке)
- Для HTML: GWT/плагин для сборки web-версии

Основные команды (из корня репозитория):

Собрать всё:
```
./gradlew build
```

Запуск Desktop-приложения (локально):
```
./gradlew :desktop:run
```

Запуск Desktop в режиме отладки:
```
./gradlew :desktop:debug
```

Собрать исполняемый JAR (desktop/dist):
```
./gradlew :desktop:dist
```

Android:
- Подготовка нативных библиотек (если нужно):
```
./gradlew :android:copyAndroidNatives
```
- Установить / собрать APK (требуется Android SDK / локальные настройки):
```
./gradlew :android:assembleDebug
./gradlew :android:installDebug
```
- В репозитории есть пользовательская задача `run` в модуле `android`, которая использует `adb` для запуска лаунчера:
```
./gradlew :android:run
```

HTML:
```
./gradlew :html:build
```
(для развёртывания/создания WAR/веб-ресурсов используйте соответствующие задачи модуля `html` — GWT-плагин присутствует в конфигурации)

iOS:
- Модуль `ios` настроен с плагином RoboVM; сборка / запуск требует macOS и Xcode:
```
./gradlew :ios:build
```
(точные задачи и параметры зависят от установленного плагина RoboVM и Xcode)

Примечание: используйте `./gradlew tasks` внутри конкретного модуля (например, `cd desktop` и `../gradlew tasks`), чтобы увидеть доступные задачи.

## Структура репозитория (верхний уровень)
```
android/     — проект Android (assets, res, manifest, сборочные скрипты)
core/        — общая игровая логика и ресурсы (используется всеми платформами)
desktop/     — Desktop-лаунчер и задачи для запуска/сборки локально
html/        — GWT/веб-реализация (webapp)
ios/         — iOS-лаунчер (RoboVM)
build.gradle — корневая конфигурация (версии зависимостей, определённые проекты)
settings.gradle
gradle/      — wrapper и скрипты Gradle
gradlew*     — Gradle wrapper (Unix + Windows)
```

Как это работает
- Вся общая логика и игровые сущности находятся в `core/`.
- Платформенные модули (`desktop`, `android`, `html`, `ios`) зависят от `core` и содержат только код запуска/интеграции с платформой и биндингами нативных библиотек.
- В `desktop/build.gradle` указана `mainClassName` — `com.isometric.main.desktop.DesktopLauncher`, и есть задачи `run`, `debug`, `dist`.
- Android-модуль содержит задачи для копирования нативных библиотек (`copyAndroidNatives`) и задачу `run`, использующую `adb`.

## Полезные заметки
- В корневом `build.gradle` определены версии: `gdxVersion = '1.9.8'`, `ashleyVersion = '1.7.0'`, `roboVMVersion = '2.3.3'`.
- Код совместим с более старым уровнем sourceCompatibility (1.6) — при необходимости обновите источники/настройки Gradle для современных JDK.
- В репозитории нет файла LICENSE — при публичном использовании/распространении добавьте подходящую лицензию.

## Как помочь / внести изменения
- Изучите `core/src` — туда нужно вносить игровую логику.
- Тестируйте изменения на Desktop (`:desktop:run`) до того, как переносить их в Android/iOS/HTML.
- Если добавляете новые ресурсы, поместите их в `android/assets` (Desktop `desktop` ссылается на эту директорию для запуска).

## Контакты / источники
- Описание репозитория: "Source code for LibGDX: Isometric Game Tutorial Series".
- Основной класс для Desktop: `com.isometric.main.desktop.DesktopLauncher`
- При необходимости добавлю примеры запуска, шаги для CI или шаблон LICENSE.

