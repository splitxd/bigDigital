# АНАЛИЗ ДАННЫХ В РАЗРАБОТКЕ ИГР [in GameDev]
Отчет по лабораторной работе #2 выполнил(а):
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
- Задание 0.
- Скриншот выполненного примера изменения google-таблицы при помощи python и воспроизведение изменений в Unity.
- Задание 1.
- Игровая переменная "здоровья".
- Задание 2.
- Скриншот выполненного задания реализации скрипта заполнения таблицы Python и описание реализации изменения.
- Задание 3.
- Скриншот настройки на сцене Unity воспроизведение звуковых файлов изменения здоровья
- Выводы.

## Цель работы
Научиться передавать в Unity данные из Google Sheets с помощью Python и разобрать одну из переменных игры "Спасти РТФ".

## Задание 0
### Изменения google-таблицы при помощи python и воспроизведение изменений в Unity.
Ход работы:

![GoogleAPI](https://github.com/splitxd/bigDigital/blob/main/HW2/GoogleAPI.png)

![GoogleTab](https://github.com/splitxd/bigDigital/blob/main/HW2/GoogleTab.png)

![JupNoteB](https://github.com/splitxd/bigDigital/blob/main/HW2/py.png)

![gspread](https://github.com/splitxd/bigDigital/blob/main/HW2/gspread.png)

![script](https://github.com/splitxd/bigDigital/blob/main/HW2/script.png)

![Unity](https://github.com/splitxd/bigDigital/blob/main/HW2/Unity.png)

![Component](https://github.com/splitxd/bigDigital/blob/main/HW2/Component.png)


## Задание 1
### Описание игровой переменная "здоровья"

![HP](https://github.com/splitxd/bigDigital/blob/main/HW2/HP.png)

# Здоровье
Здоровье является важнейшей частью игры и представляет собой ресурс продолжительности выживаемости, условно "сколько раз тебя
может ударить зомби, прежде чем ты начнешь новую игру". Ресурс пополняемый и может увеличиваться при прокачке. 
Для увеличения ограничения ресурса необходимо в навыках прокачивать "+ Здоровье", на сколько я понял прокачка не ограничена
 количеством, просто в какой то момент будет стоить дорого очков навыков
 
![Health](https://github.com/splitxd/bigDigital/blob/main/HW2/Health.png)

Для пополнения используются два навыка и один предмет из магазина, который восстанавливает здоровье при полной его утрате, возраждая персонажа.
Как я понимаю эти способности тоже не имеют ограничений в покупке, как и количество воскрешений.

![Wamp](https://github.com/splitxd/bigDigital/blob/main/HW2/Wamp.png)

![PassiveHR](https://github.com/splitxd/bigDigital/blob/main/HW2/PassiveHR.png)

Схема экономической модели:

![Econom](https://github.com/splitxd/bigDigital/blob/main/HW2/Economics.png)

## Задание 2
###  Реализации скрипта заполнения таблицы Python и описание реализации изменения здоровья.

Предложение для обучения ML-Agent-ом: Можно добавить персонажу способности.
Условно, будет древо прокачки таких умений, а очки для их прокачки будут получаться при убийстве боссов.
Будут несколько веток, по типу "Здоровье", "Оружие", "Способности", и например в способностях остановка времени, в оружии 
пополнение патрон со временем, в здоровье мгновенная регенерация.
У каждой способности будет свой уникальный CoolDown, который зависит от влияния игры, именно эту особеность, а так же 
влияние на игровой процесс будет изменяться ML-Agent-ом.
## Задание 3
### 
## Выводы

Были установлены необходимые программы и прорешаны задания, научился пользоваться Git-hub-ом и изучил игру, для которой необходим ML-Agent

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
