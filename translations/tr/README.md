# XEQM Labs - EXIOM Platformu
## Token Ekonomisi Teknik Belgesi
### Taslak v11 | 26.07.2026

> *Bu çeviri, yapay zeka çeviri araçları kullanılarak üretilmiştir. Yalnızca bilgilendirme amacıyla sunulmaktadır. Bu çeviri ile İngilizce orijinal arasında herhangi bir çakışma veya belirsizlik olması durumunda, İngilizce versiyon geçerlidir. İngilizce versiyon [github.com/XEQMLabs/whitepaper](https://github.com/XEQMLabs/whitepaper) adresinde bulunabilir.*

---

## Bugün Aktif Olanlar vs. Planlanananlar

| Bileşen | Durum |
|---|---|
| EXIOM ana ağı | Aktif, 6 Mayıs 2026'dan beri çalışıyor |
| Servis düğümü ağı | Aktif, 693 aktif düğüm, 184 operatör (Temmuz 2026) |
| Lokinet (LLARP) | Kod tabanında mevcut, aktivasyon durumu mühendislik değerlendirmesinde |
| XEQ'den XEQM'ye coin takası | Teslim edildi ve kapatıldı, 35 günlük üretim çalışması, halka açık denetlenebilir defter |
| GUI cüzdanı | Aktif, github.com/XEQMLabs/XEQMLabs-GUI |
| Düğüm gezgini | Aktif, aktif servis düğümü izleme |
| EXIOM geliştirici API'si | Geliştirme aşamasında, Faz 2 (AKTİF) |
| EXIOM Gizlilik Oracle'ı | Tasarlandı, ön uygulama, Faz 3 |
| EXIOM RFQ ticaret platformu | Geliştirme aşamasında, Faz 2/3, ilk çift XEQM/BTC |
| HF22, cüzdan anahtarı quorum tekilleştirme ve kilit açma birleşimi | Test ağına giriyor, doğrulandı, Lokinet bağımlılığı yok |
| HF23, yakınlık kümesi limiti, ödül değiştiricisi, Lokinet taşıması | Tasarım aşaması, Lokinet mühendislik değerlendirmesi bekleniyor |
| Resmi zincir içi yönetim | Planlandı, Faz 6 |

---

## 1. XEQM Labs Nedir

XEQM Labs bir gizlilik teknolojisi şirketidir. Amiral gemisi ürünü EXIOM, küresel bir servis düğümü seti tarafından işletilen, gizliliği koruyan bir Proof-of-Stake Layer 1 ağı ve ticari geliştirici platformudur. XEQM, platformun erişim ve kullanım coindir.

Proje, yedi yılı aşkın bir topluluğu ve operasyonel geçmişi sürdürmektedir. EXIOM ana ağı, bu topluluğa doğrulanabilir bir arz, öngörülebilir bir emisyon takvimi, Proof-of-Work bileşeni olmayan saf Proof-of-Stake konsensüsü sağlamak için inşa edilmiştir.

XEQM, başka hiçbir zincirde tokenize edilmemiş, ERC-20 veya sarılmış varlık olmayan ve köprüsüz yerel bir Layer 1 coindir. Sahipler doğrudan EXIOM ana ağıyla etkileşime girer.

### EXIOM Ürün Ailesi

**EXIOM Servis Düğümü Ağı.** Ana ağda aktif. Temmuz 2026 itibarıyla 184 bağımsız operatörde 693 aktif düğüm.

**EXIOM Coin Takası.** Projelerin sahip topluluklarını tam kriptografik denetlenebilirlikle eski bir zincirden yeni bir zincire taşımasını sağlayan ticari bir ürün. Pilot uygulama, XEQ sahiplerinin XEQM'ye geçişiydi; 35 gün boyunca her gönderim, kamuya açık SHA256 parmak izi içeren kriptografik olarak doğrulanmış bir defterde işlendi.

**EXIOM Özel Geliştirici API'si.** Geliştirme aşamasında. Ağın gizlilik yeteneklerini yapılandırılmış bir API aracılığıyla sunan geliştirici platformu. Faz 2, aktif.

**EXIOM Gizlilik Oracle'ı.** Tasarlandı, ön uygulama. Temel kaynağı açığa çıkarmadan özel web verilerini kanıtlayan gizlilik odaklı bir oracle. Faz 3.

**EXIOM RFQ Ticaret Platformu.** Geliştirme aşamasında. Kriptografik uzlaşma doğrulamalarıyla EXIOM API'si üzerine kurulu eşten eşe tezgah üstü ticaret platformu. İlk ticaret çifti XEQM/BTC. Faz 2/3.

XEQM Labs, spekülatif fiyat artışına dayalı XEQM satın alımını teşvik etmez.

---

## 2. Arz Kaynağı

Geçiş tamamlandı. Eski varlıklar karşılığında EXIOM ana ağında 276.917.604 XEQM ihraç edildi. Bu rakam, 6 Mayıs 2026'daki ana ağ lansmanındaki doğrulanmış başlangıç arzıdır. Her eski mevduat, SHA256 parmak iziyle kamuya açık bir deftere kaydedildi. Takasla ilgili her cüzdanın harcama anahtarları yayımlandı.

**Takdiri ihraç yok.** Protokol geçici ihraç, manuel arz ayarlamaları veya plansız basımlara izin vermez.

**Yakma yok.** Bu ağın kriptografik mimarisi, bu terimin genellikle kullanıldığı şekliyle kanıtlanabilir yakmaları desteklememektedir. Hiçbir cüzdanı yakma adresi olarak temsil etmeyeceğiz.

---

## 3. Token Ekonomisi Modeli

Ağ her 60 saniyede bir yeni blok üretir ve seçilen servis düğümüne 8,25 XEQM verir, günde 11.880 XEQM üretir. 700 aktif düğümde her düğüm günde yaklaşık 17,0 XEQM veya ayda 516 XEQM kazanır.

Hazine günde yaklaşık 17.857 XEQM alır. Bu, platform gelir öncesi aşamasındaki aktif ticari yazılım geliştirme ekibinin operasyonel bütçesidir.

### Emisyon Dağılımı

| Tahsis | Pay | Amaç |
|---|---|---|
| Servis Düğümü Ödülleri | %40 | Doğrudan servis düğümlerine ödenen blok ödülleri |
| Temel Protokol Geliştirme | %25 | Blok zinciri, EXIOM platformu ve temel ağ hizmetleri |
| Pazarlama ve Farkındalık | %15 | Ağ görünürlüğü ve benimseme |
| Ekosistem ve Topluluk | %10 | Hibeler, ödüller, topluluk primleri |
| Güvenlik ve Denetimler | %5 | Denetimler ve güvenlik incelemeleri |
| Uzun Vadeli Rezerv | %5 | Kararlılık ve acil ihtiyaçlar |

### EXIOM Platform Ücreti Dağılımı

| Alıcı | Pay |
|---|---|
| API Düğümü Operatörleri | %35 |
| XEQM Labs Hazinesi | %35 |
| Topluluk Yönetimi | %30 |

---

## 4. Servis Düğümü Yapısı

| Parametre | Değer |
|---|---|
| Tam düğüm gereksinimi | 200.000 XEQM |
| Minimum operatör stake'i | 100.000 XEQM (%50) |
| Maksimum operatör ücreti | %10 |
| Kilit açma süresi, gönüllü çekilme | 14 gün, ödüller devam eder |
| Kilit açma süresi, zorla kaydı silme | 14 gün, ödül yok (HF22) |
| Maksimum katkıda bulunan slot sayısı | 11 (operatör dahil) |
| Slot başına minimum topluluk katkısı | 10.000 XEQM |

### Düğüm Ekonomisi

Aylık yaklaşık 5,28 USD karşılığında ücretli bir VPS, 10 servis düğümünü çalıştırabilir ve düğüm başına maliyeti yaklaşık aylık 0,53 USD'ye düşürür. Pecunia aracılığıyla yönetilen barındırma, düğüm başına aylık 1,76 USD karşılığında mevcuttur.

| Fiyat | Brüt/ay | Net: kendi barındırma ($0,53) | Net: Pecunia ($1,76) | 200k stake APY |
|---|---|---|---|---|
| $0,01547 (bugün) | $0,008 | -$0,52 | -$1,75 | %3,1 |
| $0,05 | $0,026 | -$0,50 | -$1,73 | %3,1 |
| $0,10 | $0,052 | -$0,48 | -$1,71 | %3,1 |
| $0,25 | $0,129 | -$0,40 | -$1,63 | %3,1 |
| $0,50 | $0,258 | -$0,27 | -$1,50 | %3,1 |
| $1,00 | $0,516 | -$0,01 | -$1,24 | %3,1 |
| $2,00 | $1,032 | +$0,50 | -$0,73 | %3,1 |
| $5,00 | $2,580 | +$2,05 | +$0,82 | %3,1 |

---

## 6. Yardımcı Coin Olarak XEQM

| Kademe | Gerekli Stake | Dahil Çağrılar |
|---|---|---|
| Ücretsiz | Yok | Ayda 10.000 test ağı çağrısı |
| Builder | 1.000 XEQM | Ayda 100.000 ana ağ çağrısı |
| Üretim | 10.000 XEQM | Ayda 1.000.000 çağrı, webhook'lar, öncelikli destek |
| Kurumsal | 50.000 XEQM | Sınırsız çağrı, özel hız sınırları, SLA |

---

## 8. Parametre Özeti

| Parametre | Değer |
|---|---|
| Konsensüs mekanizması | %100 Proof-of-Stake |
| Blok süresi | 60 saniye |
| Blok ödülü | Blok başına 8,25 XEQM |
| Günlük blok emisyonları | 11.880 XEQM |
| Yönetim emisyonu | Günde ~17.857 XEQM |
| Tam düğüm gereksinimi | 200.000 XEQM |
| Quorum boyutu | Tur başına 12 koltuk |
| Nakamoto katsayısı (Temmuz 2026) | 7 (hedef: 8) |
| Temel depolar | github.com/XEQMLabs |

---

## Mevcut Diller

| Dil | Teknik Belge |
|---|---|
| English | [README.md](../../README.md) |
| Español | [../es/README.md](../es/README.md) |
| Français | [../fr/README.md](../fr/README.md) |
| Deutsch | [../de/README.md](../de/README.md) |
| 中文 | [../zh/README.md](../zh/README.md) |
| Português | [../pt/README.md](../pt/README.md) |
| Polski | [../pl/README.md](../pl/README.md) |

---

*Bu bir taslak belgedir. Burada açıklanan parametreler, emisyon takvimleri ve yol haritası aşamaları amaçlanan tasarımdır.*

*Bu belge finansal veya hukuki tavsiye niteliği taşımaz. XEQM, bir yatırım ürünü değil, EXIOM platformu için bir yardımcı coindir. Token sınıflandırması, menkul kıymet durumu ve geçerli düzenlemeler yargı bölgesine göre değişir. Katılımcılar, XEQM edinmeden veya işlem yapmadan önce yerel hukuki ve düzenleyici çerçevelerine başvurmalıdır. XEQM Labs, spekülatif fiyat artışına dayalı XEQM satın alımını teşvik etmez.*
