# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
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
- 
![Снимок экрана (302)](https://user-images.githubusercontent.com/104080323/195136859-c5bb12ca-0529-410c-abf5-4080f1438694.png)

- Написать функционал на Unity, в котором будет воспроизводиться аудио-файл в зависимости от значения данных из таблицы.

https://user-images.githubusercontent.com/104080323/195136659-fd83ac2f-c9b9-4122-bf89-8af3a476e00d.mov


## Задание 2
### Пошагово выполнить каждый пункт раздела "ход работы" с описанием и примерами реализации задач
Ход работы:
1. Произвести подготовку данных для работы с алгоритмом линейной регрессии. 10 видов данных были установлены случайным образом, и данные находились в линейной зависимости. Данные преобразуются в формат массива, чтобы их можно было вычислить напрямую при использовании умножения и сложения.

```py

import numpy as np
import matplotlib.pyplot as plt
%matplotlib inline

x = [3,21,22,34,54,34,55,67,89,99]
x = np.array(x)
y = [2,22,24,65,79,82,55,130,150,199]
y = np.array(y)

plt.scatter(x,y)

```

2. Определите связанные функции. Функция модели: определяет модель линейной регрессии wx+b. Функция потерь: функция потерь среднеквадратичной ошибки. Функция оптимизации: метод градиентного спуска для нахождения частных производных w и b.

```py

import numpy as np
import matplotlib.pyplot as plt
%matplotlib inline

x = [3,21,22,34,54,34,55,67,89,99]
x = np.array(x)
y = [2,22,24,65,79,82,55,130,150,199]
y = np.array(y)

plt.scatter(x,y)

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

```

3. Начать итерацию
- Шаг 1 Инициализация и модель итеративной оптимизации

```py

import numpy as np
import matplotlib.pyplot as plt
%matplotlib inline

x = [3,21,22,34,54,34,55,67,89,99]
x = np.array(x)
y = [2,22,24,65,79,82,55,130,150,199]
y = np.array(y)
plt.scatter(x,y)

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

a = np.random.rand(1)
print(a)
b = np.random.rand(1)
print(b)
Lr = 0.000001

a,b = iterate(a,b,x,y,1)
prediction=model(a,b,x)
loss = loss_function(a, b, x, y)
print(a,b,loss)
plt.scatter(x,y)
plt.plot(x,prediction)

```
![загруженное](https://user-images.githubusercontent.com/104080323/192595757-5bfdcbb9-5a5f-46fc-9f56-74e167516341.png)

- Шаг 2 На второй итерации отображаются значения параметров, значения потерь и эффекты визуализации после итерации.

```py
a,b = iterate(a,b,x,y,2)
prediction=model(a,b,x)
loss = loss_function(a, b, x, y)
print(a,b,loss)
plt.scatter(x,y)
plt.plot(x,prediction)
```

![загруженное (10)](https://user-images.githubusercontent.com/104080323/192598976-d3705698-165e-4455-9b55-7613ea04a7e8.png)

- Шаг 3 Третья итерация показывает значения параметров, значения потерь и визуализацию после итерации.

```py
a,b = iterate(a,b,x,y,3)
prediction=model(a,b,x)
loss = loss_function(a, b, x, y)
print(a,b,loss)
plt.scatter(x,y)
plt.plot(x,prediction)
```

![загруженное (3)](https://user-images.githubusercontent.com/104080323/192596933-e2a862c0-019d-40e4-a467-c2b5fefcffce.png)

- Шаг 4 На четвертой итерации отображаются значения параметров, значения потерь и эффекты визуализации

```py
a,b = iterate(a,b,x,y,4)
prediction=model(a,b,x)
loss = loss_function(a, b, x, y)
print(a,b,loss)
plt.scatter(x,y)
plt.plot(x,prediction)
```

![загруженное (8)](https://user-images.githubusercontent.com/104080323/192598403-70ba85f9-1ee5-48ab-bfe4-8c279839a567.png)

- Шаг 5 Пятая итерация показывает значение параметра, значение потерь и эффект визуализации после итерации

```py
a,b = iterate(a,b,x,y,5)
prediction=model(a,b,x)
loss = loss_function(a, b, x, y)
print(a,b,loss)
plt.scatter(x,y)
plt.plot(x,prediction)
```

![загруженное (9)](https://user-images.githubusercontent.com/104080323/192598469-4d44b603-3f88-450b-b12d-bb7ca205c903.png)

- Шаг 6 10000-я итерация, показывающая значения параметров, потери и визуализацию после итерации

```py
a,b = iterate(a,b,x,y,1000)
prediction=model(a,b,x)
loss = loss_function(a, b, x, y)
print(a,b,loss)
plt.scatter(x,y)
plt.plot(x,prediction)
```

![загруженное (7)](https://user-images.githubusercontent.com/104080323/192598154-96dc1c82-ce78-47b5-baa7-76ffea1d1e87.png)

## Задание 3
#### Должна ли величина loss стремиться к нулю при изменении исходных данных? Ответьте на вопрос, приведите пример выполнения кода, который подтверждает ваш ответ.
В связи с тем, что loss - это величина, характеризующая количество потерь, то она должна стремиться к нулю при изменении исходных данных.
В листе lossArr находятся все значения loss, полученные в 1, 100 и 1000 итерациях. Можно увидеть, что элементы уменьшаются.

```py
import numpy as np
import matplotlib.pyplot as plt
%matplotlib inline

x = [5,23,25,37,57,37,59,70,92,102]
x = np.array(x)
y = [6,26,28,69,83,86,58,134,154,204]
y = np.array(y)
plt.scatter(x,y)

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

a = np.random.rand(1)
print(a)
b = np.random.rand(1)
print(b)
Lr = 0.000001

lossArr = []

a,b = iterate(a,b,x,y,1)
prediction=model(a,b,x)
loss = loss_function(a, b, x, y)
lossArr.append(loss)
plt.scatter(x,y)
plt.plot(x,prediction)

a,b = iterate(a,b,x,y,100)
prediction=model(a,b,x)
loss = loss_function(a, b, x, y)
lossArr.append(loss)
plt.scatter(x,y)
plt.plot(x,prediction)

a,b = iterate(a,b,x,y,1000)
prediction=model(a,b,x)
loss = loss_function(a, b, x, y)
lossArr.append(loss)
plt.scatter(x,y)
plt.plot(x,prediction)

print(lossArr)
```
#### Какова роль параметра Lr? Ответьте на вопрос, приведите пример выполнения кода, который подтверждает ваш ответ. В качестве эксперимента можете изменить значение параметра.
Параметр Lr является коэфициентом, при помощи которого регулируют угол наклона прямой.

```py
import numpy as np
import matplotlib.pyplot as plt
%matplotlib inline

x = [5,23,25,37,57,37,59,70,92,102]
x = np.array(x)
y = [6,26,28,69,83,86,58,134,154,204]
y = np.array(y)
plt.scatter(x,y)

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

a = np.random.rand(1)
print(a)
b = np.random.rand(1)
print(b)

Lr = 0.000001

a,b = iterate(a,b,x,y,1)
prediction=model(a,b,x)
loss = loss_function(a, b, x, y)
plt.scatter(x,y)
plt.plot(x,prediction)

Lr = 0.0001

a,b = iterate(a,b,x,y,1)
prediction=model(a,b,x)
loss = loss_function(a, b, x, y)
plt.scatter(x,y)
plt.plot(x,prediction)
```

## Выводы

В результате данной лабораторной работы мы смогли ознакомиться с основными операторами зыка Python на примере реализации линейной регрессии. 
Разобрали роли различных параметров в коде программы, а также изучили методы отрисовки графиков на языке Python.

| GitHub | https://github.com/Denis-GM/DA-in-GameDev-lab1 |

| Google Colab | https://colab.research.google.com/drive/1PXpS7XKVcOqZUt-2RmS_P1zLetryvb8l?usp=sharing |

## Powered by

**BigDigital Team: Denisov | Fadeev | Panov**
