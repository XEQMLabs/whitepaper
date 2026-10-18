# Düğüm Yoğunlaşma Limitleri - Ağ Hayatta Kalabilirliği Zorunlu Kılması
## EXIOM Tokenomi Teknik Dokümanı'na Teknik Ek
### 07/26/2026

> **Kapsam notu (Ekim 2026'da güncellendi).** Zorunlu kılınan birim, *yakınlık kümesidir* (fiziksel veya yönlendirme altyapısını paylaşan, Lokinet yönlendirme yakınlığı, çalışma-süresi kanıtı zamanlaması ve ASN aracılığıyla tespit edilen bir düğüm grubu), **ülke değildir**. Birkaç bağımsız tesisi olan bir ülke etkilenmez. Aşağıdaki ülke rakamları, yoğunlaşmanın şu anda nerede bulunduğuna dair kaba bir coğrafi vekildir; protokolün sınırladığı şey değildir. Bu ekteki düğüm sayıları bir Temmuz 2026 anlık görüntüsüdür (~672 düğüm); güncel ağ toplamları için teknik dokümana bakın (27 Eylül 2026 itibarıyla 943 düğüm). Lokinet, HF23 öncesinde zorunlu kılmayan bir sürümde yayınlanır ve HF23 zorunlu kılmayı devreye alır.

Bu belge, EXIOM Tokenomi Teknik Dokümanı'na bir ektir ve onun okunduğunu varsayar. Teknik doküman, yoğunlaşma kontrollerinin ne olduğunu ve neden var olduklarını ele alır. Bu belge, her bir kontrolün nasıl çalıştığının mekanik ayrıntısını, HF22'nin arkasındaki testnet doğrulama verilerini, sıfır-ödül düzenleyicisinin arkasındaki kesin ekonomik matematiği, bir gizlilik zincirindeki operatör kimliği sorununu ve protokolün tam olarak çözmediği artık riskleri ele alır.

---

## Mevcut Yoğunlaşma Verileri

| Country | Active nodes |
|---|---|
| France | 492 |
| Germany | 70 |
| United States | 55 |
| Canada | 18 |
| Poland | 13 |
| United Kingdom | 10 |
| Türkiye | 5 |
| Australia | 4 |
| Singapore | 2 |
| Lithuania | 2 |
| Serbia | 1 |

Fransa, bu anlık görüntüdeki 672 düğümün 492'sini tutar (ağın yaklaşık %73'ü) ve bu yoğunlaşma neredeyse tamamen Grand Est'te kabaca 426 düğüm tutan tek bir Contabo tesisidir (ağın yaklaşık %63'ü). Protokolün sınırladığı şey ülke toplamı değildir; Grand Est **kümesidir**. Hayatta kalabilirlik eşiği, yakınlık kümesi başına aktif düğümlerin %30'udur (bu anlık görüntünün 672'sinde yaklaşık 202 düğüm ve mevcut teknik dokümandaki 943 düğümde yaklaşık 283 düğüm), ağ büyüdükçe sürekli yeniden hesaplanır. Kabaca 426 düğümdeki Grand Est, bu tavanın iki katından fazladır.

---

## Bunun Düğüm Operatörleri İçin Anlamı

Bu bölüm soruyu doğrudan yanıtlar: HF23 düğümlerinizi çalıştırma şeklinizi nasıl etkiler?

**HF23 ülkeye göre sınırlama yapmaz ve IP başına bir düğüm, VPS başına bir düğüm veya cüzdan başına bir düğüm gerektirmez.** Tavan, *yakınlık kümesi* başına (fiziksel veya yönlendirme altyapısını paylaşan düğümler) aktif ağın %30'udur. Paylaşılan altyapı üzerinde 10, 50 veya hatta 100 düğüm çalıştıran bir operatör, kümesi bu eşiğin altında kaldığı sürece HF23'ten tamamen etkilenmez. Tek bir makinede, tek bir VPS hesabında ve tek bir cüzdanda birden fazla düğüm çalıştırabilirsiniz. HF23'te hiçbir şey bunu değiştirmez.

**Sıfır-ödül düzenleyicisi yalnızca küme başına tavanın (aktif düğümlerin %30'u) üzerindeki düğümlere uygulanır.** Bir kümedeki en eski kayıtlı düğümler, bu eşiğe kadar tam ödül kazanır. Yalnızca aşırı-yoğunlaşmış bir kümede bunun üzerinde sıralanan düğümler sıfır kazanır ve yalnızca daha az yoğunlaşmış bir kümeye taşınana kadar.

**Yeter sayı tekilleştirmesi, düğüm sayısını veya geliri değil, tur başına konsensüs etkisini sınırlar.** Tek bir VPS üzerinde 50 düğüm çalıştıran bir operatör, 50'sinin de blok ödüllerini kazanır ve altyapısını bugün yaptığının tam olarak aynısı şekilde yönetir. Potansiyel olarak birçok koltuk yerine, tur başına küme başına bir yeter sayı koltuğu alırlar ki amaçlanan sonuç budur.

**Yeni bir operatör için doğru yaklaşım**, düğüm gezginini kontrol etmek, mevcut kümelerin nerede yoğunlaştığını görmek ve hafif nüfuslu bir kümeye dağıtım yapmaktır. Kendi ayrı yönlendirmesine sahip tek bir sunucuda on düğüm, HF23 altında gayet iyi çalışır çünkü o küme %30 eşiğinin yanına bile yaklaşmaz. Tam ödüller, tam yeter sayı katılımı, sorun yok.

**Seyrek bölgelere dağıtım yaparsanız dinamik sizin lehinize çalışır.** Bir bölge sonunda dolarsa, düğüm gezgini bunu gösterir ve operatörlerin tavan onları etkilemeden önce taşınmak için finansal bir teşviki olur. Oraya ilk ulaşan operatörler, en eski düğümlerinde eşiğe kadar tam ödülleri korur. Aşırı-yoğunlaşmış bir kümeye yeni kayıtlar hemen hiçbir şey kazanmaz, bu nedenle ekonomi doğal olarak yeni dağıtımları daha hafif bölgelere doğru iter.

**HF23'ün çözdüğü belirli sorun**, kabaca 426 düğüm barındıran Fransa'daki bir tesistir (Grand Est Contabo kümesi); bu anlık görüntüde ağın yaklaşık %63'üdür. O tesis çevrimdışı olursa ağ durur. Amaç, o kümeyi %30 tavanın altına indirmektir. Yoğunlaşmamış bir kümede sorumlu bir çoklu-düğüm kurulumu çalıştıran diğer her operatör, tam olarak ağın daha fazlasına ihtiyaç duyduğu şeydir.

---

## Hard Fork'lar Neden Ayrılıyor

HF22, başarılı testlerin ardından sevk edilir. Cüzdan-anahtarı yeter sayısı tekilleştirmesi ve bağ çözme süresi birleştirmesinin Lokinet'e bağımlılığı yoktur. Her ikisi de testnet'te doğrulanmıştır ve Lokinet değerlendirmesi beklenirken onları tutmak gerekçesiz bir gecikmedir. HF22 sevk edilmeden önce teknik dokümanı okuyan gelişmiş bir aktör, yeter sayı kontrolünü önlemek için cüzdan bölmeyi deneyebilir, ancak bunu yapmak çalışma süresi kanıtı zamanlaması bağıntısı ve IP/ASN analizi aracılığıyla tespit edilebilir ve yönetişim eylemi için belgelenmiş bir kayıt oluşturur.

Lokinet önce kendi zorunlu kılmayan sürümünde (SQLite hafif-düğüm depolama değişikliğiyle birlikte) yayınlanır, böylece yeni taşıma tanıtıldığı anda konsensüs-kritik hâle getirilmez. O sürüm sırasında yakınlık kümelenmesi, ödül sonucu olmadan yayında ve gözlemlenebilir biçimde çalışır; gerçek küme sayısının ölçüldüğü ve HF23 eşiği ile yedeğinin ayarlandığı an budur. HF23 daha sonra izler ve zorunlu kılmayı devreye alır. Sürümleri ayırmak ayrıca temiz arıza alanları sağlar: HF23 etkinleştirilmesinden sonra bir şeyler ters giderse, izole edilecek daha az değişken olur. HF23 zorunlu kılması yayına girene kadar, Grand Est, HF22 yeter sayı tekilleştirmesinin ötesinde tam hayatta kalabilirlik riskine maruz kalmaya devam eder.

---

## HF22 Mekaniği

### Cüzdan-Anahtarı Yeter Sayısı Tekilleştirmesi

Yeter sayı seçim algoritması, kesinleştirmeden önce her aday küme üzerinde bir tekilleştirme geçişi yürütür. Çekiliş bir aday düğüm seçtiğinde, algoritma onun operatör cüzdan adresini, tur için zaten seçilmiş tüm düğümlere karşı kontrol eder. Bir eşleşme bulunursa, aday, zaten temsil edilen tüm adresler hariç tutularak kalan uygun havuzdan yeniden çekilerek değiştirilir.

Değiştirme çekilişi, zaten reddedilmiş adaylar arasında geri dönmez. Başlangıç çekilişinde kullanılan aynı olasılık-ağırlıklı sırada kalan seçilmemiş havuzdan çeker. Bu, kalan belirli bir düğüm kümesine doğru deterministik bir önyargı getirmeden yeter sayı seçiminin istatistiksel özelliklerini korur.

**Testnet doğrulama sonuçları:**
- 20 durma/kurtarma döngüsü tamamlandı (20/20)
- Tüm döngüler genelinde %100 kurtarma oranı
- Hiçbir döngüde sıfır manuel müdahale gerekti (en kötü blok boşluğu 83 saniye)
- Ana ağ HF22-öncesi referansı: 1,000 blok, %100 Pulse, sıfır GOV_SIGNED bloğu
- R0 zaman aşımı analizi: üretim koşullarında hiçbir R0 zaman aşımı oluşmadı. Mevcut ana ağın yoğunluk analizi, her yüksek-yoğunluklu IP kümesinin tek bir operatör olduğunu doğrular; bu da cüzdan-anahtarı tekilleştirmesinin mevcut balina (whale) dağıtımlarına karşı zaten tam koruma sağladığı anlamına gelir. En büyük iki tek-IP dağıtımı (sırasıyla 58 düğüm ve 51 düğüm) her biri tek bir operatördür ve HF22 altında tur başına bir yeter sayı koltuğuyla sınırlıdır.

**Bir yeter sayı koltuğunun pratikte anlamı:** Yeter sayı boyutu ve dönüşüm sıklığı, bir düğümün ne sıklıkta katıldığını belirler. Mevcut ağ boyutunda, tek-koltuk tavanı, yoğunlaşmış bir operatörün oracle oturumlarındaki, Pulse turlarındaki ve yükümlülük yeter sayılarındaki etkisinin tek düğümlü bir operatörünkiyle aynı olduğu anlamına gelir. Blok ödülü gelirleri değişmez.

**Cüzdan-bölme açığı ve ara dönem tespiti:** 426 düğümü 10 cüzdana bölen bir operatör, tur başına bir yerine 10 yeter sayı koltuğuna kadar alır. Bu, HF23'ün kapattığı bilinen açıktır. Ara dönemde, cüzdan bölme, daemon değişiklikleri olmadan hâlihazırda mevcut iki sinyal aracılığıyla tespit edilebilir. Birincisi, çalışma süresi kanıtı zamanlaması: aynı fiziksel sunucu veya hipervizördeki düğümler, cüzdan anahtarından bağımsız olarak kanıtları birbirinden milisaniyeler içinde gönderir. Farklı cüzdanlara kayıtlı düğümlerden 10ms-altı pencerelerde gelen bir kanıt kümesi, paylaşılan altyapının güçlü bir sinyalidir. İkincisi, IP ve ASN bağıntısı: farklı cüzdanlardaki, bir IP, alt ağ veya ASN paylaşan düğümler, günlüğe kaydedilir ve yönetişim incelemesi için işaretlenir. Cüzdan bölen ancak tüm düğümlerini aynı Contabo tesisinde tutan bir operatör, her iki sinyal aracılığıyla tanımlanabilir ve engel listesi politikası kapsamında yönetişim eylemine tabidir.

### Bağ Çözme Süresi Birleştirmesi

Zorunlu kayıt iptali bağ çözme süresi, gönüllü çekilme süresiyle eşleşecek şekilde 10,080 bloktan (yaklaşık 7 gün) 20,160 bloğa (yaklaşık 14 gün) değişir. Bu bir konsensüs sabiti değişikliğidir.

Orijinal 7 günlük zorunlu süre, ağ istikrarı sırasında, kontrolleri dışındaki altyapı olayları yaşayan operatörler üzerindeki cezayı sınırlamak için bilinçli bir seçimdi. Bu gerekçe artık geçerli değildir. Ağ istikrarlıdır, kayıttan düşürme kredisi sistemi kısa kesintiler için tamponu sağlar ve birleşik 14 günlük süre, kalan hiçbir gerekçesi olmayan bir asimetriyi ortadan kaldırır.

XEQM coin'leri, bağ çözme süresi boyunca kayıt işlemi aracılığıyla zincir üstünde kilitlenir. Kilidi bir protokol değişikliği olmadan erken serbest bırakacak bir mekanizma yoktur. Belgelenmiş altyapı arızaları için, yönetişim kaçırılan ödülleri yönetişim cüzdanından bir XEQM transferi olarak telafi edebilir, ancak zincir üstü kilit, bağımsız olarak tam süresini tamamlar.

---

## HF23 Mekaniği

### Lokinet Yakınlık Kümelenmesi

Lokinet (Low Latency Anonymous Routing Protocol, LLARP), trafiği katman 3'te servis düğümü ağı üzerinden yönlendirir ve TCP, UDP ve ICMP'yi destekler. Her servis düğümü bir aktarma (relay) olarak katılır. Ortaya çıkan yönlendirme grafiği fiziksel ağ topolojisini yansıtır: aynı tesisteki düğümler aynı yukarı-akış anahtarı ve aynı veri merkezi omurgası üzerinden yönlendirir; bu da bağıntılı yol seçimleri ve milisaniye-altı düğümler-arası gecikme üretir. Farklı tesislerdeki düğümler, ölçülebilir biçimde daha yüksek gecikmeyle farklı yollar üzerinden yönlendirir.

Kümelenme algoritması, tüm aktif düğümler genelinde ikili Lokinet yönlendirme gecikmesi ve yol örtüşmesi ölçümlerini alır ve bu ölçümleri yakınlık sinyali olarak kullanarak onları kümeler hâlinde gruplar. Bir küme sabit bir coğrafi bölge değildir; yönlendirme davranışı paylaşılan fiziksel altyapıyı gösteren düğümlerin dinamik bir gruplamasıdır. Farklı ülkelerdeki farklı Contabo tesislerindeki iki düğüm, yol örtüşmeleri yeterince yüksekse aynı kümede görünecek kadar yeterli paylaşılan Contabo omurga altyapısı üzerinden yönlendirebilir. Aynı veri merkezinde ancak farklı yukarı-akış bağlantılarına sahip farklı fiziksel makinelerdeki iki düğüm, yol örtüşmeleri düşükse farklı kümelerde görünecektir.

Lokinet yakınlığının yanında kullanılan tamamlayıcı sinyaller:

**Çalışma süresi kanıtı zamanlaması bağıntısı.** Ağ, tüm aktif düğümlerden düzenli bir takvimde zaten çalışma süresi kanıtları alır. Her düğümden gelen kanıt varışlarının zaman damgası dağılımı, alıcı düğümler tarafından kaydedilir. Aynı fiziksel sunucu veya VM hipervizöründeki düğümler, kanıtları tipik olarak 10 milisaniyenin altında karakteristik bir sıkı pencere içinde gönderir. Bu varış zamanlaması dağılımını kümelemek, daemon değişiklikleri gerektirmeyen ve Lokinet aktif olmadan önce çalışan bir fiziksel aynı-yerde-bulunma sinyali sağlar.

**ASN analizi.** Her düğümün IP adresi, kamuya açık BGP verileri aracılığıyla bir Autonomous System Number ile eşleşir. Bir ASN paylaşan düğümler, sağlayıcı düzeyinde yönlendirme altyapısını ve sağlayıcı düzeyinde yasal maruziyeti paylaşır. Tüm altyapısını etkileyen bir yargı-bölgesi düzeyinde emir alan bir sağlayıcı, kaç Lokinet kümesinde göründüklerinden bağımsız olarak tüm ASN düğümlerini aynı anda devre dışı bırakır. ASN yoğunlaşması tamamlayıcı bir sinyal olarak izlenir ve küme eşiğine yakın operatörlerin yönetişim incelemesine katkıda bulunur.

### Küme Kayıt Tavanı

Kayıt sırasında, protokol tüm mevcut kümelere karşı bir yakınlık değerlendirmesi yürütür. Kaydolan düğümün Lokinet yönlendirme özellikleri, her mevcut kümenin ağırlık merkezine (centroid) karşı ölçülür. En yakın küme zaten aktif düğümlerin %30'unu veya daha fazlasını içeriyorsa, kayıt, küme kapasitesini ve en yakın kümenin düğüm sayısını belirten belirli bir hata koduyla reddedilir.

Reddetme deterministiktir: aşırı-yoğunlaşmış bir kümeye atanacak kadar ona benzer şekilde yönlendiren herhangi bir düğüm, operatörün cüzdan anahtarından, kayıt geçmişinden veya teminat miktarından bağımsız olarak reddedilir. Operatör reddetmeye yönetişim aracılığıyla itiraz edemez. İleriye dönük tek yol, farklı bir kümeye yönlendiren altyapıya kaydolmaktır.

Eşik, kayıt anındaki aktif düğüm sayısına karşı değerlendirilir. Ağ büyüdükçe, mutlak terimlerle %30 eşiği onunla birlikte büyür. Bugün tavandaki bir operatör, ağ büyüdükçe ve mutlak tavan yükseldikçe, mevcut hiçbir düğümü taşımadan, daha önce tavan konan bir kümeye ek düğümler kaydedebilir.

### Sıfır-Ödül Düzenleyicisi

Sıfır-ödül düzenleyicisi, blok ödülü hesaplama sırasında uygulanır. Seçilen bir düğüm için ödül hesaplaması bir küme uygunluk kontrolü içerir. Düğümün kümesi tavan eşiğinden daha fazla düğüm içeriyorsa ve düğümün o küme içindeki kayıt sırası eşiğin üzerindeyse (en eskiden en yeniye sıralanmış), ödül hesaplaması sıfır döndürür.

Sıralama, düğümün küme ataması içindeki kayıt blok yüksekliğinden hesaplanır. Kümedeki en eski kayıtlı düğüm 1. sırayı alır, en son kaydedilen N. sırayı alır. Tavan eşiğinden büyük sıraya sahip düğümler sıfır kazanır. Tavan eşiğinde veya altında sıraya sahip düğümler tam standart ödülü kazanır. Sıralama, düğümler kümeden taşındığında, yeni düğümler katıldığında veya ağ topolojisi değişiklikleri nedeniyle küme sınırı kaydığında meydana gelen küme ataması her değiştiğinde yeniden hesaplanır.

**Grand Est için ekonomik matematik:** 208 düğümlük bir tavanla 426 düğümde, 218 düğüm sıfır blok ödülü kazanır. Düğüm başına ayda 0.53 $ kendi kendine barındırma fiyatlandırmasında, o 218 düğüm ayda 115.54 $'a mal olur ve sıfır gelir sağlar. Düğüm başına ayda 1.76 $ Pecunia fiyatlandırmasında maliyet ayda 383.68 $'dır. Operatörün iki rasyonel yanıtı vardır: fazla düğümleri yoğunlaşmamış kümelere taşımak, yeni kayıt kabul edilir edilmez ödüllerini geri yüklemek; veya fazla düğümlerin kaydını iptal etmek ve teminatlı XEQM'yi bağ çözme süreci aracılığıyla geri almak. Her iki yanıt da yoğunlaşmayı azaltır. Fazla düğümleri sıfır ödülde tutmanın rasyonel bir temeli yoktur.

**Müsamaha dönemi mekaniği:** HF23 etkinleştirme bloğunda, protokol tüm aktif kümelerin ve düğüm sayılarının bir anlık görüntüsünü alır. %30 eşiğini aşan herhangi bir küme, aşırı-yoğunlaşmış olarak işaretlenir. Etkinleştirme bloğunu takip eden 30 gün boyunca, sıfır-ödül düzenleyicisi, tavan eşiğinin üzerindekiler de dâhil olmak üzere tüm düğümler için askıya alınır. Müsamaha dönemi sırasında, düğüm sahipleri düğüm gezgininin küme atamalarını gözlemleyebilir, taşımaları planlayabilir ve bunları uygulamaya başlayabilir. Müsamaha dönemi süre sonu bloğunda düzenleyici etkinleşir. O bloğa kadar aşırı-yoğunlaşmış kümeden taşınmış düğümler, o bloktan itibaren tam ödül kazanır. Hâlâ eşiğin üzerindeki düğümler, taşınana kadar o bloktan itibaren sıfır kazanır.

### Yakınlık Kümesi Yeter Sayısı Tekilleştirmesi

HF23 yeter sayı tekilleştirme yükseltmesi, cüzdan adresi kontrolünü bir küme üyeliği kontrolüyle değiştirir. Çekiliş bir aday düğüm seçtiğinde, algoritma onun küme atamasını, tur için zaten seçilmiş tüm düğümlere karşı kontrol eder. İki düğüm bir küme atamasını paylaşıyorsa, ikincisi, zaten temsil edilen tüm kümeler hariç tutularak kalan havuzdan bir çekilişle değiştirilir.

Cüzdan bölen bir operatör üzerindeki pratik etki: tümü aynı Contabo tesisinde 426 düğüm genelinde 10 cüzdan adresi aynı yakınlık kümesinde görünür. Küme kontrolü hepsini tek bir birim olarak yakalar. O kümeden bir düğüm bir koltuk tutar. O kümeden diğer 425 düğüm, kaç farklı cüzdan adresi altında kayıtlı olduklarından bağımsız olarak tutmaz.

### Minimum Küme Sayısı Gereksinimi ve Yedek Kuralı

EXIOM ağı yeter sayı boyutu tur başına 12 koltuktur. Bu nedenle yakınlık kümesi tekilleştirmesi, yeter sayı oluşumunu garanti etmek için aktif düğüm kümesinde en az 12 ayrı yakınlık kümesi gerektirir. Ağ 12'den az ayrı küme üretirse, algoritma küme-başına-bir-koltuk kısıtlamasını karşılayamaz ve yeter sayı oluşumu başarısız olur.

Mevcut ağ dağılımının, Lokinet yakınlık kümelenmesi uygulandığında, 12 ile 18 arasında ayrı küme üretmesi tahmin edilmektedir. Bu, 12-koltuk minimumuna rahatsız edici biçimde yakındır. Nominal olarak ayrı tesisler arasındaki paylaşılan sağlayıcı omurga altyapısı, iki ayrı IP konumunun Lokinet yönlendirme grafiğinde tek bir yakınlık kümesine birleşmesine neden olabilir. Küme sayısını 12'nin altına düşüren böyle bir birleşme, yeter sayı oluşumunu tamamen bozar.

Bu nedenle algoritma zorunlu bir yedek kuralı uygular:

1. Algoritma, mevcut kümeleri rastgele sırayla işleyerek, ayrı küme başına bir düğümle tüm 12 koltuğu doldurmaya çalışır.
2. 12 koltuk dolmadan tüm ayrı kümeler tükenirse, algoritma bir yedek geçişine girer.
3. Yedek geçişinde, en küçük kümelerden başlanarak her kümeden ikinci bir düğüme izin verir. En az yoğunlaşmış kümeler, en yoğunlaşmış olanlardan önce ikinci bir koltuk alır.
4. Algoritma, 12 koltuk dolana kadar, her geçişte küme başına maksimum koltuğu bir artırarak yedek geçişlerine devam eder.
5. En yoğunlaşmış küme, mevcut koşullar altında Grand Est gibi, yalnızca tüm daha küçük kümelere yedek tahsisleri verildikten sonra ek koltuklar alır.

Yedeği tetikleyen her tur, ona neden olan küme sayısıyla günlüğe kaydedilir. Yönetişim, yedek sıklığını doğrudan bir yoğunlaşma riski göstergesi olarak izler. 12 veya daha fazla ayrı kümeye sahip bir ağ yedeği asla tetiklemez. Tutarlı biçimde yedeği tetikleyen bir ağ, HF23 yoğunlaşma zorunlu kılmasının henüz yeterli fiziksel çeşitliliği sağlamadığını ve küme tavanının veya müsamaha dönemi zorunlu kılmasının yönetişim dikkati gerektirdiğini işaret eder.

Yedek günlüğü, operatör topluluğunun yoğunlaşma riskini gerçek zamanlı gözlemleyebilmesi için küme atamalarıyla birlikte düğüm gezgininde yayımlanır.

---

## Bir Gizlilik Zincirinde Operatör Kimliği

Protokolün, küme tavanını ve sıfır-ödül düzenleyicisini zorunlu kılmak için hangi insan operatörün hangi düğümlere sahip olduğunu tanımlamasına gerek yoktur. Her iki kontrol de küme düzeyinde çalışır. Neyin belirlenip neyin belirlenemeyeceği, yönetişim izlemesi için yararlı bir bağlamdır ancak protokol zorunlu kılması için gerekli değildir.

**Zincir-üstü verilerden deterministik olan:** aynı operatör cüzdan anahtarı altında kayıtlı düğümler kesinlikle aynı operatördür. Bu, kayıt işlemindeki kamuya açık bilgidir.

**Lokinet ve zamanlama verilerinden yüksek güvenle çıkarsanabilen:** kaç cüzdan anahtarı kullandıklarından bağımsız olarak, bir düğüm kümesinin altında yatan ayrı fiziksel sunucuların sayısı. Her biri 85 düğüm çalıştıran, tümü aynı iki fiziksel sunucuda olan beş cüzdan anahtarı, beş değil iki ayrı zamanlama imzası ve iki Lokinet yakınlık ağırlık merkezi üretir.

**Bir gizlilik zincirinde belirlenemeyecek olan:** farklı altyapıya sahip iki farklı cüzdan anahtarının aynı insan operatöre ait olup olmadığı. Her cüzdan anahtarının fonlama kaynağı tasarım gereği özeldir. Gizlilik zincirinin işlem katmanı aracılığıyla beş farklı kaynaktan fonlanan beş cüzdan kullanan gelişmiş bir operatör, protokol düzeyinde beş ayrı kimlik sunar.

Hayatta kalabilirlik zorunlu kılması için bu önemli değildir. Küme 426 düğüm içerir. En eski 208 ödül kazanır. En yeni 218 sıfır kazanır. Operatörün kimliği o hesaplama için önemsizdir.

---

## Uygulama Durumu

| Control | Status |
|---|---|
| Operatör cüzdan-anahtarı yeter sayısı tekilleştirmesi | HF22, blok 219120'de etkinleştirildi |
| Bağ çözme süresi birleştirmesi, 7'den 14 güne | HF22, etkinleştirildi |
| Pulse durma-kurtarma (imza yedeği, snode_revision 1) | Blok 236920'de etkinleştirildi, 18 Ekim 2026 |
| Ağ taşıması olarak Lokinet etkinleştirmesi | Geliştirme aşamasında; HF23 öncesinde zorunlu kılmayan bir sürümde yayınlanır |
| SQLite hafif-düğüm depolaması | Geliştirme aşamasında; HF23 öncesi Lokinet sürümüyle yayınlanır |
| Yakınlık kümelenmesi algoritması | Tasarım aşaması, Lokinet değerlendirmesi bekleniyor |
| Küme kayıt tavanı, %30 eşik | HF23, tasarım aşaması |
| Fazla düğümler için sıfır-ödül düzenleyicisi | HF23, tasarım aşaması |
| Müsamaha dönemi mekanizması | HF23, tasarım aşaması |
| Yedek kurallı yakınlık kümesi yeter sayısı tekilleştirmesi | HF23, tasarım aşaması |
| Minimum küme sayısı izleme ve yedek günlüğü | HF23, tasarım aşaması |
| Çalışma süresi kanıtı zamanlaması bağıntısı araçları | Daemon değişikliği gerekmez, araçlar geliştirme aşamasında |
| ASN kümelenmesi tamamlayıcısı | Daemon değişikliği gerekmez, araçlar geliştirme aşamasında |

---

## Bu Kontrollerin Çözmediği Şeyler

**Sağlayıcı düzeyinde yasal yoğunlaşma.** Tüm küresel altyapısını etkileyen bir yargı-bölgesi düzeyinde yasal emir alan bir sağlayıcı, o düğümler birden fazla Lokinet yakınlık kümesinde görünse bile tüm düğümlerini aynı anda devre dışı bırakır. ASN analizi bu riski yüzeye çıkarır, ancak protokol, operatörün sağlayıcı kimliğini açıklamasını gerektirmeden sağlayıcı çeşitliliğini zorunlu kılamaz. Küme tavanının doğal olarak ürettiği coğrafi yayılma, pratikte bu riski önemli ölçüde azaltır çünkü kümeler arasında dağılmaya zorlanan operatörler pratikte birden fazla sağlayıcı kullanacaktır.

**Gizlilik-zinciri cüzdan bölmeleri genelinde insan operatör kimliğinin belirlenmesi.** Yukarıda açıklandığı gibi, gizlilik zinciri aracılığıyla fonlanan birden fazla cüzdan kullanan gelişmiş bir operatör protokol düzeyinde tanımlanamaz. Küme tavanı ve sıfır-ödül düzenleyicisi, kimlikten bağımsız olarak arıza alanı riskini ele alır. Yeter sayı tekilleştirmesi, HF23'te konsensüs etkisi açığını kapatır. Artık risk, gelişmiş bir operatörün, gerçekten ayrı birçok küme genelinde birçok düğüm çalıştırması, düğüm sayısıyla orantılı blok ödülü geliri biriktirmesi ve ağ sağlığına orantılı katkıda bulunmasıdır. Bu kabul edilebilir sonuçtur: yoğunlaşmış konsensüs etkisi sınırlıdır; dağıtık sermaye katılımı ödüllendirilir.

Küme ataması, taşıma planlaması veya HF22/HF23 zaman çizelgesi hakkında soruları olan operatörler, Node Operators Telegram kanalında paylaşım yapmaya veya bu depoda bir issue açmaya teşvik edilir.

---

## Mevcut Diller (Available Languages)

Bu belgenin topluluk çevirileri, whitepaper deposunda tutulmaktadır. Bir çeviri ile İngilizce sürüm arasında herhangi bir çelişki durumunda İngilizce sürüm geçerlidir.

| Language | Document |
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

*Bu belge finansal veya yasal tavsiye teşkil etmez. XEQM, EXIOM platformu için bir yarar coin'idir, bir yatırım ürünü değildir. Token sınıflandırması, menkul kıymet statüsü ve geçerli düzenlemeler yargı bölgesine göre değişir. Katılımcılar, XEQM edinmeden veya XEQM ile işlem yapmadan önce kendi yerel hukuki ve düzenleyici çerçevelerine danışmalıdır. XEQM Labs, spekülatif fiyat artışı temelinde XEQM satın alınmasını teşvik etmez.*
