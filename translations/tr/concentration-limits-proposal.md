# Düğüm Yoğunlaşma Sınırları - Ağ Hayatta Kalabilirliğinin Uygulanması
## EXIOM Tokenomik Teknik Dökümanına Ek
### 07/26/2026

> **Kapsam notu (19 Ekim 2026 tarihinde güncellendi).** Uygulanan birim *yakınlık kümesidir* (Lokinet yönlendirme yakınlığı, çalışma süresi kanıtı zamanlaması ve ASN aracılığıyla tespit edilen, fiziksel veya yönlendirme altyapısını paylaşan bir düğüm grubu), **ülke değil** ve bir sağlayıcının kayıt ülkesi değil. Gerçekten bağımsız birkaç tesise sahip bir ülke veya sağlayıcı, büyük bir payı elinde tutan tek bir tesisten daha az risklidir. Aşağıdaki yoğunlaşma verileri, barındırma sağlayıcısına göre gruplandırılmış, Lokinet öncesinde mevcut en iyi vekil olan 19 Ekim 2026 tarihli bir anlık görüntüdür (893 aktif düğüm). Lokinet, HF23'ten önce uygulama yapmayan bir sürümde yayınlanır ve HF23 uygulamayı devreye alır.

Bu belge, EXIOM Tokenomik Teknik Dökümanına bir ek niteliğindedir ve onun okunmuş olduğunu varsayar. Teknik döküman, yoğunlaşma kontrollerinin ne olduğunu ve neden var olduklarını kapsar. Bu belge, her kontrolün nasıl çalıştığının mekanik ayrıntısını, HF22'nin arkasındaki testnet doğrulama verilerini, sıfır-ödül değiştiricisinin arkasındaki kesin ekonomik matematiği, bir gizlilik zincirindeki operatör kimliği sorununu ve protokolün tam olarak çözemediği artık riskleri kapsar.

---

## Mevcut Yoğunlaşma Verileri

19 Ekim 2026 tarihinde 893 aktif düğümde ölçülmüş, Lokinet öncesinde bugün mevcut olan yoğunlaşma sinyali olan barındırma sağlayıcısına (ASN) göre gruplandırılmıştır. Sağlayıcı, paylaşılan bir arıza etki alanı için ülke bayrağından çok daha iyi bir vekildir, çünkü bir şirketin ağı ve tesisleri birlikte arızalanma veya çevrimdışı olmaya zorlanma eğilimindedir.

| Sağlayıcı (ASN) | Aktif düğümler | Pay |
|---|---|---|
| NodeHub (AS214083) | 444 | 49.7% |
| Contabo (AS51167, ayrıca AS40021 ve Contabo Asia AS141995) | ~303 | ~34% |
| OVH (AS16276) | 62 | 6.9% |
| Oracle (AS31898) | 22 | 2.5% |
| WebNX (AS18450) | 12 | 1.3% |
| diğer tüm sağlayıcılar birleştirilmiş (12 ASN daha) | ~50 | ~5.6% |

Tek başına NodeHub, ağın %49.7'sini elinde tutuyor; bu, %30'luk hayatta kalabilirlik üst sınırının (893 aktif düğümde 267 düğüm) hayli üzerinde ve tek bir /24 alt ağı %41.2'sini elinde tutuyor. Bu tek sağlayıcı, HF23'ün kırmak için inşa edildiği yoğunlaşmadır.

Buraya nasıl geldi. Operatörler için XEQM düğümleri çalıştırmayı teklif eden bir barındırma hizmeti olan Pecunia, düğümlerinin çoğunu Contabo üzerine yerleştirdi. Pecunia'nın performansı kötü oldu ve o zamandan beri birçok operatör NodeHub'a geçti. Böylece baskın arıza etki alanı, hâlâ ağın yaklaşık üçte birini elinde tutan (çoğu Grand Est tesisi) Contabo'dan, şu anda ağdaki tek en büyük küme olan NodeHub'a kaydı.

Ülke rakamları hakkında bir not. Bir sağlayıcının kayıt ülkesi, sunucularının bulunduğu yer değildir. NodeHub ABD'de kayıtlı ve Contabo Almanya'da kayıtlı, bu nedenle ülkeye göre bir görünüm, fiziksel veri merkezi ne olursa olsun düğümlerini US ve DE olarak etiketler (Contabo'nun en büyük XEQM tesisi Fransa'nın Grand Est bölgesindedir). Protokol ne ülkeyi ne de sağlayıcı kaydını üst sınırla sınırlar. Yakınlık kümesini, yani gerçekten fiziksel veya yönlendirme altyapısını paylaşan düğüm kümesini sınırlar. ASN ve alt ağ, bugün bunun vekilidir ve HF23 onları, bir sağlayıcının içindeki farklı tesisleri de ayırabilen Lokinet yönlendirme yakınlığıyla değiştirir. Eşik, küme başına aktif düğümlerin %30'udur (mevcut 893'te 267) ve ağ büyüdükçe sürekli olarak yeniden hesaplanır.

---

## Bunun Düğüm Operatörleri İçin Anlamı

Bu bölüm soruyu doğrudan yanıtlar: HF23 düğümlerinizi nasıl çalıştırdığınızı nasıl etkiler?

**HF23 ülkeye göre sınırlama yapmaz ve IP başına bir düğüm, VPS başına bir düğüm veya cüzdan başına bir düğüm gerektirmez.** Üst sınır, *yakınlık kümesi* başına aktif ağın %30'udur (fiziksel veya yönlendirme altyapısını paylaşan düğümler). Paylaşılan altyapı üzerinde 10, 50 ve hatta 100 düğüm çalıştıran bir operatör, kümesi bu eşiğin altında kaldığı sürece HF23'ten tamamen etkilenmez. Tek bir makinede, tek bir VPS hesabında ve tek bir cüzdanda birden fazla düğüm çalıştırabilirsiniz. HF23'teki hiçbir şey bunu değiştirmez.

**Sıfır-ödül değiştiricisi yalnızca küme başına üst sınırın (aktif düğümlerin %30'u) üzerindeki düğümlere uygulanır.** Bir kümedeki en eski kayıtlı düğümler, o eşiğe kadar tam ödül kazanır. Yalnızca aşırı yoğunlaşmış bir kümede bunun üzerinde sıralanan düğümler sıfır kazanır ve yalnızca daha az yoğunlaşmış bir kümeye taşınana kadar.

**Çekirdek (quorum) tekilleştirmesi, düğüm sayısını veya geliri değil, tur başına konsensüs etkisini sınırlar.** Tek bir VPS üzerinde 50 düğüm çalıştıran bir operatör, 50 düğümün hepsinden blok ödülü kazanır ve altyapısını tam olarak bugün yaptığı gibi yönetir. Potansiyel olarak çok sayıda yerine, tur başına küme başına bir çekirdek koltuğu alırlar; bu, amaçlanan sonuçtur.

**Yeni bir operatör için doğru yaklaşım**, düğüm gezginini kontrol etmek, mevcut kümelerin nerede yoğunlaştığını görmek ve az nüfuslu bir kümeye yerleştirmektir. Kendi farklı yönlendirmesine sahip tek bir sunucuda on düğüm, HF23 altında mükemmel şekilde çalışır çünkü o küme %30 eşiğinin yakınında bile değildir. Tam ödüller, tam çekirdek katılımı, sorun yok.

**Seyrek bölgelere yerleşirseniz dinamik lehinize çalışır.** Bir bölge sonunda dolarsa, düğüm gezgini bunu gösterir ve operatörlerin üst sınır kendilerini etkilemeden önce taşınmaları için finansal bir teşvikleri olur. Oraya ilk ulaşan operatörler, eşiğe kadar en eski düğümlerinde tam ödülleri korur. Aşırı yoğunlaşmış bir kümeye yapılan yeni kayıtlar hemen hiçbir şey kazanmaz, bu nedenle ekonomi doğal olarak yeni yerleşimleri daha az yoğun bölgelere doğru iter.

**HF23'ün çözdüğü özel sorun**, şu anda ağın yaklaşık yarısını barındıran (444 düğüm, %49.7) tek bir sağlayıcı olan NodeHub'dır; ikinci sırada kabaca üçte biriyle Contabo yer alır. NodeHub'ın altyapısı çevrimdışı olursa veya kapatılması emredilirse, ağ durur. Amaç, herhangi bir kümeyi %30 üst sınırının altına indirmektir. Farklı, yoğunlaşmamış bir sağlayıcı veya tesis üzerinde sorumlu bir çoklu düğüm kurulumu çalıştıran her operatör, ağın tam olarak daha fazlasına ihtiyaç duyduğu şeydir.

---

## Hard Fork'lar Neden Ayrılmıştır

HF22, başarılı testten sonra yayınlanır. Cüzdan-anahtarı çekirdek tekilleştirmesi ve bağ çözme (unbonding) süresi birleştirmesinin Lokinet'e bağımlılığı yoktur. Her ikisi de testnet üzerinde doğrulanmıştır ve Lokinet değerlendirmesi beklerken onları tutmak haksız bir gecikmedir. HF22 yayınlanmadan önce teknik dökümanı okuyan sofistike bir aktör, çekirdek kontrolünü önlemek için cüzdan bölmeyi deneyebilir, ancak bunu yapmak çalışma süresi kanıtı zamanlama korelasyonu ve IP/ASN analizi yoluyla tespit edilebilir ve yönetişim eylemi için belgelenmiş bir kayıt oluşturur.

Lokinet önce kendi uygulama yapmayan sürümünde yayınlanır (SQLite hafif düğüm depolama değişikliğiyle birlikte), bu nedenle yeni taşıma, tanıtıldığı anda konsensüs açısından kritik hale getirilmez. O sürüm sırasında yakınlık kümeleme, hiçbir ödül sonucu olmadan canlı ve gözlemlenebilir şekilde çalışır; işte bu, gerçek küme sayısının ölçüldüğü ve HF23 eşiği ile yedeğin ayarlandığı zamandır. Ardından HF23 gelir ve uygulamayı devreye alır. Sürümleri ayırmak ayrıca temiz arıza etki alanları sağlar: HF23 etkinleştirmesinden sonra bir şeyler ters giderse, izole edilecek daha az değişken olur. HF23 uygulaması canlı olana kadar, Grand Est, HF22 çekirdek tekilleştirmesinin ötesinde tam hayatta kalabilirlik riskine maruz kalmaya devam eder.

---

## HF22 Mekanikleri

### Cüzdan-Anahtarı Çekirdek Tekilleştirmesi

Çekirdek seçim algoritması, kesinleştirmeden önce her aday kümesi üzerinde bir tekilleştirme geçişi çalıştırır. Çekiliş bir aday düğüm seçtiğinde, algoritma onun operatör cüzdan adresini tur için zaten seçilmiş tüm düğümlerle karşılaştırır. Bir eşleşme bulunursa, aday, zaten temsil edilen tüm adresler hariç tutularak, kalan uygun havuzdan yeniden çekiliş yapılarak değiştirilir.

Değiştirme çekilişi, önceden reddedilmiş adaylar arasında geri dönmez. İlk çekilişte kullanılan aynı olasılık-ağırlıklı sırada, kalan seçilmemiş havuzdan çeker. Bu, kalan düğümlerin herhangi bir belirli kümesine yönelik deterministik bir önyargı getirmeden çekirdek seçiminin istatistiksel özelliklerini korur.

**Testnet doğrulama sonuçları:**
- 20 durma/kurtarma döngüsü tamamlandı (20/20)
- Tüm döngülerde %100 kurtarma oranı
- Hiçbir döngüde manuel müdahale gerekmedi (en kötü blok boşluğu 83 saniye)
- Mainnet HF22-öncesi referansı: 1,000 blok, %100 Pulse, sıfır GOV_SIGNED blok
- R0 zaman aşımı analizi: üretim koşullarında hiçbir R0 zaman aşımı getirilmedi. Mevcut mainnet'in yoğunluk analizi, her yüksek yoğunluklu IP kümesinin tek bir operatör olduğunu doğrulamaktadır; bu da cüzdan-anahtarı tekilleştirmesinin mevcut balina yerleşimlerine karşı zaten tam koruma sağladığı anlamına gelir. En büyük iki tek-IP yerleşimi (sırasıyla 58 düğüm ve 51 düğüm) her biri tek bir operatördür ve HF22 altında tur başına bir çekirdek koltuğuyla sınırlıdır.

**Bir çekirdek koltuğunun pratikte anlamı:** Çekirdek büyüklüğü ve rotasyon sıklığı, bir düğümün ne sıklıkla katıldığını belirler. Mevcut ağ büyüklüğünde, tek-koltuk üst sınırı, yoğunlaşmış bir operatörün oracle oturumlarındaki, Pulse turlarındaki ve yükümlülük çekirdeklerindeki etkisinin tek düğümlü bir operatörünkiyle aynı olduğu anlamına gelir. Blok ödülü gelirleri değişmez.

**Cüzdan-bölme açığı ve ara dönem tespiti:** 426 düğümü 10 cüzdana bölen bir operatör, tur başına bir yerine 10 çekirdek koltuğuna kadar alır. Bu, HF23'ün kapattığı bilinen açıktır. Ara dönemde, cüzdan bölme, daemon değişiklikleri olmadan zaten mevcut olan iki sinyal yoluyla tespit edilebilir. İlk olarak, çalışma süresi kanıtı zamanlaması: aynı fiziksel ana makinede veya hiperviziörde bulunan düğümler, cüzdan anahtarından bağımsız olarak kanıtlarını birbirlerinden milisaniyeler içinde gönderir. Farklı cüzdanlara kayıtlı düğümlerden 10ms-altı pencerelerde gelen bir kanıt kümesi, paylaşılan altyapının güçlü bir sinyalidir. İkinci olarak, IP ve ASN korelasyonu: bir IP, alt ağ veya ASN'yi paylaşan farklı cüzdanlardaki düğümler kaydedilir ve yönetişim incelemesi için işaretlenir. Cüzdan-bölen ancak tüm düğümlerini aynı Contabo tesisinde tutan bir operatör, her iki sinyal yoluyla tanımlanabilir ve kara liste politikası altında yönetişim eylemine tabidir.

### Bağ Çözme (Unbonding) Süresi Birleştirmesi

Zorunlu kayıt silme bağ çözme süresi, 10,080 bloktan (yaklaşık 7 gün) 20,160 bloğa (yaklaşık 14 gün) değişir ve gönüllü çekilme süresiyle eşleşir. Bu bir konsensüs sabiti değişikliğidir.

Orijinal 7 günlük zorunlu süre, kontrolleri dışındaki altyapı olaylarını yaşayan operatörler üzerindeki cezayı sınırlamak için ağ stabilizasyonu sırasında bilinçli bir seçimdi. Bu gerekçe artık geçerli değil. Ağ istikrarlı, hizmet dışı bırakma kredisi sistemi kısa kesintiler için tampon sağlıyor ve birleştirilmiş 14 günlük bir süre, kalan hiçbir gerekçesi olmayan bir asimetriyi kaldırıyor.

XEQM coinleri, kayıt işlemi aracılığıyla bağ çözme süresi boyunca zincir üzerinde kilitlenir. Bir protokol değişikliği olmadan kilidi erkenden serbest bırakacak hiçbir mekanizma yoktur. Belgelenmiş altyapı arızaları için, yönetişim kaçırılan ödülleri yönetişim cüzdanından bir XEQM transferi olarak telafi edebilir, ancak zincir üzerindeki kilit ne olursa olsun tam süresini çalıştırır.

---

## HF23 Mekanikleri

### Lokinet Yakınlık Kümeleme

Lokinet (Low Latency Anonymous Routing Protocol, LLARP), trafiği hizmet düğümü ağı üzerinden 3. katmanda yönlendirir ve TCP, UDP ve ICMP'yi destekler. Her hizmet düğümü bir röle olarak katılır. Ortaya çıkan yönlendirme grafiği, fiziksel ağ topolojisini yansıtır: aynı tesisteki düğümler aynı yukarı akış anahtarı ve aynı veri merkezi omurgası üzerinden yönlendirir, bu da ilişkili yol seçimleri ve milisaniye-altı düğümler arası gecikme üretir. Farklı tesislerdeki düğümler, ölçülebilir şekilde daha yüksek gecikmeyle farklı yollar üzerinden yönlendirir.

Kümeleme algoritması, tüm aktif düğümler arasında ikili Lokinet yönlendirme gecikmesi ve yol örtüşme ölçümlerini alır ve bu ölçümleri yakınlık sinyali olarak kullanarak onları kümelere gruplar. Bir küme sabit bir coğrafi bölge değildir; yönlendirme davranışı paylaşılan fiziksel altyapıyı gösteren düğümlerin dinamik bir gruplamasıdır. Farklı ülkelerdeki farklı Contabo tesislerindeki iki düğüm, yol örtüşmeleri yeterince yüksekse, aynı kümede görünecek kadar yeterince paylaşılan Contabo omurga altyapısı üzerinden yönlendirebilir. Aynı veri merkezindeki ancak farklı yukarı akış bağlantılarına sahip farklı fiziksel makinelerdeki iki düğüm, yol örtüşmeleri düşükse farklı kümelerde görünür.

Lokinet yakınlığının yanında kullanılan tamamlayıcı sinyaller:

**Çalışma süresi kanıtı zamanlama korelasyonu.** Ağ, tüm aktif düğümlerden düzenli bir programda zaten çalışma süresi kanıtları alır. Her düğümden gelen kanıt varışlarının zaman damgası dağılımı, alıcı düğümler tarafından kaydedilir. Aynı fiziksel ana makinede veya VM hiperviziöründe bulunan düğümler, kanıtlarını tipik olarak 10 milisaniyenin altında, karakteristik olarak dar bir pencere içinde gönderir. Bu varış zamanlaması dağılımını kümelemek, hiçbir daemon değişikliği gerektirmeyen ve Lokinet aktif olmadan önce çalışan bir fiziksel birlikte-konumlandırma sinyali sağlar.

**ASN analizi.** Her düğümün IP adresi, genel BGP verileri aracılığıyla bir Otonom Sistem Numarasına (ASN) eşlenir. Bir ASN'yi paylaşan düğümler, sağlayıcı düzeyinde yönlendirme altyapısını ve sağlayıcı düzeyinde yasal maruziyeti paylaşır. Tüm altyapısını etkileyen bir yargı yetkisi düzeyinde emir alan bir sağlayıcı, kaç Lokinet kümesinde görünürlerse görünsünler, tüm ASN düğümlerini aynı anda kapatır. ASN yoğunlaşması tamamlayıcı bir sinyal olarak izlenir ve küme eşiğine yakın operatörlerin yönetişim incelemesine katkıda bulunur.

### Küme Kayıt Üst Sınırı

Kayıt zamanında, protokol mevcut tüm kümelere karşı bir yakınlık değerlendirmesi çalıştırır. Kaydolan düğümün Lokinet yönlendirme özellikleri, mevcut her kümenin merkez noktasına (centroid) karşı ölçülür. En yakın küme zaten aktif düğümlerin %30'unu veya daha fazlasını içeriyorsa, kayıt, küme kapasitesini ve en yakın kümenin düğüm sayısını gösteren belirli bir hata koduyla reddedilir.

Red deterministiktir: aşırı yoğunlaşmış bir kümeye atanacak kadar benzer şekilde yönlendiren herhangi bir düğüm, operatörün cüzdan anahtarından, kayıt geçmişinden veya stake miktarından bağımsız olarak reddedilir. Operatör, reddi yönetişim yoluyla temyiz edemez. İlerlemenin tek yolu, farklı bir kümeye yönlendiren altyapıya kaydolmaktır.

Eşik, kayıt zamanındaki aktif düğüm sayısına karşı değerlendirilir. Ağ büyüdükçe, mutlak terimlerle %30 eşiği de onunla birlikte büyür. Bugün üst sınırda olan bir operatör, ağ büyüdükçe ve mutlak üst sınır yükseldikçe, mevcut hiçbir düğümü taşımadan önceden sınırlanmış bir kümede ek düğümler kaydedebilir.

### Sıfır-Ödül Değiştiricisi

Sıfır-ödül değiştiricisi, blok ödülü hesaplama zamanında uygulanır. Seçili bir düğüm için ödül hesaplaması bir küme uygunluk kontrolü içerir. Düğümün kümesi üst sınır eşiğinden daha fazla düğüm içeriyorsa ve düğümün o küme içindeki kayıt sıralaması eşiğin üzerindeyse (en eskiden en yeniye sıralanmış), ödül hesaplaması sıfır döndürür.

Sıralama, düğümün küme atamasındaki kayıt blok yüksekliğinden hesaplanır. Kümedeki en eski kayıtlı düğüm 1. sırayı alır, en son kaydedilen N. sırayı alır. Üst sınır eşiğinden büyük sıralamaya sahip düğümler sıfır kazanır. Üst sınır eşiğinde veya altında sıralamaya sahip düğümler tam standart ödülü kazanır. Sıralama, küme ataması her değiştiğinde yeniden hesaplanır; bu, düğümler kümeden çıktığında, yeni düğümler katıldığında veya ağ topolojisi değişiklikleri nedeniyle küme sınırı kaydığında gerçekleşir.

**Grand Est için ekonomik matematik:** 208 düğümlük bir üst sınırla 426 düğümde, 218 düğüm sıfır blok ödülü kazanır. Düğüm başına aylık $0.53'lük kendi kendine barındırma fiyatlandırmasında, bu 218 düğüm sıfır gelirle aylık $115.54 maliyet oluşturur. Düğüm başına aylık $1.76'lık Pecunia fiyatlandırmasında maliyet aylık $383.68'dir. Operatörün iki rasyonel yanıtı vardır: fazla düğümleri yoğunlaşmamış kümelere taşımak, yeni kayıt kabul edilir edilmez ödüllerini anında geri yüklemek veya fazla düğümlerin kaydını silmek ve stake edilmiş XEQM'yi bağ çözme süreci yoluyla geri almak. Her iki yanıt da yoğunlaşmayı azaltır. Fazla düğümleri sıfır ödülde tutmanın rasyonel bir temeli yoktur.

**Erteleme süresi (grace period) mekanikleri:** HF23 etkinleştirme bloğunda, protokol tüm aktif kümelerin ve düğüm sayılarının bir anlık görüntüsünü alır. %30 eşiğini aşan herhangi bir küme aşırı yoğunlaşmış olarak işaretlenir. Etkinleştirme bloğunu takip eden 30 gün boyunca, üst sınır eşiğinin üzerindekiler de dahil olmak üzere tüm düğümler için sıfır-ödül değiştiricisi askıya alınır. Erteleme süresi boyunca, düğüm sahipleri düğüm gezgininin küme atamalarını gözlemleyebilir, taşımaları planlayabilir ve bunları yürütmeye başlayabilir. Erteleme süresi sona erme bloğunda, değiştirici etkinleşir. O bloğa kadar aşırı yoğunlaşmış kümeden çıkmış olan düğümler, o bloktan itibaren tam ödül kazanır. Hâlâ eşiğin üzerinde olan düğümler, taşınana kadar o bloktan itibaren sıfır kazanır.

### Yakınlık Kümesi Çekirdek Tekilleştirmesi

HF23 çekirdek tekilleştirme yükseltmesi, cüzdan adresi kontrolünü bir küme üyelik kontrolüyle değiştirir. Çekiliş bir aday düğüm seçtiğinde, algoritma onun küme atamasını tur için zaten seçilmiş tüm düğümlerle karşılaştırır. İki düğüm bir küme atamasını paylaşıyorsa, ikincisi, zaten temsil edilen tüm kümeler hariç tutularak kalan havuzdan bir çekilişle değiştirilir.

Cüzdan-bölen bir operatör üzerindeki pratik etki: aynı Contabo tesisindeki 426 düğüm boyunca 10 cüzdan adresinin tümü aynı yakınlık kümesinde görünür. Küme kontrolü hepsini tek bir birim olarak yakalar. O kümeden bir düğüm bir koltuk tutar. O kümeden diğer 425 düğüm, kaç farklı cüzdan adresi altında kayıtlı olurlarsa olsunlar, tutmaz.

### Minimum Küme Sayısı Gereksinimi ve Yedek Kural

EXIOM ağ çekirdek büyüklüğü tur başına 12 koltuktur. Bu nedenle yakınlık kümesi tekilleştirmesi, çekirdek oluşumunu garantilemek için aktif düğüm kümesinde en az 12 farklı yakınlık kümesi gerektirir. Ağ 12'den az farklı küme üretirse, algoritma küme başına bir koltuk kısıtlamasını karşılayamaz ve çekirdek oluşumu başarısız olur.

Lokinet yakınlık kümelemesi uygulandığında, mevcut ağ dağılımının 12 ile 18 arasında farklı küme üretmesi tahmin edilmektedir. Bu, 12 koltukluk minimuma rahatsız edici derecede yakındır. Nominal olarak ayrı tesisler arasındaki paylaşılan sağlayıcı omurga altyapısı, iki farklı IP konumunun Lokinet yönlendirme grafiğinde tek bir yakınlık kümesine birleşmesine neden olabilir. Küme sayısını 12'nin altına düşüren böyle herhangi bir birleşme, çekirdek oluşumunu tamamen bozar.

Bu nedenle algoritma zorunlu bir yedek kural uygular:

1. Algoritma, mevcut kümeleri rastgele sırada işleyerek, farklı küme başına bir düğümle 12 koltuğun tümünü doldurmaya çalışır.
2. 12 koltuk doldurulmadan önce tüm farklı kümeler tükenirse, algoritma bir yedek geçişe girer.
3. Yedek geçişte, en küçük kümelerden başlayarak her kümeden ikinci bir düğüme izin verir. En az yoğunlaşmış kümeler, en yoğunlaşmış olanlardan önce ikinci bir koltuk alır.
4. Algoritma, geçiş başına küme başına maksimum koltuğu birer birer artırarak, 12 koltuk doldurulana kadar yedek geçişlere devam eder.
5. Mevcut koşullar altında Grand Est gibi en yoğunlaşmış küme, yalnızca tüm küçük kümelere yedek tahsisleri verildikten sonra ek koltuklar alır.

Yedeği tetikleyen her tur, ona neden olan küme sayısıyla kaydedilir. Yönetişim, yedek sıklığını doğrudan bir yoğunlaşma risk göstergesi olarak izler. 12 veya daha fazla farklı kümeye sahip bir ağ, yedeği asla tetiklemez. Yedeği sürekli tetikleyen bir ağ, HF23 yoğunlaşma uygulamasının henüz yeterli fiziksel çeşitlilik sağlamadığını ve küme üst sınırının veya erteleme süresi uygulamasının yönetişim dikkatine ihtiyaç duyduğunu işaret ediyor demektir.

Yedek günlüğü, operatör topluluğunun yoğunlaşma riskini gerçek zamanlı olarak gözlemleyebilmesi için düğüm gezgininde küme atamalarının yanında yayınlanır.

---

## Bir Gizlilik Zincirinde Operatör Kimliği

Protokolün, küme üst sınırını ve sıfır-ödül değiştiricisini uygulamak için hangi insan operatörün hangi düğümlere sahip olduğunu tanımlaması gerekmez. Her iki kontrol de küme düzeyinde çalışır. Neyin belirlenebileceği ve neyin belirlenemeyeceği, yönetişim izlemesi için yararlı bir bağlamdır ancak protokol uygulaması için gerekli değildir.

**Zincir üzerindeki verilerden deterministik olan şey:** aynı operatör cüzdan anahtarı altında kayıtlı düğümler kesinlikle aynı operatördür. Bu, kayıt işlemindeki genel bilgidir.

**Lokinet ve zamanlama verilerinden yüksek güvenle çıkarılabilen şey:** kaç cüzdan anahtarı kullandıklarından bağımsız olarak, bir düğüm kümesinin altında yatan farklı fiziksel ana makinelerin sayısı. Her biri 85 düğüm çalıştıran, hepsi aynı iki fiziksel sunucuda olan beş cüzdan anahtarı, beş değil, iki farklı zamanlama imzası ve iki Lokinet yakınlık merkez noktası üretir.

**Bir gizlilik zincirinde belirlenemeyen şey:** farklı altyapıya sahip iki farklı cüzdan anahtarının aynı insan operatöre ait olup olmadığı. Her cüzdan anahtarının fonlama kaynağı tasarım gereği özeldir. Gizlilik zincirinin işlem katmanı aracılığıyla beş farklı kaynaktan fonlanan beş cüzdan kullanan sofistike bir operatör, protokol düzeyinde beş farklı kimlik sunar.

Hayatta kalabilirlik uygulaması için bu önemli değildir. Küme 426 düğüm içerir. En eski 208 düğüm ödül kazanır. En yeni 218 düğüm sıfır kazanır. Operatörün kimliği bu hesaplama için alakasızdır.

---

## Uygulama Durumu

| Kontrol | Durum |
|---|---|
| Operatör cüzdan-anahtarı çekirdek tekilleştirmesi | HF22, 219120 bloğunda etkinleştirildi |
| Bağ çözme süresi birleştirmesi, 7'den 14 güne | HF22, etkinleştirildi |
| Pulse durma-kurtarma (imza yedeği, snode_revision 1) | 236920 bloğunda, 18 Ekim 2026'da etkinleştirildi |
| Ağ taşıması olarak Lokinet etkinleştirmesi | Geliştirme aşamasında; HF23'ten önce uygulama yapmayan bir sürümde yayınlanır |
| SQLite hafif düğüm depolama | Geliştirme aşamasında; HF23-öncesi Lokinet sürümüyle yayınlanır |
| Yakınlık kümeleme algoritması | Tasarım aşaması, Lokinet değerlendirmesi bekleniyor |
| Küme kayıt üst sınırı, %30 eşik | HF23, tasarım aşaması |
| Fazla düğümler için sıfır-ödül değiştiricisi | HF23, tasarım aşaması |
| Erteleme süresi mekanizması | HF23, tasarım aşaması |
| Yedek kurallı yakınlık kümesi çekirdek tekilleştirmesi | HF23, tasarım aşaması |
| Minimum küme sayısı izleme ve yedek günlüğü | HF23, tasarım aşaması |
| Çalışma süresi kanıtı zamanlama korelasyonu araçları | Daemon değişikliği gerekmez, araçlar geliştirme aşamasında |
| ASN kümeleme eklentisi | Daemon değişikliği gerekmez, araçlar geliştirme aşamasında |

---

## Bu Kontrollerin Çözmediği Şeyler

**Sağlayıcı düzeyinde yasal yoğunlaşma.** Tüm küresel altyapısını etkileyen bir yargı yetkisi düzeyinde yasal emir alan bir sağlayıcı, bu düğümler birden fazla Lokinet yakınlık kümesinde görünse bile, tüm düğümlerini aynı anda kapatır. ASN analizi bu riski ortaya çıkarır ancak protokol, operatörün sağlayıcı kimliğini açıklamasını gerektirmeden sağlayıcı çeşitliliğini uygulayamaz. Küme üst sınırının doğal olarak ürettiği coğrafi yayılım, pratikte bu riski önemli ölçüde azaltır, çünkü kümeler arasında dağılmaya zorlanan operatörler pratikte birden fazla sağlayıcı kullanacaktır.

**Gizlilik-zinciri cüzdan bölmeleri arasında insan operatör kimliğinin belirlenmesi.** Yukarıda açıklandığı gibi, gizlilik zinciri aracılığıyla fonlanan birden fazla cüzdan kullanan sofistike bir operatör, protokol düzeyinde tanımlanamaz. Küme üst sınırı ve sıfır-ödül değiştiricisi, kimlikten bağımsız olarak arıza etki alanı riskini ele alır. Çekirdek tekilleştirmesi, HF23'te konsensüs etkisi açığını kapatır. Artık risk, sofistike bir operatörün birçok gerçekten farklı küme boyunca birçok düğüm çalıştırması, ağ sağlığına orantılı olarak katkıda bulunurken düğüm sayısıyla orantılı blok ödülü geliri biriktirmesidir. Bu kabul edilebilir bir sonuçtur: yoğunlaşmış konsensüs etkisi sınırlıdır; dağıtılmış sermaye katılımı ödüllendirilir.

Küme ataması, taşıma planlaması veya HF22/HF23 zaman çizelgesi hakkında soruları olan operatörlerin, Node Operators Telegram kanalında paylaşım yapmaları veya bu depoda bir issue açmaları teşvik edilir.

---

## Mevcut Diller

Bu belgenin topluluk çevirileri, teknik döküman deposunda tutulmaktadır. Bir çeviri ile İngilizce sürüm arasında herhangi bir çelişki olması durumunda, İngilizce sürüm geçerlidir.

| Dil | Belge |
|---|---|
| Español | [translations/es/concentration-limits-proposal.md](./translations/es/concentration-limits-proposal.md) |
| Français | [translations/fr/concentration-limits-proposal.md](./translations/fr/concentration-limits-proposal.md) |
| Deutsch | [translations/de/concentration-limits-proposal.md](./translations/de/concentration-limits-proposal.md) |
| 中文 | [translations/zh/concentration-limits-proposal.md](./translations/zh/concentration-limits-proposal.md) |
| Português | [translations/pt/concentration-limits-proposal.md](./translations/pt/concentration-limits-proposal.md) |
| Türkçe | [translations/tr/concentration-limits-proposal.md](./translations/tr/concentration-limits-proposal.md) |
| Polski | [translations/pl/concentration-limits-proposal.md](./translations/pl/concentration-limits-proposal.md) |
| Bahasa Indonesia | [translations/id/concentration-limits-proposal.md](./translations/id/concentration-limits-proposal.md) |

---

*Bu belge finansal veya hukuki tavsiye teşkil etmez. XEQM, EXIOM platformu için bir fayda coinidir, bir yatırım ürünü değildir. Token sınıflandırması, menkul kıymet durumu ve geçerli düzenlemeler yargı yetkisine göre değişir. Katılımcılar, XEQM edinmeden veya onunla işlem yapmadan önce yerel hukuki ve düzenleyici çerçevelerine danışmalıdır. XEQM Labs, spekülatif fiyat artışı temelinde XEQM satın almayı teşvik etmez.*
