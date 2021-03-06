## Классы. Динамическое использование - объекты. Наследование

### часть 1

> В программирование часто используется такой тип "контейнера" как "очередь". Очередь (Queue) Queue - коллекция, предназначенная для хранения элементов в порядке, нужном для их обработки. Очереди обычно, но не обязательно, упорядочивают элементы в FIFO (first-in-first-out, "первым вошел - первым вышел") порядке. 

---

Нам необходимо создать приложение которое предоставляет нам логику очереди, структура проекта:

```
PhoneInheritanceHistory
 - src/
   - main(package)
     - Application(Class + static main())
   - collections(package)
     - SimplePositiveQueue(Class)
```


* Структура класса **SimplePositiveQueue** (простая очередь с положительными числами) которая будет состоять из 3 ячеек (first,middle,last). Обычно внутренняя реализация очереди основывается на списке или массиве значений, но в данном примере у нас будут внутри 3 однотипные, отдельные ячейки - целого типа.

* Вот стартовый код
  ```java
  public class SimplePositiveQueue {
    // properties
    private int length;

    private int first;
    private int middle;
    private int last;
   
  }
  
  - наша очередь предоставит доступ только к первому и последнему элементу.
  - наша очередь сможет лишь вытащить первый элемент и лишь добавить в конец значение. т е работать очередь будет так
    
    ```
    poll()  <----   [first] <---- [middle] <---- [last] <---- push()
                     -1            -1             -1          push(1000)
                     1000          -1             -1          push(2000)
                     1000          2000           -1          push(3000)
                     1000          2000           3000        push(4000) --> error Queue is full!!
    --------------------------------------------------------------------------------------------------                     
    1000 < poll()    2000           3000          -1
    2000 < poll()    3000          -1             -1
    3000 < poll()    -1            -1             -1
    -1   < poll()    -1            -1             -1      --> error Queue is empty!
    ```


* Добавьте конструктор класса, он должен инициализировать **length** в 0, а так же все 3 ачейки в **-1** - что указывает на то что очередь пуста.
* Добавьте метод ```boolean push(int value)```, этот метод должен во-первых проверить если значение положительное (иначе выводить ошибку), после полученное **value** установить на на последнюю свободную ячейку в очереди. ЕСЛИ еще есть свободные ячейки то после установки вернуть **true** если очередь занята - **false**.
* Добавьте метод ```int poll()```, этот метод должен вернуть значение первой ячейки (вырезая ее из очереди), соответственно сдвинуть значения ячеек на одну позицию левее. Если очередь пуста - вернуть - **-1**

---
* Проверяем в **main()**
  ```
  SimplePositiveQueue spq = new SimplePositiveQueue();
  spq.push(1000);
  spq.push(2000);
  spq.push(3000);
  if( !spq.push(4000) ){
    System.out.println("The queue is full!!");
  }
  
  int value;
  do{
    value = spq.poll();
    System.out.println( value );
  }while( value!= -1 );
  ``` 