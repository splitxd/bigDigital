# АНАЛИЗ ДАННЫХ В РАЗРАБОТКЕ ИГР [in GameDev]
Отчет по лабораторной работе #5 выполнил(а):
- Христолюбов Данил Александрович
- РИ-230932

Отметка о выполнении заданий (заполняется студентом):

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 60 |
| Задание 2 | * | 20 |
| Задание 3 | * | 20 |

знак "*" - задание выполнено; знак "#" - задание не выполнено;

Работу проверили:
- к.т.н., доцент Денисов Д.В.
- к.э.н., доцент Панов М.А.
- ст. преп., Фадеев В.О.

[![N|Solid](https://cldup.com/dTxpPi9lDf.thumb.png)](https://nodesource.com/products/nsolid)

[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)

Структура отчета

- Данные о работе: название работы, фио, группа, выполненные задания.
- Цель работы.
- Задание 1.
- “коэффициент корреляции ”.
- Задание 2.
- Параметры файла yaml-агента.
- Задание 3.
- Примеры задач.
- Выводы.

## Цель работы
Изучить ML Agent'ы  на примере, изучить их параметры, предположить в чем
они необходимы.


## Задание 0
### Ход работы

#### Часть 1
![succes](https://github.com/splitxd/bigDigital/blob/main/HW5/succes.png)
![2models](https://github.com/splitxd/bigDigital/blob/main/HW5/2models.png)
![9models](https://github.com/splitxd/bigDigital/blob/main/HW5/9models.png)
![27models](https://github.com/splitxd/bigDigital/blob/main/HW5/27models.png)
![learning](https://github.com/splitxd/bigDigital/blob/main/HW5/Learning.png)
![Model](https://github.com/splitxd/bigDigital/blob/main/HW5/Model.png)
_____________________________________________________________________________________________

#### Часть 2
![miner](https://github.com/splitxd/bigDigital/blob/main/HW5/1miner.png)
![miners](https://github.com/splitxd/bigDigital/blob/main/HW5/moreminers.png)
![intime](https://github.com/splitxd/bigDigital/blob/main/HW5/intime.png)
![results](https://github.com/splitxd/bigDigital/blob/main/HW5/results.png)
![board](https://github.com/splitxd/bigDigital/blob/main/HW5/board.png)

## Задание 1
### “коэффициент корреляции ”

В этом случае, я подозреваю, коэффициент корреляции это перемення "tempInf", которая определяет 
награду для ML агента. Она при получении инфляции менее 6 процентов награждает его, а за
инфляцию больше 6 процентов "наказывает" его. Влияние следующее: если увеличить максимальный процент,
то обучение будет менее качественным, но будет происходить быстрее, а уменьшение приведет к
обратному эффекту. Если же будет 0 процентов - это не достижимый результат.

## Задание 2
###  Параметры файла yaml-агента

batch_size (размер пакета данных)
Сейчас: 1024
-Увеличение (до 2048):
Агент будет обучаться надежнее и точнее, но обучение станет медленнее и потребует больше памяти.
Подходит для сложных задач.
-Уменьшение (до 512):
Обучение будет быстрее, но менее точным и менее стабильным. Подходит для простых задач.
Вывод: Размер пакета влияет на скорость обучения и точность обновления модели.

learning_rate (скорость обучения)
Сейчас: 3.0e-4
-Увеличение (до 1.0e-3):
Агент будет учиться быстрее, но может начать вести себя нестабильно и не дойти до хорошего результата.
-Уменьшение (до 1.0e-5):
Обучение будет медленнее, но агент будет учиться аккуратнее и с меньшей вероятностью "перепрыгнет" нужное решение.
Вывод: Скорость обучения влияет на быстроту и стабильность обучения агента.

gamma (учёт будущих наград)
Сейчас: 0.99
-Увеличение (до 0.999):
Агент будет больше обращать внимание на долгосрочные награды и меньше на краткосрочные. Это хорошо для задач,
 где важен итоговый результат, но обучение может стать дольше.
-Уменьшение (до 0.9):
Агент будет делать упор на быстрые награды, что упрощает обучение, но может привести к неоптимальному поведению.
Вывод: Gamma определяет, насколько агент думает о будущих наградах или решает задачи здесь и сейчас.

beta (исследование среды)
Сейчас: 1.0e-2
-Увеличение (до 5.0e-2):
Агент будет чаще пробовать новые действия, что полезно в начале обучения, но мешает быстро "устаканиться" на хорошей стратегии.
-Уменьшение (до 1.0e-3):
Агент будет больше использовать то, что уже знает, что ускорит обучение на поздних этапах, но он может застрять в одном решении.
Вывод: Beta влияет на баланс между поиском новых решений и использованием уже изученных стратегий.

## Задание 3
### Примеры задач
#### Примеры 1 агента:
-Как по мне это подходит идеально для ситуаций поиска пути до цели. Например, игры с видом сверху, 
где курсором нужно тыкать по экрану для перемещения персонажа. Это позволит оптимизировать путь.

-Так же игры типа догонялок, где агент будет навешан на бота, который будет бежать за игроком,
строить различные пути как короче добраться до игрока

#### Примеры 2 агента:
-Регулировка внутриигровых рынков мультиплеерных игр, где рынок становится перенасыщенным 
из-за товара, например игры про фермерство, где если продавать большое количество пшеницы
цена будет постепенно меняться. 

-Балансировка сложности врагов, может например влиять на урон стрельбы ботов в шутере 
на выживание, где сложность будет скейлиться со временем, и для баланса будет использоваться 
ML Agent.

#### Когда использовать вместо программной реализации
Как по мне, актуальность булет в том, что модель обучаема и в долгосрочной перспективе 
будет проще и удобнее работать с ней. Так же упрощение и автоматизация рабочих процессов.
Так же иногда проще обучать модель на ошибках, чем пытаться написать код, учитывающий все 
возможные ошибки, как в пример модель перемещения - проще научить ее ходить по лабиринту и 
обучаться, чем прописывать код для каждого из них

## Выводы

Были изучены ML Agent'ы и их параметры, на примере построены модели обучения, изучены влияние переменных на
его работу и изучена актуальность и пременение.

| Plugin | README |
| ------ | ------ |
| Dropbox | [plugins/dropbox/README.md][PlDb] |
| GitHub | [plugins/github/README.md][PlGh] |
| Google Drive | [plugins/googledrive/README.md][PlGd] |
| OneDrive | [plugins/onedrive/README.md][PlOd] |
| Medium | [plugins/medium/README.md][PlMe] |
| Google Analytics | [plugins/googleanalytics/README.md][PlGa] |

## Powered by

**BigDigital Team: Denisov | Fadeev | Panov**
