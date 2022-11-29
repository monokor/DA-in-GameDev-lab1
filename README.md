# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #4 выполнил(а):
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
Изучить работу перцептрона в Unity.

## Задание 1
### В проекте Unity реализовать перцептрон, который умеет производить вычисления.

Создаем пустой объект, вешаем на него скрипт перцептрона и заполняем ts.


OR

![image](https://user-images.githubusercontent.com/49882084/204563068-d22886d9-079b-401c-b78e-aadb82389f30.png)
![image](https://user-images.githubusercontent.com/49882084/204563135-7df68f72-98e9-499a-9c57-e948b0902055.png)


AND

![image](https://user-images.githubusercontent.com/49882084/204563836-5c0011f0-1c99-47bc-92ab-61d6bc86033c.png)
![image](https://user-images.githubusercontent.com/49882084/204563877-f7c901bf-0e1b-4b2e-968d-4af144db6194.png)


NAND

![image](https://user-images.githubusercontent.com/49882084/204564298-69cf91a5-3a67-48a7-89c9-66366e089cb0.png)
![image](https://user-images.githubusercontent.com/49882084/204564341-b3855ebe-75a9-4027-b947-88adf67c170f.png)


XOR

![image](https://user-images.githubusercontent.com/49882084/204564941-3deccfd9-ee93-4029-96d1-e424c18d783b.png)
![image](https://user-images.githubusercontent.com/49882084/204564966-25bfdc84-8fdb-4e2b-8029-478e2ca40205.png)

Одиночный перцептрон не сможет научиться решать XOR, потому что это не задача линейной классификации



## Задание 2
### Построить графики зависимости количества эпох от ошибки обучения. Указать от чего зависит необходимое количество эпох обучения.

![image](https://user-images.githubusercontent.com/49882084/204572655-8744d6d7-c9ca-4903-915b-7b2712e03d64.png)
![image](https://user-images.githubusercontent.com/49882084/204572710-494306b1-f62a-4160-8cbd-14258d0fab7e.png)
![image](https://user-images.githubusercontent.com/49882084/204572764-294e708b-0b41-481c-ab79-5bfa1e0e0431.png)
![image](https://user-images.githubusercontent.com/49882084/204572801-8f99ead6-b53a-45f2-a3e5-37236317bec9.png)

Необходимое количество эпох зависит от сложности задачи и рандома, который участвует в инициализации весов.
На графике "исключающего или" видно, что увеличение эпох не решит эту задачу.



## Задание 3
### Построить визуальную модель работы перцептрона на сцене Unity.

![image](https://user-images.githubusercontent.com/49882084/204587270-ab5de9a7-3941-4095-8cce-4dcc686220d7.png)

Создал простую сцену с двумя кубами. Красный = 0, Зелёный = 1.

Добавил нижнему кубу скрипт на столкновение с верхним. Он изменяет цвета обоих кубов как логический оператор "или":

```
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class TriggerOR : MonoBehaviour
{
    private void OnTriggerEnter(Collider other) 
    {
        if (other.gameObject.GetComponent<Renderer>().material.color == Color.green || this.gameObject.GetComponent<Renderer>().material.color == Color.green) 
        {
            other.gameObject.GetComponent<Renderer>().material.color = Color.green;
            this.gameObject.GetComponent<Renderer>().material.color = Color.green;
        }
        else
        {
            other.gameObject.GetComponent<Renderer>().material.color = Color.red;
            this.gameObject.GetComponent<Renderer>().material.color = Color.red;
        }
    }
}
```


![image](https://user-images.githubusercontent.com/49882084/204588315-ba86ca98-e9d9-493b-887c-a2db7a3d934c.png)
![image](https://user-images.githubusercontent.com/49882084/204588384-c7e0a378-4f52-4aad-8b7e-0a8315545a5b.png)


![image](https://user-images.githubusercontent.com/49882084/204588495-09648cdc-464f-4af4-a9bb-c9ac85e2392c.png)
![image](https://user-images.githubusercontent.com/49882084/204588525-8ffe0e70-133f-4295-89ea-cff610eda80b.png)


![image](https://user-images.githubusercontent.com/49882084/204588572-27cb4e5e-1790-4012-900e-d059e3b1a9a2.png)
![image](https://user-images.githubusercontent.com/49882084/204588600-9ffacb76-5578-422f-83c9-f07fd4a0144c.png)


![image](https://user-images.githubusercontent.com/49882084/204588844-fea29725-0ad2-482a-853e-64aff723c679.png)
![image](https://user-images.githubusercontent.com/49882084/204588871-9f8c26d1-d921-426f-966c-8e8a3d8e96df.png)


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
