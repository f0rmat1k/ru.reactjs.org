---
id: faq-versioning
title: Политика версионирования
permalink: docs/faq-versioning.html
layout: docs
category: FAQ
---

React следует принципам [семантического версионирования (semver)](https://semver.org/lang/ru/).

Это значит, что для номера версии вида **x.y.z**:

* При выпуске **исправлений ошибок**, мы делаем **патч-релиз**, изменяя число **z** (например, с 15.6.2 до 15.6.3).
* При выпуске **новых возможностей** или **несущественных исправлений**, мы делаем **минорный релиз**, изменяя число **y** (например, с 15.6.2 до 15.7.0).
* При выпуске **обратно несовместимых изменений**, мы делаем **мажорный релиз**, изменяя число **x**  (например, с 15.6.2 до 16.0.0).

Мажорные релизы могут содержать новые возможности. Каждый релиз может содержать исправления ошибок.

Минорный релиз — самый распостранённый тип релизов.

### Обратно несовместимые изменения {#breaking-changes}

Обратно несовместимые изменения неудобны для всех, поэтому мы стараемся минимизировать количество мажорных релизов. Например, React 15 был выпущен в апреле 2016 года, а React 16 — в сентябре 2017 года. React 17 ожидается не раньше 2019 года.

Вместо этого мы выпускаем новые возможности в минорных релизах. Это значит, что минорные релизы зачастую более интересны, чем мажорные, несмотря на порядковый номер версии.

### Ответственное отношение к стабильности {#commitment-to-stability}

Изменяя React, мы стараемся упростить изучение новых возможностей. Кроме этого, мы стараемся сохранить работу старых API, даже если требуется их перенос в отдельный пакет. Например, [мы отказались от примесей несколько лет назад](/blog/2016/07/13/mixins-considered-harmful.html), но они до сих пор поддерживаются [через create-react-class](/docs/react-without-es6.html#mixins) и многие проекты продолжают их использовать в стабильном, устаревшем коде.

Больше миллиона разработчиков React используют, поддерживая миллионы компонентов. Только в кодовой базе Facebook более 50 000 React-компонентов. Всё это обязывает нас делать обновления до новых версий как можно проще. Если мы не предоставим возможности для обновления, люди застрянут на старых версиях. Мы тестируем наши *пути обновления* прямо в Facebook -- если наша команда из 10 человек может обновить более 50 тысяч компонентов, мы думаем, что с этим справятся и другие React-разработчики. Во многих случаях для обновления синтаксиса компонентов мы пишем [скрипты автоматизации](https://github.com/reactjs/react-codemod), которые выкладываем в открытый доступ для всеобщего использования.

### Постепенное обновление через предупреждения {#gradual-upgrades-via-warnings}

Сборки в режиме разработки в React включают множество полезных предупреждений. Когда возможно, мы добавляем предупреждения для будущих обратно несовместимых изменений. Таким образом, если ваше приложение не показывает предупреждений в консоли в последнем релизе, значит оно готово к следующей мажорной версии. Это позволяет вам обновлять приложение компонент за компонентом по одиночке.

Предупреждения в режиме разработки не влияют на то, как исполняется ваше приложение. Таким образом, вы можете быть уверены, что ваше приложение будет вести себя одинаково в режиме разработки и продакшен-режиме. Разница лишь в том, что продакшен-сборка не будет показывать предупреждения в консоли, что, к тому же, более производительно. (Если вы вдруг заметили предупреждение в продакшен-режиме, откройте ишью.)

### Что считается обратно несовместимым изменением? {#what-counts-as-a-breaking-change}

Как правило, мы *не* повышаем мажорную версию для следующих изменений:

* **Предупреждения для разработчиков.** Поскольку они не затрагивают поведение в продакшен-режиме, мы можем добавлять или изменять существующие предупреждения между мажорными версиями. Это позволяет нам заранее предупреждать о новых мажорных изменениях.
* **API с приставкой `unstable_`.** Они добавляют экспериментальные возможности, в API которых мы не уверены до конца. Выпуская такие возможности с приставкой `unstable_`, мы можем их обновлять и переходить к стабильному API быстрее.
* **Альфа и канареечные версии React.** Альфа-версии React позволяют попробовать новые возможности раньше. Мы можем вносить в них изменения на основе обратной связи, полученной в период альфа-тестирования. Если вы используете такие версии, имейте в виду, что API может измениться в стабильной версии.
* **Недокументированные API и внутренние структуры данных.** Мы не гарантируем работоспособность кода в случае использования `__SECRET_INTERNALS_DO_NOT_USE_OR_YOU_WILL_BE_FIRED`, `__reactInternalInstance$uk43rzhitjg` или других внутренних переменных.

Наша политика разработана, чтобы быть практичной. Мы не хотим создавать вам головную боль. Если бы мы поднимали мажорную версию слишком часто, то доставили бы множество проблем всему сообществу. И это бы не позволило улучшать React так быстро, как нам хотелось.

Если мы думаем, что изменения могут вызвать проблемы в сообществе, мы постараемся сделать всё возможное, чтобы предоставить плавный переход от старой версии к новой.

### Если минорный релиз не содержит новых возможностей, почему это не патч релиз? {#minors-versus-patches}

Иногда минорный релиз может не включать новых возможностей. [Это допускается семантическим версионированием](https://semver.org/lang/ru/#spec-item-7), в котором говорится, что **"[минорная версия] МОЖЕТ быть увеличена в случае реализации новой функциональности или существенного усовершенствования в приватном коде. Версия МОЖЕТ включать изменения, характерные для патчей."**

Тем не менее, возникает вопрос, почему эти версии не являются патчами.

Ответ прост: любое изменение в React (как и в любой другой программе) несёт определённый риск непредвиденных ситуаций. Представьте ситуацию, в которой выпуск патч-релиза, исправляющий один баг, случайно вносит новый. Подобное не только негативно влияет на разработчиков, но и подрывает их уверенность в будущих патч-релизах. Особенно печально, если исправлялся баг, редко встречающийся на практике.

У нас довольно хороший опыт в выпуске релизов React без багов, но патч-релизы имеют более высокую планку надёжности, поскольку большинство разработчиков предполагают, что они могут быть приняты без негативных последствий.

По этим причинам мы используем патч-релизы только для критических багов и уязвимостей в безопасности.

Если в релиз включены несущественные изменения — такие как внутренний рефакторинг, изменения деталей реализации, улучшение производительности или исправление мелких багов — мы увеличим минорную версию, даже если ничего нового нет.
