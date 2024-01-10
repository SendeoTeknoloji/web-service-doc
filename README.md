
<img align="center" width="45%" src="logo.png">

# Web Servis Teknik Dokümanı


***İçindekiler***

| Konu | Sayfa |
| -------- | ------- |
|[Giriş	5](#_toc101346603) | 5|
|[Genel Bilgiler](#_toc101346604) | 5|
|[Generic Kargo Entegrasyon](#_toc101346605) | 	6|
|[Cargo Servisleri	](#_toc101346606) | 8|
|[SETDELIVERY](#_toc101346607) | 9|
|[İstek Parametreleri	](#_toc101346608) | 9|
|[Cevap Parametreleri (200 = Başarılı)	](#_toc101346609) | 14|
|[Hatalı Dönüş Parametreleri	](#_toc101346610) | 15|
|[CANCELDELIVERY	](#_toc101346611) | 16|
|[İstek Parametreleri	](#_toc101346612) | 16|
|[Cevap Parametreleri (200 = Başarılı)	](#_toc101346613) | 16|
|[Hatalı Dönüş Parametreleri	](#_toc101346614) | 16|
|[TRACKDELIVERY	](#_toc101346615) | 16|
|[İstek Parametreleri	](#_toc101346616) | 16|
|[Cevap Parametreleri (200 = Başarılı)	](#_toc101346617) | 16|
|[Hatalı Dönüş Parametreleri	](#_toc101346618) | 19|
|[CARGOMEASUREMENTUPDATE	](#_toc101346619) | 19|
|[İstek Parametreleri	](#_toc101346620) | 20|
|[Cevap Parametreleri (200 = Başarılı)	](#_toc101346621) | 21|
|[Hatalı Dönüş Parametreleri	](#_toc101346622) | 21|
|[GETBARCODEBYTRACKINGNUMBER	](#_toc101346623) | 22|
|[İstek Parametreleri	](#_toc101346624) | 22|
|[Cevap Parametreleri (200 = Başarılı)	](#_toc101346625) | 22|
|[Hatalı Dönüş Parametreleri	](#_toc101346626) | 22|
|[GETBARCODE	](#_toc101346627) | 22|
|[İstek Parametreleri	](#_toc101346628) |22|
|[Cevap Parametreleri (200 = Başarılı)	](#_toc101346629) | 23|
|[Hatalı Dönüş Parametreleri	](#_toc101346630) | 23|
|[Servislerde Kullanılacak Bilgiler	](#_toc101346631) | 24|
|[Sendeo Statü Listesi	](#_toc101346632) | 24|
|[Sendeo İl ve İlçe Listesi	](#_toc101346633) | 26|
|[Delivery Type Request Örnekleri	](#_toc101346634) | 28|
|[Kod Örnekleri	](#_toc101346635) | 28|



***Tablo Listesi***



[**Şekil 1 Login Yöntemi Swagger	4****](#_toc100827509)

[**Şekil 2 Cargo Servisleri Listesi	6****](#_toc100827510)

[**Şekil 3 SetDelivery İstek Parametreleri	10****](#_toc100827511)

[**Şekil 4 SetDelivery products array	11****](#_toc100827512)

[**Şekil 5 SetDelivery Cevap Parametreleri (200 = Başarılı)	12****](#_toc100827513)

[**Şekil 6 SetDelivery Hatalı Dönüş Parametreleri	13****](#_toc100827514)

[**Şekil 7 SetDelivery Exception Message	13****](#_toc100827515)

[**Şekil 8 CancelDelivery Hatalı Dönüş Parametreleri	14****](#_toc100827516)

[**Şekil 9 TrackDelivery Cevap Parametreleri (200 = Başarılı)	15****](#_toc100827517)

[**Şekil 10 TrackDelivery products.array	16****](#_toc100827518)




# <a name="_toc101346603"></a>Giriş
![](Sendeo.9822246f-99c5-433f-9aec-66c86d8463a9.002.png)

Bu doküman, Sendeo web servis entegrasyonları için hazırlanmıştır. <a name="ole_link18"></a><a name="ole_link19"></a>Entegrasyon için kullanılacak web servisler ve ilgili servislere erişimi tariflenmektedir.
 
# <a name="_toc101346604"></a>Genel Bilgiler

Sendeo servisleri <https://api.sendeo.com.tr>  üzerinden çalışmaktadır. 

Servislerin kullanılması için müşteri bazlı token alınması gerekmektedir. Bu bilgi Token/LoginAES servisi üzerinden müşteri bazlı alınmaktadır. “BEARER” token kullanılmaktadır. Token expire süremiz 20 saattir. Bu süre bitiminde yeniden token alınması gerekmektedir. Erişimde TLS 1.2 kullanılmalıdır.

![Login Yönetimi parametreleri](Sendeo.9822246f-99c5-433f-9aec-66c86d8463a9.003.png)

<a name="_toc100827509"></a>*Şekil 1 Login Yöntemi Parametreleri*

Yapılan entegrasyon testlerinin takibinin hem müşteri hem Sendeo tarafından kolay takibi amacıyla farklı müşteriler için tek test hesabı bulunmaktadır. Testler başarılı şekilde tamamlandıktan sonra canlı geçiş sürecinde api kullanıcı tanımı sube.sendeoo.com.tr üzerinden tanımlanması gerekmektedir. API servislerimiz herkese açıktır. Dışarıdan gelen istekler için herhangi bir IP iznimiz bulunmamaktadır. Ancak çok sayıda hatalı kullanıcı adı veya şifre bilgisi girildiğinde bloklanma olmaktadır. Bu durumda entegrasyon mail adresimize bilgi verilmelidir.

Test HESABI Bilgileri

“musteri”: “**TEST”**

“sifre”: **TesT.43e54**


Canlı APi Bilgilerinin tanımı aşağıdaki gibi yapılması gerekmektedir.

1. Sube.sendeo.com.tr sayfasına giriş yapılır
1. Açılan ekran üzerinden “Kayıt Ol” butonuna tıklanır

![](Sendeo.9822246f-99c5-433f-9aec-66c86d8463a9.004.png)

1. Kayıt oluştururken satış temsilcinizin ana müşteriye tanımladığı cep telefonu numarası ile kayıt olunması gerekmektedir.
1. Kayıt Olma aşamasında ekranda gösterilen bilgiler giriş yapılır. Bilgiler giriş yapılması sonrasında “Kayıt Ol” butonuna basıldığında giriş yapılan cep telefonuna doğrulama kodu gönderilir. Gönderilen doğrulama kodu giriş yapılarak Kayıt Ol denildiğinde ilgili kullanıcının tanımı gerçekleştirilmektedir.

![](Sendeo.9822246f-99c5-433f-9aec-66c86d8463a9.005.png)

1. Kayıt işleminin başarılı olması sonrasında kullanıcı Şube Sende Login sayfasına yönlendirilmektedir. Ekran üzerinden OTP kodu da giriş yapılarak login işlemi gerçekleşir.
1. Kayıt olunan Cep telefonu bilgisi ana müşteriye ait ise tanımlanan Admin kullanıcı alt müşterilere ilişkin kullanıcı tanımları yapılabilmektedir.
1. Şube Uygulamasına OTP ile giriş yapılması sonrasında menü üzerinde “Kullanıcılar” keranı görülecektir. Kullanıcılar ekranı açılarak ekrandaki bilgiler giriş yapılarak API kullanıcısı için “Kullanıcı Tipi”  API seçilerek web servis kullanıcısı oluşturulabilir

![](Sendeo.9822246f-99c5-433f-9aec-66c86d8463a9.006.png)

# <a name="_toc101346605"></a>Generic Kargo Entegrasyon 

Sendeo kargo entegrasyonu çalışma prensibi, müşterinin giden kargoları için web servis ile göndermiş olduğu bilgilerin kullanılarak Sendeo tarafında toplama işleminin yapılarak, gönderinin oluşturulmasıdır. 

Generic Web servis entegrasyonu ile müşterimiz kendi etiketi üzerinde barkodunu oluşturduğu tekil bir numara (refernceNo) ile ya da Sendeo taşıma barkodunu oluşturarak entegrasyon gerçekleştirebilir.

Gönderi toplama işlemi için tekil bir numara (referenceNo) oluşturulur. Oluşturduğu tekil numara ile gönderilerin tüm statülerini takip edebilir. Web servisten dönen parametrik takip linkini kullanarak link üzerinden gönderinin takibi son kullanıcı tarafında yapılabilir.


#### ***Generic Kargo Entegrasyonu iş akışı:***

1. Müşteri gönderilerine ait verileri “SetDelivery” ile Sendeo sistemine aktarır.
1. “SetDelivery” servisindeki cityId ve districtId bilgilerini “GetCityDistricts” servisinden sorgulayabilirsiniz. GetCityDistricts servisinden il ismine ya da il/ilçe ismine göre sorgulama yapılarak il ve ilçe kodlarına ulaşılabilir. İlgili servisin kullanılmadığı durumda teknik dökümanımızda bulunan il-ilçe excel listesi üzerinden il ve ilçe kodlarımıza ulaşabilirsiniz.
1. Sisteme aktarılan verilerdeki ReferenceNo bilgisi oluşturulan barkod üzerinde bulunması gerekmektedir. 
1. Fiziken toplama işlemi yapılmadan önce veri “CancelDelivery” ile iptal edilmesi mümkündür. Toplama işlemi yapılmış olan iş emirleri için iptal işlemi gerçekleştirilememektedir. Gönderi düzenlenmesi sonrasında taşıma süreci başladığı için iptal işlemi gerçekleştirilemez.
1. Toplama sürecinde müşterimizin oluşturduğu ReferenceNo bilgisini okutarak toplama işlemini gerçekleştirir.
1. Gönderi oluşması sonrasında “TrackDelivery” metodu ile gönderinin durumu takip edilebilir.
1. Adet ve Desi/Kg bilgisini ileten müşteriler için SETDELIVERY servisi ile veri iletildikten sonra CARGOMEASURMENTUPDATE servisi ile gönderdiği sipariş için kargo adet ve desi bilgilerini yeniden gönderilmesi gerekmektedir. SETDELIVERY sonrasında CARGOMEASURMENTUPDATE servisinden desi bilgisi gönderilmediği durumda operasyon tarafından ölçüm-tartım işlemi yapılarak ilerlenecektir.











# <a name="_toc101346606"></a>Cargo Servisleri

![](Sendeo.9822246f-99c5-433f-9aec-66c86d8463a9.007.png)

![](Sendeo.9822246f-99c5-433f-9aec-66c86d8463a9.008.png)

![](Sendeo.9822246f-99c5-433f-9aec-66c86d8463a9.009.png)

![](Sendeo.9822246f-99c5-433f-9aec-66c86d8463a9.010.png)

![](Sendeo.9822246f-99c5-433f-9aec-66c86d8463a9.011.png)

![](Sendeo.9822246f-99c5-433f-9aec-66c86d8463a9.012.png)

<a name="_toc100827510"></a>*Şekil 2 Cargo Servisleri Listesi*

Genel kullanıma sunulmuş kargo servislerimiz yukarıdaki gibidir. Başarılı isteklerde 200, başarısız/hatalı isteklerde hatanın tipine göre hata mesajıyla birlikte 500 hatası dönmektedir. Eğer token ile authentication sağlanmazsa 401 döner.

Bu servislerin ana kullanım amaçları kısa özetlerle aşağıdaki gibidir:

#### GetCityDistricts

Gönderici ve alıcı müşteriye ait adreslerde Setdelivery servisine iletilecek il ve ilçe kodları bilgisinin sorgulandığı web servistir. İl adı ya da il/ilçe adı ile sorgulama yapılabilmektedir.

#### SETDELIVERY

Müşterilerin Sendeo’ya istek atarak Gönderi/İş Emri oluşturulması sağlar.

#### TRACKDELIVERY

Müşterilerin Sendeo’ya istek atarak daha önce oluşturduğu Gönderinin farklı bilgilerle takibini sağlar.

#### CANCELDELIVERY

Müşterilerin Sendeo’ya istek atarak daha önce oluşturduğu Gönderi/İş Emri’ni iptal etmesini sağlar.

#### CARGOMEASUREMENTUPDATE

Müşterilerin Sendeo’ya istek atarak daha önce oluşturduğu Gönderi/İş Emri için adet ve ölçüm bilgilerini güncelleyebilmesini sağlar.

#### GETBARCODEBYTRACKINGNUMBER

Müşterilerin Sendeo’ya istek atarak daha önce oluşturduğu Gönderi/İş Emri için takip numarasını kullanarak barkod bilgilerini alabilmesini sağlar.
## <a name="_toc101346607"></a> GetCityDistricts
Gönderici ya da Alıcı müşteriye ait adreslerde il ve ilçe kodu bilgisinin alındığı web servistir. Servisten il adına ya da il ve ilçe adına göre sorgulama yapılabilir.  Servisten dönen CityId ve DistrictId bilgileri setdelivery servisinde ilgili alanlara gönderilerek iş emri oluşturulabilir. İl ve ilçe kodları bilgisi web servis haricinde teknik dokümanımızdaki il ve ilçe kodları excel listesinden alınabilir.
## SETDELIVERY
Müşterilerin belirli bilgileri kullanarak Sendeo tarafında gönderi/iş emri oluşturmasını sağlayan servistir. POST metodu ile çalışır. 6 farklı şekilde gönderi/iş emri oluşturulabilir. Bunlar:

- **DeliveryType 1:** Lokasyonunuz >> Müşteriniz: Lokasyon’dan Müşteriye giden gönderilerde kullanılmaktadır. Birden fazla lokasyon var ve her biri için ayrı fatura düzenlenecek ise; farklı kullanıcılar ile yönetilmelidir. Eğer fatura Ana Müşteriye düzenlenecek ise deliveryType=3 kullanılmalıdır.
- **DeliveryType 2:** Müşteriniz >> Lokasyonunuz : Müşteriden Lokasyona normal gönderi ya da iade gönderisi yapmak için kullanılmaktadır
- **DeliveryType 3:** Tedarikçiniz v.b. >> Müşteriniz  
- **DeliveryType 4:** Yeniden gönderi talimatı 
- **DeliveryType 5:** Teslimat Noktası . Sendeo Teslimat noktasına teslim edilecek gönderiler için kullanılmaktadır
- **DeliveryType 6:** İade Noktası. Sendeo İade noktasından alınacak gönderiler için kullanılmaktadır

Müşterilerimiz çalıştığı tüm birimler arasında gönderi oluşturabilirsiniz. Ayrıca teslimat ve iade noktası olarak da servis alabilirsiniz.

Teknik dökümanımızda bilgilerini paylaştığımız City ve District bilgileri ile gönderi ilgili il-ilçe için şubeye iletilecektir. 

Teslimat ve İade noktası için de kullanmak istediğiniz bayi bilgisini ID olarak size verilen Id’ler ile hedefleyebilirsiniz.** 

### <a name="_toc101346608"></a>İstek Parametreleri


|**Parametre**|**Tipi**|**Zorunluluk**|**Örnek Değer**|**Açıklama**|
| :- | :- | :- | :- | :- |
|DeliveryType|integer|Zorunlu|1|<p>Yukarıda belirtilen Type 1, 2, 3, 4, 5, 6 seçeneklerini içerir. Gönderinin nereden alınıp nereye gönderileceğini veya hangi noktadan alınıp verileceğini belirtir.</p><p></p>|
|ReferenceNo|string|Zorunlu|“sendeo-aygaz-12345”|Müşterilerin iç işleyişinde kullandığı referans numarasını içerir. Bu değer ile gönderiler takip edebilir, iade talepleri oluşturabilir.|
|Description|string|Zorunlu Değil|“sendeo hakkında kitap içeren gönderi”|Gönderiye ait özel bir bilgi veya açıklama girmek isterseniz bu alanı kullanabilirsiniz.|
|Sender|string|Değişken|“Ali Sendeo”|<p>Gönderen müşteri ünvanını içerir. DeliveryType = 2,3 için **zorunludur**.</p><p>DeliveryType = 1 için **doldurulmaz**.</p>|
|SenderId|string|Zorunlu Değil||Sendeo tarafında olan müşteri kodu bilgisidir. Sendeo tarafında kayıtlı müşteriler kullanılmıyor ise ilgili alan gönderilmemesi gerekmektedir.|
|SenderAuthority|string|Zorunlu Değil|“Can Sendeo”|Gönderen müşteri yetkilinizi belirtir.|
|SenderBranchCode|integer|Değişken|123|İade noktası operasyonunda gönderilmesi **zorunlu** alandır. DeliveryType = 6 seçilmemesi durumunda boş **bırakılmalıdır**.|
|SenderAddress|string|Zorunlu |TEST ADRES TEST ADRES|DeliveryType bilgisine göre değişkenlik göstermektedir. Açık adresi girilmelidir. |
|SenderCityId|integer|Zorunlu|34|City tablosundan gelecek şehir Id’si ile gönderen müşteri ili olarak girilmelidir.|
|SenderDistrictId|integer|Zorunlu|34139|District tablosundan gelecek Id gönderen müşterinin bulunduğu ilçe girilmelidir.|
|senderPhone|string|Değişken|2121234567|<p>Gönderen müşterinin telefon numarasını belirtir. İdealde xyz1234567 şeklinde 10 hane olarak gönderilmesi beklenmektedir.</p><p>*Phone veya GSM alanlarından bir tanesi mutlaka gönderilmelidir.*</p>|
|SenderGSM|string|Değişken|5361234567|<p>Gönderen müşterinin GSM numarasını belirtir. İdealde 5xx1234567 şeklinde 10 hane olarak gönderilmesi beklenmektedir.</p><p>*Phone veya GSM alanlarından bir tanesi mutlaka gönderilmelidir.*</p>|
|SenderEmail|string|Zorunlu Değil|<sendeo@sendeo.com>|Gönderen müşterinin mail adresini içerir.|
|Receiver|string|Değişken|“Ali Sendeo”|<p>Alıcı müşteri ünvanını içerir. deliveryType = 1,3 için **zorunludur**.</p><p>deliveryType = 2 için **doldurulmaz**.</p>|
|ReceiverId|string|Değişken||Alıcı müşterinin kodudur. Sendeo tarafında değeri biliniyor ise gönderilmelidir. |
|ReceiverAuthority|string|Zorunlu Değil|“Can Sendeo”|Alıcı müşteri yetkilisini belirtir.|
|ReceiverBranchCode|integer|Değişken|123|Teslimat noktası operasyonunda gönderilmesi **zorunlu** alandır. deliveryType = 5 seçilmemesi durumunda boş **bırakılmalıdır**.|
|ReceiverAddress|string|Değişken|“Kemerburgaz Caddesi Vadi İstanbul Park 7B Blok Kat:12 Sarıyer İstanbul”|<p>Alıcı müşterinin adres bilgileri girilmelidir.</p><p>Alıcı müşteri ünvanını içerir. deliveryType = 1,3 için **zorunludur**.</p><p>deliveryType = 2 için **doldurulmaz**.</p>|
|ReceiverCityId|integer|Zorunlu|34|City tablosundan gelecek şehir Id’si ile alıcı müşteri ili olarak girilmelidir.|
|ReceiverDistrictId|integer|Zorunlu|34139|District tablosundan gelecek Id alıcı müşterinin bulunduğu ilçe girilmelidir.|
|receiverPhone|string|Değişken|2121234567|<p>Alıcı müşterinin telefon numarasını belirtir. İdealde xyz1234567 şeklinde 10 hane olarak gönderilmesi beklenmektedir.</p><p>*Phone veya GSM alanlarından bir tanesi mutlaka gönderilmelidir.*</p>|
|ReceiverGSM|string|Değişken|5361234567|<p>Alıcı müşterinin GSM numarasını belirtir. İdealde 5xx1234567 şeklinde 10 hane olarak gönderilmesi beklenmektedir.</p><p>*Phone veya GSM alanlarından bir tanesi mutlaka gönderilmelidir.*</p>|
|ReceiverEmail|string|Zorunlu Değil|<sendeo@sendeo.com>|Alıcı müşterinin mail adresini içerir.|
|PaymentType|integer|Zorunlu|1|Standart olarak 1 **girilmelidir**.|
|CollectionType|integer|Zorunlu|0|<p>Tahsilatlı kargolarda ödeme şeklini gösterir:</p><p>0 – Tahsilatsız kargo</p><p>1 – Nakit</p><p>2 – Kredi Kartı</p>|
|CollectionPrice|double|Zorunlu|0|Tahsilatlı kargolarda müşteriden ne kadar tahsilat yapılacağını gösterir. Tahsil edilecek tutar gönderilmelidir. collectionType değerinin 0 olması halinde collectionPrice = 0 olmalıdır. Bu alan 5000 lira ile sınırlıdır.|
|DispatchNoteNumber|string|Zorunlu Değil|“1a2b3-SendeO”|Müşteriye oluşturulan resmi irsaliye seri ve numarasını içerir. Giriş yapılması halinde buna göre gönderiler sorgulanabilir.|
|ServiceType|integer|Zorunlu|1|<p>Servis tipini belirtir. Özel operasyonlar dışında default 1 gönderilmelidir.</p><p></p>|
|BarcodeLabelType|integer|Zorunlu|<p>1 </p><p></p>|<p>Servis dönüşünde alınacak barkod etiket yazdırma tipini belirtir.</p><p>0 – ZPL</p><p>1 – Base64</p><p>2 – ZPL</p><p>3 – ZPLs</p><p>8–  ZPL - BarcodeLabelType alanında 8 değeri gönderilir ise   “additionalValue” alanında verinin **ZPL** formatında eklenmesi gerekmektedir.</p><p>9 – Base64 - BarcodeLabelType alanında 9 değeri gönderilir ise   “additionalValue” alanında verinin **HTML** formatında eklenmesi gerekmektedir.</p><p>10–Base64- BarcodeLabelType alanında 10 değeri gönderilir ise   “additionalValue” alanında verinin **TEXT** formatında eklenmesi gerekmektedir.</p><p></p><p>BarcodeLabelType = 8 , 9 veya 10 için additionalValue alanı gönderildiğinde</p><p>additionalValue </p><p>barkodun alt kısmında bulunan 2\*10’luk alanda gösterilecektir.</p><p></p><p>Array olarak alınan gönderi bilgilerinin detayıdır. Toplam adet şeklinde gönderilebileceği gibi aynı zamanda gönderileri detaylandırıp farklı şekillerde girilebilir.</p><p></p>|
|AdditionalValue|string|Zorunlu Değil|BarcodeLabelType alanında gönderilen bilgiye göre değişmektedir.Bu kısma girilen değer barkodun alt kısmında bulunan 2\*10’luk alanda gösterilmektedir.|BarcodeLabelType bilgisine göre “ZPL”,”HTML” veya “TEXT” formatında bilgi iletilebilir.|
|customerReferenceType|string|Zorunlu Değil|A123|referenceNo alanının müşteri iş işleyişinde referans bazlı gönderi ayırmaya yeterli olmadığı durumlar için müşterinin daha fazla detay girebilmesini sağlayan alandır.|



<a name="_toc100827511"></a>*Şekil 3 SetDelivery İstek Parametreleri*

|products array|||||
| :-: | :- | :- | :- | :- |
|Count|İnteger|Zorunlu|2|Gönderi adetini belirtir. Her bir detay için adet girilmelidir. Count toplamı kadar barkod numarası oluşur.|
|ProductCode|String|Zorunlu Değil||Boş string olarak **gönderilmelidir**.|
|Description|string|Zorunlu Değil||<p>Ürüne ilişkin açıklama bilgisidir</p><p>Boş string olarak **gönderilmelidir**.</p>|
|Deci|integer|Zorunlu Değil|20|<p>Gönderiye ait paketlerin deci bilgilerini içerir. count ile beraber kullanılmaktadır. Gönderilmediği durumda ölçüm Sendeo Operasyon’da yapılmaktadır.</p><p>*Tek gönderi biri 3 deci, diğeri 4 deci olan 2 kutunuz varsa:*</p><p>- *count : 1, deci : 4*</p><p>- *count : 1, deci : 3*</p><p>*gönderilir.*</p><p>*Tek gönderi iki adet 5 deci kutudan oluşuyorsa:*</p><p>- *count : 2, deci : 5*</p><p>*gönderilir.*</p><p>Deci ya da kg ölçülememesi durumunda 0(sıfır) olarak gönderilmelidir*.*</p>|
|Weigth|integer|Zorunlu Değil||Gönderi paketlerinin ağırlığını belirtir.|
|DeciWeight|integer|Zorunlu Değil||Gönderi paketlerinin deci/ağırlık değerini belirtir.|
|Price|double|<p>Zorunlu</p><p>Değil</p>||0\.0 -> Double değer olarak gönderilebilir. Nihai tutarı deci girildiğinde sistem hesaplamaktadır.|

<a name="_toc100827512"></a>*Şekil 4 SetDelivery products array*


### <a name="_toc101346609"></a>Cevap Parametreleri (200 = Başarılı)


|**Parametre**|**Tipi**|**Örnek Değer**|**Açıklama**|
| :- | :- | :- | :- |
|TrackingNumber|string|9124356789047|Oluşturulan iş emri/gönderinin takip numarası|
|TrackingUrl|string|https://sube.sendeo.com.tr/takip?ccode=111111&musref=sendeo-aygaz-12345|Oluşturulan iş emri/gönderiye ait sendeo takip URL’i. İş emirleri gönderiye dönüştükten sonra takip URL’i aktif olmaktadır.|
|Barcode|string|Base64 barkod örneği döner|barcodeLabelType 1 ile atılan istek için dönen Base64 barkodu içerir.|
|BarcodeZpl|string|ZPL barkod örneği döner|barcodeLabelType 2 ile atılan istek için dönen ZPL Zebra barkodu içerir.|
|BarcodeNumbers|string|Gönderiye ait barkod numarası bilgisidir|Gönderiye ait barkod numaralarını içerir.|
|BarcodeZpls|string|ZPL detay array olarak döner|barcodeLabelType 3 ile atılan istek için dönen gönderiye ait ürünlerin birden fazla ZPL’ini içerir.|

<a name="_toc100827513"></a>*Şekil 5 SetDelivery Cevap Parametreleri (200 = Başarılı)*


### <a name="_toc101346610"></a>Hatalı Dönüş Parametreleri

|**Parametre**|**Tipi**|**Örnek Değer**|**Açıklama**|
| :- | :- | :- | :- |
|RequestId|string|f1d6d72c-643b-4a40-a142-d61b47f01187|Atılan istek için sistemdeki unique Id|
|ExceptionMessage|string|102|Atılan isteğin hatasıyla ilgili dönen mesaj|

<a name="_toc100827514"></a>*Şekil 6 SetDelivery Hatalı Dönüş Parametreleri*

|**ExceptionMessage**|**statusCode**|**Aksiyon**|
| :- | :-: | :- |
|Delivery Reference No Cannot be Null.|102|ReferenceNo bilgisi dolu olarak gönderilmelidir|
|Wrong Delivery Type|103|DeliveryType bilgisi dökümanda iletilenler dışında gönderilmemelidir|
|Products Cannot Be Null|104|Product Array boş gönderilmemelidir |
|Payment Type Is Not Correct.|411|PaymentType bilgisi dolu olarak gönderilmelidir|
|Collection Type Not Found|105|CollectionType bilgisi gönderilmelidir|
|Product Price Cannot Be Zero.|410|CollectionType sıfırdan farklı olduğu durumda productPrice sıfırdan farklı gönderilmelidir|
|Receiver Cannot Be Null|201|Alıcı adı bilgisi dolu olarak gönderilmelidir|
|Please Enter Receiver Phone or GSM Number|207|Alıcıya ilişkin telefon ya da GSM bilgisi dolu olarak gönderilmelidir|
|Receiver Address Cannot Be Null|202|Alıcı adresi bilgisi dolu olarak gönderilmelidir|
|Receiver District Id Cannot Be Zero.|203|Alıcı ilçe kodu bilgisi dolu olarak gönderilmelidir|
|Receiver City Id Cannot Be Zero.|204|Alıcı il kodu bilgisi dolu olarak gönderilmelidir|
|Receiver City Id is Not Correct.|205|Alıcı il kodu bilgisi hatalı olarak gönderilmiştir|
|Receiver District Id is Not Correct.|206|Alıcı ilçe kodu hatalı olarak gönderilmiştir|
|Sender Cannot Be Null.|301|deliveryType bilgisine göre gönderen bilgisi dolu olarak gönderilmelidir|
|Please Enter Sender Phone or GSM Number|307|deliveryType bilgisine göre gönderen telefon ya da GSM bilgisi dolu olarak gönderilmelidir|
|Sender Address Cannot Be Null.|302|deliveryType bilgisine göre gönderen adresi bilgisi dolu olarak gönderilmelidir|
|Sender District Id Cannot Be Zero.|303|deliveryType bilgisine göre gönderen ilçe bilgisi dolu olarak gönderilmelidir|
|Sender City Id Cannot Be Zero.|304|deliveryType bilgisine göre il kodu dolu olarak gönderilmelidir|
|Sender City Id is Not Correct.|305|deliveryType bilgisne göre gönderen il kodu bilgisi hatalı olarak gönderilmiştir|
|Sender District Id is Not Correct.|306|deliveryType bilgisne göre gönderen ilçe kodu bilgisi hatalı olarak gönderilmiştir|

<a name="_toc100827515"></a>*Şekil 7 SetDelivery Exception Message*
## <a name="_toc101346611"></a>CANCELDELIVERY
Takip Numarası (trackingNumber) veya müşteriler tarafından girilen Referans Numarası (referenceNo) alanları ile gönderi iptal edilebilmektedir. Sendeo tarafından teslim alınmayan ürünler için iptal işlemi yapılabilmektedir. Gönderi teslim alınmış ise iptal işlemi **gerçekleşmez**. (101 statüsünde olduğu durumda cancel işlemi yapılabilir)

Post metodu ile çalışır.
### <a name="_toc101346612"></a>İstek Parametreleri
trackingNumber veya referenceNo parametrelerini URL üzerinden query string olarak alır.
### <a name="_toc101346613"></a>Cevap Parametreleri (200 = Başarılı)
İptal etme işlemi başarılı gerçekleştiği takdirde response’da IsSuccess = true olarak dönüş sağlar.

### <a name="_toc101346614"></a>Hatalı Dönüş Parametreleri

|**ExceptionMessage**|**statusCode**|**Aksiyon**|
| :- | :-: | :-: |
|Please Enter Tracking Number or Reference Number.|701|İptal işlemi için mutlaka trackingNumber ya da referenceNumber bilgisi gönderilmelidir|
|No Delivery Found.|702|İptal isteği iletilen iş emri sistemde bulunamamıştır. |
|You Cannot Cancel , Delivery Has Already Sent.|703|Toplama işlemi yapldığı için iptal işlemi yapılamamaktadır|

<a name="_toc100827516"></a>*Şekil 8 CancelDelivery Hatalı Dönüş Parametreleri*

## <a name="_toc101346615"></a>TRACKDELIVERY
Gönderiye ait bilgileri döndürür. Müşterinin elindeki trackingNo veya müşteri tarafından girilen referenceNo alanları ile gönderi takip edilebilir. 30 dakika içerisindeki aynı sorgulamalarda cache üzerinden sonuç döndürmektedir. Dolayısıyla TRACKDELIVERY sorgulamasını 30 dakika da bir olacak şekilde ayarlanması gerekmektedir.

Get metodu ile çalışır.
### <a name="_toc101346616"></a>İstek Parametreleri
trackingNumber veya referenceNo parametrelerini URL üzerinden query string olarak alır.


### <a name="_toc101346617"></a>Cevap Parametreleri (200 = Başarılı)


|**Parametre**|**Tipi**|**Örnek Değer**|**Açıklama**|
| :- | :- | :- | :- |
|TrackingNo|integer|912345678|Oluşturulan iş emri/gönderinin takip numarası|
|ReferenceNo|string|sendeo-aygaz-12345|Oluşturulan iş emri/gönderiye ait müşteri tarafında belirlenen referans numarası|
|SendDate|string|02/02/2022 16:55:03|Oluşturulan iş emri/gönderinin gönderilme tarihi|
|Receiver|string|Ali Sendeo|Alıcı bilgisi|
|CargoAmount|double|10\.03|Gönderiye ait fiyatlandırma bilgisi (KDV dahil)|
|Sender|string|Ali Sendeo|Gönderici bilgisi|
|State|integer|105|Gönderinin durumunu belirten statü için unique Id|
|StateText|string|Hat Aracına Yüklendi|Gönderinin durumunu belirten statü için bilgilendirme|
|UpdateDate|string|04/02/2022 10:00:27|Gönderide gerçekleşen son statü değişimi için güncellenme tarihi|
|DeliveryDescription|string|TM Hat Yükleme|Gönderi için gerçekleşen süreçle ilgili bilgilendirme|
|DealerId|integer|851|Gönderi için Sendeo alıcı bayisinin unique Id bilgisi|
|DeciWeight|integer|20|Gönderinin desi/kg|
|Quantity|integer|1|Gönderideki paket adedi|
|TotalPrice|double|8\.50|Gönderi için belirlenmiş gönderi ücreti|
|departureBranchName|string|İLKADIM DM|Gönderi için gönderen Sendeo bayi adı|
|ArrivalBranchName|string|DÖRTYOL DN|Gönderi için varış Sendeo bayi adı|
|deliveryPlannedDate|string|2022-02-04T16:55:17.3590867+03:00|Planlanan teslim tarihi|

<a name="_toc100827517"></a>*Şekil 9 TrackDelivery Cevap Parametreleri (200 = Başarılı)*



|products array|||||
| :-: | :- | :- | :- | :- |
|Count|integer|2|Gönderideki paket adedi||
|ProductCode|string|kitapSendeo|Stoklu gönderiler için ürün kodu||
|Description|string|3 adet kitap|Stoklu gönderiler için ürün tanımı||
|Price|double|8\.50|Gönderi paket fiyatı||
|StockCount|||||
|MinStockCount|||||

<a name="_toc100827518"></a>*Şekil 10 TrackDelivery products.array*



|statusHistories array|||||
| :-: | :- | :- | :- | :- |
|StatusDate|integer|2|Gönderi için gerçekleşen hareketlerin gerçekleşme tarihi bilgisi||
|StatusId|string|106|Gönderi için gerçekleşen statü değişiminin unique Id bilgisi||
|Status|string|TM Hat İndirme|Gönderi için gerçekleşen statü değişiminin adı||
|Description|string|TM Hat İndirme|Gönderi için gerçekleşen statü değişiminin detayı||

### <a name="_toc101346618"></a>Hatalı Dönüş Parametreleri
##
## <a name="_toc101346619"></a>CARGOMEASUREMENTUPDATE
SETDELIVERY metodu ile daha önce oluşturulmuş gönderinin ölçüm değerlerinin güncellenmesi için kullanılan servistir. Gönderiye ait bilgileri döndürür. Müşterinin elindeki trackingNo veya müşteri tarafından girilen referenceNo alanları ile gönderi takip edilebilir.

Post metodu ile çalışır.



### <a name="_toc101346620"></a>İstek Parametreleri


|**Parametre**|**Tipi**|**Zorunluluk**|**Örnek Değer**|**Açıklama**|
| :- | :- | :- | :- | :- |
|customerReferenceNo|string|Zorunlu|1|Yukarıda belirtilen Type 1, 2, 3, 4, 5, 6 seçeneklerini içerir. Gönderinin nereden alınıp nereye gönderileceğini veya hangi noktadan alınıp verileceğini belirtir.|



|measurements array|||||
| :-: | :- | :- | :- | :- |
|quantity|integer|Zorunlu|2|Gönderideki paket adedinin güncellenmesini sağlar|
|Width|integer|Zorunlu|15|0 gönderilebilir|
|Length|integer|Zorunlu|10|0 gönderilebilir|
|Height|İnteger|Zorunlu|20|0 gönderilebilir|
|Deci|double|Zorunlu|2\.0||
|weight|double|Zorunlu|1\.0|0\.0 gönderilebilir|

### <a name="_toc101346621"></a>Cevap Parametreleri (200 = Başarılı)
Ölçüm güncelleme işlemi başarılı gerçekleştiği takdirde response’da IsSuccess = true olarak dönüş sağlar.
### <a name="_toc101346622"></a>Hatalı Dönüş Parametreleri


## <a name="_toc101346623"></a>GETBARCODEBYTRACKINGNUMBER
SETDELIVERY metodu ile daha önce oluşturulmuş gönderinin barkodunu takip numarasını kullanarak almayı sağlayan servistir.

Post metodu ile çalışır.

### <a name="_toc101346624"></a>İstek Parametreleri


|**Parametre**|**Tipi**|**Zorunluluk**|**Örnek Değer**|**Açıklama**|
| :- | :- | :- | :- | :- |
|trackingNumber|integer|Zorunlu|912345678|Barkodu alınmak istenen gönderinin takip numarası|
###

### <a name="_toc101346625"></a>Cevap Parametreleri (200 = Başarılı)


|**Parametre**|**Tipi**|**Örnek Değer**|**Açıklama**|
| :- | :- | :- | :- |
|barcode|string||Gönderinin barkodunu içerir.|

### <a name="_toc101346626"></a>Hatalı Dönüş Parametreleri
## <a name="_toc101346627"></a>GETBARCODE
SETDELIVERY metodu ile daha önce oluşturulmuş gönderinin barkodunu barkod tipi ve referans numarası kullanarak almayı sağlayan servistir.

Post metodu ile çalışır.

### <a name="_toc101346628"></a>İstek Parametreleri


|**Parametre**|**Tipi**|**Zorunluluk**|**Örnek Değer**|**Açıklama**|
| :- | :- | :- | :- | :- |
|barcodeLabelType|integer|Zorunlu|1|Alınmak istenen barkod tipini belirtir.|
|referenceNo|integer|Zorunlu|8880000793512692|Gönderi referans numarasıdır.|
###

### <a name="_toc101346629"></a>Cevap Parametreleri (200 = Başarılı)


|**Parametre**|**Tipi**|**Örnek Değer**|**Açıklama**|
| :- | :- | :- | :- |
|TrackingNumber|string|912345678|Oluşturulan iş emri/gönderinin takip numarası|
|ShipmentId|int|122425|Gönderi idsi.|
|TrackingUrl|string|https://sube.sendeo.com.tr/takip?ccode=111111&musref=sendeo-aygaz-12345|Oluşturulan iş emri/gönderiye ait sendeo takip URL’i. İş emirleri gönderiye dönüştükten sonra takip URL’i aktif olmaktadır.|
|Barcode|string|Base64 barkod örneği döner|barcodeLabelType 1 ile atılan istek için dönen Base64 barkodu içerir.|
|BarcodeZpl|string|ZPL barkod örneği döner|barcodeLabelType 2 ile atılan istek için dönen ZPL Zebra barkodu içerir.|
|BarcodeNumbers|string|Gönderiye ait barkod numarası bilgisidir|Gönderiye ait barkod numaralarını içerir.|
|BarcodeZpls|string|ZPL detay array olarak döner|barcodeLabelType 3 ile atılan istek için dönen gönderiye ait ürünlerin birden fazla ZPL’ini içerir.|

### <a name="_toc101346630"></a>Hatalı Dönüş Parametreleri

|**exceptionMessage**|**statusCode**|**Aksiyon**|
| :- | :-: | :-: |
|Bad Request |**400**|Gönderilen request bilgisi kontrol edilmelidir|
|Unauthorized |**401**|<p>Token bilgisi kontrol edilmelidir.</p><p></p>|
|Internal Server Error|**500**|Server Hatası – Sendeo ile iletişime geçilmelidir.|
|Server Error|**5XX**|Server Hatası – Sendeo ile iletişime geçilmelidir.|




# <a name="_toc101346631"></a>Servislerde Kullanılacak Bilgiler

### <a name="_toc101346632"></a>Sendeo Statü Listesi

|**statusId**|**statusName**|**statusDescription**|
| :-: | :- | :- |
|101|Kargo Sevk Emri Alındı|İş Emri Alındı|
|102|Belge Düzenlendi|Gönderi Oluşturuldu|
|103|Şube TM Yükleme|Çıkış Şubesinden Hareket Etti|
|104|TM Şube İndirme|Teslimat Noktasında|
|105|TM Hat Yükleme|Hat Aracına Yüklendi|
|106|TM Hat İndirme|Hat Aracından İndi|
|107|TM Şube Yükleme|Transfer Merkezinden Şubeye Yüklendi|
|108|Şube TM İndirme|Transfer Merkezine İndi|
|109|Şube Dağıtım Yükleme|Dağıtıma Çıkarıldı|
|110|Şube Dağıtım İndirme|Şube Dağıtım İndirme|
|111|Teslim Edildi|Teslim Edildi|
|112|Alıcı Telefonu Yanlış|Alıcı Telefonu Yanlış|
|113|İade Talebi|İade Talebi|
|114|Alıcı Adresinde Yok|Alıcı Adresinde Yok|
|115|Alıcı Adresi Yanlış|Alıcı Adresi Yanlış|
|117|Hasarlı Gönderi|Hasarlı Gönderi|
|118|Kayıp Kargo|Kayıp Kargo|
|119|Devir|Devir|
|120|Eksik Teslim Edildi|Eksik Teslim Edildi|
|121|Dağıtım Alanı Dışında|Dağıtım Alanı Dışında|
|122|Ödeme Tipi Kabul Edilmedi|Ödeme Tipi Kabul Edilmedi|
|123|Randevulu Teslimat|Randevulu Teslimat|
|124|Mobil Dağıtım Bölgesi|Mobil Dağıtım Bölgesi|
|125|Eksik Kargo|Eksik Kargo|
|126|Yönlendirme|Yönlendirme|
|127|Hat Aracı Gecikmesi|Hat Aracı Gecikmesi|
|128|Olumsuz Hava Koşulları|Olumsuz Hava Koşulları|
|129|Taşıma Fiyatı Yüksek Bulundu|Taşıma Fiyatı Yüksek Bulundu|
|130|Teslim Edilemedi|Teslim edilemedi|
|131|İade Gönderi|İade Edilen Gönderi|
|132|Ölçüm Tartım|Ölçüm Tartım yapıldı|
|133|İptal Gönderi|İptal Gönderi|
|134|İade Onay|İade Talebine Onay Verildi|
|135|İş Emri İadesi|İş Emri ile İade Edilen Gönderi|
|136|İade Red|Müşteri tarafından red edildi|
|137|Randevulu Alım|Müşteri Randevu Verdi|
|138|Gönderi Alındı|Gönderi Alındı|
|139|İptal İş Emri|İptal İş Emri|
|140|Kurye Teslimatta|Kurye Teslimatta|
|141|Kurye Zimmete Aldı|Kurye zimmete alma|
|142|Kurye Zimmetten Çıkardı|Kurye zimmetten çıkarma|
|143|Kayıp Kargo|Kayıp Kargo İş Emri|
|151|İade Olarak Teslim|İade Olarak Teslim|


### <a name="_toc101346633"></a>Sendeo İl ve İlçe Listesi

İl ve ilçelere ilişkin listeye ekteki excel ile ulaşabilirsiniz.

[İl-İçe Listesi](il-ilce.xlsx)

DeliveryType 1 ,2 ve 3 Örnekleri

\*\*Müşteri ihtiyacına göre alanlar farklılık gösterecektir. Örnek olması açısından paylaşılmıştır.


### <a name="_toc101346634"></a>Delivery Type Request Örnekleri : 

#### <a href="Deliverytype 1 örnek request bilgisi.txt" >Delivery Type 1</a>
#### <a href="Deliverytype 2 örnek request bilgisi.txt" >Delivery Type 2</a>
#### <a href="Deliverytype 3 örnek request bilgisi.txt" >Delivery Type 3</a>
#### <a href="./deliveryType6 Örnek Request.docx" >Delivery Type 6</a>
#### <a href="./deliveryType6 stn iade.docx" >Delivery Type 6 STN iade</a>


### <a name="_toc101346635"></a> Kod Örnekleri : 

#### <a href="https://github.com/SendeoTeknoloji/Sendeo.Client.CSharp" >C# Örnek Proje</a> 

#### <a href="https://github.com/SendeoTeknoloji/Sendeo.Client.PHP" >PHP Örnek Proje</a>

 
