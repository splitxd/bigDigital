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

#### Здоровье
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

![Acckey](https://github.com/splitxd/bigDigital/blob/main/HW2/acckey.png)

![python](https://github.com/splitxd/bigDigital/blob/main/HW2/python.png)

![googlesheets](https://github.com/splitxd/bigDigital/blob/main/HW2/googlesheets.png)

В данном случае для изменения в скрипте Python я решил взять изменение здоровья в циклах его исцеления или ранения. 
Второй столбик - это нанесенный урон, третий - изменение здоровья. В этом случае в ограничение идет "100" - это максимальная
граница, выше которой "хп" не поднимется и изменяться будет только вниз, и нижняя граница "0 и меньше" - ведь в таком случае
герой умирает и счетчик останавливается. Недостаток - неопределенное цифра увеличения или уменьшения "хп", которое надо
расчитывать по сложности

Модификации:
 - Получение здоровья сверх "100" ведет к медленному уменьшению здоровья к "100", допустм игрок отхилился до 120 хп, 
здоровье будет уменьшаться каждую секунду на 2 хп вплоть до 100, то есть игрок будет иметь смысл отхиливаться 
больше чем на 100
- Получение эффекта кровотечения\отравления , которое медленно отнимает здоровья, в количестве  "х" хп\сек, 
действует опрделенное время

## Задание 3
### Cцена Unity воспроизведение звуковых файлов

Я написал скрипт, который в зависимости от полного здоровья(100), смерти (0), при получении урона и при исцелении будет воспроизводить различные звуки в Unity, а данные будут браться из гугл-таблицы.

Code:
'''
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.Networking;
using SimpleJSON;

public class scriptHW : MonoBehaviour
{
    public AudioClip getHealth;
    public AudioClip fullHealth;
    public AudioClip zeroHealth;
    public AudioClip wasteHealth;

    private AudioSource selectAudio;
    private Dictionary<string, List<float>> dataSet = new Dictionary<string, List<float>>();
    private bool statusStart = false;
    private int i = 1;

    void Start()
    {
        StartCoroutine(GoogleSheets());
    }

    void Print(float a, float b)
    {
        Debug.Log("Изменение: " + a.ToString() + " HP: " + b.ToString());
    }

    void Update()
    {
        if (i <= dataSet.Count)
        {
            if (dataSet[i.ToString()][1] < 100 && dataSet[i.ToString()][1] > 0 && dataSet[i.ToString()][0] >= 0 && statusStart == false)
            {
                StartCoroutine(PlaySelectAudioGet());
                Print(dataSet[i.ToString()][0], dataSet[i.ToString()][1]);
            }

            if (dataSet[i.ToString()][1] == 100 && dataSet[i.ToString()][0] >= 0 && statusStart == false)
            {
                StartCoroutine(PlaySelectAudioFull());
                Print(dataSet[i.ToString()][0], dataSet[i.ToString()][1]);
            }

            if (dataSet[i.ToString()][1] == 0 && statusStart == false)
            {
                StartCoroutine(PlaySelectAudioZero());
                Print(dataSet[i.ToString()][0], dataSet[i.ToString()][1]);
            }

            if (dataSet[i.ToString()][1] >= 0 && dataSet[i.ToString()][0] < 0 && statusStart == false)
            {
                StartCoroutine(PlaySelectAudioWaste());
                Print(dataSet[i.ToString()][0], dataSet[i.ToString()][1]);
            }
        }
    }

    IEnumerator GoogleSheets()
    {
        UnityWebRequest curentResp = UnityWebRequest.Get("https://sheets.googleapis.com/v4/spreadsheets/1Df3vDa83goSeOlv1OV9K-HfapAIHB_KnhdVyIQqaMRg/values/Лист1?key=AIzaSyBNKXlLNi7ZuoB85CdanQEpK3tDGlwrtYQ");
        yield return curentResp.SendWebRequest();
        string rawResp = curentResp.downloadHandler.text;
        var rawJson = JSON.Parse(rawResp);

        foreach (var itemRawJson in rawJson["values"])
        {
            var parseJson = JSON.Parse(itemRawJson.ToString());
            var selectRow = parseJson[0].AsStringList;
            dataSet.Add(selectRow[0], new List<float> { float.Parse(selectRow[1]), float.Parse(selectRow[2]) });
        }
    }

    IEnumerator PlaySelectAudioGet()
    {
        statusStart = true;
        selectAudio = GetComponent<AudioSource>();
        selectAudio.clip = getHealth;
        selectAudio.Play();
        yield return new WaitForSeconds(3);
        statusStart = false;
        i++;
    }

    IEnumerator PlaySelectAudioFull()
    {
        statusStart = true;
        selectAudio = GetComponent<AudioSource>();
        selectAudio.clip = fullHealth;
        selectAudio.Play();
        yield return new WaitForSeconds(3);
        statusStart = false;
        i++;
    }

    IEnumerator PlaySelectAudioZero()
    {
        statusStart = true;
        selectAudio = GetComponent<AudioSource>();
        selectAudio.clip = zeroHealth;
        selectAudio.Play();
        yield return new WaitForSeconds(4);
        statusStart = false;
        i++;
    }

    IEnumerator PlaySelectAudioWaste()
    {
        statusStart = true;
        selectAudio = GetComponent<AudioSource>();
        selectAudio.clip = wasteHealth;
        selectAudio.Play();
        yield return new WaitForSeconds(4);
        statusStart = false;
        i++;
    }
}

'''
![code1](https://github.com/splitxd/bigDigital/blob/main/HW2/code1.png)

![code2](https://github.com/splitxd/bigDigital/blob/main/HW2/code2.png)

![code3](https://github.com/splitxd/bigDigital/blob/main/HW2/code3.png)

![console](https://github.com/splitxd/bigDigital/blob/main/HW2/console.png)

![sound](https://github.com/splitxd/bigDigital/blob/main/HW2/sound.png)

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
