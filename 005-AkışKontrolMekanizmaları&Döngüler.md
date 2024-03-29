# Akış Kontrol Mekanizmaları

Akış kontrol mekanizmaları 2 tanedir.

1. if - if else - else if Yapısı
1. Switch-Case Yapısı

## if - if else - else if Yapısı

Koşul doğruysa if bloğu çalıştırılır. Değil ise else bloğu çalıştırılır.

```cs
int sayi;
Console.Write("Lütfen bir sayı girin:");
sayi = Convert.ToInt32(Console.ReadLine());
if (sayi > 0)
    Console.WriteLine("{0} sayısı pozitif bir sayıdır.", sayi);
else if (sayi < 0)
    Console.WriteLine("{0} sayısı negatif bir sayıdır.", sayi);
else
    Console.WriteLine("Girilen sayı 0'a eşittir.");
```

**Not:** Tek satırlık if yapılarında scope kullanmaya gerek yoktur. Birden fazla satır için scpoe kullanılması gerekir.

## Switch-Case Yapısı

Switch-Case yapılanmasında bir değişkenin değeri için sadece eşitlik durumlarını kontrol etmek için kullanılır. Switch-Case yapılanmasında default yapısı zorunlu değildir.

```cs
string job = "CE";
switch (job)
{
    case "Police":
        // ...
        break;
    case "Lawyer":
        // ...
        break;
     default:
        // ...
        break;
}
```

**Not:** When anahtar kelimesi ile Switch-Case yapısı zenginleştirilebilir.

```cs
int salary = 50_000;
switch (job)
{
    case int x when x > 10_000 || x < 20_000:
        // ...
        break;
}
```

**Video:** [Switch Expressions](https://www.youtube.com/watch?v=bbaKxvFELB4&list=PLQVXoXFVVtp3e_urGZcMNAHx2Eo4Rm5Xk&index=134)

## Döngüler

for, while ve do-while olmak üzere üç çeşit döngü yapısı vardır.

**Not:** Döngülerde tek satırlık kodlar için scope kullanılmasına gerek yoktur.

**Not:** foreach yapısı bir döngü değil iterasyondur.

### For Döngüsü

```cs
Console.Write("Bir sayı giriniz:");
int v_sayi = Convert.ToInt32(Console.ReadLine());
int sonuc = 1;
for (int i = v_sayi; i > 1; i--)
{
    sonuc *= i;
    Console.Write("Sonuç Hesaplanıyor...");
}
Console.Write("Faktöriyeli:" + sonuc);
Console.ReadKey();
```

Aşağıdaki şekilde sonsuz döngü yapılabilir:

```cs
for (;;)
    Console.WriteLine("Sonsuz Döngü");
```

### While Döngüsü

```cs
int counter = 0;
while (counter <= 10)
{
    Console.WriteLine(counter);
    counter++;
}
```

Aşağıdaki şekilde sonsuz döngü yapılabilir:

```cs
while (true)
  Console.WriteLine("Sonsuz Döngü");
```

### Do-While Döngüsü

Do-while döngüsü, döngünün koşuldan bağımsız en az bir kere çalışması istendiği zaman kullanılır.

```cs
int counter1 = 1;
do
{
    Console.WriteLine(counter1);
    counter1++;
} while (counter1 <= 10);
```

Aşağıdaki şekilde sonsuz döngü yapılabilir:

```cs
do
{
    Console.WriteLine("Sonsuz Döngü");
} while (true);
```

### Break Ve Continue Komutları

Break komutu: Break komutu döngüyü sonlandırır. Switch-Case yapısında ise, switch koşulunun scope'u({}) dışına çıkmamızı sağlar.

Continue komutu: Döngü içinde bu komutun bulunduğu satırdan sonrası işlenmeden döngünün sonraki değerini işlemek üzere başa dönmesini (sonraki tekrarı yapmasını) sağlar.

```cs
for (int i = 0; i < 20; i++)
{
    if (i == 5)
        continue;

    if (i == 10)
        break;

    Console.WriteLine(i);
}
```

**Not:** Break komutu foreach mekanizmasını sonlandırmak için de kullanabilir.

**Not:** Break komutu sadece döngülerde, switclerde ve foreachlerde kullanılırken, continue komutu sadece döngülerde kullanılır.

**Not:** Return anahtar kelimesi metod içerisinde kullanılır. ve metodu sonlandırmaya yarar. Geriye değer döndürme özelliğide vardır. Returnler döngüyü değil metodu sonlandırır.

### Foreach Iterasyon Yapısı

Foreach yapısı döngü değildir. Listeler, koleksiyonlar ya da diziler üzerinde işlem yapmak için kullanılır. Özellikle eleman sayısının bilinmediği durumlarda büyük olaylık sağlamaktadır.

**Not:** Foreach yapısı sadece dizi elemanlarını okumak için kullanılır. Dizi elemanları üzerinde düzenleme işlemlerine izin verilmez. Bu tür engelleme ReadOnly (Sadece okunabilir) olarak bilir.

```cs
string[] isimler = { "Alperen", "Ahmet", "Elif", "Hakan", "Sema" };
foreach (string eleman in isimler)
    Console.WriteLine(eleman);
Console.ReadKey();
```

## Goto Komutu

C# goto deyimi koşulsuz olarak belirtilen etikete atlar. Etiket tanımlaması goto kullanımından önce veya sonra yapılabilir. Performassızdır ve tavsiye edilmez.

```cs
int sayı;
baslangıc: // Etiket
Console.Write("Notunuzu Giriniz: ");
sayı = Convert.ToInt32(Console.ReadLine());

if (sayı >= 0 && sayı < 50)
    Console.WriteLine("Kötü");

if (sayı >= 50 && sayı < 60)
    Console.WriteLine("Geçer");

if (sayı >= 60 && sayı < 70)
    Console.WriteLine("Orta");

if (sayı >= 70 && sayı < 85)
    Console.WriteLine("İyi");

if (sayı >= 85 && sayı <= 100)
    Console.WriteLine("Pekiyi");

if ((sayı < 0 || sayı > 100))
{
    Console.WriteLine("Yanlış Sayı Birimi Girdiniz.");
    goto baslangıc;
}
Console.ReadKey();
Console.WriteLine("--------------------------------------");
```
