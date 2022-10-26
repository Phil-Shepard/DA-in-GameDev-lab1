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

![image](https://user-images.githubusercontent.com/103362219/198066284-724455f0-b8d9-456e-b2d8-8d28b1dafbec.png)

![image](https://user-images.githubusercontent.com/103362219/198061363-3ac00231-2e27-41cc-8b50-a36aa505d37d.png)

- Сделал 9 копий модели «Плоскость-Сфера-Куб», запустил симуляцию сцены и наблюдал за обучением модели.

![image](https://user-images.githubusercontent.com/103362219/198065700-475107cb-b018-48db-8f94-370ba373ce72.png)

![image](https://user-images.githubusercontent.com/103362219/198063056-c0d9e9e8-8a44-4696-9993-ab567b1361b1.png)

- Сделал 27 копий модели «Плоскость-Сфера-Куб», запустил симуляцию сцены и наблюдал за обучением модели.
 
![image](https://user-images.githubusercontent.com/103362219/198064819-aaf578c5-e7c2-4f46-918b-fc78494e202f.png)

![image](https://user-images.githubusercontent.com/103362219/198066858-ecad9314-3d98-41a7-b91f-c26df223f558.png)

- После завершения обучения проверил работу модели.

![Снимок](https://user-images.githubusercontent.com/103362219/198068765-10447176-6291-4c28-b8b0-961613ecac39.JPG)


- **Выводы из задания №1: в ходе выполнения задания я смог успешно подключить ML-агент, обучить модель и протестировать её.**

## Задание 2
### Подробно описать каждую строку файла конфигурации нейронной сети. Самостоятельно найти информацию о компонентах Decision Requester, Behavior Parameters, добавленных на сфере. 
#### Описание каждой строки файла конфигурации нейронной сети.
* содержимое файла конфигурации
   ```yaml
   behaviors:
    RollerBall:
      trainer_type: ppo
      hyperparameters:
        batch_size: 10
        buffer_size: 100
        learning_rate: 3.0e-4
        beta: 5.0e-4
        epsilon: 0.2
        lambd: 0.99
        num_epoch: 3
        learning_rate_schedule: linear
      network_settings:
        normalize: false
        hidden_units: 128
        num_layers: 2
      reward_signals:
        extrinsic:
          gamma: 0.99
          strength: 1.0
      max_steps: 500000
      time_horizon: 64
      summary_freq: 10000
   ```
Ссылка на документацию ml-агента - https://github.com/Unity-Technologies/ml-agents/blob/main/docs/Training-Configuration-File.md 
  * ```trainer_type``` - (по умолчанию = ppo) Тип используемого тренера: ppo, sac, или poca.  
  * ```hyperparameters```(гиперпараметры):  
    * ```batch_size``` - количество опытов в каждой итерации градиентного спуска. Это всегда должно быть в несколько раз меньше, чемbuffer_size.  
    * ```buffer_size``` - количество опытов, которые необходимо собрать перед обновлением модели политики. Соответствует тому, сколько опыта должно быть собрано, прежде чем мы будем изучать или обновлять модель.  
    * ```learning_rate``` - начальная скорость обучения для градиентного спуска. Соответствует силе каждого шага обновления градиентного спуска. Обычно это значение следует уменьшать, если обучение нестабильно, а вознаграждение не увеличивается постоянно.  
    * ```beta``` - сила регуляризации энтропии, которая делает политику «более случайной». Это гарантирует, что агенты должным образом исследуют пространство действия во время обучения. Увеличение этого параметра обеспечит выполнение большего количества случайных действий.  
    * ```epsilon``` - влияет на скорость изменения политики во время обучения. Соответствует допустимому порогу расхождения между старой и новой политикой при обновлении градиентного спуска. Установка небольшого значения этого параметра приведет к более стабильным обновлениям, но также замедлит процесс обучения.  
    * ```lambd``` - параметр регуляризации (лямбда), используемый при расчете обобщенной оценки преимущества ( GAE ). Это можно рассматривать как то, насколько агент полагается на свою текущую оценку стоимости при вычислении обновленной оценки стоимости.   
    * ```num_epoch``` -  количество проходов через буфер опыта при выполнении оптимизации градиентного спуска. Чем больше размер партии, тем больше это допустимо. Уменьшение этого параметра обеспечит более стабильные обновления за счет более медленного обучения.  
    * ```learning_rate_schedule``` - определяет, как скорость обучения изменяется с течением времени. (**linear** скорость обучения уменьшается линейно, достигая 0 на max_steps, сохраняя при этом constant скорость обучения постоянной для всего тренировочного прогона.)  
  * ```network_settings```(сетевые настройки):  
    * ```normalize``` - (по умолчанию = false) Применяется ли нормализация к входным данным векторных наблюдений. Эта нормализация основана на скользящем среднем и дисперсии векторного наблюдения. Нормализация может быть полезна в случаях со сложными задачами непрерывного управления, но может быть вредна для более простых задач дискретного управления.  
    * ```hidden_units``` - (по умолчанию = 128) Количество единиц в скрытых слоях нейронной сети. Соответствуют количеству единиц в каждом полносвязном слое нейронной сети. Для простых задач, где правильное действие представляет собой простую комбинацию входных данных наблюдения, это значение должно быть небольшим. Для задач, где действие представляет собой очень сложное взаимодействие между переменными наблюдения, это значение должно быть больше.  
    * ```num_layers``` - (по умолчанию = 2) Количество скрытых слоев в нейронной сети. Соответствует количеству скрытых слоев после ввода наблюдения или после кодирования CNN визуального наблюдения. Для простых задач меньше слоев, скорее всего, будут обучать быстрее и эффективнее. Для более сложных задач управления может потребоваться больше слоев.  
  * ```reward_signals``` -  позволяет задавать настройки как для внешних (т. е. основанных на среде), так и для внутренних сигналов вознаграждения.
    * ```extrinsic``` - настройки для внешних.
      * ```gamma``` - (по умолчанию = 0.99) Фактор скидки для будущих вознаграждений, поступающих из окружающей среды. Это можно рассматривать как то, как далеко в будущем агент должен заботиться о возможных вознаграждениях. В ситуациях, когда агент должен действовать в настоящем, чтобы подготовиться к вознаграждению в отдаленном будущем, это значение должно быть большим.  
      * ```strength``` - (по умолчанию = 1.0) Коэффициент, на который умножается вознаграждение, данное средой. Типичные диапазоны будут варьироваться в зависимости от сигнала вознаграждения.  
  * ```max_steps``` - Общее количество шагов (т. е. собранных наблюдений и предпринятых действий), которые необходимо выполнить в среде (или во всех средах при параллельном использовании нескольких) перед завершением процесса обучения.  
  * ```time_horizon``` - (по умолчанию = 64) Сколько шагов опыта необходимо собрать для каждого агента, прежде чем добавить его в буфер опыта. Когда этот предел достигается до конца эпизода, оценка значения используется для прогнозирования общего ожидаемого вознаграждения из текущего состояния агента. Таким образом, этот параметр является компромиссом между менее предвзятой, но более высокой оценкой дисперсии.  
  * ```summary_freq``` - Количество опытов, которое необходимо собрать перед созданием и отображением статистики обучения. Это определяет детализацию графиков в Tensorboard.  

#### Информация о компонентах, добавленных на сфере.
**DecisionRequester** - компонент, который автоматически запрашивает решения для экземпляра агента через регулярные промежутки времени. Должен быть прикреплён к тому же [GameObject], что и компонент Agent. Компонент DecisionRequester предоставляет удобный и гибкий способ запуска процесса принятия решения агентом. Без DecisionRequester реализация вашего агента должна вручную вызывать функцию **RequestDecision()**. 

**BehaviorParameters** - компонент для настройки поведения экземпляра агента и свойств мозга. Во время выполнения этот компонент генерирует объекты политики агента в соответствии с настройками, указанными в редакторе. 
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
