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
Ознакомиться с основными операторами зыка Python на примере реализации линейной регрессии.

## Задание 1
### Написать программы Hello World на Python и Unity.
- Для Python в отчете привести скриншоты с демонстрацией сохранения документа google.colab на свой диск с запуском программы, выводящей сообщение Hello World.

 ![GoogleCollabe](https://user-images.githubusercontent.com/103362219/192449521-7a9d9cbf-9c8c-419d-8ab6-6f2952fd045a.png)
 
 ![Диск](https://user-images.githubusercontent.com/103362219/192449660-553da15f-d5fa-456a-b4e5-06a3de686887.png)
 
- Для Unity в отчете привести скриншоты вывода сообщения Hello World в консоль.
 
 ![UnityHelloWorld](https://user-images.githubusercontent.com/103362219/192449702-89f297d9-abda-448f-9eeb-9d1246a7b736.png)

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
