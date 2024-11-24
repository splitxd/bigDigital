# АНАЛИЗ ДАННЫХ В РАЗРАБОТКЕ ИГР [in GameDev]
Отчет по лабораторной работе #4 выполнил(а):
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
- Unity реализовать перцептрон.
- Задание 2.
- Построить графики зависимости количества эпох от ошибки  обучения.
- Задание 3.
- Построить визуальную модель работы перцептрона на сцене Unity
- Выводы.

## Цель работы
Изучить parceptron на примере, построить графики и реализовать визуализацию.




## Задание 1
### Unity реализовать перцептрон

#### OR
Для OR понадобилось в среднем 4 поколения для устранения ошибок.

![OR](https://github.com/splitxd/bigDigital/blob/main/HW4/OR.png)

#### AND
Для AND понадобилось в среднем 6 поколения для устранения ошибок.

![AND](https://github.com/splitxd/bigDigital/blob/main/HW4/OR.png)

#### NAND
Для NAND понадобилось в среднем 6 поколения для устранения ошибок.

![NAND](https://github.com/splitxd/bigDigital/blob/main/HW4/NAND.png)

#### XOR
Для XOR количество покелений может превышать и 10, но количество total error не будет уменьшатся с 4

![XOR](https://github.com/splitxd/bigDigital/blob/main/HW4/XOR.png)


## Задание 2
###  Сцены Unity со сложностями 

Я скопировал первую сцену и вставил ее 10 раз, меняя значения параметров, которвые хотел усложнять 
по уровням с помощью инспектора.

![Scenes](https://github.com/splitxd/bigDigital/blob/main/HW3/IMGHW3/Scenes.png)

![inspector](https://github.com/splitxd/bigDigital/blob/main/HW3/IMGHW3/inspector.png)


## Задание 3
### Визуализация данных из гугл таблицы

В Python я передавал реализованую за ранее систему балансировки сложности из таблицы, созданной выше
![cloud](https://github.com/splitxd/bigDigital/blob/main/HW3/IMGHW3/cloud.png)
![python](https://github.com/splitxd/bigDigital/blob/main/HW3/IMGHW3/python.png)

Так же я создал метод для Unity считывания данных в списки, для удобного чтения.


## Выводы

Была изучена система балансировки игры Dragon Picker и предложена система балансировки сложности уровня, для
ее изменения была подключена таблица с данными, которые можно по необходимости легко менять.

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
