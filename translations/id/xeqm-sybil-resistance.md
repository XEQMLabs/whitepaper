# Risiko Sybil dan Model Mitigasi EXIOM
## Pendamping Teknis untuk Whitepaper Tokenomics EXIOM
### 07/26/2026

> **Catatan (diperbarui Oktober 2026).** Konsentrasi ditegakkan per *cluster kedekatan* (infrastruktur fisik atau routing bersama), **bukan per negara**. Angka node di sini adalah snapshot Juli 2026; lihat whitepaper untuk total saat ini. Lokinet dirilis dalam rilis non-penegakan sebelum HF23, dan HF23 mengaktifkan penegakan.

Dokumen ini adalah pendamping untuk Whitepaper Tokenomics EXIOM dan proposal Batas Konsentrasi Node, dan mengasumsikan keduanya telah dibaca. Whitepaper mencakup apa kontrol itu. Concentration-limits-proposal mencakup mekanika tentang bagaimana setiap kontrol bekerja. Dokumen ini mencakup model ancaman: seperti apa serangan Sybil sebenarnya pada chain privasi, apa yang membuat arsitektur EXIOM secara spesifik tahan atau rentan, dan bagaimana metodologi pemantauan berkelanjutan mengidentifikasi konsentrasi dalam praktik.

---

## Ancaman Sybil pada Chain Privasi

Serangan Sybil pada jaringan service node berarti satu aktor mengoperasikan banyak node di bawah identitas tampak yang berbeda untuk memperoleh pengaruh yang tidak proporsional. Pada blockchain transparan, analisis grafik wallet sering kali dapat mengungkapkan bahwa beberapa alamat operator node didanai dari sumber yang sama, mengekspos Sybil. Pada chain privasi, perkakas itu tidak tersedia secara desain. Jaminan privasi yang melindungi transaksi pengguna juga menghapus metode deteksi Sybil yang paling umum.

Oleh karena itu permukaan Sybil EXIOM berbeda dari chain transparan dengan cara yang spesifik: operator yang menggunakan fitur privasi dengan benar dapat menyajikan beberapa alamat wallet yang tampak tidak berhubungan pada tingkat protokol, terlepas dari seberapa banyak modal yang mereka kendalikan. Ini bukan cacat dalam desain privasi. Ini adalah properti inheren dari setiap chain privasi yang harus diatasi melalui mekanisme selain analisis grafik transaksi.

Dua permukaan serangan Sybil pada EXIOM berbeda dan memerlukan kontrol terpisah:

**Serangan pengaruh konsensus.** Operator mengakumulasi cukup node, melalui struktur wallet apa pun, untuk memegang jumlah kursi kuorum yang tidak proporsional secara bersamaan. Ini memungkinkan mereka memengaruhi hasil sesi oracle, ronde Pulse, dan kuorum kewajiban melebihi apa yang proporsi stake individual mereka sarankan sebagai adil. Kerusakannya adalah pada integritas konsensus, tidak harus pada uptime jaringan.

**Serangan failure domain.** Operator mengonsentrasikan node di satu fasilitas fisik. Ini mungkin atau mungkin tidak disengaja sebagai serangan; itu dapat dihasilkan dari optimisasi biaya. Kerusakannya adalah pada daya tahan jaringan: satu pemadaman fasilitas membawa node operator offline secara bersamaan, berpotensi memacetkan produksi blok jika konsentrasinya cukup besar.

---

## Apa yang Membuat EXIOM Tahan Secara Struktural

**Biaya modal per identitas.** Tidak seperti serangan Sybil murni di mana identitas gratis, setiap service node EXIOM memerlukan 200,000 XEQM yang di-stake, dengan operator secara pribadi men-stake setidaknya 100,000 XEQM. Operator yang menjalankan 100 node memiliki 10,000,000 XEQM modal yang di-stake dan terkunci. Menciptakan identitas tampak tambahan melalui pemecahan wallet tidak mengurangi biaya ini -- setiap node masih memerlukan 100,000 XEQM stake operator. Serangan Sybil mahal pada setiap skala.

**Friksi unbonding.** Periode unbonding 14-hari pada baik penarikan sukarela maupun deregistrasi paksa berarti modal yang dikomitmenkan ke node Sybil tidak dapat diekstraksi dengan cepat. Penyerang yang memutuskan untuk keluar tidak dapat melakukannya lebih cepat dari operator lain mana pun.

**Registri node publik.** Kunci registrasi dan alamat wallet operator setiap service node bersifat publik. Sebuah node tidak dapat berpartisipasi dalam konsensus secara anonim. Meskipun identitas manusia di balik alamat wallet bersifat privat, sidik jari operasional node terakumulasi dari waktu ke waktu melalui pola registrasi, timing bukti uptime, dan perilaku routing.

---

## Bagaimana Konsentrasi Diidentifikasi Tanpa Analisis Grafik Transaksi

Karena analisis tingkat-transaksi tidak tersedia, deteksi konsentrasi EXIOM mengandalkan empat sinyal yang dapat diamati dari perilaku node alih-alih riwayat pendanaan.

**Pengelompokan kunci registrasi.** Node yang terdaftar di bawah kunci wallet operator yang sama secara definitif adalah operator yang sama. Ini deterministik dari data on-chain. Operator besar yang tidak memecah-wallet sepenuhnya terlihat melalui sinyal ini saja. Deployment terbesar saat ini pada jaringan, termasuk node yang masing-masing menjalankan 58 dan 51 node dari alamat IP tunggal, masing-masing adalah operator tunggal yang dikonfirmasi melalui analisis kunci registrasi.

**Pengelompokan alamat IP dan subnet.** Saat ini sinyal kolokasi fisik utama. Beberapa node dari alamat IP yang sama hampir pasti berada pada server yang sama. Beberapa node dari subnet yang sama menyarankan akun hosting atau blok datacenter yang sama. Sinyal ini tersedia hari ini tanpa perubahan daemon apa pun dan akan tetap ada sebagai sinyal suplemental setelah aktivasi Lokinet.

**Korelasi timing bukti uptime.** Jaringan menerima bukti uptime dari setiap node aktif pada jadwal reguler. Distribusi timestamp kedatangan bukti ini dicatat oleh node penerima. Node yang berjalan pada host fisik atau hypervisor VM yang sama mengirimkan bukti dalam jendela rapat yang khas, biasanya di bawah 10 milidetik, karena mereka berbagi jam sistem dan antarmuka jaringan yang sama. Cluster node dari kunci wallet berbeda yang buktinya secara konsisten tiba dalam jendela ini adalah sinyal kuat infrastruktur fisik bersama, dapat dideteksi tanpa perubahan daemon apa pun dan tanpa Lokinet aktif.

Sinyal ini secara spesifik berguna untuk mengidentifikasi operator pemecah-wallet yang menjaga node mereka pada infrastruktur bersama. Kunci wallet berbeda; timing bukti tidak.

**Kedekatan routing Lokinet (dirilis non-penegakan sebelum HF23; ditegakkan di HF23).** Begitu Lokinet aktif sebagai transport jaringan, routing graph menyediakan peta topologi fisik berkelanjutan dari jaringan node. Node di fasilitas yang sama merutekan melalui infrastruktur upstream yang sama, menghasilkan pemilihan jalur berkorelasi dan latensi antar-node sub-milidetik terlepas dari kunci wallet atau alamat IP yang diumumkan mereka. Ini adalah sinyal paling kuat karena mencerminkan realitas jaringan fisik yang tidak dapat diubah oleh konfigurasi perangkat lunak tanpa benar-benar memindahkan infrastruktur.

---

## Serangan Pemecahan-Wallet Secara Detail

Pendekatan Sybil paling canggih yang tersedia pada EXIOM adalah pemecahan wallet: meregistrasi node di bawah beberapa alamat wallet yang didanai melalui lapisan transaksi chain privasi sehingga sumber pendanaan bersama tidak terlihat. Ini mengalahkan sinyal pengelompokan kunci registrasi tetapi tidak yang lain.

Operator yang menjalankan 426 node di seluruh 10 wallet, semuanya di-host di fasilitas Contabo yang sama, terekspos oleh:

- Timing bukti uptime: bukti dari semua 426 node tiba dalam jendela sub-10ms khas infrastruktur bersama
- Analisis IP dan subnet: bahkan dengan beberapa IP, penetapan blok datacenter dan ASN dibagikan
- Kedekatan Lokinet (pasca-HF23): semua 426 node merutekan melalui backbone Contabo yang sama terlepas dari kunci wallet

Operator yang menjalankan 426 node di seluruh 10 wallet, benar-benar terdistribusi di seluruh 10 penyedia berbeda di 10 negara berbeda, tidak terekspos secara bermakna oleh sinyal apa pun saat ini. Kunci registrasi berbeda, timing bukti berbeda karena infrastruktur berbeda, ASN berbeda, dan jalur Lokinet berbeda. Pada tingkat protokol, ini terlihat seperti 10 operator berbeda.

Ini adalah risiko Sybil residual pada EXIOM setelah semua kontrol diterapkan. Ini dibatasi dalam konsekuensinya: deduplikasi kuorum HF23 membatasi setiap cluster kedekatan menjadi satu kursi kuorum per ronde terlepas dari struktur wallet, sehingga bahkan operator pemecah-wallet terdistribusi tidak memperoleh pengaruh konsensus tak terbatas. Pendapatan block reward mereka berskala dengan jumlah node mereka, yang adil karena mereka telah men-stake modal proporsional. Pengaruh konsensus mereka per ronde dibatasi oleh dedup cluster terlepas dari berapa banyak wallet yang mereka gunakan.

---

## Metodologi Pemantauan Berkelanjutan

**Blocklist tata kelola.** Blocklist kunci publik yang dikelola tata kelola mencegah kunci registrasi yang di-blocklist meregistrasi node baru. Operator yang pindah ke kunci wallet baru sementara yang asli di-blocklist menciptakan catatan terdokumentasi penghindaran, dan timing bukti serta perilaku routing kunci baru dikorelasikan terhadap profil historis kunci yang di-blocklist.

**Analisis grafik slot kontributor.** Slot kontributor service node adalah sinyal identitas sekunder. Operator yang mendanai slot kontributor di seluruh beberapa kunci wallet mereka sendiri menciptakan grafik hubungan yang dapat diamati bahkan pada chain privasi, karena transaksi registrasi kontributor membawa data yang dapat diamati tentang node mana yang mereka kontribusikan. Operator yang secara konsisten berkontribusi ke node yang terdaftar di bawah wallet A dari wallet B dan C, sementara wallet B dan C yang sama itu meregistrasi node mereka sendiri, menciptakan grafik korelasi yang melengkapi sinyal pengelompokan kunci registrasi langsung.

**Pemantauan ASN.** IP setiap node aktif dipetakan ke Autonomous System Number melalui data BGP publik. Jaringan melacak konsentrasi ASN di seluruh himpunan node aktif. Node yang berbagi ASN berbagi infrastruktur tingkat-penyedia dan eksposur hukum. Konsentrasi ASN tinggi ditandai untuk peninjauan tata kelola bahkan ketika registrasi node individual tampak tidak berhubungan. Sinyal ASN tidak mengidentifikasi operator manusia, tetapi ia mengidentifikasi failure domain.

Status implementasi saat ini untuk semua kontrol yang dijelaskan dalam dokumen ini dipelihara dalam [proposal Batas Konsentrasi Node](https://github.com/XEQMLabs/whitepaper/blob/main/concentration-limits-proposal.md).

---

*Dokumen ini bukan merupakan nasihat keuangan atau hukum. XEQM adalah koin utilitas untuk platform EXIOM, bukan produk investasi. Klasifikasi token, status sekuritas, dan regulasi yang berlaku bervariasi menurut yurisdiksi. Peserta harus berkonsultasi dengan kerangka hukum dan regulasi lokal mereka sebelum memperoleh atau beroperasi dengan XEQM. XEQM Labs tidak mendorong pembelian XEQM atas dasar apresiasi harga spekulatif.*
