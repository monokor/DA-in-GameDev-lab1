# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #1 выполнил(а):
- Зуев Владислав Анатольевич
- РИ210915

Отметка о выполнении заданий (заполняется студентом):

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 60 |
| Задание 2 | * | 20 |
| Задание 3 | # | 20 |

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

Подготавливаем данные, переводим их в массивы
![image](https://user-images.githubusercontent.com/49882084/192350141-09edc065-197a-4f16-9404-749f355f5adb.png)

Определяем функции модели, потерь и оптимизации
![image](https://user-images.githubusercontent.com/49882084/192350437-76642447-97b8-4f30-bf53-cba2e8077dee.png)

Инициализируем и начинаем первую итерацию
![image](https://user-images.githubusercontent.com/49882084/192352363-720345b1-1019-4d0e-b556-ebf62cd700d4.png)

Итерации 2-5
![image](https://user-images.githubusercontent.com/49882084/192352479-17a00257-b300-4f23-b47d-6aff933333f3.png)
![image](https://user-images.githubusercontent.com/49882084/192352532-771d7493-adaf-48aa-9921-b3e21aad10cc.png)
![image](https://user-images.githubusercontent.com/49882084/192352572-99583997-c232-4f10-98d7-2380672ac73e.png)
![image](https://user-images.githubusercontent.com/49882084/192352636-34211705-a781-483b-99e0-cc86f582fa6c.png)

10000-я итерация
![image](https://user-images.githubusercontent.com/49882084/192352861-fc072184-d37c-4512-874c-cf022fb787ed.png)


## Задание 3
### Какова роль параметра Lr? Ответьте на вопрос, приведите пример выполнения кода, который подтверждает ваш ответ. В качестве эксперимента можете изменить значение параметра.

- Перечисленные в этом туториале действия могут быть выполнены запуском на исполнение скрипт-файла, доступного [в репозитории](https://github.com/Den1sovDm1triy/hfss-scripting/blob/main/ScreatingSphereInAEDT.py).
- Для запуска скрипт-файла откройте Ansys Electronics Desktop. Перейдите во вкладку [Automation] - [Run Script] - [Выберите файл с именем ScreatingSphereInAEDT.py из репозитория].

```py

import ScriptEnv
ScriptEnv.Initialize("Ansoft.ElectronicsDesktop")
oDesktop.RestoreWindow()
oProject = oDesktop.NewProject()
oProject.Rename("C:/Users/denisov.dv/Documents/Ansoft/SphereDIffraction.aedt", True)
oProject.InsertDesign("HFSS", "HFSSDesign1", "HFSS Terminal Network", "")
oDesign = oProject.SetActiveDesign("HFSSDesign1")
oEditor = oDesign.SetActiveEditor("3D Modeler")
oEditor.CreateSphere(
	[
		"NAME:SphereParameters",
		"XCenter:="		, "0mm",
		"YCenter:="		, "0mm",
		"ZCenter:="		, "0mm",
		"Radius:="		, "1.0770329614269mm"
	], 
)

```

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
