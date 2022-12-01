# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #5 выполнил(а):
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
Интегрировать экономическую систему в Unity-проект с использованием ML-Agent.


## Задание 1
### Изменить параметры файла yaml-агента и определить какие параметры и как влияют на обучение модели.

Я изменил систему награждения в скрипте:


```
tempInf = ((pricesMonth[1] - pricesMonth[0]) / pricesMonth[0]) * 100;

if (tempInf <= 1f) SetReward(1.0f);
else if (tempInf <= 3f) SetReward(0.6f);
else if (tempInf <= 6f) SetReward(0.3f);
else if (tempInf <= 20f) SetReward(0.1f);
else if (tempInf <= 50f) SetReward(0.0f);
else SetReward(-0.5f);

EndEpisode();
```

Так я рассчитываю, что обучение и графики будут стабильнее, а модели будет проще обучаться.


Прочитал документацию, проверил около 60 вариантов конфигурации Economic.yaml и, не считая погрешностей, пришел к следующим выводам:

batch_size - количество опытов в каждой итерации. В нашем случае лучше поставить поменьше

buffer_size - количество собранных опытов перед обновлением политики. Должно быть в разы больше batch_size, но, если переборщить, политика будет обновляться очень редко и картина будет нестабильной

learning_rate - скорость (интенсивность) обучения. Возможно, большие значения ускорят обучение, но меньшие способствуют стабильности. В нашем небольшом эксперименте желательно поставить поменьше, потому что модель либо слишком быстро научится (не наглядно), либо учиться будет нестабильно

beta - изменение энтропии (разброса значений при обучении). По аналогии с прошлым, лучше уменьшить

epsilon - насколько быстро модели можно обучаться. Чем меньше, тем стабильнее, но медленнее обучение. В нашей небольшой сцене обучение итак недолгое, я выбрал стабильность

max_steps - ограничение по общему количеству шагов. На самом деле важный параметр, ведь beta и learning_rate уменьшаются линейно вплоть до 0 на последнем шаге; поэтому влияет на обучение.



Также увеличил количество префабов, что сильно ускорило обучение и повлияло на него. Не разобрался почему, но на шагах больше 200000 модель резко ломалась (после 100000 успешных шагов)

Явное влияние остальных параметров ("изменить, чтобы стало лучше") не заметил, но у меня обучение в принципе вело себя непредсказуемо


Пример одной из конфигураций:

```
behaviors:
  Economic:
    trainer_type: ppo
    hyperparameters:
      batch_size: 256
      buffer_size: 10240
      learning_rate: 1.0e-5
      learning_rate_schedule: linear
      beta: 0.0001
      epsilon: 0.1
      lambd: 0.93
      num_epoch: 3      
    network_settings:
      normalize: false
      hidden_units: 128
      num_layers: 2
    reward_signals:
      extrinsic:
        gamma: 0.99
        strength: 1.0
    checkpoint_interval: 500000
    max_steps: 200000
    time_horizon: 64
    summary_freq: 1000
    self_play:
      save_steps: 20000
      team_change: 100000
      swap_steps: 10000
      play_against_latest_model_ratio: 0.5
      window: 10
```





## Задание 2
### Описать результаты, выведенные в TensorBoard.

Примеры некоторых полученных графиков (сглаживание - 0.999):

![image](https://user-images.githubusercontent.com/49882084/205174015-99644dab-ee80-4515-85cd-f4b7756caace.png)
![image](https://user-images.githubusercontent.com/49882084/205174056-b23605e1-69e3-453b-b002-6e84f32c5ddc.png)
![image](https://user-images.githubusercontent.com/49882084/205174078-13b22ccf-78b7-4638-b526-45e82fe17fe1.png)

Cumulative Reward - награда модели за выполненные действия. Должна постепенно приходить к максимуму (= 1). Часто модель сразу попадала в единицу (удачный случай?), но тогда не понятен её процесс обучения. Также можно заметить аномальный провал после 200000

Episode Length - длина эпизода; хорошо, если снижается. Но в нашем случае, видимо, мало что означает и почти не зависит от параметров


Policy Loss - насколько изменяется политика модели. В общем, должно снижаться, по мере обученности модели. У меня были примеры с явным снижением, но часто остается неизменным (возможно, простой пример для обучения)

Value Loss - насколько хорошо агент прогнозирует значение своего следующего состояния. В теории, должно сначала увеличиться, а затем остановиться/снижаться. В моем случае всегда снижается (возможно, в этом примере сразу попадает в момент пика и затем снижается)


Entropy - энтропия. Должна снижаться. У меня часто увеличивалась, так и не понял почему

Extrinsic Value Estimate - оценка внешней стоимости. Чтобы отражать увеличение знаний, должно расти, а затем остановиться. У меня, как и энтропия, часто вела себя зеркально, не нашел объяснения


Beta, Epsilon и Learning Rate - отражают заданные в конфигурации значения


## Выводы

В ходе лабораторной работы, на практике внедрил MLAgent в экономическую систему на Unity. Познакомился с TensorBoard. Узнал больше об ML-агентах, настройке их параметров и общей работе.

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
