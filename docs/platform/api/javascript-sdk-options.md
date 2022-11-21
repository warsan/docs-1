---
title: Справочник по параметрам SDK
---

# {{ $frontmatter.title }}

## <var>Project</var> {#project}

Объект, определяющий содержимое и настройки проекта StackBlitz.

| Property | Required |  Type | Description |
| --- | --- | --- | --- |
| `title` | Yes | String | Название проекта. |
| `description` | Yes | String | Краткое описание этого проекта. |
| `template` | Yes | [ProjectTemplate][] (String) | Определяет, как компилируется и выполняется код. |
| `files` | Yes | [ProjectFiles][] (Object) | Файлы проекта и их содержимое. |
| `dependencies` | No | [ProjectDependencies][] (Object) | Указывает зависимости npm (только для [EngineBlock][available_env_docs]). |
| `settings` | No | [ProjectSettings][] (Object) | Поведение при компиляции кода (только для [EngineBlock][available_env_docs]). |

## <var>ProjectTemplate</var> {#projecttemplate}

Строка, представляющая поддерживаемый тип шаблона.

Каждый шаблон имеет свои правила компиляции исходных файлов и требует наличия определенных файлов.

| Template name | Environment | Required files |
| --- | --- | --- |
| `'angular-cli'` | [EngineBlock][available_env_docs] | `index.html` and `main.ts` |
| `'create-react-app'` | [EngineBlock][available_env_docs] | `index.html` and `index.js` |
| `'html'` | [EngineBlock][available_env_docs] | `index.html` |
| `'javascript'` | [EngineBlock][available_env_docs] | `index.html` and `index.js` |
| `'polymer'` | [EngineBlock][available_env_docs] | `index.html` |
| `'typescript'` | [EngineBlock][available_env_docs] | `index.html` and `index.ts` |
| `'vue'` | [EngineBlock][available_env_docs] | `public/index.html` and `src/main.js` |
| `'node'` | [WebContainers][available_env_docs] | _No requirements_ |

## <var>ProjectFiles</var> {#projectfiles}

Обычный объект, представляющий пути к файлам и их содержимое.

- Ключи объектов: строки, представляющие пути к файлам (от корня проекта).
- Значения объектов: строки, представляющие содержимое файла (только текст).

:::warning Поддерживаемые типы файлов
В ProjectFiles поддерживаются только обычные текстовые файлы (включая код, данные и изображения SVG).

Бинарные файлы (такие как архивные форматы, двоичные и исполняемые файлы, растровые изображения, аудио- и видеофайлы) в настоящее время не поддерживаются.
:::

## <var>ProjectDependencies</var> {#projectdependencies}

Обычный объект, представляющий пакеты npm и их версии, которые будут установлены во время выполнения при загрузке проекта.

- Ключи объектов: строки, представляющие имена пакетов npm.
- Значения объектов: строки, представляющие спецификаторы версий пакетов npm.

:::info Различия в окружающей среде
ProjectDependencies используются только в среде [EngineBlock][available_env_docs]. Для WebContainers, пожалуйста, предоставьте файл `package.json`.

Подробнее о [рекомендуемых способах указания зависимостей проекта](/platform/api/javascript-sdk-dependencies) для каждой среды выполнения.
:::

## <var>ProjectSettings</var> {#projectsettings}

Настройки компиляции для проектов [EngineBlock][available_env_docs].

| Property | Type | Description | Default |
| --- | --- | --- | --- |
| `compile.trigger` | `'auto'`, `'save'`, or `'keystroke'` | Определяет, когда изменения источника должны инициировать компиляцию. | `'auto'` |
| `compile.action` | `'hmr'` or `'refresh'` | Определяет, как должны внедряться скомпилированные изменения. | `'hmr'` |
| `compile.clearConsole` | Boolean | Определяет, следует ли очищать консоль после компиляции. | `true` |

В проектах, работающих на [WebContainers][available_env_docs] (которые используют `template: 'node'`), используется только `compile.trigger`. Это влияет на время записи изменений файлов в редакторе в виртуальную файловую систему.

## <var>OpenOptions</var> {#openoptions}

Отображение опций, доступных при открытии проекта в новом окне.

:::tip DEMO
Посмотрите этот демо-ролик, демонстрирующий все доступные открытые опции:

- [TypeScript demo](https://stackblitz.com/edit/sdk-open-embed-sb-projects-with-openoptions-ts)
- [JavaScript demo](https://stackblitz.com/edit/sdk-open-embed-sb-projects-with-openoptions-js)
:::

| Property | Type | Description | Default Value |
| --- | --- | --- | --- |
| `clickToLoad` | Boolean | Показывает диалоговое окно пользовательского интерфейса, предлагающее пользователям запустить проект. | `false` |
| `devToolsHeight` | Number | Устанавливает высоту [Console][ui_docs] (от `0` до `100`). [EngineBlock][available_env_docs] only. | - |
| `forceEmbedLayout` | Boolean | Использовать ли макет вставки или полный макет редактора. *Эта опция устарела и будет удалена в будущем релизе.* | `false` |
| `hideDevTools` | Boolean | Полностью скрывает [Console][ui_docs]. [EngineBlock][available_env_docs] only. | `false` |
| `hideExplorer` | Boolean | Скрывает панель [ActivityBar][ui_docs]. | `false` |
| `newWindow` | Boolean | Открывает проект в новой вкладке. | `true` |
| `openFile` | [OpenFileOption][] (String or Array) | Указывает, какой файл(ы) открыть в редакторе и какие строки кода выделить. | - |
| `origin` | String | StackBlitz Enterprise Edition: устанавливает URL-адрес происхождения экземпляра StackBlitz EE. | - |
| `showSidebar` | Boolean | Показывает [Sidebar][ui_docs] как открытый (`true`) или закрытый (`false`) при загрузке страницы. | - |
| `terminalHeight` | Number | Устанавливает высоту [Terminal][ui_docs] (от `0` до `100`). [WebContainers][available_env_docs] only. | `30` |
| `theme` | [UiThemeOption][] (String) | Устанавливает желаемую цветовую тему. | see [UiThemeOption][] |
| `view` | [UiViewOption][] (String) | Устанавливает начальный вид [UI view][ui_docs]: редактор, предварительный просмотр или и то, и другое. | see [UiThemeOption][] |

## <var>EmbedOptions</var> {#embedoptions}

Отображение опций, доступных при встраивании проекта в iframe.

:::tip DEMO
Посмотрите этот демо-ролик, демонстрирующий все доступные варианты встраивания:

- [TypeScript demo](https://stackblitz.com/edit/sdk-open-embed-sb-projects-with-embedoptions-ts)
- [JavaScript demo](https://stackblitz.com/edit/sdk-open-embed-sb-projects-with-embedoptions-js)
:::

| Property | Type | Description | Default Value |
| --- | --- | --- | --- |
| `clickToLoad` | Boolean | Показывает диалоговое окно пользовательского интерфейса, предлагающее пользователям запустить проект. | `false` |
| `devToolsHeight` | Number | Устанавливает высоту [Console][ui_docs] (от `0` до `100`). Только [EngineBlock][available_env_docs]. | - |
| `forceEmbedLayout` | Boolean | Использовать ли макет вставки или полный макет редактора. *Эта опция устарела и будет удалена в будущем релизе.* | `true` |
| `height` | Number | Устанавливает высоту встроенного iframe. | `300` |
| `hideDevTools` | Boolean | Полностью скрывает [Console][ui_docs]. [EngineBlock][available_env_docs] only. | `false` |
| `hideExplorer` | Boolean | Скрывает панель [ActivityBar][ui_docs]. | `false` |
| `hideNavigation` | Boolean | Скрывает URL-адрес предпросмотра во вставках. | `false` |
| `openFile` | [OpenFileOption][] (String or Array) | Указывает, какой файл(ы) открыть в редакторе и какие строки кода выделить. | - |
| `origin` | String | StackBlitz Enterprise Edition: устанавливает URL-адрес происхождения экземпляра StackBlitz EE. | - |
| `showSidebar` | Boolean | Показывает [Sidebar][ui_docs] как открытый (`true`) или закрытый (`false`) при загрузке страницы. | - |
| `terminalHeight` | Number | Устанавливает высоту [Terminal][ui_docs] (от `0` до `100`). Только [WebContainers][available_env_docs]. | `30` |
| `theme` | [UiThemeOption][] (String) | Устанавливает желаемую цветовую тему. | see [UiThemeOption][] |
| `view` | [UiViewOption][] (String) | Устанавливает начальный вид [UI view][ui_docs]: редактор, предварительный просмотр или и то, и другое. | see [UiViewOption][] |
| `width` | Number | Устанавливает ширину встроенного iframe. | `100%` |

## <var>OpenFileOption</var> {#openfileoption}

Указывает пути к файлам для открытия в редакторе. Это может быть одна строка или массив строк, где каждая строка представляет собой список путей к файлам, разделенных запятыми.

:::tip DEMO
Посмотрите этот демо-ролик, демонстрирующий все доступные варианты открытых файлов:

- [TypeScript demo](https://stackblitz.com/edit/sdk-openfileoption-ts)
- [JavaScript demo](https://stackblitz.com/edit/sdk-openfileoption-js)
:::

Пути к файлам могут включать строки кода, которые нужно выделить, используя формат `{путь}:L{начало}` для одной строки и `{путь}:L{начало}-L{конец}` для диапазона. Любое изменение файла приведет к удалению выделенной области.

Пример с одним файлом:

```js
  // Открывает один файл
  openFile: 'src/App.tsx',
```

Пример с одним файлом с выделенной третьей строкой:

```js
  // Открывает один файл и выделяет третью строку
  openFile: 'src/App.tsx:L3',
```

Пример с одним файлом с выделенным диапазоном (строки 5-8):

```js
  // Открывает один файл и выделяет диапазон
  openFile: 'src/App.tsx:L5-L8',
```

Пример с тремя вкладками редактора (отображается последний файл):

```js
  // Открывает три вкладки редактора с отображением последнего файла
  openFile: 'index.html,package.json,src/App.tsx',
```

Пример с тремя панелями редактора с одной вкладкой в каждой панели:

```js
  // Открывает три боковые панели редактора с одной вкладкой в каждой панели
  openFile: ['index.html', 'package.json', 'src/App.tsx'],
```

Пример с двумя панелями редактора с двумя вкладками в каждой панели:

```js
  // Открывает две панели редактора с двумя вкладками в каждой панели
  openFile: ['index.html,package.json', 'src/App.tsx,src/App.css'],
```

## <var>UiThemeOption</var> {#uithemeoption}

Имя цветовой темы, поддерживаемой встроенным редактором.

| Value | Description |
| --- | --- |
| `'default'` | Использует тему по умолчанию (в настоящее время: `'тёмный'`). |
| `'dark'` | Встроенная тёмная тема. |
| `'light'` | Встроенная световая тема. |

## <var>UiViewOption</var> {#uiviewoption}

Управляет режимом отображения проекта.

Это только декларирует _намерение_, и доступные значения могут вести себя по-разному в зависимости от:

- ширина области просмотра;
- отображается ли проект во вкладке ("стандартный макет") или в iframe ("встроенный макет").

| Value | Description |
| --- | --- |
| `'default'` | Показывает предпросмотр и редактор на больших видовых экранах, редактор только на маленьких видовых экранах |
| `'preview'` | Показывает только предпросмотр (только для макета встраивания) |
| `'editor'` | Показывает только редактор (встраивание и стандартные макеты) |

[available_env_docs]: /guides/user-guide/available-environments
[ui_docs]:  /guides/user-guide/ide-whats-on-your-screen

[embedoptions]: #embedoptions
[openfileoption]: #openfileoption
[openoptions]: #openoptions
[project]: #project
[projectdependencies]: #projectdependencies
[projectfiles]: #projectfiles
[projectsettings]: #projectsettings
[projecttemplate]: #projecttemplate
[uithemeoption]: #uithemeoption
[uiviewoption]: #uiviewoption
