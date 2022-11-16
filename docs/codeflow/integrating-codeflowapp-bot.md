---
title: Интеграция CodeflowApp Bot
---

# {{ $frontmatter.title }}

На этой странице рассказывается об интеграции CodeflowApp Bot в ваши репозитории GitHub.

## Что такое CodeflowApp Bot?

<!--@include: ./parts/codeflowapp-bot.md-->

### Pull requests
После интеграции он будет комментировать каждый PR со ссылкой для мгновенного запуска и просмотра:

<img lang="en" src="./assets/codeflowapp-pr.jpg" alt="CodeflowApp bot in action" style="max-width: 550px"/>

### Вопросы

При каждом открытии проблемы CodeflowApp проверяет, присутствует ли в тексте комментария URL-адрес воспроизведения ошибки с сайта stackblitz.com.

Если URL воспроизведения присутствует, CodeflowApp прокомментирует его с помощью комментария "Исправьте эту проблему". кнопка, позволяющая начать новый запрос на исправление ошибки с ее воспроизведением в дочерней папке рядом с каталогом вашего репозитория для тестирования в реальном времени:

<img lang="en" src="./assets/codeflowapp-issue.jpg" alt="CodeflowApp bot in action" style="max-width: 550px"/>

## Установка бота CodeflowApp

Чтобы установить бота CodeflowApp на репозиторий, вы установите его с помощью GitHub UI.

1. Посетите [страницу профиля CodeflowApp](https://stackblitz.com/install-github-app)
2. Выберите учетную запись или организацию, а также репозитории, к которым вы хотите предоставить доступ боту. 
  - Если вы выберете "all in Organization", бот CodeflowApp будет установлен на все репозитории в вашей организации.
  - Пожалуйста, не волнуйтесь - если вы передумаете, вы можете изменить доступ к боту или полностью отключить его!

<!--@include: ./parts/installing-codeflowapp.md-->

## Отключение бота CodeflowApp

После установки бот будет включен по умолчанию в хранилище и будет срабатывать всякий раз, когда появится новый PR или проблема.

Чтобы отключить бота:

1. Создайте папку `.stackblitz` в корневом каталоге проекта.
2. Внутри этой папки создайте файл `codeflow.json`, указав, какие действия вы хотите отключить:

```json
// .stackblitz/codeflow.json

{
    "bot": {
        "issues": {
            "enabled": false
        },
        "pullRequests": {
            "enabled": false
        }
    }
}
```

Кроме того, вы можете приостановить или удалить бота [через пользовательский интерфейс GitHub](https://docs.github.com/en/developers/apps/managing-github-apps/deleting-a-github-app).


## Включение переопределения пакетов для воспроизведения проблем

Codeflow позволяет пользователям указывать, какие пакеты они хотят переопределить в `package.json` и где эти пакеты расположены. Переопределение pnpm - это то, что будет установлено при запуске pnpm i вместо того, что определено в файле package.json.

:::info pnpm override
[pnpm override](https://pnpm.io/package_json#pnpmoverrides) "инструктирует pnpm отменить зависимость в графе зависимостей. Это полезно для того, чтобы заставить все ваши пакеты использовать одну версию зависимости, сделать бэкпорт исправления или заменить зависимость форком."
:::

### сценарий использования pnpm override

Например, в Vite поступает выпуск с репродукцией StackBlitz.
1. Мейнтейнер открывает проблему в Codeflow IDE. Codeflow IDE извлекает воспроизведение, определенное в выпуске, помещает его в папку воспроизведения, и
считывает файл `codeflow.json`. 
2. Если в этом файле определены переопределения, Codeflow добавляет их в файл `package.json`. Так, например, вместо извлечения Vite из npm, он свяжет локальный проект vite с этим воспроизведением.
3. The maintainer can then run `pnpm i` in the repro and pnpm will install the dependencies defined in the override.

:::info TL;DR
Using pnpm override, you can fix a bug and immediately try it out in the reproduction the user provided.
:::

### Enabling pnpm overrides

To set up pnpm overrides, follow these steps:
1. In the project's root directory, create `.stackblitz` directory.
2. Inside it, create a file called `codeflow.json`.
3. In the file, specify the overrides by providing a key-vaue pair of the dependency to override and the folder where it is located. Please note that the location is relative to the root of the project.

```json
// .stackblitz/codeflow.json

{
    "pnpm": {
        "overrides": {
            "vite": "./packages/vite"
        }
    }
}
```
