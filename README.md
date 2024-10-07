# Patika Week2 Yol Arkadaşı : Tatil uygulaması
Merhaba,
Bu proje C# ile alıştırma için yapılmış bir uygulamadır.

## 📚 Proje Hakkında
Bu proje, aşağıdaki konuları öğrenmeye yardımcı olmak için tasarlanmıştır:
- Basit bir C# programı yazmak
- C# konsol uygulamasının yapısını anlamak
- basit uygulama geliştirmek

## 📚 Proje Açıklaması
Bu pratikte bir yardımcı seyehat uygulaması ile kullanıcılarımızın planlayacakları 3 günlük bir tatilde harcayacakları yaklaşık tutarı hesaplamalarına yardımcı oluyoruz.

3 adet lokasyonumuz var:

1 - Bodrum (Paket başlangıç fiyatı 4000 TL)

2 - Marmaris (Paket başlangıç fiyatı 3000 TL)

3 - Çeşme (Paket başlangıç fiyatı 5000 TL)

Kullanıcımıza gitmek istediği lokasyonu sormalıyız. Bu noktada Büyük-Küçük harf duyarlılığını ortadan kaldırmalı eğer yukarıdaki 3 seçenek dışında bir lokasyon girilirse bir hata olduğunu söylemeli, girebileceği lokasyon isimlerini hatırlatmalı ve yeniden bir veri girmesini istemeliyiz.

Kullanıcının girdiği veriyi bir değişkende tutalım.

Kullanıcıya kaç kişi için tatil planlamak istediğini soralım.

Kişi sayısını bir değişkende tutalım.

Ardından gitmek istenilen lokasyon ve o lokasyonda tatili sırasında yapabilecekleri ile ilgili bir özet bilgiyi ekrana yazdırmalıyız.

Kullanıcıya tatiline ne şekilde gitmek istediğini sorarak aşağıdaki seçenekleri gösterelim..

2 seçeneğimiz var:

1 - Kara yolu ( Kişi başı ulaşım tutarı gidiş-dönüş 1500 TL )

2 - Hava yolu ( Kişi başı ulaşım tutarı gidiş-dönüş 4000 TL)

" Lütfen yukarıdaki seçeneklerden bir tanesini seçiniz diyerek cevabı kullanıcıdan "1" ya da "2" olarak alalım, farklı bir değer girilmesi durumunda bir hata olduğunu söyleyerek soruyu yeniden yöneltelim.

Ardından gidilecek lokasyon, kişi sayısı ve ulaşım aracı seçenekleriyle bir toplam fiyat hesaplayıp bunu kullanıcıya sunalım.

Kullanıcıya başka bir tatil planlamak isteyip istemediğini soralım, istiyorsa uygulama ilk aşamadan çalışmaya başlayabilir, kullanıcı istemiyorsa iyi günler dileyerek uygulamayı sonlandırabiliriz. 

## 🚀 Kod
```csharp
using System.Security.Cryptography.X509Certificates;

namespace patika_w2_yolArkadasi
{
    internal class Program
    {
        static void Main(string[] args)
        {
            bool isContinuing = true;

            while (isContinuing)
            {
                // Lokasyonlar ve fiyatlar
                string[] locaions = { "Bodrum", "Marmaris", "Çeşme" };
                int[] prices = { 4000, 3000, 5000 };
                string current_location = "";
                int vacationPrice = 0; //tatil fiyatını atayacağımız değişken
                int peopleCount; //kişi sayısı

                // Kullanıcıdan lokasyon al
                while (true) //sonsuz döngüye aldım koşulu sağladığı an döngüden çıkılacak.
                {
                    Console.Write("Gitmek istediğiniz yer (bodrum/marmaris/çeşme): ");
                    current_location = Console.ReadLine().ToLower(); //küçük harf'e çevirdim.

                    //kullanıcıdan kişi sayısı al
                    Console.Write("Kaç kişi için tatil planlamak istiyorsunuz: ");
                    peopleCount = int.Parse(Console.ReadLine());

                    switch (current_location)
                    {
                        case "bodrum":
                            Console.WriteLine("Güzel plajları ve tarihi kalıntıları ile ünlü.");
                            vacationPrice = peopleCount * prices[0]; //bodrum seçilince kişi sayısı ile ücret çarpılıp toplam çıkar
                            break;
                        case "marmaris":
                            Console.WriteLine("Doğal güzellikleri ve lüks tatil köyleri ile bilinir.");
                            vacationPrice = peopleCount * prices[1];//marmaris seçilince kişi sayısı ile ücret çarpılıp toplam çıkar
                            break;
                        case "çeşme":
                            Console.WriteLine("Serin denizi ve tarihi yerleri ile tanınır.");
                            vacationPrice = peopleCount * prices[2];//çeşme seçilince kişi sayısı ile ücret çarpılıp toplam çıkar
                            break;
                        default:
                            Console.Write("Hata! Geçerli Lokasyon Giriniz (bodrum/marmaris/çeşme): ");
                            continue;
                    }

                    break; //geçerli lokasyon seçilince döngüden çıkılıcak.
                }



                //kullanıcıdan ulaşım tercihini al
                int travelCost = 0; //ulaşım fiyatını değişkene atadım.
                while (true)
                {
                    Console.WriteLine("Ulaşım Türünü Seçin");
                    Console.WriteLine("1 - Kara yolu (Kişi başı ulaşım tutarı gidiş-dönüş 1500 TL)");
                    Console.WriteLine("2 - Hava yolu (Kişi başı ulaşım tutarı gidiş-dönüş 4000 TL)");
                    Console.Write("Seçiminiz (1 veya 2): ");
                    string transportOption = Console.ReadLine(); //ulaşım türü seçimi değişkeni

                    switch (transportOption)
                    {
                        case "1":
                            travelCost = 1500 *peopleCount;
                            break;
                        case "2":
                            travelCost = 4000 * peopleCount;
                            break;
                        default:
                            Console.WriteLine("HATA! Lütfen 1 veya 2 Seçiniz");
                            break;
                    }
                    break;
                }


                //Toplam Fiyat Hesaplama
                int total_price = (vacationPrice + travelCost );
                // ulaşım fiyatı ile insan sayısını çarpıyor daha sonra tatil fiyatı ile topluyor.

                //özet bilgi
                Console.WriteLine("\nTatili planladığınız lokasyon: " + current_location.ToUpper());
                Console.WriteLine("Kişi sayısı: " + peopleCount);
                Console.WriteLine("Ulaşım tipi: " + (travelCost == 1500 ? "Kara yolu" : "Hava yolu"));//if else yerine tek satırda gitme seçeneğini öğrendik
                Console.WriteLine("Toplam tatil maliyetiniz: " + total_price + " TL");

                Console.Write("\nBaşka bir tatil planlamak istiyor musunuz? (Evet/Hayır): ");
                string cevap = Console.ReadLine().ToLower();

                if (cevap == "hayır" || cevap == "hayir")
                {
                    isContinuing = false; //en başta döngünün çalışmasını sağlayan true değer false girilirse döngüden çıkılıyor.
                    Console.WriteLine("İyi günler dileriz!");
                }

            }
        }
    }
}


