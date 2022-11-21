---
title: POST API
---

# Создание проекта с помощью POST-запроса

Создавайте новые проекты, размещая нужные данные проекта в форме. Этот метод полезен, когда вы не используете или не можете использовать наш JavaScript SDK.

Эта страница поможет вам выполнить настройку. Вы также можете взглянуть на [демонстрационный проект](#demo) в конце.

## Обязательные поля формы

```
project[title] = Название проекта
project[description] = Описание проекта
project[files][FILE_PATH] = Содержимое файла, в качестве ключа укажите путь к файлу
project[files][ANOTHER_FILE_PATH] = Содержимое файла, в качестве ключа укажите путь к файлу
project[dependencies] = JSON-строка поля зависимостей из package.json
project[template] = Может быть одним из: typescript, angular-cli, create-react-app, javascript
```

:::warning
Бинарные файлы (такие как архивы или изображения не-SVG) не поддерживаются для динамически создаваемых проектов.
:::

## Пример полезной нагрузки

Ниже приведен пример HTML-формы, которая генерирует проект из документации RxJS с использованием шаблона `typescript`:

```html
<html lang="en">
<head></head>
<body>

<form id="mainForm" method="post" action="https://stackblitz.com/run" target="_self">
<input type="hidden" name="project[files][index.ts]" value="import { Observable } from 'rxjs/Observable';
import 'rxjs/add/observable/fromEvent';
import 'rxjs/add/operator/scan';

var button = document.querySelector('button');
Observable.fromEvent(button, 'click')
  .scan((count: number) => count + 1, 0)
  .subscribe(count => console.log(`Clicked ${count} times`));
">
<input type="hidden" name="project[files][index.html]" value="<button>Click Me</button>
">
<input type="hidden" name="project[description]" value="RxJS Example">
<input type="hidden" name="project[dependencies]" value="{&quot;rxjs&quot;:&quot;5.5.6&quot;}">
<input type="hidden" name="project[template]" value="typescript">
<input type="hidden" name="project[settings]" value="{&quot;compile&quot;:{&quot;clearConsole&quot;:false}}">
</form>
<script>document.getElementById("mainForm").submit();</script>

</body></html>
```

## Демо

:::tip DEMO
Посмотрите это [демонстрация использования POST API для создания проекта](https://stackblitz.com/edit/sdk-create-via-post-api).
:::
