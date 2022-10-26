# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе №3 выполнил:
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
Познакомиться с программными средствами для создания системы машинного обучения и ее интеграции в Unity.

## Задание 1
### Реализовать систему машинного обучения в связке Python - Google-Sheets – Unity.
- Создал новый пустой 3D проект на Unity.
![1](https://user-images.githubusercontent.com/103362219/198036078-d7bc4fa1-4166-43f3-bc49-2066cbd69eb2.png)

- Скачал папку с ML агентом. 
![2](https://user-images.githubusercontent.com/103362219/198037649-26ff0001-5c40-4250-9501-acd0ba0a22ef.png)


- В созданный проект добавил ML Agent, выбрав Window - Package
Manager - Add Package from disk. Последовательно добавил .json –
файлы:
o ml-agents-release_19 / com,unity.ml-agents / package.json
o ml-agents-release_19 / com,unity.ml-agents.extensions / package.json
![3](https://user-images.githubusercontent.com/103362219/198038456-d018bcb2-1b18-443f-a9f6-1f5307d6b013.png)

- Запустил Anaconda Prompt для создания виртуальной среды и активации нового ML-агента, также скачал необходимые библиотеки:
o mlagents 0.28.0;
o torch 1.7.1;

![image](https://user-images.githubusercontent.com/103362219/198039669-9a15e86c-b656-4ab7-92f3-dd728f1ea70f.png)

![image](https://user-images.githubusercontent.com/103362219/198039830-1224fa23-0f23-4875-bec4-67ede56501cf.png)

![image](https://user-images.githubusercontent.com/103362219/198040110-6729184d-232a-4d00-9b8c-1f8c9dc8cc6e.png)

![Снимок](https://user-images.githubusercontent.com/103362219/198043420-09afc11e-4396-4c1d-83bf-bbe3e7abe744.JPG)

- Создал на сцене куб, сферу и пллоскость, потом я создал C# скрипт и подключил его к сфере. Добавил сфере компоненты Rigidbody, Decision Requester, Behavior Parameters и настроил их.
C# скрипт:
```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using Unity.MLAgents;
using Unity.MLAgents.Sensors;
using Unity.MLAgents.Actuators;

public class RollerAgent : Agent
{
    Rigidbody rBody;
    // Start is called before the first frame update
    void Start()
    {
        rBody = GetComponent<Rigidbody>();
    }

    public Transform Target;
    public override void OnEpisodeBegin()
    {
        if (this.transform.localPosition.y < 0)
        {
            this.rBody.angularVelocity = Vector3.zero;
            this.rBody.velocity = Vector3.zero;
            this.transform.localPosition = new Vector3(0, 0.5f, 0);
        }

        Target.localPosition = new Vector3(Random.value * 8-4, 0.5f, Random.value * 8-4);
    }
    public override void CollectObservations(VectorSensor sensor)
    {
        sensor.AddObservation(Target.localPosition);
        sensor.AddObservation(this.transform.localPosition);
        sensor.AddObservation(rBody.velocity.x);
        sensor.AddObservation(rBody.velocity.z);
    }
    public float forceMultiplier = 10;
    public override void OnActionReceived(ActionBuffers actionBuffers)
    {
        Vector3 controlSignal = Vector3.zero;
        controlSignal.x = actionBuffers.ContinuousActions[0];
        controlSignal.z = actionBuffers.ContinuousActions[1];
        rBody.AddForce(controlSignal * forceMultiplier);

        float distanceToTarget = Vector3.Distance(this.transform.localPosition, Target.localPosition);

        if(distanceToTarget < 1.42f)
        {
            SetReward(1.0f);
            EndEpisode();
        }
        else if (this.transform.localPosition.y < 0)
        {
            EndEpisode();
        }
    }
}

```

![Снимок экрана (87)](https://user-images.githubusercontent.com/103362219/198045770-564b5632-55cf-4af2-9a41-a6b2b406ecd9.png)

- В корень проекта добавил файл конфигурации rollerball_config.yaml
 
код rollerball_config.yaml:
![image](https://user-images.githubusercontent.com/103362219/198048230-fcab8c91-d4ec-4dd8-b3d4-77263ab8c93b.png)

- Вернулся в проект Unity, запустил сцену, проверил работу ML-Agent’a.
- Сделал 3 копии модели «Плоскость-Сфера-Куб», запустил симуляцию сцены и наблюдал за обучением модели.

![image](https://user-images.githubusercontent.com/103362219/198061363-3ac00231-2e27-41cc-8b50-a36aa505d37d.png)

- Сделал 9 копий модели «Плоскость-Сфера-Куб», запустил симуляцию сцены и наблюдал за обучением модели.

![image](https://user-images.githubusercontent.com/103362219/198065700-475107cb-b018-48db-8f94-370ba373ce72.png)

![image](https://user-images.githubusercontent.com/103362219/198063056-c0d9e9e8-8a44-4696-9993-ab567b1361b1.png)

- Сделал 27 копий модели «Плоскость-Сфера-Куб», запустил симуляцию сцены и наблюдал за обучением модели.
 
![image](https://user-images.githubusercontent.com/103362219/198064819-aaf578c5-e7c2-4f46-918b-fc78494e202f.png)


## Задание 2. В разделе "ход работы" пошагово выполнить каждый пункт с описанием и примером реализации задачи по теме лабораторной работы.
Ход работы:
1. Произвести подготовку данных для работы с алгоритмом линейной регрессии. 10 видов данных были установлены случайным образом, и данные находились в линейной зависимости. Данные преобразуются в формат массива, чтобы их можно было вычислить напрямую при использовании умножения и сложения.

```py

import numpy as np
import matplotlib.pyplot as plt
%matplotlib inline

x = [3,21,22,34,54,34,55,67,89,99]
x = np.array(x)
y = [2,22,24,65,79,82,55,130,150,199]
y = np.array(y)

plt.scatter(x,y)

```
![2_1](https://user-images.githubusercontent.com/103362219/192523354-b128497e-690b-4e1f-94a0-8b8fb9460bab.png)


2. Функция модели: определяет модель линейной регрессии wx+b. Функция потерь: функция потерь среднеквадратичной ошибки. Функция оптимизации: метод градиентного спуска для нахождения частных производных w и b.

```py
def model(a,b,x):
  return a*x+b

def loss_function(a,b,x,y):
    num = len(x)
    prediction=model(a,b,x)
    return (0.5/num) * (np.square(prediction-y)).sum()
    
def optimize(a,b,x,y):
    num = len(x)
    prediction = model(a,b,x)
    da = (1.0 /num) * ((prediction - y) * x).sum()
    db = (1.0 / num) * ((prediction - y). sum())
    a = a - Lr*da
    b = b - Lr*db
    return a, b 
def iterate(a, b, x, y, times):
    for i in range(times):
        a, b = optimize(a, b, x, y)
    return a, b
```
![2_2](https://user-images.githubusercontent.com/103362219/192523417-4ee5b4d5-9eaa-4585-86c3-e0482d37facb.png)
3. Начать итерацию

  Шаг 1. Инициализация и модель итерактивной оптимизации
```py
a = np. random. rand(1)
print(a)
b = np. random. rand(1)
print(b)
Lr = 0.000001
 
a, b = iterate(a, b, x, y, 1)
prediction = model(a, b, x)
loss = loss_function(a, b, x, y)
print(a, b, loss)
plt. scatter(x, y)
plt. plot(x, prediction)
```
![2_3](https://user-images.githubusercontent.com/103362219/192523477-53488c0d-1a20-4e30-9440-d55fc67f0b76.png)

Шаг 2. На второй итерации отображаются значения параметров, значения потерь и эффекты визуализации после итерации
```py
a, b = iterate(a, b, x, y, 2)
prediction = model(a, b, x)
loss = loss_function(a, b, x, y)
print(a, b, loss)
plt. scatter(x, y)
plt. plot(x, prediction)
```
![2_4](https://user-images.githubusercontent.com/103362219/192523511-316b9558-b41e-4598-893e-479591078958.png)

Шаг 3. Третья итерация показывает значения параметров, значения потерь и эффекты визуализации после итерации
```py
a, b = iterate(a, b, x, y, 3)
prediction = model(a, b, x)
loss = loss_function(a, b, x, y)
print(a, b, loss)
plt. scatter(x, y)
plt. plot(x, prediction)
```
![2_5](https://user-images.githubusercontent.com/103362219/192523553-f994400b-c15d-47f5-a823-cdd1e414a222.png)

Шаг 4. На четвертой итерации отображаются значения параметров, значения потерь и эффекты визуализации
```py
a, b = iterate(a, b, x, y, 4)
prediction = model(a, b, x)
loss = loss_function(a, b, x, y)
print(a, b, loss)
plt. scatter(x, y)
plt. plot(x, prediction)
```
![2_6](https://user-images.githubusercontent.com/103362219/192523590-b97127e3-2a49-48a6-bf3a-7280d3cb4041.png)

Шаг 5. Пятая итерация показывает значения параметров, значения потерь и эффекты визуализации после итерации
```py
a, b = iterate(a, b, x, y, 5)
prediction = model(a, b, x)
loss = loss_function(a, b, x, y)
print(a, b, loss)
plt. scatter(x, y)
plt. plot(x, prediction)
```
![2_7](https://user-images.githubusercontent.com/103362219/192523652-a88eb7f4-6ce7-4ca4-bb56-0a223de7b6a0.png)

Шаг 6. 10000-я итерация, показывающая значения параметров, потери и визуализацию после итерации
```py
a, b = iterate(a, b, x, y, 10000)
prediction = model(a, b, x)
loss = loss_function(a, b, x, y)
print(a, b, loss)
plt. scatter(x, y)
plt. plot(x, prediction)
```
![2_8](https://user-images.githubusercontent.com/103362219/192523687-9089addd-b15a-427c-89fb-41739a1bb0c6.png)



## Задание 3
### Какова роль параметра Lr? 

Параметр Lr определяет, как резко будет возрастать, либо же убывать график в зависимости от его значения.

![2_9](https://user-images.githubusercontent.com/103362219/192588607-f6caee8e-c547-49da-986d-ee24dc3ef9c0.png)
![2_10](https://user-images.githubusercontent.com/103362219/192588636-f875088a-ebf6-4fe8-a1d4-cc32697d82dc.png)
![2_11](https://user-images.githubusercontent.com/103362219/192588656-6d9de998-437f-4c06-8793-578aaa7a3612.png)
![2_12](https://user-images.githubusercontent.com/103362219/192588688-e404dbae-4904-40e9-a289-0e3b4711e561.png)

### Должна ли величина loss стремиться к нулю при изменении исходных данных? 
Нет, не должна, это видно по построенному графику:

![LOSS1](https://user-images.githubusercontent.com/103362219/192590834-619814f1-e08c-4dc3-9d11-e4ff307e3a14.png)
![LOSS2](https://user-images.githubusercontent.com/103362219/192590847-fa9f424f-750a-4442-b683-1f2183bde3be.png)

## Выводы

В ходе проделанной работы я ознакомился с основными операторами зыка Python на примере реализации линейной регрессии, получил опыт работы с анализом данных, а также поработал в таких средах разработки, как: PyCharm, Anaconda и Unity. В целом, я усвоил для себя много нового и интересного.

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
