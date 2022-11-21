---
title: Руководство администратора
---

# {{ $frontmatter.title }}

:::info
В этом документе подробно рассматривается пользовательская установка и работа с кластером. Для более мягкого введения в процесс установки, пожалуйста, ознакомьтесь с [Quickstart](/enterprise/installation/quickstart).
:::

StackBlitz Enterprise - это приложение Kubernetes. Вы можете установить программное обеспечение на существующий кластер или воспользоваться нашей программой установки, в которую встроен готовый к производству дистрибутив Kubernetes.

## Установка встроенного Kubernetes

Если у вас нет кластера, то наши сценарии установки могут его предоставить. Минимальные требования для этого - 16 vCPU, 32 ГБ памяти и 200 ГБ хранилища под управлением Ubuntu LTS.

```sh
curl -sSL https://k8s.kurl.sh/stackblitz | sudo bash
```

Вы должны быть в состоянии следовать инструкциям на экране к порту 8800 на вашем сервере для настройки вашего экземпляра, добавления дополнительных узлов, проверки обновлений и т.д.

<!-- Если в какой-то момент вы захотите перенести это развертывание на существующий кластер Kubernetes, смотрите [Руководство по миграции существующего кластера] (миграция). -->

## Существующая установка кластера

Если у вас есть существующий кластер, вы можете выполнить следующую команду с рабочей станции, имеющей доступ kubectl к кластеру.

```sh
 curl https://kots.io/install | bash
 kubectl kots install stackblitz
```

Это позволит установить плагин kots (Kubernetes off-the-shelf software) на рабочей станции, затем установить StackBlitz Enterprise Admin Console на кластере и настроить проброс порта на ClusterIP, чтобы вы могли получить доступ к администратору с `http://localhost:8800`. После этого вы пройдете через предсветовую проверку, конфигурацию и первоначальное развертывание приложения.

Если вам необходимо использовать существующий конвейер развертывания (например, внутренний реестр образов, систему контроля версий), внести пользовательские изменения в конфигурацию и/или развернуть в нескольких или удаленных средах, пожалуйста, ознакомьтесь с нашими расширенными инструкциями по установке существующего кластера.

# Устранение неполадок

StackBlitz Enterprise имеет встроенный инструмент для устранения неполадок. На консоли администратора перейдите на вкладку "Устранение неполадок", и вы сможете загрузить пакет поддержки. По умолчанию он будет проходить через серию предварительно построенных анализаторов, чтобы помочь выявить потенциальные проблемы. Если вы не можете устранить проблему, вы можете передать пакет поддержки в нашу службу поддержки, и мы поможем вам выявить любые проблемы с установкой StackBlitz Enterprise.

## Автоматизация операций второго дня

### Использование внутреннего реестра
После установки консоли администратора StackBlitz вы можете настроить ее таким образом, чтобы образы StackBlitz были перемаркированы и перенесены в ваш внутренний реестр для дальнейшего сканирования и многое другое. YAML будет переписан таким образом, что изображения будут извлекаться из указанного внутреннего реестра во время выполнения.

### Хранение
В качестве опции вы можете указать сервер Postgres. Если вы решите принести свой собственный сервер Postgres, он должен быть не ниже Postgres 10.4. Если вы не принесете свой собственный, программа установки предоставит Postgres в качестве набора Stateful в вашем кластере.

## Дополнительные инструменты и процессы

### Изменение развёртывания консоли администратора

Для начала вам нужно начать процесс с развертывания нашей консоли администратора. Консоль администратора - это место, где вы можете предоставить свою лицензию. Консоль администратора остается запущенной после установки и будет местом, где вы сможете проверять наличие обновлений, настраивать приложение, читать заметки о выпуске, генерировать пакеты поддержки и многое другое. Вы можете в любой момент снова открыть панель администратора локально, выполнив команду `kubectl kots admin-console -n $NAMESPACE`.

### Начальная конфигурация

Once the admin console is running, visit `http://localhost:8800` and upload your license. StackBlitz Enterprise is delivered as ready-to-run YAML, but you might need to make some changes for your specific environment. In the Admin Console, click “Config”. This will show a form where you can provide your settings. These will be written as Kubernetes secrets in the deployment manifests.

### Config options

#### DNS Zone

Sets the DNS hostname used to expose the application and its services.

#### Database

Allows you to pick which database to use. By default, an embedded Postgres will be used. You can also choose to provide an inline Postgres or Postgres via a secret.

#### Storage

An embedded Minio is used as bucket by default. You can also provide your own S3-compatible bucket to be used.

You can also configure the bucket names to be used for Turbo, bundle hydration caching, and image storage. 

#### TLS settings

Here you can provide the certificate to be used for domain on which you are hosting your app.

#### Kubernetes settings 

Here you can define the namespace in which you installed the application. For embedded installs, the default should be fine. For 'existing cluster' installs, you should provide the namespace.
