# Risiko Sybil dan Model Mitigasi EXIOM
## Pendamping Teknis untuk Whitepaper Tokenomics EXIOM
### 26/07/2026

Dokumen ini merupakan pendamping untuk Whitepaper Tokenomics EXIOM dan proposal Batasan Konsentrasi Node, serta mengasumsikan bahwa keduanya telah dibaca. Whitepaper tersebut mencakup apa saja kontrolnya. Proposal batasan konsentrasi mencakup mekanika cara kerja setiap kontrol. Dokumen ini mencakup model ancaman: seperti apa serangan Sybil sebenarnya pada rantai privasi, apa yang membuat arsitektur EXIOM secara khusus resisten atau rentan, dan bagaimana metodologi pemantauan berkelanjutan mengidentifikasi konsentrasi dalam praktiknya.

---

## Ancaman Sybil pada Rantai Privasi

Serangan Sybil pada jaringan node layanan berarti satu aktor yang mengoperasikan banyak node di bawah identitas yang tampak berbeda untuk memperoleh pengaruh yang tidak proporsional. Pada blockchain yang transparan, analisis grafik dompet sering kali dapat mengidentifikasi bahwa beberapa alamat operator node didanai dari sumber yang sama, sehingga mengungkap serangan Sybil tersebut. Pada rantai privasi, alat tersebut tidak tersedia secara desain. Jaminan privasi yang melindungi transaksi pengguna juga menghilangkan metode deteksi Sybil yang paling umum.

Oleh karena itu, area serangan Sybil pada EXIOM berbeda dari rantai transparan dalam hal tertentu: seorang operator yang menggunakan fitur privasi secara benar dapat menyajikan beberapa alamat dompet yang tampak tidak saling berhubungan pada tingkat protokol, terlepas dari seberapa besar modal yang mereka kuasai. Ini bukanlah cacat dalam desain privasi. Ini adalah sifat bawaan dari setiap rantai privasi yang harus ditangani melalui mekanisme selain analisis grafik transaksi.

Dua area serangan Sybil pada EXIOM berbeda dan memerlukan kontrol yang terpisah:

**Serangan pengaruh konsensus.** Seorang operator mengumpulkan cukup banyak node, melalui struktur dompet apa pun, untuk memegang sejumlah kursi kuorum yang tidak proporsional secara bersamaan. Hal ini memungkinkan mereka untuk memengaruhi hasil sesi oracle, putaran Pulse, dan kuorum kewajiban di luar apa yang dianggap adil oleh proporsi stake individu mereka. Kerusakan terjadi pada integritas konsensus, tidak selalu pada waktu aktif pada jaringan.

**Serangan kegagalan domain.** Seorang operator mengonsentrasikan node dalam satu fasilitas fisik. Hal ini bisa jadi disengaja sebagai serangan atau tidak disengaja; ini bisa dihasilkan dari optimasi biaya. Kerusakan terjadi pada kelangsungan hidup jaringan: satu pemadaman fasilitas membawa node operator offline secara bersamaan, berpotensi menghentikan produksi blok jika konsentrasinya cukup besar.

---

## Apa yang Membuat EXIOM Secara Struktural Resisten

**Biaya modal per identitas.** Tidak seperti serangan Sybil murni di mana identitas bisa didapatkan secara gratis, setiap node layanan EXIOM membutuhkan 200.000 XEQM yang distake, dengan operator secara pribadi men-stake setidaknya 100.000 XEQM. Seorang operator yang menjalankan 100 node memiliki 10.000.000 XEQM modal yang distake dan terkunci. Membuat identitas tambahan yang tampak baru melalui pemisahan dompet tidak mengurangi biaya ini -- setiap node tetap membutuhkan 100.000 XEQM stake dari operator. Serangan Sybil sangat mahal di setiap skala.

**Gesekan unbonding.** Periode unbonding selama 14 hari untuk penarikan sukarela maupun pendaftaran ulang paksa berarti modal yang ditaruh pada node Sybil tidak dapat diekstraksi dengan cepat. Penyerang yang memutuskan untuk keluar tidak dapat melakukannya lebih cepat daripada operator lain.

**Pendaftaran node publik.** Setiap kunci pendaftaran node layanan dan alamat dompet operator bersifat publik. Sebuah node tidak dapat berpartisipasi dalam konsensus secara anonim. Meskipun identitas manusia di balik alamat dompet bersifat privat, sidik jari operasional node terakumulasi dari waktu ke waktu melalui pola pendaftaran, bukti waktu aktif, dan perilaku perutean.

---

## Bagaimana Konsentrasi Diidentifikasi Tanpa Analisis Grafik Transaksi

Karena analisis tingkat transaksi tidak tersedia, deteksi konsentrasi EXIOM bergantung pada empat sinyal yang dapat diamati dari perilaku node alih-alih riwayat pendanaan.

**Pengklusteran kunci pendaftaran.** Node yang terdaftar di bawah kunci dompet operator yang sama secara pasti merupakan operator yang sama. Ini bersifat deterministik dari data on-chain. Operator besar yang tidak melakukan pemisahan dompet terlihat sepenuhnya melalui sinyal ini saja. Penerapan terbesar saat ini di jaringan, termasuk node yang menjalankan masing-masing 58 dan 51 node dari alamat IP tunggal, masing-masing merupakan operator tunggal yang dikonfirmasi melalui analisis kunci pendaftaran.

**Pengklusteran alamat IP dan subnet.** Saat ini merupakan sinyal ko-lokasi fisik utama. Beberapa node dari alamat IP yang sama hampir pasti berada pada server yang sama. Beberapa node dari subnet yang sama menunjukkan akun hosting atau blok pusat data yang sama. Sinyal ini tersedia hari ini tanpa perubahan daemon apa pun dan akan tetap ada sebagai sinyal tambahan setelah aktivasi Lokinet.

**Korelasi waktu bukti waktu aktif.** Jaringan menerima bukti waktu aktif dari setiap node aktif secara teratur. Distribusi stempel waktu (timestamp) dari kedatangan bukti-bukti ini dicatat oleh node penerima. Node yang berjalan pada host fisik atau VM hypervisor yang sama mengirimkan bukti dalam jendela ketat yang khas, biasanya di bawah 10 milidetik, karena mereka berbagi jam sistem dan antarmuka jaringan yang sama. Kluster node dari kunci dompet yang berbeda yang buktinya secara konsisten tiba dalam jendela ini adalah sinyal kuat dari infrastruktur fisik yang berbagi, dapat dideteksi tanpa perubahan daemon dan tanpa Lokinet aktif.

Sinyal ini secara khusus berguna untuk mengidentifikasi operator pemisah dompet yang mempertahankan node mereka pada infrastruktur berbagi. Kunci dompetnya berbeda; waktu buktinya tidak.

**Kedekatan perutean Lokinet (HF23, menunggu penilaian).** Setelah Lokinet aktif sebagai transport jaringan, grafik perutean menyediakan peta topologi fisik yang berkelanjutan dari jaringan node. Node pada fasilitas yang sama merute melalui infrastruktur upstream yang sama, menghasilkan pilihan jalur yang berkorelasi dan latensi antar-node sub-milidetik terlepas dari kunci dompet atau alamat IP yang diumumkan. Ini adalah sinyal yang paling kuat karena mencerminkan realitas jaringan fisik yang tidak dapat diubah oleh konfigurasi perangkat lunak tanpa benar-benar memindahkan infrastruktur.

---

## Rincian Serangan Pemisahan Dompet

Pendekatan Sybil paling canggih yang tersedia di EXIOM adalah pemisahan dompet: mendaftarkan node di bawah beberapa alamat dompet yang didanai melalui lapisan transaksi rantai privasi sehingga sumber pendanaan bersama tidak terlihat. Ini mengalahkan sinyal pengklusteran kunci pendaftaran tetapi tidak mengalahkan sinyal lainnya.

Seorang operator yang menjalankan 426 node di 10 dompet, semuanya dihosting di fasilitas Contabo yang sama, terungkap oleh:

- Waktu bukti waktu aktif: bukti dari seluruh 426 node tiba dalam jendela sub-10ms khas infrastruktur berbagi
- Analisis IP dan subnet: bahkan dengan beberapa IP, penetapan blok pusat data dan ASN tetap dibagikan
- Kedekatan Lokinet (pasca-HF23): seluruh 426 node merute melalui backbone Contabo yang sama terlepas dari kunci dompet

Seorang operator yang menjalankan 426 node di 10 dompet, yang benar-benar didistribusikan di 10 penyedia berbeda di 10 negara berbeda, tidak terungkap secara signifikan oleh sinyal mana pun saat ini. Kunci pendaftarannya berbeda, waktu buktinya berbeda karena infrastrukturnya berbeda, ASN-nya berbeda, dan jalur Lokinet-nya berbeda. Pada tingkat protokol, ini terlihat seperti 10 operator berbeda.

Ini adalah risiko Sybil yang tersisa pada EXIOM setelah semua kontrol diterapkan. Risiko ini dibatasi dalam konsekuensinya: deduplikasi kuorum HF23 membatasi setiap kluster kedekatan hingga satu kursi kuorum per putaran terlepas dari struktur dompet, sehingga operator pemisah dompet yang terdistribusi sekalipun tidak mendapatkan pengaruh konsensus tanpa batas. Pendapatan imbalan blok mereka ditingkatkan secara proporsional dengan jumlah node mereka, yang mana ini adil karena mereka telah men-stake modal yang proporsional. Pengaruh konsensus mereka per putaran dibatasi oleh dedup kluster terlepas dari berapa banyak dompet yang mereka gunakan.

---

## Metodologi Pemantauan Berkelanjutan

**Daftar hitam tata kelola.** Daftar hitam kunci publik yang dikelola tata kelola mencegah kunci pendaftaran yang masuk daftar blokir untuk mendaftarkan node baru. Operator yang berpindah ke kunci dompet baru saat kunci asli telah diblokir membuat rekam jejak penghindaran yang terdokumentasi, dan waktu bukti serta perilaku perutean kunci baru dikorelasikan terhadap profil historis kunci yang telah diblokir.

**Analisis grafik slot kontributor.** Slot kontributor node layanan adalah sinyal identitas sekunder. Operator yang mendanai slot kontributor di beberapa kunci dompet mereka sendiri membuat grafik hubungan yang dapat diamati bahkan pada rantai privasi, karena transaksi pendaftaran kontributor membawa data yang dapat diamati tentang node mana yang mereka kontribusikan. Operator yang secara konsisten berkontribusi pada node yang terdaftar di bawah dompet A dari dompet B dan C, sementara dompet B dan C tersebut mendaftarkan node mereka sendiri, membuat grafik korelasi yang melengkapi sinyal pengklusteran kunci pendaftaran langsung.

**Pemantauan ASN.** IP setiap node aktif dipetakan ke Nomor Sistem Otonom (ASN) melalui data BGP publik. Jaringan melacak konsentrasi ASN di seluruh set node aktif. Node yang berbagi ASN berbagi infrastruktur tingkat penyedia dan paparan hukum. Konsentrasi ASN yang tinggi ditandai untuk peninjauan tata kelola bahkan ketika pendaftaran node individu tampak tidak berhubungan. Sinyal ASN tidak mengidentifikasi operator manusia, tetapi mengidentifikasi domain kegagalan.

Status implementasi saat ini untuk semua kontrol yang dijelaskan dalam dokumen ini dikelola dalam [proposal Batasan Konsentrasi Node](https://github.comXEQMLabs/whitepaper/blob/main/concentration-limits-proposal.md).

---

*Dokumen ini bukan merupakan nasihat keuangan atau hukum. XEQM adalah koin utilitas untuk platform EXIOM, bukan produk investasi. Klasifikasi token, status sekuritas, dan peraturan yang berlaku bervariasi menurut yurisdiksi. Peserta harus berkonsultasi dengan kerangka hukum dan kualifikasi lokal mereka sebelum memperoleh atau beroperasi dengan XEQM. XEQM Labs tidak mendorong pembelian XEQM berdasarkan apresiasi harga spekulatif.*
