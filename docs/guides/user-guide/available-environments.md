---
title: Доступные среды
description: "Существует два вида сред, в которых выполняются проекты в StackBlitz: EngineBlock и WebContainers. Каждый проект в StackBlitz связан с тем или иным проектом."
---

<script setup lang="ts">
  import SupportIcon from '@theme/components/SupportIcon.vue';
</script>

# {{ $frontmatter.title }}

Существует два вида сред, в которых выполняются проекты в StackBlitz: **EngineBlock** и **WebContainers**. Каждый проект в StackBlitz связан с тем или иным проектом.

В зависимости от среды, StackBlitz IDE включает немного разные функции и элементы пользовательского интерфейса. Обзор обеих сред приведен в таблице ниже - или вы можете напрямую обратиться к разделу [EngineBlock](#engineblock) или [WebContainers](#webcontainers).

| Feature | EngineBlock | WebContainers |
| --- | --- | --- |
| Supported frameworks | <SupportIcon value="star-half" label="" /> Front-end | <SupportIcon value="star" label="" /> Front-end & back-end |
| Supported package managers | <SupportIcon value="star-half" label="" /> Turbo v1 | <SupportIcon value="star" label="" /> Turbo v2, pnpm, yarn v1 |
| Full Node.js environment | <SupportIcon value="no" label="Not available" /> | <SupportIcon value="yes" label="Available" /> |
| Classic editor | <SupportIcon value="yes" label="Available" /> | <SupportIcon value="yes" label="Available" /> |
| [Codeflow IDE](/codeflow/working-in-codeflow-ide) (beta) | <SupportIcon value="no" label="Not available" /> | <SupportIcon value="yes" label="Available" /> |
| [Web Publisher](/codeflow/content-updates-with-web-publisher) (beta) | <SupportIcon value="no" label="Not available" /> | <SupportIcon value="yes" label="Available" /> |
| Shareable preview URL | <SupportIcon value="yes" label="Available" /> | <SupportIcon value="no" label="Not available" /> |
| [Console](/guides/user-guide/ide-whats-on-your-screen#console) | <SupportIcon value="yes" label="Available" /> | <SupportIcon value="no" label="Not available" /> |
| [Terminal](/guides/user-guide/ide-whats-on-your-screen#terminal) | <SupportIcon value="no" label="Not available" /> | <SupportIcon value="yes" label="Available" /> |

Чтобы изучить эти различия на практике, мы взяли проект React и превратили его в:

- [проект React, работающий на EngineBlock](https://stackblitz.com/fork/react)
- [проект React, работающий на WebContainers](https://vite.new/react) (powered by Vite)

### Моторный блок

EngineBlock - это пользовательская среда выполнения на основе [SystemJS](https://github.com/systemjs/systemjs#systemjs), способная запускать популярные front-end фреймворки и библиотеки. В зависимости от того, хотите ли вы, чтобы другие взаимодействовали с кодовой базой или приложением, вы можете выбрать, поделиться ссылкой на редактор или предварительный просмотр приложения.

Обратите внимание, что эта среда запускает пользовательский процесс сборки и не совместима с Node.js.

Время выполнения EngineBlock работает со всеми основными браузерными движками.

### WebContainers

> 💡 [Читайте недавний анонс WebContainers] (https://blog.stackblitz.com/posts/webcontainers-are-now-supported-on-firefox/)

Будучи средой исполнения, ориентированной на создание собственной среды Node.js, WebContainers способны запускать инструментальные цепочки Node.js, включая Webpack или Vite. Используя один из этих инструментов, вы можете работать с любым front-end фреймворком так же, как и в локальной среде. WebContainers, однако, также поддерживают различные back-end фреймворки, а также другие инструменты ([включая `sqlite3`](https://blog.stackblitz.com/posts/introducing-sqlite3-webcontainers-support/)!).

Что касается вариантов совместного использования, вы можете поделиться только ссылкой на редактор, поскольку для предварительного просмотра требуется запущенный редактор. Предварительный просмотр виден в окне редактора.

В этой среде есть терминал, который поддерживает различные обычные команды, которые можно выполнить локально.

В настоящее время WebContainers поддерживаются браузерами на базе Chromium и [в Firefox, с некоторыми оговорками](/platform/webcontainers/browser-support).

Наша [Codeflow IDE](/codeflow/what-is-codeflow) работает на среде исполнения WebContainers.
