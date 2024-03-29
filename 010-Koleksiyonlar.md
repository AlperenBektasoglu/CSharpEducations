# Koleksiyonlar

Programlamadaki temel ihtiyaçlarımızın biri de verilerimizin toplu olarak tutulduğu yapılardır. Bu ihtiyaçlarımızı genellikle diziler ya da koleksiyonlar ile gideririz. .NET Platformu programcılar tarafından sıkça kullanılan yapıları (stack, queu...) sisteme entegre ederek, hazır bir şekilde geliştiriciye sunmaktadır. Platform tarafından verilerimizi toplu olarak tutmamızı sağlayan bu çözümleri Koleksiyon Sınıfları başlığı altında ele alabiliriz.

## Koleksiyonların Sağladığı Avantajlar Nedir?

1. Diziler sabit boyutludur ve eleman sayısının önceden belirtilmesi gerekir. Koleksiyonlar ise dinamik yapıdadır yani sabit boyutlu değildir.
1. Eleman eklendikçe boyutu dinamik olarak artmaktadır.
1. Diziler aynı veri tipindeki elemanları içermektedir. Koleksiyonlarda ise böyle bir kısıtlama bulunmamaktadır.

## Koleksiyonların Dezavantajları Nelerdir?

1. .NET Platformunda kullanmış olduğumuz veri tipleri, Değer tipleri ve Referans tipleri olarak ikiye ayrılmaktadır. Bir Değer Tipinin,
   - Referans Tipine dönüştürülmesi işlemine Boxing, tersi bir işlemede Unboxing denmektedir. Koleksiyonlar verileri object olarak tutmaktadır.
   - Bu yüzden koleksiyonlara her veri eklediğimizde Boxing işlemi gerçekleşecektir. Yani verimiz object'e dönüştürülecektir.
   - Koleksiyona eklenen verileri bir değişene aktarmak istediğimizde de Unboxing işlemi gerçekleşecektir. Koleksiyonun eleman sayısındaki artışa bağlı olarak boxing ve unboxing işlemleri artacaktır ve buna bağlı olarak da uygulamamızın performansı düşecektir.

## Koleksiyonların Namespaceleri Nelerdir ve Bu Namespacelerin Classları Nelerdir?

1. System.Collections.Generic: List, Stack, Queue, LinkedList, HashSet, SortedSet, Dictionary, SortedDictionary, SortedList ...
1. System.Collections: ArrayList, Stack, Queue, Hashtable, BitArray, SortedList ...
1. System.Collections.Concurrent: BlockingCollection, ConcurrentBag, ConcurrentStack, ConcurrentQueue, ConcurrentDictionary, Partitioner ...

## Koleksiyon Tipleri Nelerdir?

.NET Platformu 3 koleksiyon tipini desteklemektedir.

1. Genel Amaçlı Koleksiyonlar: Her tipten veriyi saklamak için kullanılabilirler.

   - ArrayList
   - Dictionary
   - HashTable
   - Queue
   - SortedList
   - Stack

1. Özel Amaçlı Koleksiyonlar: Belirli bir veri tipi veya çalışma şekli için optimize edilmişlerdir.
   - CollectionsUtil
   - ListDictionary: Anahtar-Değer çiftlerini bir bağlı liste içinde saklar. Küçük veri kümeleri için tercih edilir.
   - HybridDictionary: Belirli bir büyüklüğü geçene kadar Anahtar-Değer çiftlerini ListDictionary koleksiyonunda tutmaktadır, geçtikten sonra otomatik olarak bir Hashtable koleksiyonuna geçiş yapar.
   - NameValueCollection: Anahtar-Değer çiftlerinin her ikisininde string tipinde olduğu durumlarda tercih edilebilir.
   - StringCollection: Karakter katarlarını saklamak için optimize edilmiş bir koleksiyondur.
   - StringDictionary: Anahtar-Değer çiftlerinin her ikisininde string tipinde olduğu bir hash tablodur. Anahtar-Değer çiftleri küçük harflere çevrilerek saklanır.

Aşağıda en çok kullanılan koleksiyon yapıları anlatılmıştır:

## ArrayList Kullanımı

ArrayList sınırları dinamik olarak değişebilen diziler olarak tanımlanır. Farklı veri tipindeki öğeleri ArrayList'e ekleyebiliriz. Eklenen her veri object tipindedir. Dolayısı ile her veri için boxing ve unboxing işlemleri uygulanır. Dizilerden çok daha performanslı çalışır. ArrayList'e eklenen her bir elemana indeks numarasıyla erişe bilmekteyiz. ArrayList'in başlangıç kapasitesi 4'tür. Mevcut kapasite yeterli gelmediğinde, arkaplanda kapasite 2 katına çıkarılmaktadır.

```cs
ArrayList liste1 = new ArrayList();
liste1.Add(5);
liste1.Add("Alperen");
liste1.Add(10);
liste1.Add(new Exception());

Console.WriteLine(liste1[1]); // 1. indisteki elemanı döndürür.

liste1.Remove("Alperen"); // Remove() metoduna parametre olarak girilen ifade koleksiyon içerisinden silinir.
liste1.Clear(); // Clear() metodu koleksiyon içerisindeki tüm öğeleri silmektedir.
int elemanSayisi = liste1.Count; // Koleksiyon içerisinde yer alan elemanların sayısını döndürmektedir.
int kapasite = liste1.Capacity; // Koleksiyonun kapasitesinin döndürmektedir.
bool varmi = liste1.Contains(456); // Koleksiyon içerisinde parametre olarak girilen öğeyi arar. Öğe bulunursa TRUE, bulanamazsa FALSE döndürür.
liste1.Sort(); // Metodu: Koleksiyon içerisindeki öğeleri artan sırada sıralamaktadır. Sıralama işlemi için öğelerin karşılaştırılabilir olması gerekmektedir.

string[] dizi = new string[20];
liste1.CopyTo(dizi, 2); // CopyTo(dizi,i) metodu, koleksiyon içerisindeki tüm öğeleri, diziye i.indeksten başlayarak kopyalayacaktır.

// Daha fazla Metot ve Özellik için: https://www.srdrylmz.com/c-arraylist-sinifi/
```

## GenericList Kullanımı

Generic List, sınırları dinamik olarak değişebilen diziler olarak tanımlanır. Aynı veri tipindeki öğeleri Generic List'e ekleyebiliriz. Bu yönü ile ArrayList'lerden ayrılırlar. ArrayList ile aynı metodlara sahiptir.

**Not:** Tipi kendimiz belirlediğimiz yapılara generic diyoruz.

```cs
List<int> liste1 = new List<int>();
liste1.Add(200);
liste1.Add(100);
liste1.Add(300);
liste1.Sort();
```

## Hashtable Kullanımı

Bir koleksiyondaki elemanlara bir anahtar değer ile erişmek isteyebiliriz. Bu durumu System.Collections isim alanında bulunan Hashtable sınıfı kullanarak çözebiliriz. Hashtable sınıfında koleksiyonlar, bir anahtar (key) ve değer (value) ikilisi olarak saklanır. Verdiğimiz "Key" değeri unique olmak ve null olmamak zorundadır. Büyük-küçük harf duyarlılığına sahiptir. Bir Hashtable koleksiyonu oluşturup, Anahtar-Değer çifti eklemek istediğimizde arkaplanda gerçekleşen işlemler;

1. Öncellikle depolama işlemi için kullanılacak bir hash tablosu oluşturulur.
1. Anahtar kullanılarak hash kod denilen benzersiz bir değer üretilir (Hashing). Bu değer anahtar ile ilişkili verilerin, hash tablosunda saklanacağı indeksi belirtecektir.
1. Anahtar ile ilişkili veriler, hash tablosunda Hash kodunun belirttiği indekse eklenir.

**Not:** Arkaplanda gerçekleşen tüm bu işlemler büyük veri kümelerini içeren koleksiyonlar da arama süresini ciddi anlamda düşürmektedir.

Hashtable Koleksiyonu Metotları ve Özellikleri: <https://www.srdrylmz.com/c-dictionary-sinifi/>

```cs
 Hashtable Arac = new Hashtable();
Arac.Add("41 ABC 123", "Alfa Romeo");  // Arac.Add(Anahtar(key),Değer(value));
Arac.Add("56 ABC 456", "Audi");
Arac.Add("25 ABC 789", "Mercedes-Benz");

foreach (DictionaryEntry oge in Arac) // DictionaryEntry sınıfı ile koleksiyonda ki Anahtar-Değer çiftlerine ulaşabiliriz.
    Console.WriteLine("Anahtar:{0} - Değer:{1}", oge.Key, oge.Value);

string plaka = "41 ABC 123";
string model = "Audi";
Console.WriteLine(Arac[plaka]);
bool keyVarMı = Arac.ContainsKey(plaka); // ContainsKey() metodu key değerinin koleksiyonda olup olmadığına bakar.
bool valueVarMı = Arac.ContainsValue(model); // ContainsValue() metodu value değerinin koleksiyonda olup olmadığına bakar.
Console.WriteLine("Eleman sayısı: " + Arac.Count); // Count Özelliği
Arac.Remove("56 ABC 456"); // Remove Metodu
Arac.Clear(); // Clear Metodu

// Keys Özelliği: Anahtarları (Keys) içeren bir koleksiyon döndürmektedir.
ICollection Koleksiyon_1 = Arac.Keys;

// Values Özelliği: Değerleri (Values) içeren bir koleksiyon döndürmektedir.
ICollection Koleksiyon_2 = Arac.Values;
```

## Dictionary Kullanımı

Standart dizilere eklenen elemanlar, belleğe sıralı bir şekilde yerleştirilmektedir. Sıfırdan başlanarak her bir elemana birer indeks değeri verilip, elemanlara o indeksler aracılığıyla erişmemiz sağlanmaktaydı. Koleksiyon sınıflarından biri olan ArrayList içinde aynı durum söz konusu. ArrayList’e eklenen her bir elemana indeks numarasıyla erişe bilmekteyiz. Dictionary koleksiyonunda ise veriler Anahtar(Key) ve Değer(Value) yapısı ile tutulur. Koleksiyon içerisinde yer alan Anahtarlar birbirinden farklı olmalıdır. Dictionary sınıfından bir nesne oluştururken, anahtar ve değerin veri tiplerini belirtmemiz gerekmektedir.

Dictionary Koleksiyonu Metotları ve Özellikleri: <https://www.srdrylmz.com/c-dictionary-sinifi/>

### Hashtable ile Dictionary Arasındaki Farklar Nelerdir?

Hashtable:

- Generic değildir.
- System.Collections namesapce'i içindedir.
- Hashtable'da, aynı türdeki veya farklı türdeki anahtar/değer çiftlerini saklayabilirsiniz.
- Hashtable'da, anahtarın ve değerin türünü belirtmeye gerek yoktur.
- Boxing ve Unboxing olayları nedeniyle veri alımı Dicitionary'ye göre daha yavaştır.
- Hashtable'da, verilen Hashtable'da bulunmayan bir anahtara erişmeye çalışırsanız, o zaman boş değerler verecektir.
- Depolanan değerlerin sırasını korumaz.

Dicitionary:

- Generictir.
- System.Collections.Generic namesapce'i içindedir.
- Dicitionary'de, aynı türden anahtar/değer çiftlerini saklayabilirsiniz.
- Dicitionary'de, anahtarın ve değerin türünü belirtmelisiniz.
- Boxing ve Unboxing olayları olmadığı için veri alımı Hashtable'dan daha hızlıdır.
- Dicitionary'de, verilen bir anahtara erişmeye çalışırsanız ve o anahtar dictionary'de yok ise, hata verecektir.
- Her zaman saklanan değerlerin sırasını korur.

```CS
Dictionary<int, string> Ogrenci = new Dictionary<int, string>();
Ogrenci.Add(134, "Tolga Demirer");
Ogrenci.Add(158, "Ümit Özkan");
Console.WriteLine(Ogrenci[158]);
```

## SortedList Kullanımı

Verileri Key Value olarak tutar. Tutulan veriler sıralı olarak saklanır. Her eklenen elemandan sora yeniden sıralanır. Verdiğimiz "Key" değeri unique olmak ve null olmamak zorundadır. Sıralama işlemini, Anahtar(Key) değerlerine göre yapar. Sıralamayı küçükten büyüğe yapar. SortedList generic yada nongeneric şekilde oluşturulabilir. Büyük-küçük harf duyarlılığına sahiptir.

SortedList Koleksiyonu Metotları ve Özellikleri: <https://www.muratoner.net/csharp/csharp-sortedlist-kullanimi-ve-ornekleri>

**Not:** Hastable sınıfında olduğu gibi SortedList sınıfında da Anahtar-Değer çiftlerini bir DictionaryEntry yapısında tutabiliriz.

```cs
SortedList SiraliKoleksiyon_1 = new SortedList(); // Non-Generic
SortedList<int, string> SiraliKoleksiyon_2 = new SortedList<int, string>(); // Generic

SiraliKoleksiyon_1.Add(41, "Kocaeli");
SiraliKoleksiyon_1.Add(54, "Sakarya");
SiraliKoleksiyon_1.Add(25, "Erzurum");
```

## CollectionsUtil Sınıfı Kullanımı

SortedList ve HashTable koleksiyonları büyük-küçük harf duyarlılığına sahiptir. Örnek vermek gerekirse; "Serdar" Anahtarına sahip bir öğe koleksiyona eklendikten sonra, "SerdaR" Anahtarına sahip farklı bir öğe daha koleksiyona eklenebilir. Koleksiyon büyük-küçük harf duyarlılığına sahip olduğu için iki Anahtarı da farklı birer girdi olarak kabul edecektir. CollectionsUtil koleksiyonu ise büyük-küçük harf duyarlılığına sahip değildir. Bu yüzden "Serdar" Anahtarına sahip bir öğe koleksiyona eklendikten sonra "SerdaR" Anahtarına sahip farklı bir öğe daha koleksiyona eklenmek istenildiğinde istisna fırlatacaktır.

```cs
SortedList ceviriListesi = CollectionsUtil.CreateCaseInsensitiveSortedList();
ceviriListesi.Add("Computer", "Bilgisayar");
// Büyük-Küçük Harf duyarlılığı olmadığı için 3 satırda aynı çıktıyı verecektir.
Console.WriteLine(ceviriListesi["COMPUTER"]);
Console.WriteLine(ceviriListesi["computer"]);
Console.WriteLine(ceviriListesi["CoMpUtEr"]);
```

## BitArray Kullanımı

BitArray, isminden de anlaşılacağı üzere bir bit dizisidir ve yalnızca True–False değerlerini içermektedir. Bitleri saklamak haricinde And, Or, Xor gibi mantıksal işlemleri de gerçekleştirebilmektedir. BitArray diğer koleksiyon sınıfları gibi dinamik bir yapıya sahiptir. Yani boyutu dinamik olarak artmaktadır. Ayrıca standart diziler gibi BitArray'ler de indekslenebilir.

BitArray Koleksiyonu Metotları ve Özellikleri: <https://www.srdrylmz.com/c-bitarray-sinifi/>

```cs
byte[] sayilar = { 18, 56, 21 };
BitArray bitDizisi = new BitArray(sayilar);    // Koleksiyondaki Bit Sayısı:24
```

## Stack(Yığın) Kullanımı

Son Giren İlk Çıkar (LIFO) prensibi ile çalışan veri yapısı şekinde bilinirler. Stack tıpkı diğer koleksiyon sınıfları gibi dinamik bir yapıya sahiptir. Yani eleman eklendikçe boyutu dinamik olarak artmaktadır. Stack sınıfının Pop() ve Push() olmak üzere 2 temel metodu bulunmaktadır. Ekleme ve çıkarma işleminin yalnızca stack’in tepe noktasından yapılmaktadır. Stack içerisine veri tipi fark etmeksizin her türlü öğe eklenebilir. Eleman ekleme ve çıkarma işlemlerinde Boxing-Unboxing gerçekleşir.

- Pop(): Stack’in en üstündeki nesneyi çıkarır.
- Push(): Stack’in en üstüne bir nesne ekler.
- Peek(): Stack’in tepe noktasındaki öğeyi döndürmektedir, Pop() metodunda farklı olarak öğeyi Stack’ten çıkarmaz/silmez. Stack boşken Peek() metodu çağrılırsa hata fırlatır.

**Not:** Generic stack ile stack içerisine sadece belirtilen veri tipindeki öğeler eklenebilir.
Eleman ekleme ve çıkarma işlemlerinde Boxing-Unboxing gerçekleşmez.

Stack(Yığın) Koleksiyonu Metotları ve Özellikleri: <https://www.srdrylmz.com/c-stack-sinifi/>

```cs
Stack<int> yigin_1 = new Stack<int>();
Stack yigin_2 = new Stack();

yigin_2.Push("www.google.com");
yigin_2.Push("www.alperenbektasoglu.com");

string site_1 = yigin_2.Pop();  // site_1 = www.alperenbektasoglu.com
string site_2 = yigin_2.Pop();  // site_2 = www.google.com
string site_3 = yigin_2.Pop();  // Stack boşaldığı için hata fırlatır.
```

## Queue(Kuyruk) Kullanımı

Queue (Kuyruk), ilk giren ilk çıkar işleyişine sahip bir koleksiyondur(FIFO). Queue (Kuyruk) diğer koleksiyon sınıfları gibi dinamik bir yapıya sahiptir. Yani eleman eklendikçe boyutu dinamik olarak artmaktadır. Queue sınıfının Enqueue() ve Dequeue() olmak üzere 2 temel metodu bulunmaktadır. Eleman çıkarma işleminin kuyruğun başından, eleman ekleme işleminin de kuyruğun sonundan yapılmaktadır. Queue içerisine veri tipi fark etmeksizin her türlü öğe eklenebilir. Eleman ekleme ve çıkarma işlemlerinde Boxing-Unboxing gerçekleşir.

Enqueue(): Kuyruğun sonuna bir eleman ekler.
Dequeue(): Kuyruğun başındaki elemanı çıkarır.
Peek(): Kuyruğun başındaki öğeyi döndürmektedir, Dequeue() metodunda farklı olarak öğeyi kuyruktan çıkarmaz/silmez.

Queue (Kuyruk) Koleksiyonu Metotları ve Özellikleri: <https://www.srdrylmz.com/c-queue-sinifi/>

**Not:** Generic queue ile queue içerisine sadece belirtilen veri tipindeki öğeler eklenebilir.
Eleman ekleme ve çıkarma işlemlerinde Boxing-Unboxing gerçekleşmez.

```cs
Queue<string> kuyruk = new Queue<string>();
kuyruk.Enqueue("Alperen Bektaşoğlu");
kuyruk.Enqueue("Tarkan Tayşi");
kuyruk.Enqueue("Cemal Çiftçi");

string kuyruktanCikarilan = kuyruk.Dequeue();
```

## C#'ta IEnumerable ve IEnumerator Interfaceleri Nedir? ve Nasıl Kullanılır?

1. Kaynak: <https://www.gencayyildiz.com/blog/cta-ienumerable-ve-ienumerator-interfaceleri-nedir-ve-nasil-kullanilir/>
2. Kaynak: <https://www.srdrylmz.com/c-numaralandirici/>
3. Kaynak: <https://www.srdrylmz.com/icomparable-ve-icomparer-arayuzleri/>

IEnumerable; ICollection ve IList'i kapsar. ICollection'da IList'i kapsar.
IEnumerable > ICollection > IList
