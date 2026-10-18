# XEQM Labs - EXIOM Platformu
## Tokenomi Teknik Dokümanı (Whitepaper)
### Taslak v12 | 09/27/2026

---

## Bugün Yayında Olanlar ve Planlananlar

| Bileşen | Durum |
|---|---|
| EXIOM ana ağı (mainnet) | Yayında, 6 Mayıs 2026'dan beri faal |
| Servis düğümü ağı | Yayında — 27 Eylül 2026 itibarıyla 943 aktif servis düğümü |
| Lokinet (LLARP) | HF23 öncesinde zorunlu kılmayan bir sürümde yayınlanır (taşıma katmanı yayında, yakınlık kümelenmesi gözlemlenebilir); HF23 zorunlu kılmayı devreye alır. Uygulama Q4 2026'da başlar |
| SQLite hafif-düğüm depolaması | Geliştirme aşamasında; daha düşük düğüm belleği ve diski için, isteğe bağlı güncel-pencere hafif düğümleriyle birlikte HF23 öncesi Lokinet sürümüyle yayınlanır |
| XEQ'tan XEQM'ye coin takası | Teslim edildi ve kapatıldı, 35 günlük üretim süreci, kamuya açık denetlenebilir defter |
| GUI cüzdan | Yayında, github.com/XEQMLabs/XEQMLabs-GUI |
| Düğüm gezgini (node explorer) | Yayında, aktif servis düğümü izleme |
| EXIOM Oracle | Ana ağda yayında (Robinhood Chain, chainId 4663); 28 Eylül 2026 itibarıyla 12 üyeli operatör komitesi |
| EXIOM geliştirici API'si | Beta aşamasında yayında — self-servis anahtarlar, imzalı uyumluluk iddiaları ve bir doğrulama motoru, /docs adresinde OpenAPI; geliştirmesi ücretsiz, ön ödemeli çağrı başına kullanım devreye alınıyor (27 Eylül 2026) |
| EXIOM Privacy Oracle (TLSNotary / ZK) | Temeller yayında (doğrulama motoru, oracle oturumları); tam özel-web-verisi oracle'ı Phase 3'te |
| EXIOM RFQ ticaret platformu | Geliştirme aşamasında, Phase 2/3, ilk çift XEQM/BTC |
| HF22, cüzdan-anahtarı yeter sayısı tekilleştirme, bağ çözme birleştirme, Pulse durma-kurtarma | Ana ağ bloğu 219120'de etkinleştirildi. Pulse durma-kurtarma revizyonu (snode_revision 1, imza tabanlı yedek) 18 Ekim 2026'da blok 236920'de etkinleştirildi |
| HF23, yakınlık kümesi tavanı ve ödül düzenleyicisi (zorunlu kılma) | Tasarım aşamasında; zorunlu kılmayan Lokinet + hafif-düğüm sürümü oturduktan sonra yoğunlaşma limitlerini devreye alır; hedef Q4 2026 |
| Resmi zincir-üstü yönetişim | Planlandı, Phase 6 |

---

## 1. XEQM Labs Nedir

XEQM Labs bir gizlilik teknolojisi şirketidir. Amiral gemisi ürünü EXIOM, küresel bir servis düğümü kümesi tarafından işletilen, gizliliği koruyan bir Proof-of-Stake Katman 1 ağı ve ticari geliştirici platformudur. XEQM, platformun erişim ve kullanım coin'idir. Geliştiriciler ücretsiz geliştirir ve üretim kullanımını, API'yi çağırdıkça tükettikleri XEQM ile öderler. Servis düğümü operatörleri ağı güvence altına almak için XEQM kazanır ve aynı operatörler, platformun oracle ürünlerine hizmet veren bir oracle yan-birimini (sidecar) çalıştırarak ek gelir elde edebilir.

Proje, yedi yılı aşkın bir süre öncesine dayanan bir topluluk ve operasyonel geçmişi ileriye taşımaktadır. EXIOM ana ağı, o topluluğa doğrulanabilir bir arz, öngörülebilir bir emisyon takvimi, Proof-of-Work bileşeni içermeyen saf Proof-of-Stake konsensüsü ve operatörün zamanına ve sermayesine saygı gösteren servis düğümü mekaniği olan bir ağ sunmak için inşa edilmiştir.

XEQM yerel bir Katman 1 coin'idir; başka hiçbir zincirde tokenleştirilmemiştir, bir ERC-20 veya sarmalanmış (wrapped) varlık değildir ve köprülenmemiştir. Sahipleri doğrudan EXIOM ana ağıyla etkileşime girer.

### EXIOM Ürün Ailesi

**EXIOM Servis Düğümü Ağı.** Ana ağda yayında. Küresel bir servis düğümü kümesi zinciri güvence altına alır, blok ödülleri kazanır ve diğer tüm EXIOM ürünlerinin üzerinde çalıştığı altyapı katmanını oluşturur. 27 Eylül 2026 itibarıyla 943 aktif servis düğümü.

**EXIOM Coin Swap.** Projelerin sahip topluluklarını eski bir zincirden tam kriptografik denetlenebilirlikle yeni bir zincire taşımalarını sağlayan ticari bir ürün. Pilot uygulama, XEQ sahiplerinin EXIOM ana ağında XEQM'ye taşınmasıydı; 35 gün boyunca her gönderim, kamuya açık bir SHA256 parmak izi taşıyan kriptografik olarak doğrulanmış bir defter üzerinden işlendi. Ürün, doğrulanabilir bir zincir taşıması gerektiren diğer projeler için mevcuttur.

**EXIOM Oracle.** Ana ağda yayında. Platformun ilk oracle ürünü: her biri hafif bir oracle yan-birimi çalıştıran XEQM servis düğümü operatörlerinden oluşan bir komite; bu komite, uygulamaların geliştirici API'si aracılığıyla tükettiği BLS-toplamalı, EIP-712 imzalı uyumluluk tasdiklerini (örneğin bir adresin belirli bir yargı bölgesi için uygun olduğunu) üretir. Robinhood Chain (chainId 4663) üzerinde dağıtılmıştır ve 28 Eylül 2026 itibarıyla 12 üyeli bir operatör komitesi çalıştırır. Yan-birimi çalıştırmak, bir servis düğümü operatörünün blok ödüllerine ek olarak, kullanıma dayalı ek gelir elde etmesinin yoludur.

**EXIOM Geliştirici API'si.** Beta aşamasında yayında. Platformun uyumluluk ve doğrulama yeteneklerini açığa çıkaran yapılandırılmış bir API — imzalı uyumluluk iddiaları ve bir doğrulama motoru (imzalı-iddialar, TLSNotary ve sıfır-bilgi mekanizmaları) — self-servis erişim (bir DID artı API anahtarı), bir OpenAPI 3.1 spesifikasyonu, webhook'lar ve idempotent istekler ile. Geliştiriciler cömert bir aylık kota üzerinde ücretsiz geliştirir ve üretim kullanımını, çağrı başına tüketilen XEQM ile öder. Phase 2, aktif.

**EXIOM Privacy Oracle.** Tasarlandı, temelleri kuruldu. Oracle'ın daha geniş evrimi: altta yatan kaynağı ifşa etmeden özel web verileri hakkında (TLSNotary ve sıfır-bilgi teknikleri aracılığıyla) olguları kanıtlamak. Bunu destekleyen doğrulama motoru ve oracle-oturumu uç noktaları hâlihazırda yayında; tam özel-web-verisi oracle'ı bir Phase 3 teslimatıdır. Hem EXIOM RFQ platformu hem de üçüncü taraf uygulamalar oracle çıktılarını tüketebilir.

**EXIOM RFQ Ticaret Platformu.** Geliştirme aşamasında. EXIOM API'si üzerine inşa edilmiş, kriptografik takas tasdikli, uçtan uca tezgahüstü (OTC) eşler arası bir ticaret platformu. İlk işlem çifti, her ikisi de tokenleştirme, sarmalama ve köprü riski olmayan yerel Katman 1 varlıkları olan XEQM/BTC'dir. Oracle, fiyatlandırma katmanı için özel fiyat tasdikleri sağlar. Phase 2/3.

XEQM Labs, EXIOM'u ticari bir yazılım platformu olarak işletir. Amaç, zaman içinde yönetişim emisyonlarına bağımlılığı azaltan sürdürülebilir platform gelirleridir. XEQM Labs, spekülatif fiyat artışı temelinde XEQM satın alınmasını teşvik etmez.

---

## 2. Arz Kökeni (Supply Provenance)

Taşıma tamamlandı. Eski varlıklar karşılığında EXIOM ana ağında 276,917,604 XEQM ihraç edildi. Bu rakam, 6 Mayıs 2026'daki ana ağ lansmanında doğrulanmış başlangıç arzıdır. Her eski yatırma işlemi, bir SHA256 parmak izi ile kamuya açık bir deftere kaydedildi. Yeni zincir, bu tam doğrulanmış toplamla eşleşecek şekilde takasın sonunda bir kez basıldı. Takasa dâhil olan her cüzdanın harcama anahtarları yayımlandı ve herkes yatırmadan ödemeye kadar tüm işlem geçmişini doğrulayabilir.

Başlangıç arzının ötesinde, dolaşıma yeni XEQM iki protokol düzeyinde emisyon akışıyla girer: servis düğümü blok ödülleri ve yönetişim emisyonları. Her ikisi de protokole yazılmış, herkesin kamuya açık parametrelerden hesaplayabileceği sabit ve öngörülebilir takvimlerde çalışır. Oranlar ve operasyonel ayrıntılar Bölüm 3'tedir. Toplam arz zaman içinde artar. XEQM, Monero'nun kuyruk emisyonuyla aynı model üzerinde, arz tavanı olmayan bir zincirdir. Projenin taahhüt ettiği sabit-arz disiplini, protokol kaynaklı emisyonlara katı bir tavan değil, takdire bağlı ihracın yokluğunu ifade eder.

**Takdire bağlı basım yok.** Protokol, ad-hoc ihraca, manuel arz ayarlamalarına veya takvim dışı basımlara izin vermez. Dolaşıma giren her yeni XEQM, yukarıdaki iki takvimli emisyon akışı aracılığıyla girer.

**Yakma (burn) yok.** Bu ağın üzerine inşa edildiği kriptografik mimari, bu terimin tipik olarak kullanıldığı anlamda kanıtlanabilir yakmaları desteklemez. Bir coin'in gönderildiği herhangi bir adres, yalnızca anahtarın kanıtlanabilir biçimde yok edildiği ölçüde harcanamaz olur. Hiçbir cüzdanı bir yakma adresi olarak sunmayacağız. Taşıma penceresinde takas edilmeyen coin'ler, aktif olmayan eski zincirde kalır ve XEQM arzının bir parçası değildir.

---

## 3. Tokenomi Modeli

### Blok Emisyonları

Ağ her 60 saniyede bir yeni blok üretir ve seçilen servis düğümüne 8.25 XEQM verir; bu da günde 11,880 XEQM üretir. 943 aktif düğümde (27 Eylül 2026), her düğüm günde yaklaşık 12.6 XEQM, yani ayda yaklaşık 380 XEQM kazanır.

HF21'den itibaren, blok ödülleri haftalık toplu (batching) bir takvimde dağıtılır. HF21'den önce ödüller her 20 blokta bir veriliyordu. Ödüller artık her 10,080-bloklu pencere (yaklaşık 7 gün) boyunca birikir ve her pencerenin sonunda ödenir. Toplam emisyon oranı değişmemiştir; yalnızca ödeme temposu kaymıştır.

### Yönetişim Emisyonu

Hazine günde yaklaşık 17,857 XEQM, yani haftada kabaca 124,999 XEQM alır. Bu, aktif bir ticari yazılım geliştirme ekibinin işletme bütçesidir. Platform gelir öncesi aşamadayken mühendisler, güvenlik gözden geçirenler, altyapı operatörleri ve ekosistem katkıcıları bu emisyondan ücretlendirilir. Her EXIOM ürünü gelir üreten statüye ulaştıkça, yönetişim emisyonu gözden geçirilir ve buna göre azaltılır. Uzun vadeli hedef, platform gelirinin birincil finansman mekanizması olarak yönetişim emisyonunun yerini almasıdır.

### Emisyon Tahsisi

| Tahsis | Pay | Amaç |
|---|---|---|
| Servis Düğümü Ödülleri | 40% | Doğrudan servis düğümlerine ödenen blok ödülleri |
| Çekirdek Protokol Geliştirme | 25% | Blok zinciri, EXIOM platformu ve çekirdek ağ hizmetleri |
| Pazarlama ve Farkındalık | 15% | Ağ görünürlüğü ve benimsenme |
| Ekosistem ve Topluluk | 10% | Hibeler, ödüller, topluluk ödülleri, entegrasyon desteği |
| Güvenlik ve Denetimler | 5% | Denetimler, güvenlik incelemeleri, güvenilirlik testleri |
| Uzun Vadeli Rezerv | 5% | İstikrar, acil ihtiyaçlar, uzun vadeli operasyonlar |

### EXIOM Platform Geliri ve Dağıtımı

Blok ödüllerinin ötesinde, platform geliştirici kullanımından gelir elde eder. Erişim ön ödemelidir: bir geliştirici XEQM yatırarak (iade edilmez) hesabını fonlar ve bu bakiye, üretim API'sini çağrı başına fiyatlandırmayla tükettikçe azalır. Ücretsiz kota üzerindeki geliştirme ve değerlendirme ücretlendirilmez.

Tüketilen XEQM platform geliri olarak kaydedilir ve oracle'a hizmet veren operatörler ile platform operasyonları arasında dağıtılır:

| Alıcı | Pay | Amaç |
|---|---|---|
| Oracle yan-birim operatörleri | 70% | Oracle yan-birimini çalıştıran servis düğümü operatörleri, hizmet verdikleri oracle görevleriyle orantılı olarak ödüllendirilir |
| Platform operasyonları ve geliştirme | 30% | Devam eden operasyonları ve geliştirmeyi fonlar, zaman içinde yönetişim emisyonuna bağımlılığı azaltır |

Operatörler, oracle'a hizmet veren altyapıyı çalıştırdıkları için çoğunluğu alır. 70/30 oranı başlangıç değeridir ve yönetişim yoluyla ayarlanabilir. Gelir, blok ödülleriyle aynı haftalık tempoda — her 10,080-bloklu pencere (yaklaşık 7 gün), HF21 ödül toplamasına hizalı — kaydedilir ve dağıtılır; böylece bir operatör blok ödüllerini ve kullanım-geliri payını tek bir ritimde alır. Bu gelir payı, Bölüm 4'te açıklanan operatör yan-birim ödülünün emisyondan değil gerçek kullanımdan fonlanma mekanizmasıdır.

Bir servis düğümünü (ve onun oracle yan-birimini) çalıştırmak için temel donanım: 4 CPU çekirdeği, 8 GB RAM, 100 GB SSD, 100 Mbps bağlantı. Daha ağır gizlilik-oracle'ı iş yükleri, Bölüm 10'da ele alınan daha yüksek özellikler gerektirir.

---

## 4. Servis Düğümü Yapısı

### Teminat (Staking) Parametreleri

| Parametre | Değer |
|---|---|
| Tam düğüm gereksinimi | 200,000 XEQM |
| Minimum operatör teminatı | 100,000 XEQM (tam gereksinimin %50'si) |
| Maksimum operatör ücreti | 10% |
| Bağ çözme süresi, gönüllü çekilme | 14 gün, ödüller devam eder |
| Bağ çözme süresi, zorunlu kayıt iptali | 14 gün, ödül yok (HF22'de birleştirildi) |
| Maksimum katkıcı slotu | 11 (operatör dâhil) |
| Slot başına minimum topluluk katkısı | 10,000 XEQM |
| Düğüm başına topluluk teminatçısı penceresi | 10 katkıcı slotuna kadar toplam 100,000 XEQM'ye kadar |

### Düğüm Ekonomisi

Birçok bulut VPS sağlayıcısı, servis düğümü işletimini sıfır aylık maliyetle destekleyebilen ücretsiz bir hizmet katmanı sunar. Ayda yaklaşık 5.28 $ tutarındaki ücretli bir VPS, 10 servis düğümü çalıştırabilir; bu da düğüm başına barındırma maliyetini kabaca ayda 0.53 $'a getirir. Pecunia aracılığıyla yönetilen barındırma, düğüm başına ayda 1.76 $ tutarındadır.

Düğüm başına blok ödülleri, aktif düğüm sayısıyla ters orantılı ölçeklenir: 943 aktif servis düğümünde (27 Eylül 2026), ağın günlük 11,880 XEQM emisyonu, düğüm başına günde kabaca 12.6 XEQM, ayda yaklaşık 380 XEQM'ye denk gelir. Hem ödül hem de teminat XEQM cinsinden olduğundan, blok-ödülü APY'si fiyattan bağımsız olarak yaklaşık %2.3'tür; tek önemli yinelenen maliyet barındırmadır ve kendi kendine barındırmada düğüm başına ayda kabaca 0.53 $ veya Pecunia aracılığıyla 1.76 $'dır. Oracle yan-birimini (Bölüm 10) çalıştırmak, gelir temelli ve gerçek platform kullanımıyla ölçeklenen, emisyondan değil geliştirici tüketiminden fonlanan ikinci bir gelir akışı ekler.

### Katkıcı Ekonomisi

Altyapı çalıştıramayan veya çalıştırmamayı tercih eden operatörler, 10 katkıcı slotuna kadar mevcut bir düğüme teminat katkısında bulunabilir. Operatör, kalan kısım katkıcılar arasında orantılı olarak bölünmeden önce blok ödülünün %0 ila %10'unu alabilir. Katkıcıların barındırma maliyeti yoktur; bu nedenle her fiyat noktasında bir katkıcının net getirisi, kendi kendine barındıran veya Pecunia ile barındıran bir operatörünkinden fazladır.

### Düğüm Yaşam Döngüsü

Düğümler, teminat ve performans gereksinimleri sürdürüldüğü sürece süresiz olarak aktif kalır. Uyumdan çıkan bir düğüm, cezasız biçimde düzeltilebilir. Düzeltilmezse, zorunlu kayıt iptali, ödülsüz 14 günlük bir bağ çözme süresini tetikler. Gönüllü çıkış, boyunca ödüllerin devam ettiği 14 günlük bir bağ çözme süresi taşır.

---

## 5. Ağ Hayatta Kalabilirliği ve Saldırı Vektörleri

### Hayatta Kalabilirlik Gereksinimi

EXIOM ağı geliştiricilere güvenilirlik taahhütlerinde bulunur. Tek bir veri merkezi kesintisiyle çevrimdışı bırakılabilen bir ağ bu taahhütleri yerine getiremez. Protokol, maksimum bir arıza alanı (failure domain) büyüklüğünü zorunlu kılar: tek bir fiziksel tesis, veri merkezi veya yönlendirme kümesi, aktif düğümlerin %30'undan fazlasını barındıramaz.

943 düğümde (27 Eylül 2026), %30 yaklaşık 283 düğümdür. Herhangi tek bir tesisi kaybetmek, aynı anda en fazla 283 düğümü çevrimdışı bırakabilir; bu da en az 660 düğümün faal kalmasını sağlar; bu miktar, zincirleme kayıt iptalleri olmadan blok üretimini ve yeter sayı oluşumunu sürdürmeye yeterlidir. Bu bir mühendislik gereksinimidir, bir merkeziyetsizlik tercihi değildir.

### İki Hard Fork

Hayatta kalabilirlik zorunlu kılması, riski azaltmak ve doğrulanmış işi hemen sevk etmek için iki aşamada, ayrılarak teslim edilir.

**HF22, etkinleştirildi:** Operatör cüzdan-anahtarı yeter sayısı tekilleştirmesi ve bağ çözme süresi birleştirmesi, artı daha önceki Proof-of-Work kurtarma yedeğini imza tabanlı bir yedekle değiştiren bir Pulse durma-kurtarma revizyonu (snode_revision 1). Lokinet bağımlılığı yok. 20 durma/kurtarma döngüsü boyunca %100 kurtarma oranı, sıfır müdahale ve 83 saniyelik en kötü blok boşluğuyla doğrulandı. HF22 ana ağ bloğu 219120'de etkinleştirildi; durma-kurtarma revizyonu 18 Ekim 2026'da blok 236920'de etkinleştirildi.

**HF23, tasarım aşamasında, hedef Q4 2026:** Yakınlık kümesi kayıt tavanı, fazla düğümler için sıfır-ödül düzenleyicisi ve yeter sayı tekilleştirmesinin cüzdan-anahtarından yakınlık kümesine yükseltilmesi. Üçü de yakınlık sinyali olarak Lokinet yönlendirme grafiğine dayanır. Yeni bir taşıma katmanını tanıtıldığı anda konsensüs-kritik hâle getirmekten kaçınmak için, Lokinet önce ayrı, zorunlu kılmayan bir sürümde (SQLite hafif-düğüm depolama değişikliğiyle birlikte) yayınlanır; burada yakınlık kümelenmesi yayında ve gözlemlenebilirdir ancak ödül sonucu yoktur. HF23 daha sonra, bu sürüm oturduktan ve gerçek küme sayısı ölçülüp eşik ile yedek ayarlandıktan sonra, zorunlu kılmayı devreye alır.

### HF22 Kontrolleri

**Operatör cüzdan-anahtarı yeter sayısı tekilleştirmesi.** Herhangi bir Pulse turunda, oracle oturumunda veya yükümlülük yeter sayısında, operatör cüzdan adresi başına en fazla bir düğüm doğrulayıcı koltuğu tutabilir. Rastgele bir çekiliş aynı operatör adresinden iki düğüm seçerse, ikincisi farklı bir operatörün düğümüyle değiştirilir. Blok ödülleri etkilenmez; bunlar yeter sayı katılımından bağımsız olarak bekleme-süresi sıralamasıyla atanır.

Bilinen sınırlama: cüzdan bölme ile aşılır. Birden fazla cüzdan adresi kullanan bir operatör, protokole birden fazla operatör anahtarı sunar. HF23 bu açığı yakınlık kümesi tekilleştirmesiyle kapatır.

**Bağ çözme süresi birleştirmesi.** Zorunlu kayıt iptali bağ çözme süresi, gönüllü çekilmeyle eşleşecek şekilde 7 günden 14 güne uzatıldı. Her iki durum da artık 14 gündür.

### HF23 Kontrolleri

Lokinet ağ taşıması olarak aktif olduğunda, fiziksel olarak aynı yerde bulunan düğümler karakteristik yönlendirme imzaları gösterir: milisaniye-altı karşılıklı gecikme ve Lokinet yönlendirme grafiği boyunca yüksek yol örtüşmesi. Gerçekten farklı tesislerdeki düğümler daha yüksek gecikme ve daha düşük yol örtüşmesi gösterir. Bu kümelenme sinyali, operatörlerin sağlayıcılarını veya konumlarını açıklaması gerekmeden, gözlemlenebilir ağ davranışından türetilir.

**Küme kayıt tavanı.** Yeni düğüm kayıtları, mevcut kümelere Lokinet yönlendirme yakınlığına göre değerlendirilir. Hedef küme zaten aktif düğümlerin %30'unu veya daha fazlasını içeriyorsa, kayıt protokol tarafından reddedilir.

**Sıfır-ödül düzenleyicisi.** Küme tavan eşiğinin üzerindeki düğümler, yoğunlaşmamış bir kümeye taşınana kadar sıfır blok ödülü kazanır. Düğümler her küme içinde kayıt yaşına göre sıralanır; tavan eşiğine kadar en eski düğümler tam ödül kazanır. Bu eşiğin üzerindeki her düğüm sıfır kazanır. VPS maliyetlerine karşı düşük bir oran gerekçelendirilebilir; sıfır gerekçelendirilemez.

HF23 etkinleştirilmesinde 30 günlük bir ödeme müsamahası (grace period) uygulanır. Tüm düğümler müsamaha dönemi boyunca tam ödül kazanır. Süre sonunda, sıfır-ödül düzenleyicisi fazla düğümlerde etkinleşir.

**Yakınlık kümesi yeter sayısı tekilleştirmesi.** HF22 cüzdan-anahtarı tekilleştirmesini yakınlık kümesi tekilleştirmesine yükseltir. Cüzdan yapısından bağımsız olarak, tur başına yakınlık kümesi başına en fazla bir düğüm. Cüzdan-bölme açığını kapatır.

Yeter sayı boyutu tur başına 12 koltuktur. Bu nedenle tekilleştirme, bir yedek olmadan işlemek için en az 12 ayrı yakınlık kümesi gerektirir. Mevcut ağ topolojisi göz önüne alındığında, HF23 etkinleştirilmesinde küme sayısı bu minimuma yakın olabilir. Algoritma zorunlu bir yedek uygular: 12 koltuk dolmadan tüm ayrı kümeler tükenirse, en yoğunlaşmış küme ikinci bir koltuk almadan önce, en küçük (en az yoğunlaşmış) kümelerden başlanarak ek koltuklar tahsis edilir. Yedek sıklığı günlüğe kaydedilir ve gerçek zamanlı bir yoğunlaşma riski göstergesi olarak düğüm gezgininde yayımlanır. Yedeği asla tetiklemeyen bir ağ, yeterli fiziksel çeşitliliğe ulaşmıştır.

### Ek Kontroller

**Sermaye maliyeti engeli.** 100,000 XEQM minimum operatör teminatı, her operatörün her düğüme gerçek sermaye bağlamasını sağlar. N düğüm çalıştırmak en az N x 100,000 XEQM teminat gerektirir.

**Operatör ücreti ele geçirme koruması.** EXIOM, bazı servis düğümü ağlarında bulunan ve bir operatörün minimum sermayeyle bir düğüm kaydedip, katkıcı teminatından bağımsız olarak tüm blok ödülünü ele geçirmek için %100 ücret ayarladığı operatör ücreti ele geçirme saldırısına tabi değildir. Maksimum ücret %10 ile sınırlıdır ve %50 minimum operatör teminatı bunu ekonomik olarak akıl dışı kılar.

**Çalışma süresi kanıtı zamanlama analizi.** Aynı fiziksel sunucudaki düğümler, çalışma süresi kanıtlarını sıkı bağıntılı kümeler hâlinde gönderir; bu, daemon değişikliği olmadan mevcut kanıt makbuzu verilerinden tespit edilebilir.

**ASN analizi.** Aynı Autonomous System Number arkasındaki düğümler, sağlayıcı düzeyinde altyapıyı ve yasal maruziyeti paylaşır. ASN yoğunlaşması, küme atamasına ve yönetişim incelemesine katkıda bulunur.

**Yönetişim engel listesi (blocklist).** Yönetişim tarafından yönetilen bir açık anahtar engel listesi, engellenen kayıt anahtarlarının yeni düğümler kaydetmesini engeller.

**Nakamoto katsayısı hedefi.** Ağ, en az 8'lik bir operatör katsayısını hedefler. 27 Eylül 2026 itibarıyla, 943 aktif servis düğümü ve 204 operatör genelinde, operatör Nakamoto katsayısı — aktif düğümlerin çoğunluğunu kontrol eden minimum operatör sayısı — 9'dur ve hedefi karşılar (Temmuz 2026'da 184 operatör genelinde 7 iken yükselmiştir). Fiziksel-tesis yoğunlaşması ayrı ve daha akut bir sorundur: tek bir veri merkezi bölgesi hâlâ düğümlerin çoğunluğunu barındırmaktadır ki bu tam olarak HF23'ün yakınlık-kümesi tavanının kırmak için tasarlandığı yoğunlaşmadır.

Tam yoğunlaşma limitleri önerisi şu adrestedir: [concentration-limits-proposal.md](https://github.com/XEQMLabs/whitepaper/blob/main/concentration-limits-proposal.md). Sybil direnci metodolojisi şu adrestedir: [XEQMLabs/xeqm-sybil-resistance](https://github.com/XEQMLabs/xeqm-sybil-resistance).

### Gelecekteki Ağ Taşıması Olarak Lokinet

EXIOM ağının adresleme altyapısı, kamuya açık olarak duyurulan IP adreslerinden Lokinet adreslemesine geçecektir. Lokinet önce HF23 öncesinde (hedef Q4 2026) zorunlu kılmayan bir sürümde yayınlanır; HF23 daha sonra Lokinet yönlendirme grafiğini kullanan yoğunlaşma zorunlu kılmasını ekler. Lokinet (Low Latency Anonymous Routing Protocol, LLARP), herhangi bir IP tabanlı trafiği çok-sekmeli soğan yönlendirmesi (onion routing) yoluyla birden fazla servis düğümü üzerinden yönlendiren, yoldaki hiçbir tek düğümün hem kaynağı hem hedefi bilmediği bir katman 3 soğan yönlendirme protokolüdür.

Lokinet aktif olduğunda:

- Servis düğümleri, kamuya açık olarak duyurulan bir IP adresi yerine Lokinet kriptografik tanımlayıcılarıyla adreslenecek
- EXIOM geliştirici API'si, bir `.loki` adresinde gizli bir hizmet olarak erişilebilir olacak ve geliştiricinin kaynak IP'sini API düğümünden gizleyecek
- RFQ ticaret platformu, gizli bir hizmet olarak erişilebilir olacak ve talep eden ile LP'nin IP adreslerini platformdan gizleyecek
- Kanıtlayan ile doğrulayıcı yeter sayısı arasındaki oracle oturumu iletişimi Lokinet üzerinden yönlendirilecek ve merkezî koordinatör güven varsayımını ortadan kaldıracak

Lokinet, HF23 öncesinde zorunlu kılmayan bir sürümde yayınlanır, hedef Q4 2026'dır ve HF23 bu sürüm oturduktan sonra izler. LLARP kod tabanı EXIOM deposunda mevcuttur; birincil ağ taşıması olarak Lokinet'in uygulanması Q4 2026'da başlar.

---

## 6. Bir Yarar Coin'i Olarak XEQM

XEQM talebi üç kaynaktan gelir. Düğüm teminatı, arzın en büyük payını, mevcut 943 aktif düğümde (27 Eylül 2026) yaklaşık %68'ini kilitler. Geliştirici tüketimi sürekli bir hız katmanı yaratır: uygulamalar üretim API kullanımını XEQM ile öder, böylece platform benimsenmesi doğrudan coin için yinelenen talebe dönüşür. Oracle erişimi, daha yüksek hacimli tüketiciler için üçüncü bir katman ekler.

Erişim, kilit-açmak-için-teminat kapısı yerine ön ödemeli, kullanıma dayalı bir modeli izler — geliştiricilerin geliştirmek için sabit bir teminat edinip kilitlemesi gerekmez:

| Katman | Erişim modeli |
|---|---|
| Ücretsiz | Hiçbir maliyet olmadan geliştirin ve değerlendirin: cömert bir aylık çağrı kotası, yatırma gerekmez |
| Üretim | Ön ödemeli kullanım: XEQM yatırın ve çağrı başına ödeyin; webhook'lar ve daha yüksek limitler |
| Kurumsal | Özel limitler, SLA ve destek; hacim koşulları |

Üretim kullanımı API çağrısı başına ölçülür ve geliştiricinin ön ödemeli XEQM bakiyesinden çekilir. Yatırmalar iade edilmez ve tüketildikçe platform geliri olarak kaydedilir (bkz. Bölüm 3). Daha önceki bir tasarım, katmanları sabit bir XEQM teminatının arkasına koyuyordu; bu, geliştiriciler için daha basit ve ticari API'ler için standart olan bu ön ödemeli modelle değiştirilmiştir.

---

## 7. Yönetişim ve Hazine

Yönetişim cüzdan adresi ve görüntüleme anahtarı yayımlanmıştır. Herkes bakiyeyi istediği zaman doğrulayabilir. Yönetişim şu anda, açık Telegram kanalları ve GitHub tartışmaları aracılığıyla topluluk katkısıyla, kurucu ekip üzerinden yürütülmektedir.

Bölüm 3'te açıklanan yönetişim emisyonundan çekilen hazine tahsisleri:

- Çekirdek geliştirme (%25): EXIOM API'si, oracle ve RFQ platformu için mühendislik
- Pazarlama ve farkındalık (%15): borsa listelemeleri, içerik, topluluk büyümesi
- Ekosistem ve topluluk (%10): hibeler, ödüller, entegrasyon desteği
- Güvenlik ve denetimler (%5): kod denetimleri, güvenlik incelemeleri, sızma testleri
- Uzun vadeli rezerv (%5): operasyonel istikrar ve acil durum rezervleri

Phase 3, resmi bir öneri ve yorum sürecini tanıtır. Phase 6, servis düğümü ve API düğümü operatörlerinin teminat ve kıdemle orantılı resmi haklara sahip olduğu ağırlıklı oylamayı tanıtır.

---

## 8. Parametre Özeti

| Parametre | Değer |
|---|---|
| Konsensüs mekanizması | 100% Proof-of-Stake |
| Blok süresi | 60 saniye |
| Blok ödülü | blok başına 8.25 XEQM |
| Günlük blok emisyonları | 11,880 XEQM |
| Yönetişim emisyonu | ~17,857 XEQM/gün |
| Tam düğüm gereksinimi | 200,000 XEQM |
| Minimum operatör teminatı | 100,000 XEQM (50%) |
| Maksimum operatör ücreti | 10% |
| Maksimum katkıcı slotu | 11 (operatör dâhil) |
| Minimum topluluk katkısı | slot başına 10,000 XEQM |
| Düğüm başına topluluk teminatçısı penceresi | 10 slot genelinde 100,000 XEQM'ye kadar |
| Bağ çözme süresi, gönüllü çekilme | 14 gün, ödüller devam eder |
| Bağ çözme süresi, zorunlu kayıt iptali | 14 gün, ödül yok (HF22) |
| Toplam arz | lansmanda 276,917,604 XEQM, takvimli emisyonlarla büyür |
| 943 düğümde kilitli arz (27 Eyl 2026) | ~188,600,000 XEQM (başlangıç arzının ~%68'i) |
| 943 düğümde serbestçe dolaşan | başlangıç arzında ~88,300,000 XEQM, emisyonlarla büyür |
| 943 düğümde tek operatör APY'si | ~2.3% (yalnızca blok ödülleri, HF21 ile haftalık ödenir) |
| Düğüm başına kendi kendine barındırma maliyeti | ~$0.53/ay ($5.28/ay VPS, 10 düğüm) |
| Yönetilen barındırma maliyeti (Pecunia) | $1.76/düğüm/ay |
| Aktif servis düğümleri (27 Eylül 2026) | 943 |
| Operatör Nakamoto katsayısı (27 Eyl 2026) | 9 — çoğunluk kontrolü; hedef >= 8; 943 düğüm, 204 operatör |
| Oracle harici etkinleştirme | Nakamoto >= 6'ya ulaşıldı; Phase 3 tamamlanmasına bağlı |
| Yeter sayı boyutu | tur başına 12 koltuk |
| Yeter sayı tekilleştirme, HF22 | tur başına yeter sayı koltuğu başına bir operatör cüzdan adresi |
| Yeter sayı tekilleştirme, HF23 | tur başına yeter sayı koltuğu başına bir yakınlık kümesi (Lokinet gerektirir) |
| Yeter sayı tekilleştirme yedeği, HF23 | 12'den az ayrı küme varsa, en yoğunlaşmış kümelerden önce en küçük kümeler ek koltuk alır; yedek sıklığı günlüğe kaydedilir ve yayımlanır |
| Ağ hayatta kalabilirliği tavanı, HF23 | yakınlık kümesi başına aktif düğümlerin %30'u (mevcut sayıda ~283 düğüm) |
| Sıfır-ödül düzenleyicisi, HF23 | küme tavanının üzerindeki düğümler için kayıt yaşına göre sıralanmış sıfır blok ödülü |
| Çekirdek depolar | github.com/XEQMLabs |

---

## 9. Yol Haritası

**Phase 1, Ağ istikrarı. TAMAMLANDI.** Servis düğümü ağı, 27 Eylül 2026 itibarıyla 943 aktif servis düğümüne büyüdü (Temmuz 2026'da 184 operatör genelinde 693, Nakamoto katsayısı 7 iken). XEQ'tan XEQM'ye coin takası başarıyla yürütüldü ve kapatıldı.

**Phase 2, EXIOM geliştirici API'si ve EXIOM Oracle. AKTİF.** EXIOM Oracle, bir operatör komitesiyle ana ağda yayındadır ve geliştirici API'si beta aşamasında yayındadır (self-servis kimlik bilgileri, uyumluluk ve doğrulama uç noktaları, OpenAPI). Kalan Phase 2 işi: ön ödemeli tüketim faturalandırması, operatör gelir payı ve ilk üretim entegrasyonları. EXIOM RFQ ticaret platformu geliştirmesi, ilk işlem çifti olarak XEQM/BTC ile paralel olarak ilerler.

**Phase 3, EXIOM Privacy Oracle ve RFQ platformu.** Oracle aşamalar hâlinde devreye alınır: dâhili kavram kanıtı, federe testnet, ardından dâhili tüketicilerle ana ağ. RFQ ticaret platformu bu aşamada, XEQM/BTC çiftinde özel fiyat tasdiki için oracle'ı kullanarak üretime ulaşır. Her ikisi de EXIOM API'si üzerine inşa edilmiştir.

**Phase 4, Harici oracle tüketici erişimi.** Oracle çıktıları Üretim ve Kurumsal katman geliştiricilerine ve harici tüketicilere sunulur. Nakamoto katsayısı eşiği olan 6'ya zaten ulaşıldı; etkinleştirme Phase 3 tamamlanmasına bağlıdır.

**HF22, etkinleştirildi (ana ağ bloğu 219120).** Lokinet bağımlılığı olmayan iki konsensüs değişikliği: operatör cüzdan-anahtarı yeter sayısı tekilleştirmesi (tur başına yeter sayı koltuğu başına bir operatör adresi) ve bağ çözme süresi birleştirmesi (zorunlu kayıt iptali 7 günden 14 güne uzatıldı), artı 18 Ekim 2026'da blok 236920'de etkinleşen ve Proof-of-Work kurtarmasını imza tabanlı bir yedekle değiştiren bir Pulse durma-kurtarma revizyonu (snode_revision 1). 20 durma/kurtarma döngüsü boyunca doğrulandı (%100 kurtarma, en kötü blok boşluğu 83 saniye).

**Lokinet ve hafif-düğüm sürümü, HF23 öncesi.** Lokinet'i ağ taşıması olarak çevrimiçi getiren (yakınlık kümelenmesi düğüm gezgininde yayında ve gözlemlenebilir, ödül sonucu yok) ve SQLite hafif-düğüm depolamasını tanıtan (düğüm başına daha düşük bellek ve disk, isteğe bağlı güncel-pencere hafif düğümleriyle) zorunlu kılmayan bir sürüm. Bu sürüm, herhangi bir zorunlu kılma devreye girmeden önce gerçek yakınlık-kümesi sayısının ölçülebilmesi ve HF23 eşiği ile yedeğinin ayarlanabilmesi için oturur.

**HF23, tasarım aşamasında, hedef Q4 2026.** Yukarıdaki zorunlu kılmayan Lokinet ve hafif-düğüm sürümü oturduktan sonra zorunlu kılmayı devreye alır: yakınlık kümesi kayıt tavanı (bir küme aktif düğümlerin %30'unu aştığında kayıtlar reddedilir); tavan eşiğinin üzerindeki düğümler için kayıt yaşına göre sıralanmış sıfır-ödül düzenleyicisi; yeter sayı tekilleştirmesinin cüzdan-anahtarından yakınlık kümesine yükseltilmesi, 12'den az ayrı küme olduğunda bile yeter sayı oluşumunu her zaman mümkün kılan zorunlu bir yedek kuralıyla (en yoğunlaşmış kümelerden önce en küçük kümeler ek koltuk alır, yedek sıklığı günlüğe kaydedilir ve bir yoğunlaşma riski göstergesi olarak yayımlanır). Sıfır-ödül düzenleyicisi yürürlüğe girmeden önce etkinleştirmede 30 günlük bir ödeme müsamahası uygulanır.

**Phase 6, Resmi yönetişim.** Yapılandırılmış öneri süreci, operatörler için ağırlıklı oylama, kurucu-ekip yönetişiminden uzun vadeli geçiş.

---

## 10. EXIOM Oracle

### İlk yayındaki oracle: EXIOM Oracle

Platformun ilk oracle ürünü ana ağda yayındadır. EXIOM Oracle, her biri düğümünün yanında hafif bir oracle yan-birimi çalıştıran XEQM servis düğümü operatörlerinden oluşan bir komitedir; bu komite, uyumluluk olguları hakkında, en doğrudan olarak belirli bir adresin belirli bir yargı bölgesi için uygun olup olmadığı hakkında, BLS-toplamalı, EIP-712 imzalı tasdikleri toplu olarak üretir. Uygulamalar bu tasdikleri geliştirici API'si aracılığıyla tüketir ve imzalı sonucu zincir üstüne gönderebilir. Komite, Robinhood Chain (chainId 4663) üzerinde dağıtılmıştır ve 28 Eylül 2026 itibarıyla üçte iki (8/12) imzalama eşiğiyle 12 üyeli bir operatör komitesi çalıştırır.

**Güvenlik modeli: kayıtlı küme karşısında eşik.** EXIOM Oracle, tur başına bir komite örneklemez. Bir BLS toplamını doğrulamak, sekiz üye mi yoksa sekiz yüz üye mi imzaladı fark etmeksizin gate'e aynı maliyeti çıkardığı için, her kayıtlı üye her tur imzalar; bir alt küme örneklemek hiçbir şey kazandırmaz ve şanssız bir çekilişin sahte üretecek kadar iş birliği yapan üye tutması riskini yeniden ortaya çıkarır. Bu nedenle güvenlik, gate'in zorunlu kıldığı üçte iki eşikte k = ceil(2N/3) olmak üzere, N boyutundaki kayıtlı üye kümesinin iki özelliğine indirgenir:

- **Sahtecilik (Forgery)**, bir saldırganın en az k kayıtlı üyeyi kontrol etmesini gerektirir — bir iş birliği, dolayısıyla bir **operatör** yoğunlaşması sorunu.
- **Durma (Halt)** (bir canlılık başarısızlığı), en az N - k + 1 = floor(N/3) + 1 kayıtlı üyenin aynı anda devre dışı kalmasını gerektirir — bağıntılı bir kesinti, dolayısıyla bir **altyapı** yoğunlaşması sorunu.

Bunlar iki Nakamoto katsayısıdır ve daha geniş servis-düğümü filosunun değil, kayıtlı kümenin özellikleridir: filonun dağılımı konsensüsü sınırlarken, oracle'ın sahtecilik ve canlılık direnci yalnızca kayıtlı koltukları kimin tuttuğuna bağlıdır.

**Mevcut gerçekleşme.** 28 Eylül 2026 itibarıyla kayıtlı üyelerin tümü proje operatörü tarafından işletilmektedir, bu nedenle oracle'ın operatör katsayısı 1'dir: bugün sahtecilik direnci dağıtık kriptografiye değil, tek bir operatöre duyulan güvene dayanır. Bu, dürüst başlangıç durumudur. Güvenlik modeli, bağımsız operatörler genelinde k-of-N'dir; gerçekleşme, bağımsızlar kaydoldukça sertleşir ki ek servis-düğümü operatörlerini yan-birim üyeleri olarak dâhil etmenin amacı budur. Düğüm sayısı tek başına yardımcı olmaz — ek üyeler her iki katsayıyı yalnızca farklı tesislerdeki bağımsız operatörler oldukları ölçüde yükseltir.

**Çeşitlilik nasıl zorunlu kılınır.** Tur başına seçim olmadığı için, çeşitliliğe **kabul** aşamasında karar verilir: bir üye yalnızca her operatörün payını k'nin altında ve her tesisin payını floor(N/3) seviyesinde veya altında tutuyorsa kaydedilir ve küme büyüdükçe k, ceil(2N/3)'ü izleyecek şekilde yükseltilir. Kayıtlı kümenin yoğunlaşması sürekli izlenir ve bir sahtecilik marjı (k eksi en büyük operatörün payı) ve bir canlılık marjı (floor(N/3) + 1 eksi en büyük tesisin payı) olarak yayımlanır; pozitif olmayan bir marj bir alarmdır. Tesis sinyali bugün ASN ve çalışma-süresi kanıtı varış-zamanlamasıdır; HF23'te Lokinet yönlendirme yakınlığına keskinleştirilir ki bu, farklı ASN'ler arasında bile fiziksel aynı-yerde-bulunmayı tespit eder. Bu dağılım olguları, oracle'ın tipli-olgu arayüzü aracılığıyla kendileri de tasdik edilebilir, böylece yoğunlaşma metriği, tek bir güvenilen betiğin çıktısı değil, komite-imzalı bir değerdir.

Yan-birim kasıtlı olarak hafiftir: yalnızca kendi imzalama anahtarını tutar, düğümünün kimliğini yerel olarak okur ve operatörün harcama anahtarlarını asla ele almaz. Onu çalıştırmak, bir servis-düğümü operatörünün Bölüm 3 ve 4'te açıklanan ek, kullanım-fonlu geliri elde etmesinin mekanizmasıdır.

### Daha geniş vizyon: EXIOM Privacy Oracle

EXIOM Privacy Oracle, uygulamaların altta yatan kaynak verisini ifşa etmeden kimliği doğrulanmış özel veri akışlarını tüketmesini sağlar. Standart HTTPS uç noktalarından veri kökenini kanıtlamak için, sunucu tarafı iş birliği ve güvenilir donanım gerektirmeden sıfır-bilgi kanıt teknikleri kullanır. Bu bir Phase 3 teslimatıdır; Phase 2 API platformu istikrarını ve tam yapı başlamadan önce bir kriptografi danışmasını izler.

Oracle, genel amaçlı bir veri akışı değildir. Verinin kendisinin gizli kalması gereken kullanım durumları için gizlilik-öncelikli bir oracle'dır: tam fiyatları açıklamadan fiyat eşikleri, kimlik bilgilerini ifşa etmeden hesap bakiyeleri, altta yatan kaydı açıklamadan uyumluluk tasdikleri. EXIOM RFQ platformu, bir XEQM/BTC işleminin tam fiyatı platforma veya diğer tarafa açıklamadan bir referans fiyatta veya daha iyisinde gerçekleştiğini kanıtlamak için onu kullanan ilk dâhili tüketicidir.

Lokinet ağ taşıması olarak aktif olduğunda, kanıtlayan ile doğrulayıcı yeter sayısı arasındaki oracle oturumu iletişimi servis düğümü ağı üzerinden soğan-yönlendirmeli olacaktır. Ne kanıtlayanın kökeni ne de yeter sayı düğümlerinin ağ adresleri herhangi bir tek aktarma düğümüne görünür olacak; bu da merkezî koordinatör güven varsayımını ortadan kaldırır.

### Mimari

**Kanıtlayan katmanı.** Özel veri kaynağına erişimi olan uygulama veya kullanıcı, TLS yanıtını ifşa etmeden ona taahhütte bulunan bir kriptografik protokole katılır. Kimlik bilgileri ve ham veri kanıtlayanın kontrolünden asla çıkmaz.

**Doğrulayıcı katmanı.** Dönüşümlü bir servis düğümü yeter sayısı, taahhüt edilen verinin istenen koşulu karşılayıp karşılamadığını doğrular. Doğrulayıcı düğümler yalnızca sonucu (doğru ya da yanlış, bir eşiğin üstünde ya da altında) öğrenir ve altta yatan veriyi veya kimlik bilgilerini asla görmez.

**Tüketici katmanı.** Tüketiciler yalnızca minimum çıktıyı alır: bir boolean sonuç, bir eşik karşılaştırması, imzalı bir tasdik veya küçük bir türetilmiş değer. Ham kaynak verisi asla yayımlanmaz.

### Aşamalı Yapı Planı

**Phase 1, Dâhili kavram kanıtı.** Kurucu ekip, tam kriptografik protokolü küçük bir beyaz-listeli kaynak kümesine karşı uçtan uca doğrular; harici tüketici veya servis düğümü katılımı yoktur.

**Phase 2, Federe oracle testnet'i.** Güçlü çalışma süresi geçmişine sahip gönüllü servis düğümü operatörleri, testnet'te doğrulayıcı havuzuna katılır. Herhangi bir ana ağ dağıtımından önce tasdik bütünlüğünün düşmanca test edilmesi.

**Phase 3, Dâhili tüketicilerle ana ağ oracle'ı.** Oracle doğrulayıcı görevi, uygun ana ağ düğümlerine açılır. Çıktılar dâhili EXIOM sözleşmelerini ve RFQ platformunu besler. Oracle ücretleri, katılan doğrulayıcı düğümlere akmaya başlar.

**Phase 4, Harici tüketici erişimi.** Oracle çıktıları Üretim ve Kurumsal katman geliştiricilerine ve harici tüketicilere sunulur. Phase 3 tamamlanmasına bağlıdır.

### Doğrulayıcı Donanım Gereksinimleri

Gösterge niteliğinde gereksinimler: 8 CPU çekirdeği, 16 GB RAM, 200 GB SSD, düşük gecikmeli 500 Mbps. Standart API düğümü temel donanımı, oracle doğrulayıcı görevi için yeterli değildir.

### Doğrulayıcı Ödülleri

| Gelir Kaynağı | Açıklama |
|---|---|
| Blok ödülleri | Standart servis düğümü blok ödülü, değişmedi |
| Platform gelir payı | Oracle yan-birimini çalıştıran operatörler için geliştirici-tüketim gelirinin orantılı payı |
| Oracle oturumu ücretleri | Oracle tüketicilerinden oturum başına ücret, doğrulayıcı yeter sayısına dağıtılır |
| Oracle görev primi | Düşük-hacimli dönemlerde ek yönetişim emisyonu, oturum ücretleri kendi kendini sürdürdükçe azaltılır |

---

## 11. EXIOM RFQ Ticaret Platformu

EXIOM RFQ platformu, EXIOM API'si üzerine inşa edilmiş, kriptografik takas tasdikli, eşler arası tezgahüstü bir ticaret sistemidir. İlk işlem çifti, her ikisi de tokenleştirme, sarmalama ve köprü riski olmayan yerel Katman 1 varlıkları olan XEQM/BTC'dir.

Lokinet aktif olduğunda, RFQ platformu bir Lokinet gizli hizmeti olarak erişilebilir olacaktır. Ne talep edenin ne de LP'nin IP adresi platforma görünür olacaktır. Oracle fiyatlandırma katmanı, bir karşı tarafın bir işlemin, tam işlem fiyatını platforma veya diğer tarafa açıklamadan, beyaz-listeli bir kaynaktan bir referans fiyatta veya daha iyisinde gerçekleştiğini kanıtlamasına olanak tanır.

RFQ uygulama spesifikasyonu ve veri modeli tamamlanmıştır. Aktif geliştirme, API katmanında Phase 2'de ilerlemektedir. Tam ticaret platformu üretimi, EXIOM API'sinin üretime ulaşmasına ve oracle MVP'sinin dâhili kavram kanıtını tamamlamasına bağlı bir Phase 3 teslimatıdır.

---

---

## Mevcut Diller (Available Languages)

Bu teknik dokümanın topluluk çevirileri, kolaylık amacıyla translations klasöründe tutulmaktadır. **İngilizce sürüm her zaman tek yetkili belgedir.** Çeviriler mevcut İngilizce revizyonun gerisinde kalabilir ve güncel olmaları garanti edilmez; herhangi bir çelişki, belirsizlik veya herhangi türde bir farklılık durumunda İngilizce sürüm geçerlidir.

| Language | Whitepaper |
|---|---|
| Español | [translations/es/README.md](./translations/es/README.md) |
| Français | [translations/fr/README.md](./translations/fr/README.md) |
| Deutsch | [translations/de/README.md](./translations/de/README.md) |
| 中文 | [translations/zh/README.md](./translations/zh/README.md) |
| Português | [translations/pt/README.md](./translations/pt/README.md) |
| Türkçe | [translations/tr/README.md](./translations/tr/README.md) |
| Polski | [translations/pl/README.md](./translations/pl/README.md) |
| Bahasa Indonesia | [translations/id/README.md](./translations/id/README.md)

---

*Bu bir taslak belgedir. Burada açıklanan parametreler, emisyon takvimleri ve yol haritası aşamaları amaçlanan tasarımdır. Ağ ve platform geliştikçe güncellemeler yayımlanacaktır.*

*Bu belge finansal veya yasal tavsiye teşkil etmez. XEQM, EXIOM platformu için bir yarar coin'idir, bir yatırım ürünü değildir. Token sınıflandırması, menkul kıymet statüsü ve geçerli düzenlemeler yargı bölgesine göre değişir. Katılımcılar, XEQM edinmeden veya XEQM ile işlem yapmadan önce kendi yerel hukuki ve düzenleyici çerçevelerine danışmalıdır. XEQM Labs, spekülatif fiyat artışı temelinde XEQM satın alınmasını teşvik etmez.*
