# Код для исследования
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
# Описание работы JVM
1. С помощью подсистемы загрузчиков классов подгружаются класс JvmComprehension и системные в metaspace.
2. В Stack Memory создается фрейм main() 
3. В фрейм main() помещается int i = 1 (строка 1)
4. В heap добавляется Object и ссылка на него в фрейме main() (строка 2)
5. В heap добавляется объект класса Integer и ссылка на него в фрейме main() (строка 3)
6. В стек добавляется фрейм printAll(), ссылка на Object, int i = 1, ссылка на объект класса Integer (срока 4)
7. В heap добавляется объект класса Integer и ссылка на него в фрейме printAll() (строка 5)
8. В heap добавляется объект класса String = o.toString() + i + ii, далее в стек добавляется фрейм System.out.println() и в нем ссылка на созданный объект класса String (строка 6)
9. После того как метод printAll отработал сборщик мусора может почистить объекты созданные в строках 5 и 6
10. В heap добавляется объект класса String = "finished", далее в стек добавляется новый фрейм для System.out.println() и в нем ссылка на созданный объект класса String (строка 7)
11. После строки 7 сборщик мусора может почистить объект созданный в строке 7, т.к. ссылки на него не осталось
