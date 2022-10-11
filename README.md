# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #2 выполнил(а):
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
Познакомиться с программными средствами для организации передачи данных между инструментами google, Python и Unity.

## Задание 1
### Реализовать совместную работу и передачу данных в связке Python - Google-Sheets - Unity.

Создаем проект на Google Cloud, устанавливаем необходимые API и получаем ключи: 

![image](https://user-images.githubusercontent.com/49882084/195112762-432c4790-0c4e-4213-afdf-20ed427bef6b.png)


Создаем гугл-таблицу и выдаем права: 

![image](https://user-images.githubusercontent.com/49882084/195113495-ab909d8e-737c-4f0b-a17f-ea420d454a22.png)


Создаем python-проект со скачанным ключом в директории, пишем код для создания и отправки данных в гугл таблицу: 

![image](https://user-images.githubusercontent.com/49882084/195114658-be7aee87-b42d-471b-b24e-7af2f5fa988e.png)
![image](https://user-images.githubusercontent.com/49882084/195115180-e66a8f16-3a64-426d-87a5-caa2b7f53253.png)


Создаем unity-проект и загружаем туда скриптовые файлы и звуки:

![image](https://user-images.githubusercontent.com/49882084/195116435-9267d896-8fb3-431e-b25a-1859e8cbc979.png)


Создаем пустой объект, добавляем ему скрипт, достающий данные с таблицы и проигрывающий звуки:

![image](https://user-images.githubusercontent.com/49882084/195118371-5ff041cc-a410-4b32-8706-a353d541e78d.png)
![image](https://user-images.githubusercontent.com/49882084/195118473-ae7458d3-bbae-47e2-9b83-afabc4f5e545.png)
![image](https://user-images.githubusercontent.com/49882084/195118519-8d344eee-3949-40fd-8cf9-33cfd37c4238.png)


Запускаем. В консоль выводятся данные, проигрываются разные звуки в зависимости от значений:

![image](https://user-images.githubusercontent.com/49882084/195118955-5919bee9-d438-4b22-99e6-5bbe15882a83.png)



## Задание 2
### Реализовать запись в Google-таблицу набора данных, полученных с помощью линейной регрессии из лабораторной работы № 1. 

Пусть наш код записывает в таблицу loss после каждых 100 итераций:

![image](https://user-images.githubusercontent.com/49882084/195157797-023b5b7a-f295-4d06-8288-3899cf72323e.png)
![image](https://user-images.githubusercontent.com/49882084/195157848-817a5b67-0703-4264-9ebe-38c18e4e5374.png)

![image](https://user-images.githubusercontent.com/49882084/195157985-7ddbd995-44eb-401e-a41d-b888cb05780e.png)



## Задание 3
### Самостоятельно разработать сценарий воспроизведения звукового сопровождения в Unity в зависимости от изменения считанных данных в задании 2.

Переписываем скрипт так, чтобы "положительный" звук был при меньших значениях loss с таблицы.

![image](https://user-images.githubusercontent.com/49882084/195167571-e2c5bf14-9fac-40f2-8e77-d83c56bd8eb2.png)

![image](https://user-images.githubusercontent.com/49882084/195167706-b106ad7e-68a6-4a02-90e3-92bad5fa9899.png)


## Выводы



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
