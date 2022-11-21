---
title: Управление зависимостями с помощью SDK
---

# {{ $frontmatter.title }}

При создании новых проектов с помощью методов [`sdk.openProject`](/platform/api/javascript-sdk#openproject) и [`sdk.embedProject`](/platform/api/javascript-sdk#embedproject) можно указать, какие зависимости npm должны быть установлены при запуске.

Предполагаемый способ указания зависимостей зависит от [среды выполнения](/guides/user-guide/available-environments).

:::info Напоминание
Проекты, созданные с помощью `шаблона: Опция 'node'` будет использовать среду WebContainers (в настоящее время только на stackblitz.com). Проекты, созданные с другим значением `template`, будут использовать среду EngineBlock (доступна на stackblitz.com и StackBlitz Enterprise Edition).
:::

## С помощью WebContainers

Для проекта WebContainers наш [Turbo package manager](/platform/webcontainers/turbo-package-manager) будет устанавливать `dependencies` и `devDependencies` из файла проекта `package.json`, подобно тому, как это делают `npm`, `pnpm` или `yarn`.

Для этих проектов вы можете указать свои зависимости непосредственно в файле `package.json` и игнорировать опцию `project.dependencies`. Вот пример:

```js
import sdk from '@stackblitz/sdk';

const packageJson = `{
  "name": "node-starter",
  "version": "0.0.0",
  "scripts": {
    "start": "serve public"
  },
  "dependencies": {
    "serve": "^14.0.0"
  }
}`;

const project = {
  title: 'Node serve demo',
  description: 'Node.js server demo using the "serve" package',
  template: 'node',
  files: {
    'package.json': packageJson,
    'public/index.html': '<h1>Hello world!</h1>',
  },
};

sdk.openProject(project);
```

:::tip DEMO
Посмотрите этот полный проект Angular:

- [TypeScript demo](https://stackblitz.com/edit/sdk-webcontainers-dependencies-ts)
- [JavaScript demo](https://stackblitz.com/edit/sdk-webcontainers-dependencies-js)
:::

## С помощью EngineBlock

Для проектов EngineBlock укажите зависимости, используя опцию `project.dependencies`. Файл `package.json` не будет использоваться для разрешения зависимостей, но все же настоятельно рекомендуется предоставить его, чтобы ваш проект продолжал работать как ожидается при загрузке с правильными `devDependencies` и `scripts`. Вы можете настроить `devDependencies` и другие свойства `package.json`, но зависимости для EngineBlock всегда определяются с помощью `project.dependencies`, а не `package.json`.

### Зависимости плюс package.json

В следующем примере мы покажем, как сгенерировать этот проект:

<img
  width="1000"
  src="./assets/sdk-project-dependencies.png"
  alt="Screenshot of a project showing three packages in the “Dependencies” section of the sidebar, and an editor tab with the same dependencies in a package.json file."
/>

Поскольку мы не хотим рисковать несовпадением зависимостей, мы сначала определим данные `package.json`, а затем используем их для установки `project.dependencies`.

```js
import sdk from '@stackblitz/sdk';

const PACKAGE_JSON = {
  name: 'cool-project',
  version: '0.0.0',
  private: true,
  dependencies: {
    gsap: '^3.11.0',
    jquery: '^3.6.0',
    lodash: '^4.17.21',
  },
};

const project = {
  title: 'My cool project',
  description: 'Example animation project',
  template: 'javascript',
  // ТРЕБУЕТСЯ: указать зависимости
  dependencies: PACKAGE_JSON.dependencies,
  files: {
    // Рекомендуется: предоставить файл package.json с теми же зависимостями
    'package.json': JSON.stringify(PACKAGE_JSON, null, 2),
    'index.html': '<h1>Hello world!</h1>',
    'index.js': 'import gsap from "gsap";\n// etc.',
  },
};

sdk.openProject(project);
```

:::tip DEMO
Посмотрите этот полный проект Angular:

- [TypeScript demo](https://stackblitz.com/edit/sdk-angular-dependencies?file=project.ts)
- [JavaScript demo](https://stackblitz.com/edit/sdk-angular-dependencies-js)
:::

### Наследуемые зависимости

Полезной, но иногда запутанной особенностью значения `project.template` является то, что оно получает начальный список зависимостей из "родительского" проекта. Например, при использовании `template: 'angular-cli'` опция для генерации проекта Angular на stackblitz.com, изначально будут использоваться зависимости и номера версий с сайта https://stackblitz.com/edit/angular.

В настоящее время нет возможности контролировать, какой проект выбирается в качестве "родительского" для заданного значения `template`.

В некоторых случаях унаследованные зависимости могут стать причиной появления вашего проекта:

- ненужные зависимости;
- устаревшие версии пакетов.

Чтобы обойти эту проблему, мы рекомендуем указать все зависимости и диапазоны версий, которые использует ваш проект, с помощью опции `project.dependencies`.
