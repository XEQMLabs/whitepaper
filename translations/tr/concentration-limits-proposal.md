# Düğüm Konsantrasyon Limitleri - Ağ Dayanıklılığı Uygulaması
## EXIOM Token Ekonomisi Teknik Belgesi Tamamlayıcı Teknik Doküman
### 26.07.2026

> *Bu çeviri AI çeviri araçları kullanılarak üretilmiştir. Çakışma durumunda İngilizce versiyon geçerlidir: [concentration-limits-proposal.md](../../concentration-limits-proposal.md)*

---

## Bu Düğüm Operatörleri İçin Ne Anlama Gelir

HF23, IP başına bir düğüm, VPS başına bir düğüm veya cüzdan başına bir düğüm **gerektirmez**. Limit, yakınlık kümesi başına aktif ağın %30'udur ve şu anda yaklaşık 208 düğümdür. Paylaşılan altyapıda 10, 50 veya 100 düğüm çalıştıran bir operatör, kümesi bu eşiğin altında kaldığı sürece HF23'ten etkilenmez.

HF23'ün çözdüğü spesifik sorun: Fransa'daki bir tesis şu anda yaklaşık 426 düğüm barındırmakta, bu ağın %61'ini oluşturmaktadır. Bu tesis çevrimdışı olursa ağ durur.

---

## Mevcut Konsantrasyon Verileri

| Ülke | Aktif düğümler |
|---|---|
| Fransa | 492 |
| Almanya | 70 |
| Amerika Birleşik Devletleri | 55 |
| Kanada | 18 |
| Polonya | 13 |
| Birleşik Krallık | 10 |
| Türkiye | 5 |
| Avustralya | 4 |
| Singapur | 2 |
| Litvanya | 2 |
| Sırbistan | 1 |

---

## HF22 Kontrolleri (Test Ağına Giriyor, Doğrulandı)

**Operatör cüzdan anahtarı quorum tekilleştirme.** Tur başına operatör cüzdan adresi başına en fazla bir doğrulayıcı koltuk. Dokuz döngüde %100 kurtarma oranıyla doğrulandı.

**Kilit açma süresi birleşimi.** Zorunlu kayıt silme kilit açma süresi 7 günden 14 güne uzatıldı.

---

## HF23 Kontrolleri (Tasarım Aşaması)

**Küme kayıt limiti.** Bir küme aktif düğümlerin %30'unu aştığında yeni kayıtlar reddedilir.

**Sıfır ödül değiştiricisi.** Küme eşiğinin üzerindeki düğümler taşınana kadar sıfır blok ödülü alır.

**Quorum geri dönüş kuralı.** Quorum boyutu: 12 koltuk. 12'den az ayrı küme varsa, algoritma önce en küçük kümelere ek koltuklar verir.

---

*Tam teknik özellik için İngilizce versiyona bakın: [concentration-limits-proposal.md](../../concentration-limits-proposal.md)*

*Bu belge finansal veya hukuki tavsiye niteliği taşımaz. Çakışma durumunda İngilizce versiyon geçerlidir.*
