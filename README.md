# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #2 выполнил:
- Дубровский Давид Русланович
- РИ-210912
Отметка о выполнении заданий (заполняется студентом):

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 60 |
| Задание 2 | # | 20 |
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
Познакомиться с программными средствами для организции передачи данных между инструментами google, Python и Unity

## Задание 1 

Для того чтобы передавать данные между google, Python и Unity создал проект в google cloud

![создал проект](https://user-images.githubusercontent.com/92369801/195123273-55c41fd0-4bd7-45bc-b98f-0a63a48749d4.jpg


Загрузил необходимые api для google drive и google sheets. Завел сервисный аккаунт через который будет происходить передача данных между инструментами и получил ключ

![2](https://user-images.githubusercontent.com/92369801/195123341-81b6720c-7660-48cd-b8d0-77b3cdda2f92.jpg)

Создал файл google sheets связал с google cloud, также установил нужные плагины для python и привязал python по ключу к сервисному аккаунту, вследствии гугл таблица заполнялась выводами на консоль из питона

![3](https://user-images.githubusercontent.com/92369801/195123607-d4cbbf3a-9fbe-4e85-91ec-e564055553b1.jpg)

Создал проект в unity в который закинул звуки и файлы json, создал Audio Source компонент и файл скрипта

![4](https://user-images.githubusercontent.com/92369801/195123656-0eb44934-0e5c-42f7-a676-80b5a12c907b.jpg)

В скрипте импортируем и преобразуем данные из гугл таблиц, настраиваем обновление данных и создаем энумераторы для каждого звука

![5](https://user-images.githubusercontent.com/92369801/195123701-191bb326-1eed-4862-ad02-522f5d551619.jpg)

![6](https://user-images.githubusercontent.com/92369801/195123757-c97c2876-12ca-4094-9e64-6c3f859ab26b.jpg)

После чего при запуске проекта Unity воспроизводятся звуки, воспроизведение которых зависит от данных в гугл таблице

## Выводы

В ходе лабораторной работы ....

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
