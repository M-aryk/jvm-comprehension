# Задача "Понимание JVM"

```java
public class JvmComprehension {

    public static void main(String[] args) {
        int i = 1;                      // 1
        Object o = new Object();        // 2
        Integer ii = 2;                 // 3
        printAll(o, i, ii);             // 4
        System.out.println("finished"); // 7
    }

    private static void printAll(Object o, int i, Integer ii) {
        Integer uselessVar = 700;                   // 5
        System.out.println(o.toString() + i + ii);  // 6
    }
}
```


## ClassLoaders

1. Bootstrap ClassLoader (загружает стандартные библиотечные классы: *Object, Integer, String*)
2. Platform ClassLoader (загружает расширения Java)
3. Application ClassLoader (загружает *public class JvmComprehension*)
4. Linking (связывание):
    - verify (проверка кода на синтаксис);
    - prepare (подготовка, выделение памяти для статических переменных и инициализация со значениями по умолчанию: *int i = 1*);
    - resolve (разрешение символьных ссылок, связывание ссылок на другие классы: *Object o = new Object(), Integer ii = 2, Integer uselessVar = 700*).
5. Initialization (выполнение статических методов и статических инициализаторов: *public static void main, private static void printAll*)

## Runtime Data Area

1. Metaspace (хранит данные о константах, классе(имя, методы, поля и др.): *public class JvmComprehension, public static void main, private static void printAll, Object, Integer, String*)
2. Stack Memory (хранит значения примитивных переменных, создаваемых в методах, ссылки на объекты в куче, на которые ссылается метод, работает по принципу LIFO)

   Фрэймы:
   - *public static void main (значение i, ссылки o, ii,)*;
   - *private static void printAll (ссылка uselessVar)*;
   - *System.out.println(o.toString() + i + ii) - (ссылка о).*
3. Heap (хранит созданные объекты и обертки примитивных типов: *Object, Integer, String*)

## Execution Engine

1. Интерпретатор (код выполняется строка за строкой)
2. Сборщик мусора (собирает объекты из *heap*, которые больше не используются: *Object, 2, 700*)


