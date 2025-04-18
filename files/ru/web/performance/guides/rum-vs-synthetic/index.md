---
title: "Мониторинг производительности: реальные пользователи и их эмуляция"
slug: Web/Performance/Guides/Rum-vs-Synthetic
---

{{QuickLinksWithSubPages("Web/Performance")}}

**Синтетический мониторинг** и **мониторинг реальных пользователей (Real User Monitoring, RUM)** - два способа мониторинга и получения данных о веб-производительности. Эти два подхода дают два разных обзора производительности и каждый имеет свои преимущества, области применения и минусы. RUM, в основном, лучше подходит для понимания долгосрочных трендов, в то время как синтетический мониторинг хорошо подходит для тестирования регрессий, их быстрого обнаружения и быстрой реакции на них в процессе разработки. В этой статье мы определим и сравним оба подхода.

## Синтетический мониторинг

Синтетический мониторинг включает в себя мониторинг производительности в "лабораторных" условиях, обычно с помощью автоматизированных инструментов в цельном окружении. Такой подход включает в себя создание скриптов, симулирующих путь, который может пройти пользователь, пользуясь приложением. Таким образом тестируются не настоящие пользователи, но заранее определённый набор инструкций, который выполняется в предопределённом окружении.

Пример такого мониторинга - [WebPageTest.org](https://WebPageTest.org). Ресурс предоставляет контролируемое окружение, где вы определяете географию, сеть, устройства, браузеры и кешированные данные. Сервис предоставляет Waterfall график для каждого ресурса, который используется в вашем приложении и грузится сторонними библиотеками (например, рекламными или аналитическими инструментами).

Контролируя переменные окружения, вы можете понять, где в производительности узкие места и каковы их источники. Однако, все эти данные не отражают реальный пользовательский опыт, особенно если поведение пользователя не ограничивается только лишь просмотром страницы.

Синтетический мониторинг может быть важным компонентом тестирования регрессий и средством мониторинга выпущенного и работающего приложения. Ухудшение базовых метрик производительности в ходе CI/CD-процесса должно вести к приостановке релиза, по крайней мере до тех пор, пока не выяснится, почему метрики ухудшились. Если проблема возникает только в Production-режиме, синтетические тесты предоставят информацию, которая поможет идентифицировать, изолировать и решить проблему, прежде чем она отразится на пользователях.

## Мониторинг реальных пользователей (RUM)

**Мониторинг реальных пользователей (Real User Monitoring, RUM)** измеряет производительность приложения на устройствах конечных пользователей. В основе подхода - сторонний скрипт, который вставляет другие скрипты на каждую страницу. Эти дополнительные скрипты измеряют производительность и предоставляют отчёты о ней. Этот подход помогает не только узнать, насколько производительно приложение, но и даёт информацию об использовании приложения, например, о географии, распределении пользователей или влиянии такого распределения на пользовательский опыт.

В отличие от синтетического мониторинга, RUM собирает данные от настоящих пользователей, вне зависимости от их устройств, браузеров, сети или геолокации. Пока пользователь взаимодействует с приложением, тайминги такого взаимодействия записываются, вне зависимости от того, какое действие выполняется в конкретный момент. Такой мониторинг собирает данные о реальном использовании приложения, а не о том поведении, которое ожидают разработчики или, скажем, отдел маркетинга. Это особенно важно для больших веб-сайтов или сложных приложений, где функциональность или содержимое постоянно меняются, а количество пользователей может очень сильно расти, создавая новые нагрузки и требования.

Используя RUM, бизнес может лучше понять своих клиентов и определить зоны сайта, которые требуют большего внимания. Более того, RUM может помочь понять географию или канал распространения приложения. Знание своих пользователей и трендов поможет вам выстроить бизнес-планы и думать наперёд, позволяя вам определить приоритетные зоны, которые требует оптимизации и улучшения производительности.

## Сравнение подходов

Синтетический мониторинг хорошо подходит для отлавливания регрессий в ходе разработки приложения. Особенно полезным может оказаться занижение скорости сети ({{glossary('network throttling')}}). Такой подход довольно прост, недорог и великолепно подходит для тестирования определённых точек приложения по мере того, как вы вносите изменения в код. Но он даёт лишь узкий обзор производительности и не говорит о том, что испытывает пользователь.

Тестирование на реальных пользователях, в свою очередь, даёт информацию о настоящих пользователях, которые используют приложение или веб-сайт. И хотя получение и обработка таких данных обходится дороже и не так проста, такой подход даёт жизненно важные данные о пользовательском опыте.

## API для измерения производительности

Существует множество сервисов мониторинга. Если вы хотите создать свой сервис, взгляните на следующие API: не только {{domxref("PerformanceNavigationTiming")}} и {{domxref("PerformanceResourceTiming")}}, но также {{domxref("PerformanceMark")}}, {{domxref("PerformanceMeasure")}}, и {{domxref("PerformancePaintTiming")}}.
