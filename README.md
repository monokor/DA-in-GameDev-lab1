# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #3 выполнил(а):
- Зуев Владислав Анатольевич
- РИ210915

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
### Реализовать систему машинного обучения в связке Python – Unity. При выполнении задания можно использовать видео-материалы и исходные данные, предоставленные преподавателями курса.

Создаем проект в Unity, добавляем туда компонент MLAgent. Создаем необходимую сцену, шару добавляем и настраиваем 
C# скрипт и компоненты Rigidbody, Decision Requester, Behavior Parameters:

![image](https://user-images.githubusercontent.com/49882084/198287594-73521988-5462-43ac-80c7-4a17b1d63003.png)
![image](https://user-images.githubusercontent.com/49882084/198288584-e7a8d371-ee8f-4cb1-951d-3740b9b757a8.png)
![image](https://user-images.githubusercontent.com/49882084/198288888-69769cfa-e30b-4c03-acbe-9ea1610af0b2.png)


```
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


В корень проекта добавляем файл конфигурации .yaml нашей нейронной сети:

```
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


Запускаем Anaconda Promt, создаем, активируем и запускаем MLAgent:

![image](https://user-images.githubusercontent.com/49882084/198290125-6eb7e4c2-7ff8-432b-8f6f-581c57e1a475.png)

Вернувшись в Unity-проект, запускаем сцену и проверяем работу ML-агента. Затем запускаем обучение на большем количестве копий модели(плоскость, куб, шар).

Готовая модель находится в "../results/RollerBall/RollerBall.onnx", ее копируем в ассеты и переносим в Behavior Parameters:
![image](https://user-images.githubusercontent.com/49882084/198292560-192ab578-e54c-4aff-a857-ae2e900dee69.png)


Теперь можем проверить работу обученной модели, удобнее на одной копии.

![image](https://user-images.githubusercontent.com/49882084/198315156-b8d85047-f8c9-4112-88b7-c141f9ff35d3.png)


По итогу обучения мы видим, что шар научился самостоятельно двигаться к каждому новому кубу. 
При этом шар вращается по настоящему, учитывает инерцию своего движения и не падает с платформы.

Увеличение копий модели позволит обучать ее параллельно на нескольких сценах. 
Это ускорит обучение, но повысит нагрузку на ПК.

## Задание 2
### Подробно опишите каждую строку файла конфигурации нейронной сети. Найдите информацию о компонентах Decision Requester, Behavior Parameters.

trainer_type: 

    Тип обучения модели (PPO, SAC, POCA).


batch_size: 

    Количество опытов на каждой итерации. Всегда должно быть в несколько раз меньше, чем buffer_size.
    При непрерывных действиях, это значение должно быть большим (тысячи). 
    Если действия дискретные, это значение должно быть меньше (десятки).
    Типичный диапазон: (Непрерывный PPO): 512 - 5120; (Непрерывный SAC): 128 - 1024; (Дискретный, PPO & SAC): 32 - 512.



buffer_size: 

    для PPO: Сколько опыта должно быть собрано, прежде чем приступить к какому-либо изучению или обновлению модели. 
    Должно быть в несколько раз больше, чем batch_size.
    для SAC: максимальный размер - в тысячи раз больше, чем эпизоды, поэтому SAC может учиться как на старом, так и на новом опыте.
    (по умолчанию = 10240 для PPO и 50000 для SAC)
    Типичный диапазон: PPO: 2048-409600; SAC: 50000 - 1000000



learning_rate:

    Начальная скорость обучения. Соответствует силе каждого шага обновления.
    Обычно это значение следует уменьшить, если тренировка нестабильна, а вознаграждение постоянно не увеличивается.
    (по умолчанию = 3e-4)
    Типичный диапазон: 1e-5 - 1e-3



beta:

    Сила регуляризации энтропии, которая делает политику "более случайной". 
    Это гарантирует, что агенты должным образом исследуют пространство действий во время обучения. 
    Должно быть скорректировано таким образом, чтобы энтропия медленно уменьшалась вместе с увеличением вознаграждения. 
    Если энтропия падает слишком быстро, нужно увеличить значение, и наоборот.
    (по умолчанию = 5.0e-3) 
    Типичный диапазон: 1e-4 - 1e-2



epsilon:

    Влияет на то, насколько быстро политика может развиваться во время обучения.
    Установка малого значения приведет к более стабильным обновлениям, но также замедлит процесс обучения.
    (по умолчанию = 0,2)
    Типичный диапазон: 0,1 - 0,3



lambd:

    Параметр регуляризации, используемый при расчете обобщенной оценки преимущества (GAE).
    Насколько агент полагается на свою текущую оценку стоимости при расчете обновленной оценки стоимости. 
    Низкие значения соответствуют тому, чтобы больше полагаться на текущую оценку стоимости, 
    а высокие - чтобы полагаться на фактические вознаграждения, полученные в процессе. 
    Правильное значение может привести к более стабильному процессу обучения.
    (по умолчанию = 0,95)
    Типичный диапазон: 0,9 - 0,95



num_epoch:

    Количество проходов через буфер опыта при выполнении оптимизации.
    Уменьшение этого параметра обеспечит более стабильные обновления за счет более медленного обучения.
    (по умолчанию = 3) 
    Типичный диапазон: 3 - 10



learning_rate_schedule:

    Определяет, как скорость обучения изменяется с течением времени. 
    linear линейно уменьшает learning_rate, достигая 0 при max_steps, 
    constant сохраняет скорость обучения постоянной в течение всего цикла обучения.
    Для PPO рекомендуется снижать скорость обучения до max_steps, чтобы обучение сходилось более стабильно. 
    Однако в некоторых случаях (например, обучение в течение неизвестного периода времени) эта функция может быть отключена. 
    Для SAC рекомендуется поддерживать скорость обучения постоянной, 
    чтобы агент мог продолжать обучение до тех пор, пока его Q-функция не сойдется естественным образом.
    (по умолчанию = linear для PPO и constant для SAC)



normalize:

    Применяется ли нормализация к входным данным векторного наблюдения. 
    Эта нормализация основана на текущем среднем значении и дисперсии векторного наблюдения. 
    Нормализация может быть полезна со сложными задачами непрерывного управления, 
    но может быть вредным при решении простых задач дискретного управления.
    (по умолчанию = false)



hidden_units:

    Количество юнитов в скрытых слоях нейронной сети.
    Для простых задач, где правильное действие представляет собой простую комбинацию входных данных наблюдения, должно быть небольшим. 
    Для задач, где действие представляет собой очень сложное взаимодействие между переменными наблюдения, должно быть больше.
    (по умолчанию = 128)
    Типичный диапазон: 32 - 512



num_layers:

    Количество скрытых слоев в нейронной сети. 
    Для простых задач меньшее количество слоев, скорее всего, будет быстрее и эффективнее. 
    Для более сложных задач управления может потребоваться больше уровней.
    (по умолчанию = 2)
    Типичный диапазон: 1 - 3



gamma: 

    Коэффициент "дисконтирования" для будущих вознаграждений, получаемых от окружающей среды.
    Можно рассматривать как то, насколько далеко в будущем агент должен заботиться о возможных вознаграждениях. 
    В ситуациях, когда агент должен действовать в настоящем, 
    чтобы подготовиться к вознаграждению в отдаленном будущем, значение должно быть большим. 
    В тех случаях, когда вознаграждение является более немедленным, значение может быть меньше. 
    Должно быть строго меньше 1.
    (по умолчанию = 0,99)
    Типичный диапазон: 0,8 - 0,995



strength:

    Коэффициент, на который умножается вознаграждение, предоставляемое окружающей средой.
    (по умолчанию = 1,0)
    Типичный диапазон: 1,00



max_steps:

    Общее количество шагов (собранных наблюдений и предпринятых действий), 
    которые должны быть выполнены в среде (во всех средах, если используется несколько параллельно) до завершения процесса обучения.
    Если есть несколько агентов с одинаковым именем поведения, все их шаги, будут считаться в общий max_steps.
    (по умолчанию = 500000) 
    Типичный диапазон: 5e5 - 1e7



time_horizon:

    Сколько шагов опыта нужно собрать для каждого агента, прежде чем добавлять его в буфер опыта. 
    Когда в эпизоде часто бывают награды или сами эпизоды очень большие, значение лучше уменьшить. 
    Число должно быть достаточно большим, чтобы охватить все важное поведение в последовательности действий агента.
    (по умолчанию = 64)
    Типичный диапазон: 32 - 2048



summary_freq:

    Количество опытов, которые необходимо собрать перед созданием и отображением статистики обучения. 
    Определяет степень детализации графиков в Tensorboard.
    (по умолчанию = 50000)




Decision Requester заставляет агента запрашивать действия (решения) с заданным интервалом на протяжении всей симуляции.
При работе с каким нибудь сложным механизмом, агенту будет необходимо регулярнои часто выполнять действия.
При работе с, например, пошаговой игрой, решение нужно будет предпринимать разово.

Behavior Parameters позволяет настроить поведение. 
Тут также нужно дать имя, по которому модель найдет объект и здесь же устанавливается обученная модель.

## Задание 3
### Доработайте сцену и обучите ML-Agent таким образом, чтобы шар перемещался между двумя кубами разного цвета. Кубы должны, как и в первом задании, случайно изменять координаты на плоскости.


Увеличиваем Space Size у шара:

![image](https://user-images.githubusercontent.com/49882084/198334741-f0647f18-6172-4974-92d0-eab5e736dd5b.png)


Добавляем еще один куб:

![image](https://user-images.githubusercontent.com/49882084/198336019-bce141cd-4d0c-4c93-bef6-3c4e8f45cf2f.png)


Награду агент будет получать, если докоснется до обоих кубов:

```
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
    public Transform Target2;
    public bool gotTarget = false;
    public bool gotTarget2 = false;

    public override void OnEpisodeBegin()
    {
        if (this.transform.localPosition.y < 0)
        {
            this.rBody.angularVelocity = Vector3.zero;
            this.rBody.velocity = Vector3.zero;
            this.transform.localPosition = new Vector3(0, 0.5f, 0);
        }

        Target.localPosition = new Vector3(Random.value * 8-4, 0.5f, Random.value * 8-4);
        Target2.localPosition = new Vector3(Random.value * 8 - 4, 0.5f, Random.value * 8 - 4);
    }
    public override void CollectObservations(VectorSensor sensor)
    {
        sensor.AddObservation(Target.localPosition);
        sensor.AddObservation(Target2.localPosition);
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
        float distanceToTarget2 = Vector3.Distance(this.transform.localPosition, Target2.localPosition);

        if (distanceToTarget < 1.42f) gotTarget = true;
        if (distanceToTarget2 < 1.42f) gotTarget2 = true;

        if(gotTarget && gotTarget2)
        {
            SetReward(1.0f);
            gotTarget = false;
            gotTarget2 = false;
            EndEpisode();
        }
        else if (this.transform.localPosition.y < 0)
        {
            gotTarget = false;
            gotTarget2 = false;
            EndEpisode();
        }
    }
}

```


Не забываем указать второй куб второй целью:

![image](https://user-images.githubusercontent.com/49882084/198337460-22fe17bb-61b9-4d97-aeac-a097d79677ae.png)


Запускаем новое обучение:

![image](https://user-images.githubusercontent.com/49882084/198337278-a9c18be8-8419-45b3-a8bb-42654af44b74.png)
![image](https://user-images.githubusercontent.com/49882084/198337334-86c715ba-cd61-4840-b463-3774eec98206.png)


Вставляем в шар новую модель и проверяем:

![image](https://user-images.githubusercontent.com/49882084/198338059-fc73ec88-4a52-49bd-9fd4-e024161f2ce3.png)
![image](https://user-images.githubusercontent.com/49882084/198338094-f7b601c8-21ce-40e2-a12e-04938d3661e5.png)

Модель работает. Есть одна деталь - так как кубы не пропадают после касания, шар стукается об первый и после этого часто испытывает проблемы добраться до второго; но по итогу у него все равно получается.


## Выводы

Игровой баланс - баланс игровых механик между собой по самым разным параметрам, правила, по которым идет игра.

Баланс не обязан быть самым честным и справедливым. Его необходимо настроить так, чтобы игроки получали удовольствие, чувствовали
прогресс и выбор. Правила кардинально отличаются от игры к игре.

Машинное обучение позволяет создать игровой интеллект, работающий по оптимальным правилам непосредственно в настоящей игровой среде на данный момент, а не в теории.
Это, например, позволит проверить как отстроен игровой баланс. Как взаимодействуют разные механики, как в них могут повести себя игроки, и есть ли сильный перевес.
ML может заметно помочь в крупных системах, где сложно просчитать взаимодействия даже в теории.




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
