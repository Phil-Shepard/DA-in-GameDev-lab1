# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе №4 выполнил:
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
Познакомиться с программными средствами для создания системы искусственного интеллекта и их применение совместно с Unity.


## Задание 1
### В проекте Unity реализовать перцептрон, который умеет производить вычисления:
- OR

Перцептрон научился правильно производить вычисления уже после 3 итераций, всего было 8 итераций для обучения.

![1](https://user-images.githubusercontent.com/103362219/205010808-93d5ce9f-bbf3-4af5-a840-f2c13c29c4b3.png)

- AND

Перцептрон научился правильно производить вычисления уже после 6 итераций, всего было 8 итераций для обучения.

![2](https://user-images.githubusercontent.com/103362219/205011212-9216283c-700c-4a2e-b7cc-44e13712db23.png)


- NAND

Перцептрон научился правильно производить вычисления уже после 8 итераций, всего было 12 итераций для обучения.

![3](https://user-images.githubusercontent.com/103362219/205012136-2229c085-a9ff-4007-a874-f8e1bdca60b9.png)


- XOR

Перцептрон не смог научиться производить вычисления даже спустя 100 итераций, поскольку операция "XOR" нелинейная, а перцептрон может обучиться только линейным вычисленияем.

![4](https://user-images.githubusercontent.com/103362219/205022782-b66c805c-ac8a-4ed6-bde3-a0a8438b6266.png)


## Задание 2. Построить графики зависимости количества эпох от ошибки обучения. Указать от чего зависит необходимое количество эпох обучения.

- График зависимоти для операции Or

![6](https://user-images.githubusercontent.com/103362219/205047234-3f3df4ee-9f6b-40d3-83c1-0cff9e843795.JPG)

- График зависимоти для операции And

![5](https://user-images.githubusercontent.com/103362219/205047252-7514a23a-af12-446a-9888-ecc611a0ad78.JPG)

- График зависимоти для операции Nand

![7](https://user-images.githubusercontent.com/103362219/205047278-8a4d65f0-4d9a-4f97-a58e-756e846977ed.JPG)

- График зависимоти для операции Xor.
Обучение не удалось, поскольку операция нелинейная.

![8](https://user-images.githubusercontent.com/103362219/205047294-c77cade2-5b27-4fcd-8034-347624028df2.JPG)

## Необходимое количество эпох обучения зависит от сложности вычислительных операций: быстрее всего обучение реализуется для операций "Or" и "And". Перцептрон не поддаётся обучению операции "Xor", поскольку она нелинейна.

## Задание 3. Построить визуально модель работы перцептрона на сцене Unity.

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
