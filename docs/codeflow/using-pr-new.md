---
title: Использование pr.new
---

# {{ $frontmatter.title }}

Вклады в открытый исходный код еще никогда не были такими простыми 🥰 

Эта страница посвящена использованию pr.new для открытия, просмотра и внесения вклада в любой проект через нашу IDE Codeflow или Web Publisher.

## Что такое pr.new?

<!--@include: ./parts/pr-new.md-->

## Как работает pr.new?

Этот короткий URL позволяет получить волшебные впечатления, выбирая именно те инструменты, которые нужны для работы.

Ниже вы узнаете, чего следует ожидать в различных сценариях.

<!-- TODO: graph -->

### Открытие репозитория GitHub

Чтобы открыть репозиторий GitHub с помощью pr.new, посетите его на GitHub и в адресной вкладке браузера добавьте `pr.new` в начало URL, например:

> <a href="https://pr.new/github.com/stackblitz/docs" target="_blank" rel="noopener noreferrer"><b>pr.new/</b>github.com/stackblitz/docs</a>

Вы будете перенаправлены в [Codeflow IDE](./working-in-codeflow-ide), где вы можете работать над [submit a PR](./working-in-codeflow-ide#submitting-a-pr) или просто изучить кодовую базу.

### Открытие конкретного филиала 

Чтобы проверить ветку с pr.new, посетите ее на GitHub и в адресной вкладке браузера добавьте `pr.new` в начало URL, например:

> <b>pr.new/</b>github.com/stackblitz/docs/tree/BRANCH-NAME

Вы будете перенаправлены в [Codeflow IDE](./working-in-codeflow-ide), где вы можете изучить код, продолжить работу или исследовать проблему.

### Обзор PR

Чтобы просмотреть PR с pr.new, посетите поданный pull request на GitHub и в адресной вкладке браузера добавьте `pr.new` в начало URL, например:

> <a href="https://pr.new/github.com/stackblitz/docs/pull/33" target="_blank" rel="noopener noreferrer"><b>pr.new/</b>github.com/stackblitz/docs/pull/33</a>

Вы будете перенаправлены в [Codeflow IDE](./working-in-codeflow-ide) в режиме ["PR review mode"](./working-in-codeflow-ide#reviewing-a-pr-with-codeflow-ide), где вы увидите различия. Вы можете переключиться на стандартный вид файла, выбрав "файл" значок в левой вертикальной навигационной панели.

## "Открыто в Codeflow" кнопка

Чтобы помочь пользователям быстро запустить всю среду с вашим проектом, вы можете добавить кнопку CTA (call-to-action) на свой сайт или в файл README с любой из вышеуказанных ссылок pr.new. 

| Button preview | Direct URL |
| --- | --- |
| <img alt="Open in Codeflow" src="/img/open_in_codeflow.svg" /> | <a href="/img/open_in_codeflow.svg" target="_blank">open_in_codeflow.svg</a> |
| <img alt="Open in Codeflow" src="/img/open_in_codeflow_small.svg" /> | <a href="/img/open_in_codeflow_small.svg" target="_blank">open_in_codeflow_small.svg</a> |

::: tip
Вы можете разместить изображения на своих серверах или напрямую использовать наши URL-адреса изображений.
:::

Чтобы отобразить кнопку в **Markdown файле**, используйте следующий код - не забудьте обновить последний URL на путь к репозиторию проекта:

```md
[![Open in Codeflow](https://developer.stackblitz.com/img/open_in_codeflow.svg)](https:///pr.new/___GH_ACCOUNT__/___GH_REPOSITORY___)
```

Или в HTML:

```html
<a href="https:///pr.new/___GH_ACCOUNT__/___GH_REPOSITORY___">
  <img
    alt="Open in Codeflow"
    src="https://developer.stackblitz.com/img/open_in_codeflow.svg"
  />
</a>
```

Если пользователь вошел в GitHub и StackBlitz (в бета-версии), откроется IDE Codeflow. Никакой дополнительной настройки не требуется. 

## Открытие одного файла

Чтобы отредактировать отдельный файл с помощью pr.new, посетите его в репозитории GitHub и нажмите кнопку "Редактировать". значок (карандаш). Теперь в адресной вкладке браузера добавьте `pr.new` в начало URL, например:

> <a href="https://pr.new/github.com/stackblitz/docs/edit/main/docs/guides/user-guide/what-is-stackblitz.md" target="_blank" rel="noopener noreferrer"><b>pr.new/</b>github.com/stackblitz/docs/edit/main/docs/guides/user-guide/what-is-stackblitz.md</a>

Вы будете перенаправлены на [Web Publisher](./content-updates-with-web-publisher) для более приятного редактирования. Если вы предпочитаете работать в полной среде, нажмите на "Открыть в IDE". и вы будете перенаправлены на [Codeflow IDE](./working-in-codeflow-ide).