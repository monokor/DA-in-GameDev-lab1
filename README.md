# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #1 выполнил:
- Дубровский Давид Русланович
- РИ-210912
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
Написать программу Hello World на Python и на Unity

![Screenshot_1](https://user-images.githubusercontent.com/92369801/192562632-87982fdd-d9c8-4d8d-92e7-afcc0f303642.jpg)

![Screenshot_4](https://user-images.githubusercontent.com/92369801/192562734-c4012083-3f6b-4919-84a8-2ebdb755ad48.jpg)


## Задание 2
### Пошагово выполнить каждый пункт раздела "ход работы" с описанием и примерами реализации задач
- Произвести подготовку данных для работы с алгоритмом линейной регрессии. 10 видов данных были установлены случайным образом, и данные находились в линейной зависимости. Данные преобразуются в формат массива, чтобы их можно было вычислить напрямую при использовании умножения и сложения.

![Screenshot_2](https://user-images.githubusercontent.com/92369801/192563741-9209cda9-6700-4260-9f0c-1725691b481a.jpg)

- Определите связанные функции. Функция модели: определяет модель линейной регрессии wx+b. Функция потерь: функция потерь среднеквадратичной ошибки. Функция оптимизации: метод градиентного спуска для нахождения частных производных w и b.

![Screenshot_3](https://user-images.githubusercontent.com/92369801/192567212-b133ca07-1f9d-446a-86f8-4306ccc65f56.jpg)

Инициализируем и итерируем

1 по 5 итерация

![1](https://user-images.githubusercontent.com/92369801/192572165-ceb84ed3-1fad-4ebb-92fd-c53114b7173b.jpg)

![2](https://user-images.githubusercontent.com/92369801/192572174-163b2579-0ce9-48c0-b8fc-261678f4d1b2.jpg)

![3](https://user-images.githubusercontent.com/92369801/192572183-1a67ed41-4ce7-4c85-bd02-73bca6aa7640.jpg)

![4](https://user-images.githubusercontent.com/92369801/192572191-dfc22e36-7028-4b3b-a170-c2433a1750e5.jpg)

![5](https://user-images.githubusercontent.com/92369801/192572197-cfe928fd-5172-4741-8c6d-a8bb7129be75.jpg)


1000-я итерация

![10000](https://user-images.githubusercontent.com/92369801/192572204-b6b5e267-ad7f-44e3-9b3e-2a6f976d9b0e.jpg)


## Задание 3
### Должна ли величина loss стремиться к нулю при изменении исходных данных? Ответьте на вопрос, приведите пример выполнения кода, который подтверждает ваш ответ.

Величина loss стремится к нулю при множественных итерациях.

Для примера проведем те же самые действия с другими данными

![1](https://user-images.githubusercontent.com/92369801/192574589-7092d8a1-4ab9-4460-85ae-755a393dde07.jpg)

![2](https://user-images.githubusercontent.com/92369801/192574647-3c2c61ad-5ecc-41cc-80f1-636f6a007a86.jpg)

на 10000 итерации loss совсем мал

![3](https://user-images.githubusercontent.com/92369801/192574694-bfb53075-12e1-4955-936e-c9d9fcce8150.jpg)


### Какова роль параметра Lr? Ответьте на вопрос, приведите пример выполнения кода, который подтверждает ваш ответ. В качестве эксперимента можете изменить значение параметра.

- Перечисленные в этом туториале действия могут быть выполнены запуском на исполнение скрипт-файла, доступного [в репозитории](https://github.com/Den1sovDm1triy/hfss-scripting/blob/main/ScreatingSphereInAEDT.py).
- Для запуска скрипт-файла откройте Ansys Electronics Desktop. Перейдите во вкладку [Automation] - [Run Script] - [Выберите файл с именем ScreatingSphereInAEDT.py из репозитория].

Lr - коэффициент, который влияет на шаг при итерации.

При слишком большом Lr модель станет некорректной

![1](https://user-images.githubusercontent.com/92369801/192575820-33e522bb-a134-45f6-83d0-d7a0651d1d01.jpg)

![2](https://user-images.githubusercontent.com/92369801/192575828-c50db45e-e4b0-4812-a496-d19c7f5ebbf1.jpg)

А при слишком маленьком понадобиться большое количество итераций

![3](https://user-images.githubusercontent.com/92369801/192575972-5043c7a6-0666-4bcf-a645-3c5c7f6ce797.jpg)

![4](https://user-images.githubusercontent.com/92369801/192575983-b3116dd1-a5e0-4598-be64-b7c382a36a1b.jpg)

![5](https://user-images.githubusercontent.com/92369801/192575992-292b21ea-591c-4e39-a520-4d79bc3c50c9.jpg)


## Выводы

В ходе лабораторной работы вспомнил Google Colab и познакомился Unity. Опробовал библиотеки NumPy и Matplotlib, построил первую модель и узнал как она работает.

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
