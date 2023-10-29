
# DA-in-GameDev-lab-3
# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #3 выполнил(а):
- Кучеренко Валентин Сергеевич
- НМТ-223502


| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | *| 60 |
| Задание 2 | * | 20 |
| Задание 3 | * | 20 |

знак "*" - задание выполнено; знак "#" - задание не выполнено;

Работу проверили:
- к.т.н., доцент Денисов Д.В.
- к.э.н., доцент Панов М.А.
- ст. преп., Фадеев В.О.

## Цель работы
Разработать оптимальный баланс для десяти уровней игры Dragon Picker.

## Задание 1
### Предложите вариант изменения найденных переменных для 10 уровней в игре. Визуализируйте изменение уровня сложности в таблице.
-Ниже представлен список переменных для балансировки уровней:
  1. Количество энергетических щитов
  2. Скорость дракона
  3. Время между спавном яиц
  4. Минимальная дистанция до края
- Ссылка на таблицу с данными и их визуализацией: https://docs.google.com/spreadsheets/d/1RTjNz9ZCV2A4FhTNOj5D7DxRNzzhk2XX6rvUGnqdFHc/edit?usp=sharing

## Задание 2
### Создайте 10 сцен на Unity с изменяющимся уровнем сложности.

Для изменения уровня сложности я изменил переменные, перечисленные выше.
Чтобы данные корректно перенеслись из гугл таблицы в игру, а также для изменения переменных, я создал LevelController, в котором хранится номер загруженного уровня.
Я создал новое меню LevelMenu, чтобы пользователь смог выбрать любой уровень.

## Задание 3
### Решение в 80+ баллов должно заполнять google-таблицу данными из Python. В Python данные также должны быть визуализированы.

-Ниже представлен код, который генерирует необходимые значения и записывает их в таблицу. Данные визуализированы с помощью pyplot.

```py

import math
import gspread
import numpy as np
from matplotlib import pyplot as plt 

gc = gspread.service_account(filename='da-in-gamedev-lab-3-4c13cc339b76.json')
sh = gc.open("DA-in-GameDev-lab-3")

level_count = 10
levels = [i for i in range(1, level_count+1)]

shields_num_array = [3, 3, 3, 3, 2, 2, 2, 1, 1, 1]
shields_num_table_start_index = "A3"

dragon_speed_start = 5
dragon_speed_modifier = 3
dragon_speed_table_start_index = "K3"

dragon_time_between_egg_drop_start = 1
dragon_time_between_egg_drop_modifier = -0.075
dragon_time_between_egg_drop_table_start_index = "A17"

dragon_left_right_distance_start = 10
dragon_left_right_distance_modifier = -0.25
dragon_left_right_distance_table_start_index = "K17"

def create_array(length, startNum, modifier):
    array = []
    for i in range(length):
        array.append(round(startNum + (i * modifier), 2))
    return array

def load_data(values, start_index):
      for i in range(len(values)):
            sh.sheet1.update(chr(ord(start_index[0]) + i) + str(int(start_index[1:])), values[i])
            print(chr(ord(start_index[0]) + i) + str(int(start_index[1:])), values[i])

load_data(shields_num_array, shields_num_table_start_index)
plt.plot(levels, shields_num_array)  
plt.title("Shield Num")
plt.xticks(ticks=levels, labels=levels) 
plt.xlabel('Level')
plt.ylabel('Shields')
plt.show()     
    
dragon_speed_array = create_array(level_count, dragon_speed_start, dragon_speed_modifier)
load_data(dragon_speed_array, dragon_speed_table_start_index)
plt.plot(levels, dragon_speed_array)  
plt.title("Dragon Speed")
plt.xticks(ticks=levels, labels=levels) 
plt.xlabel('Level')
plt.ylabel('Speed')
plt.show()

dragon_time_between_egg_drop_array = create_array(level_count, dragon_time_between_egg_drop_start, dragon_time_between_egg_drop_modifier)
load_data(dragon_time_between_egg_drop_array, dragon_time_between_egg_drop_table_start_index)
plt.plot(levels, dragon_time_between_egg_drop_array)  
plt.title("Time between egg drop")
plt.xticks(ticks=levels, labels=levels) 
plt.xlabel('Level')
plt.ylabel('Time')
plt.show()

dragon_left_right_distance_array = create_array(level_count, dragon_left_right_distance_start, dragon_left_right_distance_modifier)
load_data(dragon_left_right_distance_array, dragon_left_right_distance_table_start_index)
plt.plot(levels, dragon_left_right_distance_array)  
plt.title("Dragon Left Right distance")
plt.xticks(ticks=levels, labels=levels) 
plt.xlabel('Level')
plt.ylabel('Distance')
plt.show()

```

## Выводы

В процессе выполнения лабораторной работы я изучил прототип игры Dragon Picker, нашёл переменные, пригодные для балансировки уровня сложности, реализовал систему контроля уровней, перенос данных из Python в Google Sheets, а также визуалировал данные для балансировки игры в Python при помощи pyplot.
