# Desenler (Patterns)

## Type Pattern

is operatörünün desenlendirilmiş halidir.
is operatörü ile belirlenen türün dönüşümü sağlanabilir.

```cs
object x = "Alperen";
if(x is string){} // is operatörü

if(x is string xx){}
// Type Pattern - Burada oluşturulan xx isimli değişkene if'in dışından da erişilebilir ama kullanırken hata alınır.
// xx değişkeninin değeri: Alperen
```

Farklı bir kullanım örneği:

```cs
object x = "Alperen";
bool result = x is string xx;
```

## Constant Pattern

Elimizdeki veriyi sabit değerler ile karşılaştırabilmemizi sağlar. Bu pattern ile is operatörünün, == operatörü gibi çalışabilmesi sağlanmış olur.

```cs
if(x is "Alperen"){}
```

## Var Pattern

Elimizdeki veriyi "var" değişkeniyle elde etmemizi sağlar. Bu pattern'in type pattern'den farkı, oluşturulan yeni değişkenin if dışında kullanılırken hata almamasını sağlar.

```cs
object x = "Alperen";
if(x is var xx){}
// xx değişkeninin değeri if içinde de, if dışında da "Alperen" dir.
```

**Not:** Normal var derleme zamanında değişkenin tipini belirler. Var pattern ise runtime da değişkenin tipini belirler.

## Simple Type Pattern

Bir değişken içerisindeki değerin belirli bir tipde olup olmadığını hızlı bir şekilde kontrol etmemizi sağlayan desendir.

```cs
object obj = new Person();

// Normal Kod
switch(obj){
  case Person p:
                ...
                break;
}

// Simple Type Pattern
switch(obj){
  case Person:
              ...
              break;
}
```

## Relational Pattern

Switch özü itibariyle sadece eşitlik durumlarını inceleyen bir yapıydı. Bu pattern ile diğer türlü karşılaştırmalarda switch expression üzerinde yapılabilmektedir.

```cs
int number = 111;
string result = number switch{
  < 50 => "Küçük",
  > 50 => "Büyük",
  _ => "Hiçbiri"
}
```

## Logical Pattern

switch expression'da and, or ve not gibi mantıksal operatörler kullanılabilmektedir. Relational pattern ile oldukça uyumludur.

## Not Pattern

switch expression'da not operatörünün kullanılabildiği bir desendir.
