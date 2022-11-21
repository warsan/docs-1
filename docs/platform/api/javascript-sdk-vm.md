---
title: Управление вставками с помощью интерфейса VM SDK
---

# {{ $frontmatter.title }}

:::info
Эти методы применимы только к проектам, внедренным на страницу.
:::

Все методы embed [StackBlitz JS SDK][sdk_docs] автоматически подключаются к встроенной StackBlitz <abbr title="Virtual Machine">VM</abbr>, предоставляя вам программный доступ к встроенному проекту.

Используйте виртуальную машину для:

- управлять пользовательским интерфейсом встроенного проекта StackBlitz;
- изменить текущий открытый файл(ы);
- чтение и запись файлов из виртуальной файловой системы проекта.

## Получение доступа к виртуальной машине

:::tip DEMO
Посмотрите этот демонстрационный пример использования виртуальной машины:

- [TypeScript demo](https://stackblitz.com/edit/sdk-vm)
- [JavaScript demo](https://stackblitz.com/edit/sdk-vm-js)
:::

### With <var>embed</var> methods

Методы SDK `embedProject`, `embedProjectId` и `embedGithubProject` возвращают Promise, разрешающий экземпляр класса SDK `VM`. Мы рекомендуем использовать `await` в функции `async` для отслеживания экземпляра виртуальной машины. Например:

```js
import sdk from '@stackblitz/sdk';

async function start() {
  // Встраивает проект и следит за VM
  const vm = await sdk.embedProjectId('embed', 'react-ts');

  // Выполняет действие с VM
  const deps = await vm.getDependencies();
  await vm.applyFsDiff({
    create: {
      'hello.txt': 'Здравствуйте, это новый файл!',
      'deps.txt': JSON.stringify(deps, null, 2),
    },
    destroy: [],
  });
}

start();
```

### With <var>connect<small>(iframe)</small></var> {#connect}

Метод SDK `connect` можно использовать для получения экземпляра `VM` для существующего iframe StackBlitz.

| Argument | Required | Type              | Description                               |
| -------- | -------- | ----------------- | ----------------------------------------- |
| `iframe` | Yes      | HTMLIframeElement | iframe, встраивающий проект StackBlitz. |

Пример:

```js
import sdk from '@stackblitz/sdk';

const EMBED_ID = 'embed';

// Встраивает iframe
sdk.embedProjectId(EMBED_ID, 'react-ts');

// Получает и использует VM при нажатии на кнопку
document.getElementById('test-button').addEventListener('click', async () => {
  const iframe = document.getElementById(EMBED_ID);
  const vm = await sdk.connect(iframe);
  const deps = await vm.getDependencies();
  console.log(deps);
});
```

## Свойства и методы VM

### <var>applyFsDiff<small>(diff)</small></var> {#applyfsdiff}

Обновляет файлы проекта. Возвращает обещание, разрешающееся в `null`.

| Argument       | Required | Type   | Description                                           |
| -------------- | -------- | ------ | ----------------------------------------------------- |
| `diff`         | Yes      | Object | Указывает файлы для создания или удаления                   |
| `diff.create`  | Yes      | Object | Объект с путями к файлам в качестве ключей и содержимым в качестве значений |
| `diff.destroy` | Yes      | Array  | Пути к файлам, которые необходимо удалить                     |

:::info
При изменении существующих файлов новое содержимое измененных файлов должно быть представлено полностью.
:::

Пример:

```js
await vm.applyFsDiff({
  create: {
    'index.js': `console.log('Hello World!')`,
    'package.json': `{ "scripts": { "start": "node index.js" } }`,
  },
  destroy: ['test.js', 'error.log'],
});
```

### <var>getDependencies<small>()</small></var> {#getdependencies}

Получает определенные зависимости проекта. Возвращает обещание, разрешающее объект [ProjectDependencies][].

В проектах [EngineBlock][env_docs] он возвращает зависимости, разрешенные встроенным менеджером пакетов, с точными версиями в качестве значений. Например: `{ 'react': '18.2.0' }`.

_С версии 1.7.0:_ в проекте, работающем на [WebContainers][env_docs], он читает содержимое файла верхнего уровня `package.json` и возвращает объект, объединяющий `dependencies` и `devDependencies`, с исходными спецификаторами версии в качестве значений. Например, `{ 'react': '^18.0.0' }`.

Пример:

```js
const deps = await vm.getDependencies();

if (typeof deps['vue'] === 'string') {
  console.log('Выглядит как проект Vue.js');
}
```

### <var>getFsSnapshot<small>()</small></var> {#getfssnapshot}

Получает снимок файлов проекта и их содержимого. Возвращает обещание, разрешающее объект [ProjectFiles][].

Пример:

```js
const files = await vm.getFsSnapshot();
console.log(files); // { 'index.js': '…', 'package.json': '…', … }
```

### <var>editor.openFile<small>(path)</small></var> {#editoropenfile}

Открывает один или несколько файлов на вкладках и/или разделенных панелях. Возвращает обещание, разрешающееся в `null`.

| Argument | Required | Type                                            | Description                |
| -------- | -------- | ----------------------------------------------- | -------------------------- |
| `path`   | Yes      | [OpenFileOption][] (String or array of strings) | Path(s) of file(s) to open |

Пример:

```js
// открывает один файл
await vm.editor.openFile('src/App.css');

// открывает две панели редактора
await vm.editor.openFile(['README.md', 'index.js']);
```

### <var>editor.setCurrentFile<small>(path)</small></var> {#editorsetcurrentfile}

_С версии 1.7.0. Экспериментальный: точное поведение может измениться._

Устанавливает файл проекта в качестве текущего выбранного файла. Возвращает обещание, разрешающееся в `null`.

| Argument | Required | Type   | Description                        |
| -------- | -------- | ------ | ---------------------------------- |
| `path`   | Yes      | String | Путь к файлу, который нужно установить в качестве текущего |

- Это может обновить выделенный файл в проводнике файлов, а также текущую открытую и/или сфокусированную вкладку редактора.
- Если указанный путь не соответствует открытой в данный момент вкладке, новая вкладка редактора _не_ откроется. См. [`vm.editor.openFile`](#editoropenfile) для открытия файлов.

Пример:

```js
await vm.editor.setCurrentFile('src/App.css');
```

### <var>editor.setTheme<small>(theme)</small></var>

_Начиная с 1.7.0._

Изменяет цветовую тему редактора. Возвращает обещание, разрешающееся в `null`.

| Argument | Required | Type                       | Description           |
| -------- | -------- | -------------------------- | --------------------- |
| `theme`  | Yes      | [UiThemeOption][] (String) | The color theme name. |

```js
await vm.editor.setTheme('light');
```

### <var>editor.setView<small>(view)</small></var>

_Начиная с 1.7.0._

Изменяет режим отображения проекта. Возвращает обещание, разрешающееся в `null`.

| Argument | Required | Type                      | Description            |
| -------- | -------- | ------------------------- | ---------------------- |
| `view`   | Yes      | [UiViewOption][] (String) | Название режима отображения. |

```js
await vm.editor.setView('preview');
```

### <var>editor.showSidebar<small>(visible)</small></var>

_Начиная с 1.7.0._

Изменяет режим отображения боковой панели. Возвращает обещание, разрешающееся в `null`.

| Argument  | Required | Type    | Description                                                |
| --------- | -------- | ------- | ---------------------------------------------------------- |
| `visible` | No       | Boolean | Используйте «true» (по умолчанию), чтобы показать боковую панель, «false», чтобы скрыть. |

```js
await vm.editor.showSidebar(true);
```

### <var>preview.origin</var> {#previeworigin}

Строка с источником (протокол и домен) предварительного просмотра iframe. Каждый проект, созданный с помощью метода embedProject, получает уникальный URL-адрес предпросмотра.

Поскольку заранее неизвестно, будет ли проект работать на веб-сервере (и если да, то на каком порту), `vm.preview.origin` всегда будет `null` в проектах, работающих в [WebContainers][env_docs]. Вместо этого вы можете использовать [`vm.preview.getUrl`](#previewgeturl).

Пример:

```js
if (vm.preview.origin) {
  console.log('Preview is running at ' + vm.preview.origin);
}
```

### <var>preview.getUrl<small>()</small></var> {#previewgeturl}

_С версии 1.7.0. Экспериментально: точное поведение может измениться._

Получает текущий URL-адрес предварительного просмотра. Возвращает обещание, разрешающееся в строку или в `null`.

URL-адрес предварительного просмотра может не отражать точный путь к текущей странице, если код пользователя или страницы инициировал навигацию в окне предварительного просмотра iframe.

В проектах WebContainers URL-адрес предварительного просмотра изначально будет нулевым, пока проект не запустит веб-сервер.

Пример:

```js
const url = await vm.preview.getUrl();

if (url != null && url.startsWith('/about')) {
  console.log('Looks like the About page!');
}
```

### <var>preview.setUrl<small>(path)</small></var> {#previewseturl}

_С версии 1.7.0. Экспериментально: точное поведение может измениться._

Изменяет путь URL-адреса предварительного просмотра. Возвращает обещание, разрешающееся в `null`.

| Argument | Required | Type   | Description                   |
| -------- | -------- | ------ | ----------------------------- |
| `path`   | Yes      | String | Путь URL, начинающийся с `/`. |

Предоставленный путь должен начинаться с `/` и не может изменить источник URL-адреса предварительного просмотра.

В проектах WebContainers вызовы vm.preview.setUrl будут игнорироваться, если в данный момент веб-сервер не запущен.

Пример:

```js
// Переходит на страницу «О программе»
await vm.preview.setUrl('/about');
```

[env_docs]: /guides/user-guide/available-environments
[openfileoption]: /platform/api/javascript-sdk-options#openfileoption
[projectdependencies]: /platform/api/javascript-sdk-options#projectdependencies
[projectfiles]: /platform/api/javascript-sdk-options#projectfiles
[sdk_docs]: /platform/api/javascript-sdk
[uithemeoption]: /platform/api/javascript-sdk-options#uithemeoption
[uiviewoption]: /platform/api/javascript-sdk-options#uiviewoption
