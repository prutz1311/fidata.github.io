---
title: Архитектура
author: Basil Peace
copyright: Copyright © 2014  Basil Peace
---

Архитектура
===========

Модульность
-----------

Платформа будет иметь модульную архитектуру. Под модулем я понимаю
набор исполняемых и вспомогательных файлов, доставляемых на компьютер
пользователя. Для развёртывания модулей я планирую использовать
[Qt Installer Framework](http://doc-snapshot.qt-project.org/qtifw-master/index.html).
С точки зрения разработчика модуль может включать как один, так и
несколько артефактов.

В платформу будет встроен движок, подобный OSGi. Он позволит описать
стандартные интерфейсы, которые должны предоставлять модули, и
динамически загружать конкретную реализацию. Примеры того, что может
работать через стандартные интерфейсы:

*	[языки программирования для разработки роботов/ТС](<%= @items["/#{@item[:lang]}/DSL/"].path %>)
*	протоколы для работы с поставщиками данных и организаторами торгов
*	форматы импорта/экспорта данных
*	виды графиков
*	индикаторы ТА
*	численные алгоритмы
*	локализация пользовательского интерфейса

Преимущества модульной архитектуры:

*	**Для пользователей**:

	*	удобство установки и обновления

		Пользователь устанавливает только необходимые ему модули, не
перегружая интерфейс и поддерживая размер установки в разумных
пределах.

	*	возможность использования сторонних модулей под несовместимыми
лицензиями (см.
[Лицензирование](<%= @items["/#{@item[:lang]}/licensing/"].path %>))

	*	удобство написания собственных модулей

*	**Для разработчиков**:

	*	удобство разработки и поддержки

	*	удобство выпуска обновлений

	*	удобство поддержки различных программных и аппаратных платформ
(выпуска платформозависимых версий модулей)

	*	удобство переиспользования готового кода из других проектов

	*	возможность иметь несколько альтернативных реализаций,
сравнивать их по производительности и выбирать лучшие решения


Клиент-серверная архитектура
----------------------------

Платформа будет иметь клиент-серверную архитектуру.

![Архитектура](<%= @items["/#{@item[:lang]}/images/architecture/"].path %>)

С программной точки зрения это будет трёх/четырёхзвенная архитектура.

С аппаратной точки зрения это будет, скорее всего, двухзвенная
архитектура. Если вычисления будут выполняться внутри сервера
приложений, тогда, по моему мнению, будет неэффективно запускать СУБД и
сервер приложений на отдельных компьютерах, так как это потребовало бы
передачи больших объёмов данных по сети. Так же это могло бы потребовать
организации дополнительного временного хранилища внутри сервера
приложений. Подробнее см. ниже.


Конкретные задачи, реализуемые на разных уровнях архитектуры
------------------------------------------------------------

1.	**СУБД**:

	*	Хранение данных

		*	Хранение временных рядов
		*	Хранение метаданных
		*	Хранение данных, получаемых при тестировании ТС
		*	Поддержание целостности данных

	*	(Возможно) Выполнение вычислений (анализ данных)

2.	**Сервер приложений**:

	*	Взаимодействие с клиентами

		*	Авторизация пользователей
		*	Получение команд
		*	Передача результатов вычислений
		*	Трансляция объектов метаданных

	*	Взаимодействие c СУБД

	*	(Возможно) Выполнение вычислений (анализ данных, тестирование
ТС)

	*	Компиляция ТС

	*	Тестирование ТС

		*	Получение реальных данных
		*	Предоставление биржевых протоколов

	*	Генерация отчётов

3.	**Тонкий клиент**:

	*	Взаимодействие с сервером

	*	Редактирование ТС (в форме исходного кода и в графическом виде)

	*	Просмотр и редактирование метаданных

	*	Построение графиков и графический анализ

		*	Получение данных от сервера
		*	Получение реальных данных

	*	Отображение результатов анализа данных и тестирования ТС

4.	**Веб-приложение**:

	*	обычный тонкий клиент

	*	технология, отрисовывающая десктопные окна в веб-страницу


Нерешённые вопросы
------------------

1.	Где следует производить вычисления?

	Теоретически возможно реализовать все вычисления внутри СУБД.

	**Аргументы "ЗА"**:

	1.	СУБД сама по себе способна выполнять отдельные вычисления (к
примеру, арифметические средние, оконные функции). Поэтому есть смысл
выполнять существующие в них алгоритмы на GPU.

	2.	СУБД с развитыми процедурными языками и возможностью подключения
библиотек на C (такая, как PostgreSQL) позволяет реализовать все
вычисления внутри СУБД.

	3.	Если выполнять вычисления только внутри СУБД, тогда возможно
реализовать трёхзвенную аппаратную архитектуру.

	**Аргументы "ПРОТИВ"**:

	1.	Нам необходимы оба метода вычислений:

		*	Вычисления на исторических данных

			Для ускорения работы эффективно рассчитать нужный индекс
на большом объёме данных, используя GPU.

		*	Вычисления на реальных данных

			Использовать GPU для расчёта одного числа неэффективно и
бессмысленно.

		Реализация внутри СУБД всё ещё требует реализации того же
алгоритма в отдельной библиотеке, подгружаемой роботом.

	2.	Реализация внутри СУБД сложнее для отладки и поиска багов.

	3.	Пока не очень понятно, как модульная архитектура могла бы
ужиться внутри СУБД. Не понятно, как будет выполняться установка,
обновление или удаление отдельных модулей.

	4.	У реализации вычислений внутри СУБД могут быть другие подводные
камни, о которых я пока не знаю.

2.	<a name="problem_compilation"></a>**Компиляция робота/ТС**

	Возможность компиляции означает, что платформа должна иметь
встроенный компилятор. Компилятор должен быть совместимым с тем, который
[использовался для компиляции платформы и библиотек](<%= @items["/#{@item[:lang]}/development_and_building/"].path %>#C_CPP_compiler).
Для С/С++ или языка на их основе мы не можем и не будем встраивать в
платформу MSVC. Однако, это нарушает
[требование работы «из коробки»](<%= @items["/#{@item[:lang]}/requirements/"].path %>#work_out_of_the_box).

	**Варианты решения**:

	*	Отказаться от компиляции в пользу интерпретации.

	*	Интерпретировать код на платформе и сделать возможность
генерации текста на C/C++ или в каком-то промежуточном формате для
самостоятельной компиляции в бинарники пользователем.

	*	Не включать в поставку никаких компиляторов. Использовать
компилятор, найденный на машине пользователя. (Не удовлетворяет
требованию работы «из коробки»).

	*	Использовать для написания роботов не-С/С++ язык (например,
Pascal).

	**Рассматриваемое решение**: требовать от пользователей Windows
установленную Visual Studio. Express-версия бесплатна и может быть
установлена пользователем самостоятельно. Поскольку:

	*	мы разрабатываем свободное ПО,
	*	необходимо поощрять пользователей Windows переходить на
свободные платформы,
	*	даже пользователи Windows будут часто запускать роботов на
серверах под управлением GNU/Linux, и возможности компиляции под Windows
будут ещё менее востребованы,
	*	других возможностей (помимо выбора другого языка), видимо, не
существует,

	то возможно сделать некоторые ограничения для ярых поклонников
Windows.

3.	<a name="problem_online_data"></a>**Архитектура подсистемы
получения онлайн-данных**

	1.	Как будут получаться данные клиентом (через сервер или напрямую
от биржи)?
	2.	Как данные будут записываться в базу данных на сервере?
	3.	Как данные будут распределяться на сервере между базой данных и
тестируемыми в данный момент ТС?
	4.	Как будут вычисляться индикаторы в реальном времени?

	Возможно, здесь нужен какой-то кэш или перераспределитель данных.
См. как это сделано в kdb+:
<http://kx.com/_papers/Kx_White_Paper-2013-131023.pdf>.
