# АНАЛИЗ ДАННЫХ В РАЗРАБОТКЕ ИГР [in GameDev]
Отчет по лабораторной работе #3 выполнил(а):
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
- Вариант изменения переменных.
- Задание 2.
- Сцены Unity.
- Задание 3.
- Визуализация
- Задание 4.
- Выводы.

## Цель работы
Изучить систему балансировки и провести балансировку самостоятельно, визуализировать данные.




## Задание 1
### Вариант изменения переменных

За изменяемые переменные я взял скорость, время появления яйца и сменить направление полета дракона.
https://docs.google.com/document/d/1gN27ekgGEVB3KuLtLUsycbMNxEL2VB5asCNMqG6O_CA/edit?tab=t.0

![tabs1](https://github.com/splitxd/bigDigital/blob/main/HW3/IMGHW3/tabs1.png)
![tabs2](https://github.com/splitxd/bigDigital/blob/main/HW3/IMGHW3/tabs2.png)


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

```csharp
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.Networking;
using Newtonsoft.Json.Linq;

public class GoogleSheetsReader : MonoBehaviour
{
    private string apiKey = "AIzaSyAHX-hJopfMO9KpDnabfsamXjN_E-WxkU0";
    private string sheetId = "1HWCBILzlUxCJIt4tFF2jhWkL5Mp0ks3CSrFkdR3yeMg";
    public List<float> speeds = new List<float>();
    public List<float> eggDropTimes = new List<float>();
    public List<float> directionChangeChances = new List<float>();

    void Start()
    {
        StartCoroutine(LoadSheetData());
    }

    private IEnumerator LoadSheetData()
    {
        yield return StartCoroutine(GetRowData("F2:P2", speeds));
        yield return StartCoroutine(GetRowData("F3:P3", eggDropTimes));
        yield return StartCoroutine(GetRowData("F4:P4", directionChangeChances));
    }

    private IEnumerator GetRowData(string range, List<float> list)
    {
        string url = $"https://sheets.googleapis.com/v4/spreadsheets/{sheetId}/values/{range}?key={apiKey}";

        using (UnityWebRequest request = UnityWebRequest.Get(url))
        {
            yield return request.SendWebRequest();

            if (request.result == UnityWebRequest.Result.Success)
            {
                ParseRowData(request.downloadHandler.text, list);
            }
            else
            {
                Debug.LogError($"Ошибка загрузки данных: {request.error}");
            }
        }
    }

    private void ParseRowData(string jsonData, List<float> list)
    {
        JObject data = JObject.Parse(jsonData);
        JArray values = (JArray)data["values"];

        foreach (var value in values[0])
        {
            if (float.TryParse(value.ToString(), out float result))
            {
                list.Add(result);
            }
            else
            {
                Debug.LogWarning($"Не удалось преобразовать значение '{value}' в float");
            }
        }
    }
}
```

Далее я изменил скрипт дракона, чтобы данные для изменения сложности подавались соответственно названию сцены

```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using System.Globalization;
using System.Text.RegularExpressions;
using UnityEngine;
using UnityEngine.SceneManagement;

public class EnemyDragon : MonoBehaviour
{
    public GameObject dragonEggPrefab;
    public float speed = 1;
    public float timeBetweenEggDrops = 1f;
    public float leftRightDistance = 10f;
    public float chanceDirection = 0.1f;

    private GoogleSheetsReader sheetsReader;

    void Start()
    {
        sheetsReader = FindObjectOfType<GoogleSheetsReader>();
        StartCoroutine(InitializeDifficulty());
    }

    private IEnumerator InitializeDifficulty()
    {
        yield return new WaitUntil(() => sheetsReader.speeds.Count > 0 && 
                                         sheetsReader.eggDropTimes.Count > 0 && 
                                         sheetsReader.directionChangeChances.Count > 0);

        ExactDifficult();
        Invoke("DropEgg", 2f);
    }

    private void ExactDifficult()
    {
        int sceneNumber = int.Parse(ExtractNumberFromSceneName(SceneManager.GetActiveScene().name));
        int index = Mathf.Clamp(sceneNumber, 1, sheetsReader.speeds.Count) - 1;

        Debug.Log(sceneNumber + " " + index);
        speed = sheetsReader.speeds[index];
        timeBetweenEggDrops = sheetsReader.eggDropTimes[index];
        chanceDirection = sheetsReader.directionChangeChances[index];
        Debug.Log(speed + " " + timeBetweenEggDrops + " " + chanceDirection);
    }

    private string ExtractNumberFromSceneName(string sceneName)
    {
        Match match = Regex.Match(sceneName, @"\d+");
        if (match.Success)
        {
            return match.Value;
        }
        return "1";
    }

    void DropEgg()
    {
        Vector3 myVector = new Vector3(0.0f, 5.0f, 0.0f);
        GameObject egg = Instantiate(dragonEggPrefab);
        egg.transform.position = transform.position + myVector;
        Invoke("DropEgg", timeBetweenEggDrops);
    }

    void Update()
    {
        Vector3 pos = transform.position;
        pos.x += speed * Time.deltaTime;
        transform.position = pos;

        if (pos.x < -leftRightDistance)
        {
            speed = Mathf.Abs(speed);
        }
        else if (pos.x > leftRightDistance)
        {
            speed = -Mathf.Abs(speed);
        }
    }

    private void FixedUpdate()
    {
        if (UnityEngine.Random.value < chanceDirection)
        {
            speed *= -1;
        }
    }
}
```


## Задание 4 (секретное)
### Будка RTF

Будка будет прекреплена так же к файлу этого проекта, а так же я ее отправлю в чат в тг


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
