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
познакомиться с программными средствами для организции
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

-Написать функционал на Unity, в котором будет воспризводиться аудио-
файл в зависимости от значения данных из таблицы.
![8](https://user-images.githubusercontent.com/103362219/195162988-799fb8c1-03aa-4f61-aa61-96d922230454.png)
![10](https://user-images.githubusercontent.com/103362219/195163046-cd7bfdfb-bcca-4581-b96a-074a833c09da.png)

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
