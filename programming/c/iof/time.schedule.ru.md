### Базовые типы данных и вычисления. Ввод вывод.

* Предположим в переменную **trips_per_day** вводиться целое число маршрутов (кругов) маршрутного автобуса с номером маршрута **bus_number** за день.
* Так же мы заранее знаем часы начала **hours_start** и конца работы этого маршрута **hours_end**. 
    ```c
    ??? trips_per_day = 32;
    ??? bus_number = 77;
    ??? hours_start = 7;   // 7:00
    ??? hours_end   = 23;  // 23:00
    ```
* Исходя из условий требуется:
  1. дополнить в коде вместо ```???``` подходящий тип данных
  2. вычислить среднюю длительность маршрута в минутах, или раз во сколько минут будет автобус
  3. вывести результат примерно в таком формате
     ```The "BUS 77" departs every DD minutes``` - где ```DD``` - кол-во минут - результат ваших вычислений.     
