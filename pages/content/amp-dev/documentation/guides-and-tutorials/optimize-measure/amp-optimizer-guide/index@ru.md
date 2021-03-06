---
"$title": Использование AMP-оптимизатора
"$order": '2'
"$hidden": 'true'
description: AMP-оптимизаторы — это класс инструментов, позволяющих оптимизировать страницы на собственном сайте подобно тому, как это делает AMP-кеш. Использование AMP-оптимизатора является залогом достижения высокого уровня удобства страницы и соответствия требованиям Core Web Vitals. Данное руководство рассказывает, как наиболее эффективно оптимизировать AMP-страницы при помощи AMP-оптимизатора.
formats:
- websites
- stories
author: sebastianbenz
---

AMP-оптимизаторы — это класс инструментов, позволяющих оптимизировать страницы на собственном сайте подобно тому, как это делает AMP-кеш. Использование AMP-оптимизатора является залогом достижения высокого уровня [удобства страницы](https://developers.google.com/search/docs/guides/page-experience) и соответствия требованиям [Core Web Vitals](https://web.dev/vitals/). Чтобы подробнее узнать, как работает AMP-оптимизатор, ознакомьтесь с нашим [детальным руководством по AMP-оптимизации](explainer.md).

## Разве AMP-страницы не являются быстрыми изначально?

Возможно, вы думаете: «Секундочку, разве AMP-страницы не должны работать быстро по умолчанию?». Так и есть: среда выполнения AMP оптимизирована для максимальной производительности, и все корректно сформированные AMP-страницы загружаются быстро. Однако вы можете сделать загрузку AMP-страниц в браузере еще быстрее путем их дополнительной оптимизации на сервере.

Первоначально большая часть AMP-страниц загружались из AMP-кешей. Эти кеши дополнительно оптимизировали код страниц, чтобы сделать их просмотр максимально комфортным для пользователя. Однако со временем платформы стали все чаще размещать ссылки на AMP-страницы, а разработчики стали создавать на основе AMP целые сайты. Именно поэтому команда AMP начала разработку AMP-оптимизаторов, чтобы дать владельцам сайтов возможность выдавать с собственного сервера AMP-страницы, чья скорость работы не уступает версиям из AMP-кеша.

## Интеграция AMP-оптимизатора

Есть три способа использовать AMP-оптимизатор:

1. Использовать генератор сайтов или CMS со встроенной интеграцией с оптимизатором.
2. Интегрировать AMP-оптимизатор с используемой системой сборки или сервером.
3. Интегрировать AMP-оптимизатор с используемой средой хостинга.

### CMS и генераторы сайтов

Лучший способ публикации оптимизированных AMP-страниц — это использование генератора сайтов или CMS со встроенной поддержкой AMP-оптимизатора. В этом случае ваши AMP-страницы будут оптимизироваться автоматически. На данный момент интеграцию с AMP-оптимизатором поддерживают следующие генераторы сайтов и CMS:

- [WordPress](https://wordpress.org/) при использовании [плагина AMP для WordPress](https://wordpress.org/plugins/amp/)
- [Next.js](https://nextjs.org/docs/api-reference/next/amp)
- [Eleventy](https://www.11ty.dev/) при использовании [eleventy-amp-plugin](https://blog.amp.dev/2020/07/28/introducing-the-eleventy-amp-plugin/)
- [Хотите добавить свой вариант?](https://github.com/ampproject/amp.dev/issues/new?assignees=&labels=Category%3A+Content%2C+Status%3A+Pending+Triage&template=content.md&title=)

### Самостоятельная интеграция с системой сборки или сервером

Вы также можете самостоятельно выполнить интеграцию AMP-оптимизатора. Существует несколько реализаций AMP-оптимизатора с открытым кодом:

- [AMP-оптимизатор (Node.js)](node-amp-optimizer.md): библиотека на основе Node.js для генерации оптимизированного AMP-кода. Ознакомьтесь с вводным руководством на данном сайте (amp.dev). Данная реализация поддерживается командой AMP.
- [AMP-оптимизатор (PHP)](https://github.com/ampproject/amp-wp/tree/develop/lib/optimizer): библиотека на основе PHP для генерации оптимизированного AMP-кода. Данная реализация поддерживается командой AMP.
- [amp-renderer (Python)](https://github.com/chasefinch/amp-renderer): порт AMP-оптимизатора для Node на Python.

Для страниц, чей рендеринг выполняется динамически на сервере, и для статических сайтов используются разные способы интеграции:

1. **Во время сборки**: страницы статических AMP-сайтов лучше всего оптимизировать на этапе сборки. Этот подход является самым эффективным, поскольку оптимизация AMP-страниц не будет влиять на скорость их выдачи. Ознакомьтесь с [примером интеграции AMP-оптимизатора с Gulp](https://github.com/ampproject/amp-toolbox/tree/main/packages/optimizer/demo/gulp).
2. **Во время рендеринга**: если страницы сайта генерируются динамически или не могут быть преобразованы статическим путем, оптимизацию можно выполнять на сервере после рендеринга AMP-документа. В этом случае, чтобы гарантировать быстрое время загрузки, преобразованные страницы следует кешировать для последующих запросов. Кеширование можно выполнять как на уровне CDN, так и с использованием внутренней инфраструктуры сайта (например, Memcached) или даже на самом сервере, если набор страниц имеет достаточно маленький объем, чтобы уместиться в памяти. Чтобы подробнее узнать об этом подходе, ознакомьтесь с [демонстрацией интеграции AMP-оптимизатора с Express.JS](https://github.com/ampproject/amp-toolbox/tree/main/packages/optimizer/demo/express).

### Интеграция с хостинг-провайдерами

Некоторые хостинг-провайдеры позволяют запускать свою собственную логику при развертывании или выдаче веб-страниц — это может быть отличным способом интеграции AMP-оптимизатора. Примеры такой интеграции:

- [Плагин AMP-оптимизатора для Netify](https://github.com/martinbean/netlify-plugin-amp-server-side-rendering#amp-server-side-rendering-netlify-plugin)
- [Cloudflare Workers](https://workers.cloudflare.com/) ([уже скоро](https://github.com/ampproject/amp-toolbox/issues/878))
- Docker-образ с AMP-оптимизатором ([уже скоро](https://github.com/ampproject/amp-toolbox/issues/879))
- [Хотите добавить свою?](https://github.com/ampproject/amp.dev/issues/new?assignees=&labels=Category%3A+Content%2C+Status%3A+Pending+Triage&template=content.md&title=)
