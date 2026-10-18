# Sybil Riski ve EXIOM'un Azaltma Modeli
## EXIOM Tokenomi Teknik Dokümanı'na Teknik Ek
### 07/26/2026

> **Not (Ekim 2026'da güncellendi).** Yoğunlaşma, *yakınlık kümesi* başına (paylaşılan fiziksel veya yönlendirme altyapısı) zorunlu kılınır, **ülke başına değil**. Buradaki düğüm rakamları bir Temmuz 2026 anlık görüntüsüdür; güncel toplamlar için teknik dokümana bakın. Lokinet, HF23 öncesinde zorunlu kılmayan bir sürümde yayınlanır ve HF23 zorunlu kılmayı devreye alır.

Bu belge, EXIOM Tokenomi Teknik Dokümanı'na ve Düğüm Yoğunlaşma Limitleri önerisine bir ektir ve her ikisinin de okunduğunu varsayar. Teknik doküman, kontrollerin ne olduğunu ele alır. concentration-limits-proposal, her bir kontrolün nasıl çalıştığının mekaniğini ele alır. Bu belge tehdit modelini ele alır: bir Sybil saldırısının bir gizlilik zincirinde gerçekte neye benzediği, EXIOM'un mimarisini özellikle dirençli veya savunmasız kılan şey ve devam eden izleme metodolojisinin yoğunlaşmayı pratikte nasıl tespit ettiği.

---

## Bir Gizlilik Zincirinde Sybil Tehdidi

Bir servis düğümü ağında Sybil saldırısı, tek bir aktörün orantısız etki kazanmak için farklı görünen kimlikler altında birçok düğüm işletmesi anlamına gelir. Şeffaf bir blok zincirinde, cüzdan grafiği analizi genellikle birden fazla düğüm operatörü adresinin ortak bir kaynaktan fonlandığını ortaya çıkarabilir ve Sybil'i açığa çıkarabilir. Bir gizlilik zincirinde, bu araç tasarım gereği mevcut değildir. Kullanıcı işlemlerini koruyan gizlilik garantisi, aynı zamanda en yaygın Sybil tespit yöntemini de ortadan kaldırır.

Bu nedenle EXIOM'un Sybil yüzeyi, şeffaf bir zincirinkinden belirli bir şekilde farklıdır: gizlilik özelliklerini doğru kullanan bir operatör, kontrol ettiği sermaye miktarından bağımsız olarak, protokol düzeyinde ilişkisiz görünen birden fazla cüzdan adresi sunabilir. Bu, gizlilik tasarımında bir kusur değildir. İşlem grafiği analizi dışındaki mekanizmalar aracılığıyla ele alınması gereken her gizlilik zincirinin doğasında olan bir özelliktir.

EXIOM'daki iki Sybil saldırı yüzeyi farklıdır ve ayrı kontroller gerektirir:

**Konsensüs etkisi saldırısı.** Bir operatör, herhangi bir cüzdan yapısı aracılığıyla, aynı anda orantısız sayıda yeter sayı koltuğu tutacak kadar düğüm biriktirir. Bu, bireysel teminat oranlarının adil göstereceğinin ötesinde oracle oturumu sonuçlarını, Pulse turlarını ve yükümlülük yeter sayılarını etkilemelerine olanak tanır. Zarar, zorunlu olarak ağ çalışma süresine değil, konsensüs bütünlüğünedir.

**Arıza alanı saldırısı.** Bir operatör düğümleri tek bir fiziksel tesiste yoğunlaştırır. Bu bir saldırı olarak kasıtlı olabilir veya olmayabilir; maliyet optimizasyonundan kaynaklanabilir. Zarar, ağ hayatta kalabilirliğinedir: bir tesis kesintisi operatörün düğümlerini aynı anda çevrimdışı bırakır ve yoğunlaşma yeterince büyükse potansiyel olarak blok üretimini durdurur.

---

## EXIOM'u Yapısal Olarak Dirençli Kılan Şey

**Kimlik başına sermaye maliyeti.** Kimliklerin ücretsiz olduğu saf Sybil saldırılarının aksine, her EXIOM servis düğümü, operatörün kişisel olarak en az 100,000 XEQM teminatıyla, 200,000 XEQM teminat gerektirir. 100 düğüm çalıştıran bir operatörün 10,000,000 XEQM sermayesi teminatlı ve kilitlidir. Cüzdan bölme yoluyla ek görünen kimlikler oluşturmak bu maliyeti azaltmaz -- her düğüm hâlâ 100,000 XEQM operatör teminatı gerektirir. Sybil saldırısı her ölçekte pahalıdır.

**Bağ çözme sürtünmesi.** Hem gönüllü çekilmede hem de zorunlu kayıt iptalinde 14 günlük bir bağ çözme süresi, Sybil düğümlerine bağlanan sermayenin hızla çıkarılamayacağı anlamına gelir. Çıkmaya karar veren bir saldırgan, bunu diğer herhangi bir operatörden daha hızlı yapamaz.

**Kamuya açık düğüm kaydı.** Her servis düğümünün kayıt anahtarı ve operatör cüzdan adresi kamuya açıktır. Bir düğüm konsensüse anonim olarak katılamaz. Bir cüzdan adresinin arkasındaki insan kimliği özel olsa da, düğümün operasyonel parmak izi, kayıt kalıpları, çalışma süresi kanıtı zamanlaması ve yönlendirme davranışı aracılığıyla zaman içinde birikir.

---

## İşlem Grafiği Analizi Olmadan Yoğunlaşma Nasıl Tespit Edilir

İşlem düzeyinde analiz mevcut olmadığından, EXIOM'un yoğunlaşma tespiti, fonlama geçmişi yerine düğüm davranışından gözlemlenebilen dört sinyale dayanır.

**Kayıt anahtarı kümelenmesi.** Aynı operatör cüzdan anahtarı altında kayıtlı düğümler kesinlikle aynı operatördür. Bu, zincir-üstü verilerden deterministiktir. Cüzdan bölmeyen büyük bir operatör, tek başına bu sinyal aracılığıyla tamamen görünürdür. Ağdaki mevcut en büyük dağıtımlar, tek IP adreslerinden sırasıyla 58 ve 51 düğüm çalıştıran düğümler dâhil, kayıt anahtarı analizi aracılığıyla doğrulanmış her biri tek operatördür.

**IP adresi ve alt ağ kümelenmesi.** Şu anda birincil fiziksel aynı-yerde-bulunma sinyali. Aynı IP adresinden birden fazla düğüm neredeyse kesinlikle aynı sunucudadır. Aynı alt ağdan birden fazla düğüm aynı barındırma hesabını veya veri merkezi bloğunu önerir. Bu sinyal bugün herhangi bir daemon değişikliği olmadan mevcuttur ve Lokinet etkinleştirmesinden sonra tamamlayıcı bir sinyal olarak kalacaktır.

**Çalışma süresi kanıtı zamanlaması bağıntısı.** Ağ, her aktif düğümden düzenli bir takvimde çalışma süresi kanıtları alır. Bu kanıtların varış zaman damgası dağılımı, alıcı düğümler tarafından kaydedilir. Aynı fiziksel sunucu veya VM hipervizöründe çalışan düğümler, aynı sistem saatini ve ağ arayüzünü paylaştıkları için kanıtları tipik olarak 10 milisaniyenin altında karakteristik bir sıkı pencere içinde gönderir. Kanıtları tutarlı biçimde bu pencere içinde gelen farklı cüzdan anahtarlarından bir düğüm kümesi, herhangi bir daemon değişikliği olmadan ve Lokinet aktif olmadan tespit edilebilen, paylaşılan fiziksel altyapının güçlü bir sinyalidir.

Bu sinyal, düğümlerini paylaşılan altyapıda tutan cüzdan bölen operatörleri tanımlamak için özellikle yararlıdır. Cüzdan anahtarları farklıdır; kanıt zamanlaması farklı değildir.

**Lokinet yönlendirme yakınlığı (HF23 öncesinde zorunlu kılmadan yayınlanır; HF23'te zorunlu kılınır).** Lokinet ağ taşıması olarak aktif olduğunda, yönlendirme grafiği düğüm ağının sürekli bir fiziksel topoloji haritasını sağlar. Aynı tesisteki düğümler aynı yukarı-akış altyapısı üzerinden yönlendirir ve cüzdan anahtarlarından veya duyurulan IP adreslerinden bağımsız olarak bağıntılı yol seçimleri ve milisaniye-altı düğümler-arası gecikme üretir. Bu en sağlam sinyaldir çünkü gerçekten altyapı taşınmadan yazılım yapılandırmasıyla değiştirilemeyen fiziksel ağ gerçekliğini yansıtır.

---

## Cüzdan-Bölme Saldırısı Ayrıntılı Olarak

EXIOM'da mevcut en gelişmiş Sybil yaklaşımı cüzdan bölmedir: düğümleri, ortak fonlama kaynağı görünmeyecek şekilde gizlilik zincirinin işlem katmanı aracılığıyla fonlanan birden fazla cüzdan adresi altında kaydetmek. Bu, kayıt anahtarı kümelenmesi sinyalini aşar ama diğerlerini aşmaz.

Tümü aynı Contabo tesisinde barındırılan 10 cüzdan genelinde 426 düğüm çalıştıran bir operatör şunlarla açığa çıkar:

- Çalışma süresi kanıtı zamanlaması: 426 düğümün tümünden gelen kanıtlar, paylaşılan altyapının karakteristik 10ms-altı penceresinde gelir
- IP ve alt ağ analizi: birden fazla IP olsa bile, veri merkezi bloğu ataması ve ASN paylaşılır
- Lokinet yakınlığı (HF23-sonrası): 426 düğümün tümü, cüzdan anahtarından bağımsız olarak aynı Contabo omurgası üzerinden yönlendirir

10 farklı ülkedeki 10 farklı sağlayıcı genelinde gerçekten dağıtılmış, 10 cüzdan genelinde 426 düğüm çalıştıran bir operatör, mevcut hiçbir sinyalle anlamlı biçimde açığa çıkmaz. Kayıt anahtarları farklıdır, altyapı farklı olduğu için kanıt zamanlaması farklıdır, ASN'ler farklıdır ve Lokinet yolları farklıdır. Protokol düzeyinde bu, 10 farklı operatör gibi görünür.

Bu, tüm kontroller uygulandıktan sonra EXIOM'daki artık Sybil riskidir. Sonuçları bakımından sınırlıdır: HF23 yeter sayı tekilleştirmesi, cüzdan yapısından bağımsız olarak her yakınlık kümesini tur başına bir yeter sayı koltuğuyla sınırlar, bu nedenle dağıtık bir cüzdan bölen operatör bile sınırsız konsensüs etkisi kazanmaz. Blok ödülü gelirleri düğüm sayılarıyla ölçeklenir ki bu adildir çünkü orantılı sermaye teminatlamışlardır. Tur başına konsensüs etkileri, kaç cüzdan kullandıklarından bağımsız olarak küme tekilleştirmesiyle sınırlıdır.

---

## Devam Eden İzleme Metodolojisi

**Yönetişim engel listesi.** Yönetişim tarafından yönetilen bir açık anahtar engel listesi, engellenen kayıt anahtarlarının yeni düğümler kaydetmesini engeller. Orijinali engellenirken yeni bir cüzdan anahtarına geçen bir operatör, belgelenmiş bir kaçınma kaydı oluşturur ve yeni anahtarın kanıt zamanlaması ile yönlendirme davranışı, engellenen anahtarın geçmiş profiline karşı bağıntılandırılır.

**Katkıcı slotu grafiği analizi.** Servis düğümü katkıcı slotları ikincil bir kimlik sinyalidir. Katkıcı slotlarını kendi cüzdan anahtarlarının birden fazlası genelinde fonlayan bir operatör, bir gizlilik zincirinde bile gözlemlenebilir bir ilişki grafiği oluşturur, çünkü katkıcı kayıt işlemleri hangi düğümlere katkıda bulunduklarına dair gözlemlenebilir veri taşır. Cüzdan A altında kayıtlı düğümlere B ve C cüzdanlarından tutarlı biçimde katkıda bulunan, aynı zamanda o B ve C cüzdanları kendi düğümlerini kaydeden bir operatör, doğrudan kayıt anahtarı kümelenmesi sinyalini tamamlayan bir bağıntı grafiği oluşturur.

**ASN izleme.** Her aktif düğümün IP'si, kamuya açık BGP verileri aracılığıyla bir Autonomous System Number ile eşleşir. Ağ, aktif düğüm kümesi genelinde ASN yoğunlaşmasını izler. Bir ASN paylaşan düğümler, sağlayıcı düzeyinde altyapıyı ve yasal maruziyeti paylaşır. Bireysel düğüm kayıtları ilişkisiz görünse bile yüksek ASN yoğunlaşması yönetişim incelemesi için işaretlenir. ASN sinyali bir insan operatörü tanımlamaz, ancak bir arıza alanı tanımlar.

Bu belgede açıklanan tüm kontroller için mevcut uygulama durumu, [Düğüm Yoğunlaşma Limitleri önerisinde](https://github.com/XEQMLabs/whitepaper/blob/main/concentration-limits-proposal.md) tutulmaktadır.

---

*Bu belge finansal veya yasal tavsiye teşkil etmez. XEQM, EXIOM platformu için bir yarar coin'idir, bir yatırım ürünü değildir. Token sınıflandırması, menkul kıymet statüsü ve geçerli düzenlemeler yargı bölgesine göre değişir. Katılımcılar, XEQM edinmeden veya XEQM ile işlem yapmadan önce kendi yerel hukuki ve düzenleyici çerçevelerine danışmalıdır. XEQM Labs, spekülatif fiyat artışı temelinde XEQM satın alınmasını teşvik etmez.*
