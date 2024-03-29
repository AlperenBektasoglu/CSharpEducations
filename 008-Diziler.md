# Diziler (Arrays)

- Diziler, koleksiyonların temelini teşkil ederler ve koleksiyonların gelişmelerine katkıda bulunmaktadırlar.
- Diziler referans tiplidir. Özlerinde class'tır.
- Dizi içine her türlü değer koyulabilir (referans/değer tip).
- Dizi içindeki bütün elemanlar aynı tipte olmak zorundadır.
- Dizi boyutu sabittir ve kodlarken belirtilmesi gerekir.
- Diziler tanımlandığında kullansakta kullanmasakta bellekte belirtilen eleman sayısı kadar alan tahsis edilir.
- Bütün dizilerin birinci elemanı 0. indeksten başlar.

```cs
int[] example1; // example1 adında int tipinde bir dizi için referans tanımlaması yapıldı. (Referans tanımlaması yapıldı ama bellekte(heap) alan açılmadı!)
example1 = new int[10];  // example1 adındaki dizi için bellekte(heap) 10 tane int tipinde değer tutacak alan açıldı.

int[] example2 = new int[10]; // Yandaki şekilde de tanımlanabilirdi.

/*
Not: Yukarıdaki iki kodda da int türünden iki dizi tanımlandı ve dizinin her bir elemanına int türünün
     varsayılan değeri atandı. Varsayılan değerler, sayısal türler için 0, object türü için NULL (yokluk),
     string türü için "", char için ' ' (boşluk) ve bool için false değerleridir.
*/

Console.WriteLine(example2[3]); // Çıktı: 0

/*
Not: Bütün dizilerin birinci elemanı 0. endeksidir. dizi isimli dizinin birinci elemanına dizi[0],
     10. elemanına dizi[9] yazarak erişebilir ve bu dizi elemanlarını bir değişkenmiş gibi kullanabiliriz.
*/

int[] example3 = new int[20];
example3[5] = 30; //6. Sıradaki elemana 30 değeri atanıyor.
Console.Write(example3[5]); // Çıktı: 30
```

**Dizi tanımlama varyasyonları:**

```cs
int[] arr1 = {1,2,3};
int[] arr1 = new int[] {1,2,3};
int[] arr1 = new int[3] {1,2,3};
int[] arr1 = new[] {1,2,3};
```

Dizilere başlangıç değerleri de atanabilir. Atama için { } işaretçileri kullanılır.

```cs
string[] example1 = { "Bir", "İki", "Üç" };
string[] example2 = new string[] { "Bir", "İki", "Üç" };
string[] example3 = new string[3] { "Bir", "İki", "Üç" };
```

**Not:** Bir dizi elemanına erişirken üst dizi indeksinden daha yukarıda bir değer verilirse program hata verir. Örneğin yukarıdaki dizi de `example3[4] = 100;` ifadesi yazıldığında program taşma hatası verir.

**Not:** Bir dizinin boyutu sabit olabileceği gibi değişkende olabilir. Ancak önemli olan bir dizinin boyutu girildikten sonra dizi boyutu tekrar değiştirilemez.

**Not:** Dikkat edilmesi gereken bir nokta şudur ki, new operatörü ile türetilmeyen dizilere erişilemez.

```cs
int[] example1 = new int[10];  // example1 dizisine ulaşılabilir.
int[] example2; // example2 dizisine ulaşılamaz.
```

**Not:** Foreach mekanizması sadece dizi elemanlarını okuma için kullanılır. Dizi elemanları üzerinde düzenleme işlemlerine izin verilmez. Bu tür engelleme ReadOnly (Sadece okunabilir) olarak bilir.

**Not:** Yukarıdaki anlatımda tek boyutlu dizi örnekleri verildi. Tabi çok boyutlu diziler de var. Çok boyutlu diziler, Multi-Dimensional Array (Düzenli Diziler / Matris Dizileri) ve Jagged Array (Düzensiz Diziler) olmak üzere ikiye ayrılır.

## Multi-Dimensional Array (Düzenli Diziler / Matris Dizileri)

Multi-Dimensional Array (Düzenli Diziler / Matris Dizileri): Bütün satırların aynı kolon sayısına sahip olduğu dizilerdir.

**İki boyutlu düzenli dizi örneği:**

```cs
int[,] arr3 = new int[3, 2]; // 3 satır, 2 sütun
int[,] arr4 = { { 1, 2 }, { 3, 4 }, { 5, 6 } }; // 3 satır, 2 sütun

arr[0,0] = 100; // 0. satır 0. sütün daki alana 100 değeri koyuldu.
```

**Üç boyutlu düzenli dizi örneği:**

```cs
int[,,] Dizi_3D = new int[2, 3, 4] // 2 Satır // 3 Kolon // Her kolonda 4 değer
{
     { // satır 1
         { // Kolon 1
           1, // Değer 1
           2, // Değer 2
           3, // Değer 3
           4  // Değer 4
         },
         { 4, 6, 7 ,8} , // Kolon 2
         { 9, 10, 11 ,12} // Kolon 3
     },
     { // satır 2
         { 12, 11, 10, 9 }, // Kolon 1
         { 8, 7, 6, 5 }, // Kolon 2
         { 4, 3, 2, 1 } // Kolon 3
     },
};
```

Daha fazla boyutlu dizi oluşturulabilir.

```cs
int[,,,,] Dizi_ND = new int[2, 3, 4, 5, 6];
```

**Not:** Bir dizinin toplam eleman sayısı, tüm boyutların çarpılması ile bulunur. Yukarıdaki örnekte dizinin eleman sayısı: 2x3x4x5x6

## Jagged Array (Düzensiz Diziler)

Jagged diziler, her satırının kolon sayısı farklı olan (aynıda olabilir) dizilerdir diyebiliriz. Tanımlamada dikkat etmemiz gereken olay dizinin boyutu verilirken sadece satırının boyutunun verildiğidir. Çünkü sütun değerleri her satır için değişecektir.

```cs
// 1. Tanımalama Örneği:

int[][] jaggedArray = new int[3][];

jaggedArray[0] = new int[] { 1, 3, 5, 7, 9 };
jaggedArray[1] = new int[] { 0, 2, 4, 6 };
jaggedArray[2] = new int[] { 11, 22 };

// 2. Tanımalama Örneği:

int[][] jaggedArray2 = new int[][]
{
new int[] { 1, 3, 5, 7, 9 },
new int[] { 0, 2, 4, 6 },
new int[] { 11, 22 }
};

// 3. Tanımalama Örneği:

int[][] jaggedArray3 =
{
new int[] { 1, 3, 5, 7, 9 },
new int[] { 0, 2, 4, 6 },
new int[] { 11, 22 }
};

// Düzensiz Diziye Değer Atamama:
jaggedArray3 [0] [0] = 100;
```

## Params Anahtar Kelimesi

C#'ta params anahtar kelimesi, değişken sayıda argüman(parametre) alan bir parametreyi belirtmek için kullanılan anahtar kelimedir. Yalnızca bir params anahtar sözcüğüne izin verilir ve bir fonksiyon bildiriminde params anahtar sözcüğünden sonra hiçbir ek parametreye izin verilmez.

```cs
public void ShowForInt(params int[] val) // Params Paramater
{
  for (int i = 0; i < val.Length; i++)
  {
      Console.WriteLine(val[i]);
  }
}

public void ShowForObject(params object[] items) // Params Paramater
{
  for (int i = 0; i < items.Length; i++)
  {
      Console.WriteLine(items[i]);
  }
}

static void Main(string[] args){
      Program program = new Program(); // Creating Object
       program.ShowForInt(2, 4, 6, 8, 10, 12, 14); // Değişken uzunluktaki argümanları iletme
       Console.WriteLine("\n------------------------------------------");
       program.ShowForObject("Ramakrishnan Ayyer", "Ramesh", 101, 20.50, "Peter", 'A');
}
```

## Array Sınıfı

Dizi olarak tanımlanan değişkenler Array sınıfından türetilmektedirler. Dolayısı ile dizilerde Array sınıfından gelen belirli metodlar ve özellikler mevcuttur.

```cs
// Tanımlama 1
int[] arr1 = new int[5]; // Bu şekildeki tanımlamada indexer operatörü([]) kullanılır.

// Tanımlama 2
Array arr2 = new int[3]; // Bu şekildeki tanımlamada indexer operatörü([]) kullanılamaz. Veri ekleme, görüntüleme vs gibi işlemler fonksiyonlar ile yapılır.
```

**Not:** Algoritmik yaklaşımlarda tanımlama 1'deki kullanım tercih edilirken, daha çok dizi hakkında bilgi edinilmesi geren durumlarda tanımlama 2'deki kullanım tercih edilir.

Aşağıda Array sınıfı kullanılarak tanımlanan dizide veri ekleme ve görüntüleme örneğini görebilirsiniz.

```cs
Array arr1 = new int[3];
// arr1[0] = 30; // Hatalı kullanım çünkü "Array arr1" şekildeki tanımlamada indexer operatörü([]) kullanılamaz.
arr1.SetValue(30,0); // 1. parametre: değer, 2. parametre: index
arr1.SetValue(60,1);
Console.WriteLine(arr1.GetValue(0)); // Çıktı: 30
Console.WriteLine(arr1.GetValue(1)); // Çıktı: 60
```

### Array Sınıfı Metodları

1. Clear Metodu: Dizinin içindeki tüm elemanlara, dizinin türüne uygun default değerleri atayan fonksiyondur. (Array.Clear(...))
1. Copy Metodu: Elimizdeki bir dizinin verilerini başka bir diziye kopyalamamızı sağlayan fonksiyondur. (Array.Copy(...))
1. IndexOf Metodu: Dizinin içinde bir eleman var olup olmadığını sorgulayabildiğimiz fonksiyondur. Arama neticesinde ilgili değer varsa int olarak o değerin index numarasını döndürecektir. Yoksa -1 değerini döndürür. (Array.IndexOf(...))
1. Reverse Metodu: Elimizdeki dizinin elemanlarını tersine sıralayan fonksiyondur. (Array.Reverse(...))
1. Sort Metodu: Diziler üzerinden sıralama işlemi yapar. Eğer string bir dizi ise alfabetik olarak olarak A'dan Z'ye sıralar. Eğer numeric bir dizi ise dizi elemanlarını küçükten büyüğe sıralar. (Array.Sort(...))

### Array Sınıfı Özellikleri

1. IsReadOnly (arr1.IsReadOnly)
1. IsFixedSize (arr1.IsFixedSize)
1. Length (arr1.Length)
1. Rank: Dizinin derecesini(boyut) verir (arr1.Rank)

Normal dizi tanımlaması yapılırken arka planda Array sınıfının CreateInstance metodu kullanılmaktadır. Bizler bu metodu kullanarak fonksiyonel diziler oluşturabilmekteyiz.

```cs
int[] arr1 = new int[3];
Array arr2 = Array.CreateInstance(typeof(int), 3);
int[,,] arr3 = new int[2,3,4];
Array arr4 = Array.CreateInstance(typeof(int), 2, 3, 4);
```

## Index ve Range Veri Tipi

Bu tipler C# 8.0 ile gelmiştir. Index, dizi ve koleksiyon yapılarındaki index kavramının tip olarak belirlenmiş halidir. Temdelde index değerini bir tür ile tutmakla beraber `^` operatörüyle birlikte daha fazla anlam ifade etmekte ve dizinin index değerlerini tersine ifadece edecek şekilde sorumluluk yüklenektedir.

```cs
int[] sayilar = {10, 20, 30, 40, 50, 60, 70, 80, 90};

Index index1 = 3;
Index index2 = ^3; // ^ operatörü ile tersine index durumları kullanılırken index değerlerinin 0 dan değil 1 den başladığına dikkat ediniz.

Console.WriteLine(sayilar[index1]); // Çıktı: 40 // 10-20-30-40
Console.WriteLine(sayilar[index2]); // Çıktı: 70 // 90-80-70
```

Range, veri kümelerinde hangi değerler ile çalışacağımızı belirleyebilmek için index üzerinden aralık vermemizi ve bunu .. operatörü ile gerçekleştirmemizi sağlayan yapıdır.

Kullanım: [Index No] .. [Sıra No]

```cs
int[] sayilar = {10, 20, 30, 40, 50, 60, 70, 80, 90};
Range range1 = 2..4; // 30, 40
Range range2 = 2..^1; // 30, 40, 50, 60, 70, 80 // Sıra numrasına(1) göre sondan sayarken bir soldaki değeri alacak şekilde çalışır.
Range range3 = ^5..^1; // 40, 50, 60, 70, 80
Range range4 = ..; // Tüm diziye karşılık gelir

int[] yeniSayilar = sayilar[range1];
```

## ArraySegment Sınıfı Nedir?

Bir dizinin bütününden ziyade belirli bir kısmına ihtiyaç dahlinde ilgili diziyi kopyalamak yerine (ki oldukça maliyetli bir operasyondur) bağımsız bir referans ile erişmemizi ve böylece salt bir şekilde temsil etmemizi sağlayan bir yapıdır.

```cs
int[] numbers = {10, 20, 30, 40, 50, 60, 70 80};
ArraySegment<int> segment1 = new ArraySegment<int>(numbers);
ArraySegment<int> segment2 = new ArraySegment<int>(numbers, 2, 5);
segment1[0] = 123; // numbers = {123, 20, 30, 40, 50, 60, 70 80}
```

Bir dizi üzerinde birden fazla parçada çalışacaksan eğer her bir parçayı ayrı bir ArraySegment olarak Slice metoduyla tanımlayabiliriz.

```cs
int[] numbers = {10, 20, 30, 40, 50, 60, 70 80};
ArraySegment<int> segment = new ArraySegment<int>(numbers);
ArraySegment<int> segment1 = segment.Slice(0,3);
ArraySegment<int> segment2 = segment.Slice(4,7);
ArraySegment<int> segment3 = segment.Slice(2,5);
```

## Span Nedir?

ArraySegment sadece string ve dizilerde temsiliyet yapabiliyorken, Span bellek üzerinde olan herhangi bir yeri temsil edebilir. Span ile referans edilen alana hertürlü müdahale edilebilirken, ReadOnlySpan ile bu verisle operasyonlar engellenebilir ve sadece okunabilir bir davranış sergilenebilir.

```cs
int[] numbers = {10, 20, 30, 40, 50, 60, 70 80};
Span<int> span1 = new Span<int>(numbers);
Span<int> span2 = numbers;
Span<int> span3 = new Span<int>(numbers, 3, 5);
Span<int> span4 = numbers.AsSpan();
ReadOnlySpan<int> span5 = numbers.AsSpan();
```
