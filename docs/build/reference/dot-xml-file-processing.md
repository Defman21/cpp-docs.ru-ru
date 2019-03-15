---
title: Обработка XML-файлов
ms.date: 11/04/2016
helpviewer_keywords:
- XML documentation, processing XML file
ms.assetid: e70fdeae-80ac-4872-ab24-771c5635cfbf
ms.openlocfilehash: 1a0d231a066209307041681232cc3410210d4d02
ms.sourcegitcommit: 8105b7003b89b73b4359644ff4281e1595352dda
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/14/2019
ms.locfileid: "57826375"
---
# <a name="xml-file-processing"></a>Обработка XML-файлов

Компилятор создает строку идентификатора для каждой конструкции в коде, помеченной для создания документации. Дополнительные сведения см. в разделе [Рекомендуемые теги для комментариев документации](recommended-tags-for-documentation-comments-visual-cpp.md). Строка идентификатора однозначно определяет конструкцию. Программы, обрабатывающие этот XML-файл, могут с помощью строки идентификатора определить, какому элементу метаданных или отражения .NET Framework соответствует эта документация.

XML-файл не содержит иерархического представления кода, а только плоский список с идентификаторами всех элементов.

Компилятор соблюдает следующие правила при формировании строк идентификаторов.

- Пробелы в строку не вставляются.

- Первая часть строки идентификатора определяет тип идентифицируемого члена. Это один символ, за которым следует двоеточие. Используются следующие типы элементов.

  | Знак | Описание: |
  |---------------|-----------------|
  | в | namespace<br /><br /> Вы не можете добавить комментарии документации для пространства имен, но можете создать для него cref-ссылки. |
  | T | тип: класс, интерфейс, структура, перечисление, делегат |
  | D | typedef |
  | C | поле |
  | С | свойство (включая индексаторы или другие индексированные свойства) |
  | M | метод (в том числе специальные методы, например конструкторы и операторы) |
  | E | событие |
  | ! | текст ошибки<br /><br /> Остальная часть строки предоставляет сведения об ошибке. Компилятор MSVC создает сведения об ошибках для ссылок, которые не удается разрешить. |

- Вторая часть строки содержит полное имя элемента, начиная от корня пространства имен. Имя элемента, включающие типы и пространство имен разделяются точками. Если в имени самого элемента есть точки, они заменяются символами решетки (#). Предполагается, что в именах элементов не может содержаться символ решетки. Например, полное имя конструктора `String` будет иметь вид System.String.#ctor.

- Для свойств и методов, имеющих аргументы, список этих аргументов заключается в круглые скобки и указывается в конце. Если аргументы не используются, скобки отсутствуют. Аргументы разделяются запятыми. Кодировка каждого аргумента указывается в точности так, как она закодирована в сигнатуре .NET Framework.

  - Базовые типы. Регулярные типы (ELEMENT_TYPE_CLASS или ELEMENT_TYPE_VALUETYPE) представляются полным именам типа.

  - Встроенные типы (например, ELEMENT_TYPE_I4, ELEMENT_TYPE_OBJECT, ELEMENT_TYPE_STRING, ELEMENT_TYPE_TYPEDBYREF и ELEMENT_TYPE_VOID) представляются полным именем соответствующего полного типа, например **System.Int32** или **System.TypedReference**.

  - ELEMENT_TYPE_PTR представляется как "\*" после имени измененного типа.

  - ELEMENT_TYPE_BYREF представляется как '\@' после имени измененного типа.

  - ELEMENT_TYPE_PINNED представляется как "^" после имени измененного типа. Компилятор MSVC никогда не создает это.

  - ELEMENT_TYPE_CMOD_REQ представляется как "&#124;" с указанием полного имени класса модификатора после имени измененного типа. Компилятор MSVC никогда не создает это.

  - ELEMENT_TYPE_CMOD_OPT представляется как "!" с указанием полного имени класса модификатора после имени измененного типа.

  - ELEMENT_TYPE_SZARRAY представляется как "[]" после типа элемента для массива.

  - ELEMENT_TYPE_GENERICARRAY представляется как "[?]" после типа элемента для массива. Компилятор MSVC никогда не создает это.

  - ELEMENT_TYPE_ARRAY представляется как [*нижняя_граница*:`size`,*нижняя_граница*:`size`] где число запятых на единицу меньше размерности массива, а нижние границы и размер каждого измерения, если они известны, представлены в десятичном формате. Если нижняя граница или размер не указаны, они опускаются. Если нижняя граница и размер для определенной размерности опущены, опускается и символ ":". Например, двухмерный массив со значением 1 для нижних границ без указания размеров обозначается так: "[1:,1:]".

  - ELEMENT_TYPE_FNPTR представляется как "=FUNC:`type`(*подпись*)", где `type` обозначает возвращаемый тип, а *подпись* представляет аргументы метода. Если аргументы не используются, скобки опускаются. Компилятор MSVC никогда не создает это.

  Следующие компоненты подписи не представляются, поскольку они никогда не используются для различения перегруженных методов:

  - соглашение о вызовах;

  - тип возвращаемого значения;

  - ELEMENT_TYPE_SENTINEL.

- Только для операторов преобразования возвращаемое значение метода кодируется как символ "~", за которым следует тип возвращаемого значения, как описано ранее.

- Для универсальных типов имя типа завершается символом обратного апострофа и числом, которое обозначает количество параметров универсального типа.  Например, примененная к объекту директива

    ```xml
    <member name="T:MyClass`2">
    ```

  Для типа, который определен как `public class MyClass<T, U>`.

  Для методов, принимающих в качестве параметров универсальные типы, параметры универсального типа указываются в виде чисел, которым предшествуют символы обратного апострофа (например, \`0, \`1).  Каждое число представляет нотацию массива с отсчетом индексации для параметров универсального типа.

## <a name="example"></a>Пример

Примеры ниже демонстрируют, как создаются строки идентификатора для класса и его элементов.

```cpp
// xml_id_strings.cpp
// compile with: /clr /doc /LD
///
namespace N {
// "N:N"

   /// <see cref="System" />
   //  <see cref="N:System"/>
   ref class X {
   // "T:N.X"

   protected:
      ///
      !X(){}
      // "M:N.X.Finalize", destructor's representation in metadata

   public:
      ///
      X() {}
      // "M:N.X.#ctor"

      ///
      static X() {}
      // "M:N.X.#cctor"

      ///
      X(int i) {}
      // "M:N.X.#ctor(System.Int32)"

      ///
      ~X() {}
      // "M:N.X.Dispose", Dispose function representation in metadata

      ///
      System::String^ q;
      // "F:N.X.q"

      ///
      double PI;
      // "F:N.X.PI"

      ///
      int f() { return 1; }
      // "M:N.X.f"

      ///
      int bb(System::String ^ s, int % y, void * z) { return 1; }
      // "M:N.X.bb(System.String,System.Int32@,System.Void*)"

      ///
      int gg(array<short> ^ array1, array< int, 2 >^ IntArray) { return 0; }
      // "M:N.X.gg(System.Int16[], System.Int32[0:,0:])"

      ///
      static X^ operator+(X^ x, X^ xx) { return x; }
     // "M:N.X.op_Addition(N.X,N.X)"

      ///
      property int prop;
      // "M:N.X.prop"

      ///
      property int prop2 {
      // "P:N.X.prop2"

         ///
         int get() { return 0; }
         // M:N.X.get_prop2

         ///
         void set(int i) {}
         // M:N.X.set_prop2(System.Int32)
      }

      ///
      delegate void D(int i);
      // "T:N.X.D"

      ///
      event D ^ d;
      // "E:N.X.d"

      ///
      ref class Nested {};
      // "T:N.X.Nested"

      ///
      static explicit operator System::Int32 (X x) { return 1; }
      // "M:N.X.op_Explicit(N.X!System.Runtime.CompilerServices.IsByValue)~System.Int32"
   };
}
```

## <a name="see-also"></a>См. также

[Документация XML](xml-documentation-visual-cpp.md)