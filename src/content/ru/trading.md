---
title: Трейдинг
author: Basil Peace
copyright: Copyright © 2014  Basil Peace
---

Трейдинг
========

Эта страница содержит информацию, которая имеет отношение к разработке
проекта и может быть полезной для людей, не знакомых с трейдингом.

Подходы к трейдингу
-------------------

*	Трейдинг по интуиции — нас не интересует

*	Механический трейдинг — предмет нашего интереса

	<table><thead>
		<tr>
			<td>Вид трейдинга</td>
			<td>Реализация ТС</td>
			<td>Кто выполняет анализ рынка</td>
			<td>Кто принимает решения и совершает сделки</td>
		</tr>
	</thead><tbody>
		<tr>
			<td>Ручной механический трейдинг</td>
			<td>Механическая торговая система</td>
			<td>Трейдер</td>
			<td>Трейдер</td>
		</tr>
		<tr>
			<td>Полуавтоматический трейдинг</td>
			<td>Советник</td>
			<td>Компьютер</td>
			<td>Трейдер</td>
		</tr>
		<tr>
			<td>Полностью автоматический трейдинг</td>
			<td>Робот</td>
			<td>Компьютер</td>
			<td>Компьютер</td>
		</tr>
	</tbody></table>

Научно-эмпирический взгляд на трейдинг
--------------------------------------

*	Трейдинг является способом эмпирической проверки гипотез
определённого вида.
*	В трейдинге проверяются гипотезы о наличии опережающей корреляции
между информацией, известной в какой-то момент времени, и будущим
движением цен финансовых инструментов.
*	Гипотеза формулируется в виде торговой системы.
*	Гипотеза не может быть доказана, но может быть опровергнута
(критерий фальсифицируемости).
*	Результаты проверки гипотезы выражаются в денежных суммах или в
процентных доходностях. Таким образом, у нас есть не только критерий
для опровержения любой гипотезы, но и численные критерии для измерения
предпочтительности одной гипотезы другой.
*	Никакое число успехов не доказывает верность гипотезы.
*	Неуспешность ТС на исторических данных опровергает гипотезу.
*	Неуспешность ТС на реальных данных опровергает гипотезу. Стоп-лоссы
и постоянный статистический контроль качества защищают от разорительных
чёрных лебедей.
*	Пока гипотеза не опровергнута, она используется для торговли с целью
попытки её опровержения.
*	После опровержения одной гипотезы трейдер формулирует новую.
Новая гипотеза должна быть успешной и там, где преуспела предыдущая
(работать на тех же исторических данных), и там, где предыдущая
потерпела неудачу. Обычно новая гипотеза обобщает предыдущую, включая её
как частный случай. Это может быть сделано через введение структурного
сдвига или введение нестационарности переменных, до этого полагавшихся
стационарными.

### Литература

1.	Карл Р. Поппер. *Объективное знание. Эволюционный подход*.
2.	Нассим Николас Талеб. *Чёрный лебедь. Под знаком непредсказуемости*.

#### <a name="SQC_in_trading"></a>Статистический контроль качества в
трейдинге

1.	Andrew Kumiega, Benjamin Van Vliet. *Quality Money Management*.
2.	Andrew Kumiega, Ben Van Vliet. A Software Development Methodology
for Research and Prototyping in Financial Markets. URL:
<http://arxiv.org/abs/0803.0162>.
3.	Andrew Kumiega. Software project managemеnt for building high
frequency trading systems // Northwestern University, MSIT Tribune
Presentation. 2011, November 12. URL:
<https://www.infotech.northwestern.edu/KumiegaNorthwestern.ppt>.

Алгоритм трейдинга
------------------

![Алгоритм трейдинга](<%= @items["/#{@item[:lang]}/images/algorithm_of_trading/"].path %>)

Более точно, работа трейдера организована по спиральной модели.
Подробнее об этом см. в литературе по статистическому контролю качества
в трейдинге (список [выше](#SQC_in_trading)).