# Batasan Konsentrasi Node - Penegakan Kelangsungan Hidup Jaringan (Network Survivability Enforcement)
## Pendamping Teknis untuk Whitepaper Tokenomics EXIOM
### 26/07/2026

Dokumen ini merupakan pendamping untuk Whitepaper Tokenomics EXIOM dan mengasumsikan bahwa whitepaper tersebut telah dibaca. Whitepaper tersebut mencakup apa itu kontrol konsentrasi dan mengapa kontrol tersebut ada. Dokumen ini mencakup rincian mekanis tentang cara kerja setiap kontrol, data validasi testnet di balik HF22, matematika ekonomi yang tepat di balik pengubah hadiah nol, pertanyaan identitas operator pada rantai privasi, serta risiko tersisa yang tidak sepenuhnya diselesaikan oleh protokol.

---

## Data Konsentrasi Saat Ini

| Negara | Node aktif |
|---|---|
| Prancis | 492 |
| Jerman | 70 |
| Amerika Serikat | 55 |
| Kanada | 18 |
| Polandia | 13 |
| Britania Raya | 10 |
| Turki | 5 |
| Australia | 4 |
| Singapura | 2 |
| Lituania | 2 |
| Serbia | 1 |

Prancis yang mencakup sekitar 71% dari jaringan hampir seluruhnya berada di satu fasilitas Contabo di Grand Est. Ambang batas kelangsungan hidup (survivability threshold) yang ditetapkan dalam whitepaper adalah 30% dari node aktif per kluster, atau sekitar 208 node pada jumlah saat ini. Grand Est dengan 426 node bernilai lebih dari dua kali lipat ambang batas tersebut.

---

## Apa Artinya Ini Bagi Operator Node

Bagian ini menjawab pertanyaan secara langsung: bagaimana HF23 memengaruhi cara Anda menjalankan node?

**HF23 tidak mewajibkan satu node per IP, satu node per VPS, atau satu node per dompet.** Batas maksimumnya adalah 30% dari jaringan aktif per kluster kedekatan (proximity cluster), saat ini sekitar 208 node. Operator yang menjalankan 10, 50, atau bahkan 100 node pada infrastruktur berbagi (shared infrastructure) sama sekali tidak terpengaruh oleh HF23 selama kluster mereka tetap berada di bawah ambang batas tersebut. Anda dapat menjalankan beberapa node pada satu mesin, satu akun VPS, dan satu dompet. Tidak ada hal dalam HF23 yang mengubah hal itu.

**Pengubah hadiah nol hanya berlaku untuk node yang berada di atas ambang batas kluster 208-node.** Node terdaftar tertua dalam sebuah kluster mendapatkan hadiah penuh hingga ambang batas tersebut. Hanya node yang berada di peringkat atasnya dalam kluster yang terlampau pekat (over-concentrated) yang menghasilkan nol hadiah, dan hanya sampai mereka dimigrasikan ke kluster yang kurang terkonsentrasi.

**Deduplikasi kuorum membatasi pengaruh konsensus per putaran (round), bukan jumlah node atau pendapatan.** Operator yang menjalankan 50 node pada satu VPS mendapatkan hadiah blok dari seluruh 50 node tersebut dan mengelola infrastruktur mereka persis seperti yang mereka lakukan hari ini. Mereka menerima satu kursi kuorum per kluster per putaran alih-alih berpotensi mendapatkan banyak kursi, yang merupakan hasil yang memang ditujukan.

**Pendekatan yang tepat untuk operator baru** adalah memeriksa penjelajah node, melihat di mana kluster yang ada terkonsentrasi, dan menerapkan node ke wilayah yang populasinya sedikit. Ten node pada satu server di Brasil atau Argentina berfungsi dengan sangat baik di bawah HF23 karena wilayah-wilayah tersebut jauh dari ambang batas 30%. Hadiah penuh, partisipasi kuorum penuh, tanpa masalah.

**Dinamika ini menguntungkan Anda jika Anda melakukan penerapan ke wilayah yang jarang.** Jika suatu wilayah akhirnya terisi penuh, penjelajah node akan menampilkannya dan operator memiliki insentif finansial untuk berpindah sebelum batas tersebut memengaruhi mereka. Operator yang tiba lebih awal tetap mempertahankan hadiah penuh pada node tertua mereka hingga mencapai ambang batas. Pendaftaran baru ke dalam kluster yang terlampau pekat tidak menghasilkan apa-apa secara langsung, sehingga secara alami insentif ekonomi akan mendorong penerapan baru ke wilayah yang lebih longgar.

**Masalah spesifik yang diselesaikan oleh HF23** adalah satu fasilitas di Prancis yang saat ini menampung sekitar 426 node, atau 61% dari jaringan. Jika fasilitas tersebut offline, jaringan akan berhenti. Tujuannya adalah membuat kluster tersebut berada di bawah 208 node. Setiap operator lain yang menjalankan penataan multi-node secara bertanggung jawab di wilayah yang tidak terkonsentrasi adalah persis apa yang lebih dibutuhkan oleh jaringan.

---

## Mengapa Hard Fork Dipisahkan

HF22 diluncurkan setelah pengujian berhasil. Deduplikasi kuorum kunci dompet dan penyatuan periode unbonding tidak memiliki ketergantungan pada Lokinet. Buahnya telah divalidasi pada testnet dan menahannya saat penilaian Lokinet masih tertunda merupakan penundaan yang tidak beralasan. Aktor canggih yang membaca whitepaper sebelum HF22 diluncurkan dapat mencoba pemisahan dompet untuk mendahului kontrol kuorum, namun tindakan tersebut dapat dideteksi melalui korelasi waktu bukti waktu aktif dan analisis IP/ASN serta menciptakan rekam jejak yang terdokumentasi untuk tindakan tata kelola.

HF23 diluncurkan setelah penilaian rekayasa Lokinet selesai. Jika penilaian tersebut menghasilkan hasil berupa perubahan konfigurasi saja, HF23 dapat menyusul HF22 dengan cepat. Jika hasilnya memerlukan upaya rekayasa yang signifikan, Grand Est akan tetap terpapar pada risiko kelangsungan hidup penuh di luar dedup kuorum hingga HF23 siap. Memisahkan rilis ini juga memberikan domain kegagalan yang bersih: jika ada masalah setelah aktivasi HF23, variabel yang harus diisolasi menjadi lebih sedikit.

---

## Mekanisme HF22

### Deduplikasi Kuorum Kunci Dompet

Algoritma pemilihan kuorum menjalankan langkah deduplikasi pada setiap set kandidat sebelum difinalisasi. Ketika pengundian memilih node kandidat, algoritma memeriksa alamat dompet operatornya terhadap semua node yang sudah dipilih untuk putaran tersebut. Jika ditemukan kecocokan, kandidat tersebut digantikan dengan mengundi kembali dari kumpulan yang tersisa yang memenuhi syarat, dengan mengecualikan semua alamat yang sudah terwakili.

Pengundian pengganti tidak berputar kembali melalui kandidat yang sudah ditolak. Pengundian dilakukan dari kumpulan yang belum terpilih berdasarkan urutan pembobotan probabilitas yang sama yang digunakan untuk pengundian awal. Ini mempertahankan sifat statistik dari pemilihan kuorum tanpa memperkenalkan bias deterministik terhadap kumpulan node tersisa tertentu.

**Hasil validasi testnet:**
- Sembilan siklus stall/pemulihan telah diselesaikan
- Tingkat pemulihan 100% di seluruh siklus
- Zero intervensi manual yang diperlukan dalam siklus mana pun
- Baseline mainnet pra-HF22: 1.000 blok, 100% Pulse, nol blok GOV_SIGNED
- Analisis batas waktu R0: tidak ada batas waktu R0 yang diperkenalkan dalam kondisi produksi. Analisis kepadatan mainnet saat ini mengonfirmasi bahwa setiap kluster IP berkepadatan tinggi adalah satu operator, yang berarti dedup kunci dompet telah memberikan perlindungan penuh terhadap penerapan paus (whale deployments) saat ini. Dua penerapan IP tunggal terbesar (masing-masing 58 node dan 51 node) merupakan satu operator dan dibatasi hingga satu kursi kuorum per putaran di bawah HF22.

**Arti satu kursi kuorum dalam praktiknya:** Ukuran kuorum dan frekuensi rotasi menentukan seberapa sering sebuah node berpartisipasi. Pada ukuran jaringan saat ini, batas satu kursi berarti pengaruh operator yang terkonsentrasi dalam sesi oracle, putaran Pulse, dan kuorum kewajiban adalah identik dengan operator yang memiliki satu node. Pendapatan hadiah blok mereka tidak berubah.

**Celah pemisahan dompet dan deteksi sementara:** Operator yang membagi 426 node ke dalam 10 dompet mendapatkan hingga 10 kursi kuorum per putaran alih-alih satu. Ini adalah celah yang diketahui yang ditutup oleh HF23. Di masa interim, pemisahan dompet dapat dideteksi melalui dua sinyal yang sudah tersedia tanpa perubahan daemon. Pertama, waktu bukti waktu aktif: node pada host fisik atau hypervisor yang sama mengirimkan bukti dalam rentang milidetik satu sama lain, terlepas dari kunci dompet. Kluster bukti yang tiba dalam jendela sub-10ms dari node yang terdaftar ke dompet berbeda adalah sinyal kuat dari infrastruktur berbagi. Kedua, korelasi IP dan ASN: node pada dompet berbeda yang berbagi IP, subnet, atau ASN dicatat dan ditandai untuk peninjauan tata kelola. Operator yang membagi dompet tetapi mempertahankan semua node di fasilitas Contabo yang sama dapat diidentifikasi melalui kedua sinyal ini dan dapat dikenakan tindakan tata kelola di bawah kebijakan daftar blokir.

### Penyatuan Periode Unbonding

Periode unbonding pendaftaran ulang paksa berubah dari 10.080 blok (sekitar 7 hari) menjadi 20.160 blok (sekitar 14 hari), mencocokkan periode penarikan sukarela. Ini merupakan perubahan konstanta konsensus.

Periode paksa 7 hari yang asli adalah pilihan sengaja selama stabilisasi jaringan untuk membatasi hukuman pada operator yang mengalami masalah infrastruktur di luar kendali mereka. Alasan tersebut tidak lagi berlaku. Jaringan telah stabil, sistem kredit penghentian layanan (decommission credit system) menyediakan penyangga untuk gangguan singkat, dan periode 14 hari yang terpadu menghilangkan asimetri yang tidak lagi memiliki pembenaran.

Koin XEQM terkunci secara on-chain selama periode unbonding melalui transaksi pendaftaran. Tidak ada mekanisme untuk melepaskan kuncian lebih awal tanpa perubahan protokol. Untuk kegagalan infrastruktur yang terdokumentasi, tata kelola dapat memulihkan hadiah yang terlewat dari dompet tata kelola sebagai transfer XEQM, tetapi kuncian on-chain tetap berjalan selama durasi penuhnya.

---

## Mekanisme HF23

### Pengklusteran Kedekatan Lokinet

Lokinet (Low Latency Anonymous Routing Protocol, LLARP) mengarahkan lalu lintas melalui jaringan node layanan di layer 3, mendukung TCP, UDP, dan ICMP. Setiap node layanan berpartisipasi sebagai relay. Grafik perutean yang muncul mencerminkan topologi jaringan fisik: node di fasilitas yang sama merute melalui sakelar upstream yang sama dan backbone pusat data yang sama, menghasilkan pilihan jalur yang berkorelasi dan latensi antar-node sub-milidetik. Node di fasilitas yang berbeda merute melalui jalur yang berbeda dengan latensi yang terukur lebih tinggi.

Algoritma pengklusteran mengagregasi pengukuran latensi perutean Lokinet berpasangan dan tumpang tindih jalur di seluruh node aktif dan mengelompokkannya ke dalam kluster menggunakan pengukuran ini sebagai sinyal kedekatan. Kluster bukanlah wilayah geografis tetap; ini adalah pengelompokan dinamis dari node-node yang perilaku peruteannya menunjukkan infrastruktur fisik yang berbagi. Dua node di fasilitas Contabo yang berbeda di negara yang berbeda dapat merute melalui cukup banyak infrastruktur backbone Contabo yang sama sehingga muncul dalam kluster yang sama jika tumpang tindih jalurnya cukup tinggi. Dua node di pusat data yang sama tetapi pada mesin fisik berbeda dengan koneksi upstream yang berbeda akan muncul dalam kluster berbeda jika tumpang tindih jalurnya rendah.

Sinyal tambahan yang digunakan bersama dengan kedekatan Lokinet:

**Korelasi waktu bukti waktu aktif.** Jaringan telah menerima bukti waktu aktif dari semua node aktif secara teratur. Distribusi stempel waktu dari kedatangan bukti setiap node dicatat oleh node penerima. Node pada host fisik atau VM hypervisor yang sama mengirimkan bukti dalam jendela ketat yang khas, biasanya di bawah 10 milidetik. Mengklusterkan distribusi waktu kedatangan ini memberikan sinyal ko-lokasi fisik yang tidak memerlukan perubahan daemon dan berfungsi sebelum Lokinet aktif.

**Analisis ASN.** Alamat IP setiap node dipetakan ke Nomor Sistem Otonom (Autonomous System Number/ASN) melalui data BGP publik. Node yang berbagi ASN berbagi infrastruktur perutean tingkat penyedia dan paparan hukum tingkat penyedia. Penyedia yang menerima perintah tingkat yurisdiksi yang memengaruhi seluruh infrastruktur mereka akan mematikan semua node ASN mereka secara bersamaan, terlepas dari berapa banyak kluster Lokinet tempat mereka muncul. Konsentrasi ASN dilacak sebagai sinyal tambahan dan berkontribusi pada peninjauan tata kelola terhadap operator yang mendekati ambang batas kluster.

### Batas Pendaftaran Kluster

Pada saat pendaftaran, protokol menjalankan evaluasi kedekatan terhadap semua kluster yang ada. Karakteristik perutean Lokinet dari node yang mendaftar diukur terhadap titik tengah dari masing-masing kluster yang ada. Jika kluster terdekat sudah berisi 30% atau lebih dari node aktif, pendaftaran ditolak dengan kode kesalahan spesifik yang menunjukkan kapasitas kluster dan jumlah node dari kluster terdekat.

Penolakan tersebut bersifat deterministik: setiap node yang merute secara cukup mirip dengan kluster yang terlampau pekat sehingga dimasukkan ke dalamnya akan ditolak, terlepas dari kunci dompet operator, riwayat pendaftaran, atau jumlah stake. Operator tidak dapat membanding penolakan tersebut melalui tata kelola. Satu-satunya jalan keluar adalah mendaftar pada infrastruktur yang merute ke kluster berbeda.

Ambang batas dievaluasi terhadap jumlah node aktif pada saat pendaftaran. Seiring tumbuhnya jaringan, ambang batas 30% dalam angka mutlak juga ikut tumbuh. Operator yang berada pada batas maksimum hari ini dapat mendaftarkan node tambahan di kluster yang sebelumnya dibatasi seiring tumbuhnya jaringan dan naiknya batas mutlak, tanpa memindahkan node yang sudah ada.

### Pengubah Hadiah Nol

Pengubah hadiah nol diterapkan pada saat perhitungan hadiah blok. Perhitungan hadiah untuk node yang dipilih mencakup pemeriksaan kelayakan kluster. Jika kluster node berisi lebih banyak node daripada ambang batas maksimum, dan peringkat pendaftaran node dalam kluster tersebut berada di atas ambang batas (diurutkan dari yang tertua hingga terbaru), perhitungan hadiah menghasilkan nol.

Peringkat dihitung dari ketinggian blok pendaftaran (registration block height) node dalam penetapan kluster-nya. Node terdaftar tertua dalam kluster mendapatkan peringkat 1, yang paling baru terdaftar mendapatkan peringkat N. Node dengan peringkat lebih besar dari ambang batas maksimum mendapatkan hadiah nol. Node dengan peringkat pada atau di bawah ambang batas mendapatkan hadiah standar penuh. Peringkat dihitung ulang setiap kali penetapan kluster berubah, yang terjadi ketika node berpindah keluar dari kluster, ketika node baru bergabung, atau ketika batas kluster bergeser karena perubahan topologi jaringan.

**Matematika ekonomi untuk Est Grand:** Pada 426 node dengan batas 208-node, 218 node menghasilkan nol hadiah blok. Pada harga self-hosted $0,53 per node per bulan, 218 node tersebut memerlukan biaya $115,54 per bulan dengan nol pendapatan. Pada harga Pecunia $1,76 per node per bulan, biayanya adalah $383,68 per bulan. Operator memiliki dua respons rasional: memindahkan node berlebih ke kluster yang tidak terkonsentrasi, yang langsung memulihkan hadiah mereka begitu pendaftaran baru diterima, atau menghapus pendaftaran node berlebih dan mengembalikan XEQM yang distake melalui proses unbonding. Salah satu dari respons ini mengurangi konsentrasi. Tidak ada dasar rasional untuk mempertahankan node berlebih pada hadiah nol.

**Mekanisme masa tenggang:** Pada blok aktivasi HF23, protokol mengambil rekaman dari semua kluster aktif dan jumlah node mereka. Setiap kluster yang melebihi ambang batas 30% ditandai sebagai terlampau pekat. Selama 30 hari setelah blok aktivasi, pengubah hadiah nol ditangguhkan untuk semua node, termasuk yang berada di atas ambang batas. Selama masa tenggang, pemilik node dapat mengamati penataan kluster pada penjelajah node, merencanakan migrasi, dan mulai mengeksekusinya. Pada blok kadaluarsa masa tenggang, pengubah diaktifkan. Node yang telah berpindah keluar dari kluster yang terlampau pekat pada blok tersebut menghasilkan hadiah penuh sejak blok tersebut dan seterusnya. Node yang masih berada di atas ambang batas menghasilkan nol sejak blok tersebut dan seterusnya hingga mereka berpindah.

### Deduplikasi Kuorum Kluster Kedekatan

Peningkatan deduplikasi kuorum HF23 menggantikan pemeriksaan alamat dompet dengan pemeriksaan keanggotaan kluster. Ketika pengundian memilih node kandidat, algoritma memeriksa penetapan kluster-nya terhadap semua node yang sudah dipilih untuk putaran tersebut. Jika dua node berbagi penetapan kluster, node kedua digantikan oleh pengundian dari kumpulan yang tersisa, dengan mengecualikan semua kluster yang sudah terwakili.

Efek praktis pada operator yang membagi dompet: 10 alamat dompet di seluruh 426 node yang semuanya berada di fasilitas Contabo yang sama muncul dalam kluster kedekatan yang sama. Pemeriksaan kluster menangkap mereka semua sebagai satu kesatuan. Satu node dari kluster tersebut memegang satu kursi. 425 node lainnya dari kluster tersebut tidak memegang kursi, tidak peduli berapa banyak alamat dompet berbeda tempat mereka terdaftar.

### Persyaratan Jumlah Kluster Minimum dan Aturan Cadangan

Ukuran kuorum jaringan EXIOM adalah 12 kursi per putaran. Oleh karena itu, deduplikasi kluster kedekatan memerlukan setidaknya 12 kluster kedekatan yang berbeda dalam kumpulan node aktif untuk menjamin pembentukan kuorum. Jika jaringan menghasilkan kurang dari 12 kluster yang berbeda, algoritma tidak dapat memenuhi batasan satu-kursi-per-kluster dan pembentukan kuorum gagal.

Distribusi jaringan saat ini, setelah pengklusteran kedekatan Lokinet diterapkan, diperkirakan menghasilkan antara 12 hingga 18 kluster yang berbeda. Ini sangat dekat dengan minimum 12 kursi. Infrastruktur backbone penyedia yang berbagi antara fasilitas yang secara nominal terpisah dapat menyebabkan dua lokasi IP yang berbeda bergabung menjadi satu kluster kedekatan dalam grafik perutean Lokinet. Penggabungan semacam itu yang mengurangi jumlah kluster di bawah 12 merusak pembentukan kuorum secara keseluruhan.

Oleh karena itu, algoritma menerapkan aturan cadangan wajib:

1. Algoritma mencoba mengisi seluruh 12 kursi dengan satu node per kluster yang berbeda, memproses kluster yang tersedia secara acak.
2. Jika semua kluster yang berbeda telah habis sebelum 12 kursi terisi, algoritma masuk ke tahap cadangan.
3. Dalam tahap cadangan, algoritma mengizinkan node kedua dari setiap kluster, dimulai dari kluster terkecil terlebih dahulu. Kluster yang paling tidak terkonsentrasi menerima kursi kedua sebelum kluster yang paling terkonsentrasi.
4. Algoritma melanjutkan tahap cadangan, menambah maksimum kursi per kluster sebanyak satu pada setiap tahap, hingga 12 kursi terisi.
5. Kluster yang paling terkonsentrasi, seperti Grand Est dalam kondisi saat ini, menerima kursi tambahan hanya setelah semua kluster yang lebih kecil diberikan alokasi cadangannya.

Setiap putaran yang memicu cadangan dicatat bersama dengan jumlah kluster yang menyebabkannya. Tata kelola memantau frekuensi cadangan sebagai indikator risiko konsentrasi langsung. Jaringan dengan 12 atau lebih kluster yang berbeda tidak pernah memicu cadangan. Jaringan yang secara konsisten memicu cadangan memberi sinyal bahwa penegakan konsentrasi HF23 belum mencapai keberagaman fisik yang memadai dan bahwa batas kluster atau penegakan masa tenggang memerlukan perhatian tata kelola.

Log cadangan dipublikasikan di penjelajah node bersama penetapan kluster sehingga komunitas operator dapat mengamati risiko konsentrasi secara real time.

---

## Identitas Operator pada Rantai Privasi

Protokol tidak perlu mengidentifikasi manusia mana yang memiliki node mana untuk menegakkan batas kluster dan pengubah hadiah nol. Kedua kontrol beroperasi pada tingkat kluster. Apa yang dapat dan tidak dapat ditentukan adalah konteks yang berguna untuk pemantauan tata kelola tetapi tidak diperlukan untuk penegakan protokol.

**Apa yang bersifat deterministik dari data on-chain:** node yang terdaftar di bawah kunci dompet operator yang sama secara pasti merupakan operator yang sama. Ini adalah informasi publik dalam transaksi pendaftaran.

**Apa yang dapat disimpulkan dengan keyakinan tinggi dari Lokinet dan data waktu:** jumlah host fisik berbeda yang mendasari sebuah kluster node, terlepas dari berapa banyak kunci dompet yang mereka gunakan. Lima kunci dompet yang masing-masing menjalankan 85 node, semuanya pada dua server fisik yang sama, menghasilkan dua tanda tangan waktu (timing signatures) berbeda dan dua titik tengah kedekatan Lokinet, bukan lima.

**Apa yang tidak dapat ditentukan pada rantai privasi:** apakah dua kunci dompet yang berbeda dengan infrastruktur terpisah milik operator manusia yang sama. Sumber pendanaan dari setiap kunci dompet bersifat privat berdasarkan desain. Operator canggih yang menggunakan lima dompet yang didanai dari lima sumber berbeda melalui lapisan transaksi rantai privasi menyajikan lima identitas berbeda pada tingkat protokol.

Untuk penegakan kelangsungan hidup, hal ini tidak masalah. Kluster tersebut berisi 426 node. 208 yang tertua menghasilkan hadiah. 218 yang terbaru menghasilkan nol. Identitas operator tidak relevan dengan perhitungan tersebut.

---

## Status Implementasi

| Kontrol | Status |
|---|---|
| Dedup kuorum kunci dompet operator | HF22, memasuki testnet, divalidasi |
| Penyatuan periode unbonding, 7 ke 14 hari | HF22, memasuki testnet |
| Aktivasi Lokinet sebagai transport jaringan | Penilaian rekayasa sedang berlangsung |
| Algoritma pengklusteran kedekatan | Tahap desain, menunggu penilaian Lokinet |
| Batas pendaftaran kluster, ambang batas 30% | HF23, tahap desain |
| Pengubah hadiah nol untuk node berlebih | HF23, tahap desain |
| Mekanisme masa tenggang | HF23, tahap desain |
| Dedup kuorum kluster kedekatan dengan aturan cadangan | HF23, tahap desain |
| Pemantauan jumlah kluster minimum dan pencatatan cadangan | HF23, tahap desain |
| Alat korelasi waktu bukti waktu aktif | Tidak ada perubahan daemon yang diperlukan, alat dalam pengembangan |
| Suplemen pengklusteran ASN | Tidak ada perubahan daemon yang diperlukan, alat dalam pengembangan |

---

## Apa yang Tidak Diselesaikan oleh Kontrol Ini

**Konsentrasi hukum tingkat penyedia.** Penyedia yang menerima perintah hukum tingkat yurisdiksi yang memengaruhi seluruh infrastruktur global mereka akan mematikan semua node mereka secara bersamaan, bahkan jika node tersebut muncul di beberapa kluster kedekatan Lokinet. Analisis ASN memunculkan risiko ini tetapi protokol tidak dapat menegakkan keberagaman penyedia tanpa mengharuskan operator mengungkapkan identitas penyedia mereka. Penyebaran geografis yang dihasilkan secara alami oleh batas kluster secara substansial memitigasi risiko ini dalam praktiknya, karena operator yang terpaksa mendistribusikan ke seluruh kluster dalam praktiknya akan menggunakan beberapa penyedia.

**Penentuan identitas operator manusia di seluruh pemisahan dompet rantai privasi.** Seperti dijelaskan di atas, operator canggih yang menggunakan beberapa dompet yang didanai melalui rantai privasi tidak dapat diidentifikasi pada tingkat protokol. Batas kluster dan pengubah hadiah nol mengatasi risiko domain kegagalan tanpa memandang identitas. Dedup kuorum menutup celah pengaruh konsensus pada HF23. Risiko tersisa adalah operator canggih menjalankan banyak node di banyak kluster yang benar-benar berbeda, mengumpulkan pendapatan hadiah blok secara proporsional dengan jumlah node mereka sambil berkontribusi secara proporsional terhadap kesehatan jaringan. Ini adalah hasil yang dapat diterima: pengaruh konsensus yang terkonsentrasi dibatasi; partisipasi modal yang terdistribusi diberi hadiah.

Operator yang memiliki pertanyaan tentang penetapan kluster, perencanaan migrasi, atau lini masa HF22/HF23 didorong untuk mengirim pesan di saluran Telegram Operator Node atau membuka issue di repositori ini.

---

## Bahasa yang Tersedia

Terjemahan komunitas untuk dokumen ini dikelola di repositori whitepaper. Jika terjadi konflik antara versi terjemahan dan versi bahasa Inggris, versi bahasa Inggris yang berlaku.

| Bahasa | Dokumen |
|---|---|
| Español | [translations/es/concentration-limits-proposal.md](./translations/es/concentration-limits-proposal.md) |
| Français | [translations/fr/concentration-limits-proposal.md](./translations/fr/concentration-limits-proposal.md) |
| Deutsch | [translations/de/concentration-limits-proposal.md](./translations/de/concentration-limits-proposal.md) |
| 中文 | [translations/zh/concentration-limits-proposal.md](./translations/zh/concentration-limits-proposal.md) |
| Português | [translations/pt/concentration-limits-proposal.md](./translations/pt/concentration-limits-proposal.md) |
| Türkçe | [translations/tr/concentration-limits-proposal.md](./translations/tr/concentration-limits-proposal.md) |
| Polski | [translations/pl/concentration-limits-proposal.md](./translations/pl/concentration-limits-proposal.md) |

---

*Dokumen ini bukan merupakan nasihat keuangan atau hukum. XEQM adalah koin utilitas untuk platform EXIOM, bukan produk investasi. Klasifikasi token, status sekuritas, dan peraturan yang berlaku bervariasi menurut yurisdiksi. Peserta harus berkonsultasi dengan kerangka hukum dan kualifikasi lokal mereka sebelum memperoleh atau beroperasi dengan XEQM. XEQM Labs tidak mendorong pembelian XEQM berdasarkan apresiasi harga spekulatif.*
