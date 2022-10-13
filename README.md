# СБОР, ОБРАБОТКА И ВИЗУАЛИЗАЦИЯ ТЕСТОВОГО НАБОРА ДАННЫХ.
Отчет по лабораторной работе #2 выполнил(а):
- Гайнутдинов Денис Маратович
- РИ210911
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
Познакомиться с программными средствами для организции передачи данных между инструментами google, Python и Unity

## Задание 1
### Написать программы Hello World на Python и Unity.
Реализовать совместную работу и передачу данных в связке Python - Google-Sheets – Unity. При выполнении задания используйте видео-материалы и исходные данные, предоставленные преподавателя курса. 

- В облачном сервисе google console подключить API для работы с google sheets и google drive.

![Снимок экрана (288)](https://user-images.githubusercontent.com/104080323/195115447-a7d13df6-a8cf-4fe9-8872-edee836b7c2f.png)

![Снимок экрана (289)](https://user-images.githubusercontent.com/104080323/195115461-93227873-de4f-44c5-b3d5-41bcd8f5cfa2.png)

- Реализовать запись данных из скрипта на python в google-таблицу. Данные описывают изменение темпа инфляции на протяжении 11 отсчётных периодов, с учётом стоимости игрового объекта в каждый период

![Снимок экрана (295)](https://user-images.githubusercontent.com/104080323/195120623-8ddb7684-eeb1-4bf5-bc26-57c190e3d8ab.png)

![Снимок экрана (296)](https://user-images.githubusercontent.com/104080323/195120679-4b7b2d75-8c1d-4154-b11c-0173dfc2c164.png)

- Создать новый проект на Unity, который будет получать данные из google-таблицы, в которую были записаны данные в предыдущем пункте

![Снимок экрана (302)](https://user-images.githubusercontent.com/104080323/195136859-c5bb12ca-0529-410c-abf5-4080f1438694.png)

- Написать функционал на Unity, в котором будет воспроизводиться аудио-файл в зависимости от значения данных из таблицы.

https://user-images.githubusercontent.com/104080323/195138580-28a0334b-27c6-4a46-9c42-c10ba730b066.mp4



## Задание 2
### Реализовать запись в Google-таблицу набора данных, полученных с помощью линейной регрессии из лабораторной работы № 1. 

```py

import gspread
import numpy as np
import matplotlib.pyplot as plt

def model(a, b, x):
    return a*x + b

def loss_function(a, b, x, y):
    num = len(x)
    prediction=model(a,b,x)
    return (0.5/num) * (np.square(prediction-y)).sum()

def optimize(a,b,x,y):
    num = len(x)
    prediction = model(a,b,x)
    da = (1.0/num) * ((prediction -y)*x).sum()
    db = (1.0/num) * ((prediction -y).sum())
    a = a - Lr*da
    b = b - Lr*db
    return a, b

def iterate(a,b,x,y,times):
    for i in range(times):
        a,b = optimize(a,b,x,y)
    return a,b

gc = gspread.service_account(filename='unitudatascience-6feb3cf2e6b7.json')
sh = gc.open('UnitySheets')
price = np.random.randint(2000, 10000, 11)
mon = list(range(1, 11))
i = 0


x = [3,21,22,34,54,34,55,67,89,99]
x = np.array(x)
y = [2,22,24,65,79,82,55,130,150,199]
y = np.array(y)
plt.scatter(x,y)

a = np.random.rand(1)
# print(a)
b = np.random.rand(1)
# print(b)
Lr = 0.000001

while i <= len(mon):
    i += 1
    a, b = iterate(a, b, x, y, i)
    prediction = model(a, b, x)
    loss = loss_function(a, b, x, y)
    print(a, b, loss)
    plt.scatter(x, y)
    plt.plot(x, prediction)
    if i == 0:
        continue
    else:
        tempInf = ((price[i - 1] - price[i - 2])/price[i - 2]) * 100
        tempInf = str(tempInf)
        tempInf = tempInf.replace('.', ',')
        sh.sheet1.update(('A' + str(i)), str(i))
        sh.sheet1.update(('B' + str(i)), str(a))
        sh.sheet1.update(('C' + str(i)), str(b))
        sh.sheet1.update(('D' + str(i)), str(loss))
        print(tempInf)

```

https://user-images.githubusercontent.com/104080323/195146514-6ffb2dec-f6d9-4930-ae52-d19db1d87066.mp4


## Задание 3
#### Самостоятельно разработать сценарий воспроизведения звукового сопровождения в Unity в зависимости от изменения считанных данных в задании 2.

![Снимок экрана (303)](https://user-images.githubusercontent.com/104080323/195151090-d51eaf0a-d61f-4a9c-8128-6ce4ce4ca59b.png)


## Выводы

В результате данной лабораторной работы мы смогли реализовать совместную работу и передачу данных в связке Python - Google-Sheets – Unity. Разобрались в работе алгоритма работы с таблицами.

| GitHub | https://github.com/Denis-GM/DA-in-GameDev-lab2 |

## Powered by

**BigDigital Team: Denisov | Fadeev | Panov**
