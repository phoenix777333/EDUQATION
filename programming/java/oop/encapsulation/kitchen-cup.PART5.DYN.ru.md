## Принцип капсулы. Наследование. Переопределение, полиморфизм.

> часть 5

* Так как объект чашки (Cup) содержит свойство "liquid" класса Liquid, это, благодаря полиморфизму, означает что чашка (Cup) может содержать внутри себя так же и любого наследника класса Liquid!!!

---

* Для этого требуется:
  1. Создать класс "DrinkableLiquid" (жидкость что можно пить) - наследника класс "Liquid"
  2. Этому классу добавить private "category" - свойство категория (например - "Alcoholic", "Cold Drinks", "Hot drinks") с сопутствующими сет / гет
  3. Создать класс "DangerousLiquid" (опасная для здоровия жидкость) - наследника класс "Liquid"
  4. Этому классу добавить private "level" - свойство степень опасности (например - "Deadly", "Toxic", ... ) с сопутствующими сет / гет
   
  5. Для проверки вы main() создать две чашки: bigCup (BigCup) с объектом из класса DrikableLiquid - например вода, вывести информацию о нем, а так же smallCup (SmallCup) - с DangerousLiquid - например - дезинфецирующее средство вывести информацию о нем

---

* БОНУС: в момент когда вы вызываете из объекта любой чашки геттер "getLiquid()" - этот метод вам выдает внутренний объект жидкости как представителя класса "Liquid" - то есть вы не знаете точно что это за жидкость (является ли представителем DrinkableLiquid или DangerousLiquid). В Java есть оператор "instanceof" который умеет работать с объектами. Данный оператор может определить ТИП (класс) объекта даже "сквозь" полиморфизм.
  * ТРЕБУЕТСЯ: дописать в main() фрагмент кода который при помощи if/else и данного оператора получив в наличие объект некой чашки - определит - можно ли выпить содержимое данной чашки или нет !!! Рекомендую для этого создать отдельный статичный класс с названием "LiquidTester" в новом пакете "tools" с единственным статичным методом "boolean isDrinkable( Cup cup )" который вернет true - если чашка содержит объект класса DrinkableLiquid.