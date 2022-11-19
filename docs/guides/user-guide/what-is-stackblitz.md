---
title: Что такое StackBlitz?
description: StackBlitz - это мгновенная fullstack web IDE для экосистемы JavaScript. Он работает на базе WebContainers, первой операционной системы на базе WebAssembly, которая загружает среду Node.js за миллисекунды, безопасно в вашей вкладке браузера.
---

# {{ $frontmatter.title }}

StackBlitz - это **постоянная fullstack web IDE** для экосистемы JavaScript. Он работает на базе [WebContainers](https://blog.stackblitz.com/posts/introducing-webcontainers/), первой операционной системы на базе WebAssembly, которая **загружает среду Node.js за миллисекунды**, безопасно внутри вкладки вашего браузера.

Теперь вы можете использовать сеть для создания сети.

## Почему я должен использовать StackBlitz?

StackBlitz безопасен, доступен для совместного использования и приносит удовлетворение.

Нет большего неудобства, чем необходимость возиться с конфигурацией инструментов развертывания и сборки, прежде чем вы сможете приступить к кодированию. **StackBlitz берет на себя все заботы по настройке**: от форка и установки зависимостей до настройки инструментов сборки и горячей перезагрузки. Работа на StackBlitz похожа на работу в вашей локальной среде разработки - за вычетом неприятных моментов.

### Основные характеристики:

- ** непревзойдённая безопасность**: вся разработка происходит во вкладке браузера, включая запуск Node.js и git
- **удивительно быстро**: вся среда разработки загружается за миллисекунды - даже переустановка `node_modules` так же проста, как обновление страницы
- **работает онлайн и офлайн**: продолжать работу, даже если вы потеряли соединение с Интернетом на полпути
- **Ваши приложения всегда онлайн**: Ваши приложения никогда не засыпают и не имеют ограничений по пропускной способности - поделитесь URL-адресом с любым количеством друзей, коллег и сообществ!
- **бесшовная отладка** с помощью Chrome Dev Tools как для внешних, так и для внутренних приложений!

![Preview & debug](./assets/what-is-sb-intro.gif)

## Для чего используется StackBlitz?

### Восхитительные документы

Добавьте интерактивные примеры [из репозитория GitHub](/guides/integration/open-from-github) или [подключите существующий проект StackBlitz](/guides/integration/create-with-sdk) в свои документы, блог или веб-сайт. Помогите пользователям влюбиться в ваш проект с первой попытки.

### Интерактивные игровые площадки

Создайте [стартовый проект](/guides/user-guide/starter-projects) или шаблонный код и дайте своим пользователям попробовать всю мощь вашего проекта. Хотите сделать еще один шаг вперед? Держите его на [пользовательском домене](https://stackblitz.new), чтобы вашим пользователям было еще проще получить к нему доступ.

### Quick demos

Working on a blog post or a conference talk? [Create a StackBlitz project that you can quickly share](/guides/integration/embedding). You can change the project title and the slug to make it effortless for others to reach it. And yes, it works with Medium or DEV.

### Entire programming workflow

One click and our Codeflow IDE spins up a whole code editor with git integration and hot-reloading preview. Now all you need for your dev work is just a browser.

### Straightforward docs editing

Every project deserves collaborative documentation. Typo fixes have never been easier - click, see what you edit as you edit, and submit a PR when you’re satisfied. All in the browser, thanks to Web Publisher.

### Effective bug reproductions

Plain bug descriptions are so 2010s. Welcome to the new era of bug hunting where every report comes with its [own StackBlitz reproduction](/guides/integration/bug-reproductions) so you can instantly filter out true issues from everything else. Never spin up heavy local installations for a simple bug report ever again.

### Build whole educational experiences

You like the idea of running Node.js in the browser and feel inspired to build your own editor? No worries. Our [WebContainers API](/platform/api/webcontainer-api) allows you to use our technology to power your own playgrounds.

### Rapid prototyping

Speed up your entire development process with **realtime hot-reloading in the fastest dev environment ever made**. Collaborate remotely on different devices, send and receive instant feedback, and **get to market faster**.

## What about other online IDEs?

Unlike StackBlitz, legacy online IDEs run on remote servers and stream the results back to your browser. This approach yields **few security benefits** and **provides a worse experience** than your local machine in nearly every way.

**StackBlitz solves these problems by doing all compute inside your browser**. This leverages decades of speed and security innovations and also **unlocks key development and debugging benefits**.

## Get involved

We love our community! Please do stay in touch and:

- Join our supportive community on [the Discord server](https://discord.gg/22zTzrwQrU)!
- Read our [blog](https://blog.stackblitz.com/) and see what we have been up to in our [monthly update posts](https://blog.stackblitz.com/categories/monthly-updates/)!
- Share your StackBlitz projects on [Twitter](https://twitter.com/stackblitz)!
- Reach out to our Developer Advocate on [Twitter](https://twitter.com/sylwiavargas) or via [an email](mailto:devrel@stackblitz.com) with your StackBlitz ideas, dreams, and wishes!
