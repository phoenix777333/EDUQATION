## Java Immutable. Неизменный объект

> Immutable (Неизменный) называется тот объект внутреннее состояние (данные) которого не могут быть изменены после его создания

> Основное приемущество иммутабильного объекта - это что что наш код может его "раздавать" по кругу разным методам без страха того что какой-нибудь метод изменит его и это как-то приведет к краху ссылающихся на него алгоритмов. 


* То есть с точки зрения потребителя, если потребительская логика захочет что-то изменить в объекте, то получит в качестве результата изменения копию объекта, вместо него самого.
* Immutable лежит в основу разных классов Java (String,Integer,etc...)
* Например

 ```java
 String message = "This is the original object";
        message.replace("original","modified");
 ``` 

 применяя метод **replace()** из класса **String** вы не влияете на оригинал, данный метод возвращает новый объект с модификацией.

---

* Попробуем создать свой собственный Immutable, для этого соблюдаем шаги:
  1. Делаем класс **final** что запретит наследование, и тем самым возможную "переделку" механизма защиты наследниками (в данном случае - наследование - это лазейка)
  2. Делаем все свойства приватными
  3. Даем только конструктору возможность установить значение - так как новое значение полей будет связанно с новым объектом
  4. Все остальные методы должны быть защищены от внутреннего изменения
  5. Если же нам захочется создать какой-то метод который "производит модификацию" - этот метод должен создать новую копию с модифицированным значением и вернуть нам копию, не меняя оригинал


* Предположим у нас есть класс **Currency** - валюта, с полями:
  * baseCode - код валюты - (напр "EUR") по отношению к которой вычисляется коэффициент обмена
  * code - (напр "MDL") код валюты
  * value - (напр 17.50) значение коэффициента по отношению к ```base```
  * date - дата (напр "2020-01-01") когда это значение было зафиксировано (так как значение может менятся в зависимости от даты)
    ```java

    final class Currency {
        private String baseCode;
        private String code;
        private Float value;
        private String date;
    }

    ```
  зачем делать такой класс Immutable? Вне контекста может показаться бессмысленным, - ответ очень прост - представьте себе ситуацию когда объект из класса **Currency** будет связан с объектом типа **TotalCost** ( стоимость заказа ) какого-то заказа. Если заказ оформлен скажем в один день, а оплата следует в другой день и за этот промежуток суток коэффициент изменился, то по какому коэффициенту производить оплату? В таком случае - передавая объект валюты в разные места в коде immutable - будет гарантировать нам то что его не поменяют в тех местах где он уже есть.

  * ТРЕБУЕТСЯ:
    1. Добавить параметризованный конструктор
    2. toString() для проверки
    3. геттеры для всех свойств
    4. и сеттеры для всех свойств но с условием того что каждый сеттер создаст точную копию текущего объекта (this), изменит только то свойство за которое он отвечает и вернет измененную копию

* Как проверять?
  * в **main()**

    ```java
    Currency todaysCurrency = new Currency("EUR","MDL",17.50f,"2020-01-01");
    Currency tomorrowsCurrency = todaysCurrency.setDate("2020-01-02");

    System.out.println(todaysCurrency);
    System.out.println(tomorrowsCurrency);
    ```  

* Вопросы:
  1. Сколько объектов **Currency** было в итоге создано?   
  2. А если для **tomorrowsCurrency** понадобилось бы изменить и коэффициент на ```18.00f``` - как это выглядело бы в коде?