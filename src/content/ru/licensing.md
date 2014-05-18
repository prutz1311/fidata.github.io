---
title: Лицензирование
author: Basil Peace
copyright: Copyright © 2014  Basil Peace
---

Лицензирование
==============

Основной код будет лицензирован под GPLv3+. Есть желание лицензировать
серверную часть под AGPLv3+. Библиотеки и отдельные модули будут
выпускаться под разными свободными лицензиями, совместимыми с GPL.

Аргументация за GPL:

*	Проект свободный и будет оставаться свободным
*	Проект большой
*	Монетизация проекта под пермиссивной лицензией значительно труднее
*	Мы получаем возможность использовать все лучшие продукты, которые
есть в мире open source

В то же время, проект модульный и требует внимательного подхода к выбору
лицензий на отдельные модули.

Важная часть проекта — движок для подключения модулей наподобие OSGi. Он
будет лицензироваться под пермиссивной лицензией (Apache License 2.0).
Это даст возможность динамически подключать неизвестные заранее модули
под разными лицензиями, в том числе несовместимыми с GPL и
проприетарными. (При условии, что эти модули не будут переиспользовать
код из библиотек под GPL.) Вопрос остаётся, будет ли возможно писать
модули без использования кода под GPL.

Нерешённые вопросы:

*	Возможные проблемы с версией GPL

	Необходимо осмотреть все требуемые нам библиотеки и убедиться, что
мы их можем использовать. Насколько я помню, мне встречались несколько
потенциально полезных библиотек, лицензированных под GPLv2 only.

*	Лицензирование кода сервера (выбор между GPL и AGPL)

	Есть желание выпустить код сервера под AGPL. В сервер будет встроена
функция, предоставляющая его исходный код. Это даст нам возможность
портировать обратно изменения, которые пользователи делают в своих
частных установках.

	Возможная проблема заключается в том, что движок для подключения
модулей не сможет работать в установке под AGPL. Я ещё буду изучать этот
вопрос подробнее.

	Если мы сможем выпустить сервер под AGPL, тогда есть возможность
продавать сборки сервера под GPL по более высокой цене.