# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #1 выполнил(а):
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
Ознакомиться с основными операторами зыка Python на примере реализации линейной регрессии.

## Задание 1
### Написать программу Hello World на Python и Unity

![colab_hello](https://user-images.githubusercontent.com/49882084/192342493-d1236441-f93e-455b-ab3a-9e2d46316ee0.jpg)
![unity_hello](https://user-images.githubusercontent.com/49882084/192342505-accb2c09-ac07-4f6a-9144-e5f33f9bdae8.jpg)


## Задание 2
### Пошагово выполнить каждый пункт раздела "ход работы" с описанием и примерами реализации задач

Подготавливаем данные, переводим их в массивы:

![image](https://user-images.githubusercontent.com/49882084/192350141-09edc065-197a-4f16-9404-749f355f5adb.png)


Определяем функции модели, потерь и оптимизации:

![image](https://user-images.githubusercontent.com/49882084/192350437-76642447-97b8-4f30-bf53-cba2e8077dee.png)


Инициализируем и начинаем первую итерацию:

![image](https://user-images.githubusercontent.com/49882084/192352363-720345b1-1019-4d0e-b556-ebf62cd700d4.png)


Итерации 2-5:

![image](https://user-images.githubusercontent.com/49882084/192352479-17a00257-b300-4f23-b47d-6aff933333f3.png)

![image](https://user-images.githubusercontent.com/49882084/192352532-771d7493-adaf-48aa-9921-b3e21aad10cc.png)

![image](https://user-images.githubusercontent.com/49882084/192352572-99583997-c232-4f10-98d7-2380672ac73e.png)

![image](https://user-images.githubusercontent.com/49882084/192352636-34211705-a781-483b-99e0-cc86f582fa6c.png)


10000-я итерация:

![image](https://user-images.githubusercontent.com/49882084/192394684-21ee8f53-2e00-4746-af09-9eb6eeb31c85.png)



## Задание 3
### Должна ли величина loss стремиться к нулю при изменении исходных данных? Ответьте на вопрос, приведите пример выполнения кода, который подтверждает ваш ответ.

Да, она всегда стремится к нулю при множественных итерациях (заметно в задании 2)


Для примера возьмем более "удобные" данные и повторим те же действия:

![image](https://user-images.githubusercontent.com/49882084/192357473-857e23c8-8df4-46cf-9127-a2ae68b3d80f.png)

![image](https://user-images.githubusercontent.com/49882084/192357502-f3baf4e5-f30b-4443-8735-355a50418934.png)

![image](https://user-images.githubusercontent.com/49882084/192357533-800a929c-9da5-4a91-a40f-9c4703b1e6e3.png)


К 10000-й итерации loss совсем мал:

![image](https://user-images.githubusercontent.com/49882084/192357689-39fff051-ef98-4435-aea9-da3b55611a57.png)



### Какова роль параметра Lr? Ответьте на вопрос, приведите пример выполнения кода, который подтверждает ваш ответ. В качестве эксперимента можете изменить значение параметра.

Lr - коэффициент, который влияет на шаг при итерации

При слишком большом Lr модель может так и не получится:

![image](https://user-images.githubusercontent.com/49882084/192394138-453599d7-402c-4596-89a0-83133f34592e.png)

![image](https://user-images.githubusercontent.com/49882084/192394168-d9f0adf0-7704-4865-8604-eb71a6c489e3.png)

![image](https://user-images.githubusercontent.com/49882084/192394193-4cb1f347-c692-4b09-830a-c1225b8d95a5.png)

![image](https://user-images.githubusercontent.com/49882084/192394205-c00c4634-2bec-4480-8335-53019d04eceb.png)


А при слишком малом займет крайне много итераций:

![image](https://user-images.githubusercontent.com/49882084/192394353-3ced2861-3517-43e4-a102-1d0b2292153c.png)

![image](https://user-images.githubusercontent.com/49882084/192394393-003f50ee-4325-4ad1-9f2f-b840ee4bd046.png)

![image](https://user-images.githubusercontent.com/49882084/192394440-e3983810-1b68-4c12-a731-d3926d03d9c8.png)


## Выводы

Абзац умных слов о том, что было сделано и что было узнано.

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
