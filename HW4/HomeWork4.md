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
- Построить визуальную модель работы перцептрона на сцене Unity.
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
Для XOR количество покелений может превышать и 100, но количество total error не будет уменьшатся с 4

![XOR](https://github.com/splitxd/bigDigital/blob/main/HW4/XOR.png)


## Задание 2
###  Построить графики зависимости количества эпох от ошибки  обучения 

Ссылка на Google tabs: [GoogleTabsParceptron](https://docs.google.com/spreadsheets/d/1kbM_nu7W_YPP1ITvdtGqjT1RNt-BHocHr7JBATfzEHc/edit?usp=sharing)

#### OR Graph

![ORG](https://github.com/splitxd/bigDigital/blob/main/HW4/ORG.png)

#### AND Graph

![ANDG](https://github.com/splitxd/bigDigital/blob/main/HW4/ANDG.png)

#### NAND Graph

![NANDG](https://github.com/splitxd/bigDigital/blob/main/HW4/NANDG.png)

#### XOR Graph

![XORG](https://github.com/splitxd/bigDigital/blob/main/HW4/XORG.png)


#### Зависимость количества эпох

Количество эпох зависит в первую очередь от сложности операции, а во вторую
от линейной разделимости, где первые три (OR AND NAND) ее имеют, а 
XOR не имеет, поэтому стандартная модель парцептрона не подойдет
(нужна модель многослойного парцептрона)

## Задание 3
### Построить визуальную модель работы перцептрона на сцене Unity

Я сделал что при создании кубиков нужно указать один из материалов 
красный или зеленый, которые соответственно равны "0" и "1". Далее они движутся 
друг к другу и при встрече, в соответствии с созданным массивом для условия (AND,OR,NAND и тд)
и значением выходного они создают один из префабов красного или зеленого кубика, которые означают
"0" или "1" соответсвенно работы функции. Для проверки вывода можно менять материалы созданных 
на сцене CubeFirst CubeSecond и массив для условий чтобы проверить работоспособность функции.

```csharp

using System.Collections;
using System.Collections.Generic;
using TMPro;
using UnityEngine;

[System.Serializable]
public class TrainingSets
{
	public double[] input;
	public double output;
}
[System.Serializable]
public class Prefabs
{
    public string name;
	public GameObject positive;
    public GameObject negative;
}


public class OnTrigger : MonoBehaviour
{
    public TrainingSet[] ts;
    public Prefabs prefs;
    public GameObject textGO;

    void Start()
    {
        var text = textGO.GetComponent<TextMeshProUGUI>();
        text.text = prefs.name;
    }

    void Update()
    {
        
    }
    void OnTriggerEnter(Collider other)
    {
        Vector3 posToSpawn = new Vector3(-0.308f,1.324f,0.9f);
        Renderer rendererThis = GetComponent<Renderer>();
        Renderer rendererOther = other.GetComponent<Renderer>();
        string materialNameThis = rendererThis.material.name.ToLower();
        string materialNameOther = rendererOther.material.name.ToLower();
        double secValue = materialNameOther.Contains("green") ? 1 : materialNameOther.Contains("red") ? 0 : -1;
        double firstValue = materialNameThis.Contains("green") ? 1 : materialNameThis.Contains("red") ? 0 : -1;

        foreach (var set in ts)
        {
            if (set.input[0] == firstValue && set.input[1] == secValue)
            {
                if (set.output == 1)
                {
                    Instantiate(prefs.positive, posToSpawn, Quaternion.identity);
                }
                else if (set.output == 0)
                {
                    Instantiate(prefs.negative, posToSpawn, Quaternion.identity);
                }
                Destroy(other.gameObject);
                Destroy(gameObject);
            }
        }  
    }
}
```



## Выводы

Была изучена система обучения parceptron и построены графики зависимости количества ошибок от поколений, 
построена визуализация на сцене юнити

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
