# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе №2 выполнил:
- Шамонин Филипп Николаевич
- РИ-210941
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
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Задание 2.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Задание 3.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Выводы.
- ✨Magic ✨

## Цель работы
Познакомиться с программными средствами для организции
передачи данных между инструментами google, Python и Unity.

## Задание 1
### Реализовать совместную работу и передачу данных в связке Python
- Google-Sheets – Unity. При выполнении задания используйте видео-материалы и
исходные данные, предоставленные преподавателя курса.

 В облачном сервисе google console подключить API для работы с google
sheets и google drive.

![1](https://user-images.githubusercontent.com/103362219/195162668-9c4eb7dc-a0bb-4ed6-93a3-200db4b7404e.png)
![2](https://user-images.githubusercontent.com/103362219/195162681-04b40ed0-95a3-4670-91d9-c27e49e715ce.png)
![3](https://user-images.githubusercontent.com/103362219/195162711-538c5723-ddf7-4849-b7e7-d7d58c9a1293.png)
![4](https://user-images.githubusercontent.com/103362219/195162747-722cba6c-5def-4567-be2b-5874d20b82c1.png)

- Реализовать запись данных из скрипта на python в google-таблицу. Данные
описывают изменение темпа инфляции на протяжении 11 отсчётных периодов, с
учётом стоимости игрового объекта в каждый период.

![5](https://user-images.githubusercontent.com/103362219/195162815-6874ff64-1458-494a-afbf-591e791f52c3.png)
![6](https://user-images.githubusercontent.com/103362219/195162852-f40c2972-e1dc-4321-9d81-e28daf887b6c.png)

- Создать новый проект на Unity, который будет получать данные из google-
таблицы, в которую были записаны данные в предыдущем пункте.

![7](https://user-images.githubusercontent.com/103362219/195162898-d30f18e5-17d1-4afa-9ead-55e78ccf36fe.png)
![9](https://user-images.githubusercontent.com/103362219/195163013-8882c2f0-b7b7-4674-92f7-5e75259b847d.png)

- Написать функционал на Unity, в котором будет воспризводиться аудио-
файл в зависимости от значения данных из таблицы.

![8](https://user-images.githubusercontent.com/103362219/195162988-799fb8c1-03aa-4f61-aa61-96d922230454.png)
![10](https://user-images.githubusercontent.com/103362219/195163046-cd7bfdfb-bcca-4581-b96a-074a833c09da.png)

## Задание 2. Реализовать запись в Google-таблицу набора данных, полученных
с помощью линейной регрессии из лабораторной работы № 1.

```py
import numpy as np
import gspread


def model(a, b, x):
    return a*x+b

def loss_function(a, b, x, y):
    num = len(x)
    prediction = model(a, b, x)
    return (0.5/num) * (np.square(prediction - y)).sum()


def optimize(a, b, x, y):
    num = len(x)
    prediction = model(a, b, x)
    da = (1.0/num) * ((prediction - y)*x).sum()
    db = (1.0/num) * ((prediction - y).sum())
    a -= Lr*da
    b -= Lr*db
    return a, b


def iterate(a, b, x, y, times):
    for i in range(times):
        a, b = optimize(a, b, x, y)
    return a, b

a = np.random.rand(1)
print(a)
b = np.random.rand(1)
print(b)
Lr = 0.000001

x = np.array([3, 21, 22, 34, 54, 34, 55, 67, 89, 99])
y = np.array([2, 22, 24, 65, 79, 82, 55, 130, 150, 199])

a, b = iterate(a, b, x, y, 100)
prediction = model(a, b, x)
loss = loss_function(a, b, x, y)
print(a, b, loss)

gc = gspread.service_account(filename='unitydatasciense-a4fb1bf44394.json')
sh = gc.open("UnitySheets")
price = np.random.randint(2000, 10000, 11)
mon = list(range(1, 11))
i = 0
while i <= len(mon):
    i += 1
    if i == 0:
        continue
    else:
        a, b = iterate(a, b, x, y, 100)
        prediction = model(a, b, x)
        loss = loss_function(a, b, x, y)
        tempInf = str(loss)
        tempInf = tempInf.replace('.', ',')
        sh.sheet1.update(('A' + str(i)), str(i))
        sh.sheet1.update(('B' + str(i)), str(tempInf))
        print(tempInf)
```

![123](https://user-images.githubusercontent.com/103362219/195166193-f79fd832-fa7b-418c-bde9-70b85b2ad304.png)

## Задание 3. Самостоятельно разработать сценарий воспроизведения звукового
сопровождения в Unity в зависимости от изменения считанных данных в задании 2.

Поменял значения + в инумераторе поменял индекс

```py
void Update()
    {
        if (dataSet.Count == 0 || dataSet.Count <= i)
        {
            return;
        }

        if (dataSet["Mon_" + i.ToString()] <= 300 & statusStart == false & 1 != dataSet.Count)
        {
            StartCoroutine(PlaySelectAudioGood());
            Debug.Log(dataSet["Mon_" + i.ToString()]);
        }

        if (dataSet["Mon_" + i.ToString()] > 300 & dataSet["Mon_" + i.ToString()] < 2000 & statusStart == false & 1 != dataSet.Count)
        {
            StartCoroutine(PlaySelectAudioNormal());
            Debug.Log(dataSet["Mon_" + i.ToString()]);
        }

        if (dataSet["Mon_" + i.ToString()] >= 2000 & statusStart == false & 1 != dataSet.Count)
        {
            StartCoroutine(PlaySelectAudioBad());
            Debug.Log(dataSet["Mon_" + i.ToString()]);
        }
    }

    IEnumerator GoogleSheets()
    {
        UnityWebRequest curentResp = UnityWebRequest.Get("https://sheets.googleapis.com/v4/spreadsheets/1LDnPyXaw05hTaRFvyQBFkONYLwtXJekyl-OzIOrYkdE/values/Лист1?key=AIzaSyDaCFe6mtKBhf9fSBc-1z8eaYQhT785igE");
        yield return curentResp.SendWebRequest();
        string rawResp = curentResp.downloadHandler.text;
        var rawJson = JSON.Parse(rawResp);
        foreach (var itemRawJson in rawJson["values"])
        {
            var parseJson = JSON.Parse(itemRawJson.ToString());
            var selectRow = parseJson[0].AsStringList;
            dataSet.Add(("Mon_" + selectRow[0]), float.Parse(selectRow[1]));
        }
        Debug.Log(dataSet["Mon_1"]);
    }
```
![End](https://user-images.githubusercontent.com/103362219/195169883-f0502e32-f2c5-4e2e-81b3-730794a778df.png)


## Выводы
В ходе проделанной работы я поработал на нескольких языках программирования, поработал на Unity со звуком, ещё понравились фразы из Stronghold Crusader!

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
