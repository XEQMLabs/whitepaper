# Batas Konsentrasi Node - Penegakan Daya Tahan Jaringan
## Pelengkap Teknis untuk Whitepaper Tokenomics EXIOM
### 07/26/2026

> **Catatan cakupan (diperbarui 19 Oktober 2026).** Unit yang ditegakkan adalah *klaster proksimitas* (sekelompok node yang berbagi infrastruktur fisik atau routing, dideteksi melalui proksimitas routing Lokinet, pengaturan waktu uptime-proof, dan ASN), **bukan negara** dan bukan negara pendaftaran sebuah penyedia. Sebuah negara atau penyedia dengan beberapa fasilitas yang benar-benar independen lebih kecil risikonya dibandingkan satu fasilitas tunggal yang memegang pangsa besar. Data konsentrasi di bawah ini adalah snapshot per 19 Oktober 2026 (893 node aktif) yang dikelompokkan berdasarkan penyedia hosting, proksi terbaik yang tersedia sebelum Lokinet. Lokinet dirilis dalam rilis non-penegakan sebelum HF23, dan HF23 mengaktifkan penegakan.

Dokumen ini adalah pelengkap untuk Whitepaper Tokenomics EXIOM dan mengasumsikan bahwa whitepaper tersebut telah dibaca. Whitepaper membahas apa saja kontrol konsentrasi itu dan mengapa kontrol tersebut ada. Dokumen ini membahas detail mekanis tentang bagaimana setiap kontrol bekerja, data validasi testnet di balik HF22, matematika ekonomi yang tepat di balik pengubah hadiah-nol (zero-reward modifier), persoalan identitas operator pada rantai privasi, dan risiko residual yang tidak sepenuhnya diselesaikan oleh protokol.

---

## Data Konsentrasi Saat Ini

Diukur pada 19 Oktober 2026 pada 893 node aktif, dikelompokkan berdasarkan penyedia hosting (ASN), yang merupakan sinyal konsentrasi yang tersedia hari ini sebelum Lokinet. Penyedia adalah proksi yang jauh lebih baik untuk domain kegagalan bersama dibandingkan bendera negara, karena jaringan dan fasilitas satu perusahaan cenderung gagal, atau diperintahkan offline, secara bersamaan.

| Penyedia (ASN) | Node aktif | Pangsa |
|---|---|---|
| NodeHub (AS214083) | 444 | 49.7% |
| Contabo (AS51167, plus AS40021 dan Contabo Asia AS141995) | ~303 | ~34% |
| OVH (AS16276) | 62 | 6.9% |
| Oracle (AS31898) | 22 | 2.5% |
| WebNX (AS18450) | 12 | 1.3% |
| semua penyedia lain digabungkan (12 ASN lagi) | ~50 | ~5.6% |

NodeHub sendiri memegang 49.7% dari jaringan, jauh di atas batas daya tahan 30% (267 node pada 893 aktif), dan satu subnet /24 tunggal memegang 41.2%. Satu penyedia inilah konsentrasi yang hendak dipecahkan oleh HF23.

Bagaimana keadaan ini terjadi. Pecunia, sebuah layanan hosting yang menawarkan untuk menjalankan node XEQM bagi operator, menempatkan sebagian besar node-nya di Contabo. Kinerja Pecunia buruk, dan sejak itu banyak operator bermigrasi ke NodeHub. Jadi domain kegagalan dominan telah bergeser dari Contabo, yang masih memegang sekitar sepertiga dari jaringan (sebagian besarnya adalah fasilitas Grand Est), ke NodeHub, yang kini menjadi klaster tunggal terbesar di jaringan.

Catatan tentang angka negara. Negara pendaftaran sebuah penyedia bukanlah tempat server-nya berada. NodeHub terdaftar di US dan Contabo terdaftar di Jerman, sehingga tampilan per-negara menandai node mereka sebagai US dan DE terlepas dari pusat data fisiknya (fasilitas XEQM terbesar Contabo berada di Grand Est, Prancis). Protokol tidak membatasi negara maupun pendaftaran penyedia. Protokol membatasi klaster proksimitas, yaitu kumpulan node yang sebenarnya berbagi infrastruktur fisik atau routing. ASN dan subnet adalah proksi untuk itu saat ini, dan HF23 menggantinya dengan proksimitas routing Lokinet, yang juga dapat memisahkan fasilitas-fasilitas berbeda di dalam satu penyedia. Ambang batasnya adalah 30% dari node aktif per klaster (267 pada 893 saat ini), dihitung ulang secara berkelanjutan seiring pertumbuhan jaringan.

---

## Apa Artinya Ini bagi Operator Node

Bagian ini menjawab pertanyaan secara langsung: bagaimana HF23 memengaruhi cara Anda menjalankan node Anda?

**HF23 tidak membatasi berdasarkan negara, dan tidak mengharuskan satu node per IP, satu node per VPS, atau satu node per wallet.** Batasnya adalah 30% dari jaringan aktif per *klaster proksimitas* (node yang berbagi infrastruktur fisik atau routing). Seorang operator yang menjalankan 10, 50, atau bahkan 100 node pada infrastruktur bersama sama sekali tidak terpengaruh oleh HF23 selama klaster mereka tetap di bawah ambang batas tersebut. Anda dapat menjalankan beberapa node pada satu mesin, satu akun VPS, dan satu wallet. Tidak ada dalam HF23 yang mengubah hal itu.

**Pengubah hadiah-nol hanya berlaku untuk node di atas batas per-klaster (30% dari node aktif).** Node yang terdaftar paling lama dalam sebuah klaster memperoleh hadiah penuh hingga ambang batas tersebut. Hanya node yang berperingkat di atasnya dalam klaster yang terlalu terkonsentrasi yang memperoleh nol, dan hanya sampai node tersebut dimigrasikan ke klaster yang kurang terkonsentrasi.

**Deduplikasi kuorum membatasi pengaruh konsensus per ronde, bukan jumlah node atau pendapatan.** Seorang operator yang menjalankan 50 node pada satu VPS memperoleh hadiah blok untuk kesemua 50 node dan mengelola infrastruktur mereka persis seperti yang mereka lakukan hari ini. Mereka menerima satu kursi kuorum per klaster per ronde alih-alih berpotensi banyak, yang merupakan hasil yang dimaksudkan.

**Pendekatan yang tepat bagi operator baru** adalah memeriksa penjelajah node (node explorer), melihat di mana klaster-klaster yang ada terkonsentrasi, dan menerapkan node ke klaster yang berpopulasi ringan. Sepuluh node pada satu server dengan routing khasnya sendiri bekerja dengan sangat baik di bawah HF23 karena klaster tersebut jauh dari ambang batas 30%. Hadiah penuh, partisipasi kuorum penuh, tanpa masalah.

**Dinamika ini bekerja untuk keuntungan Anda jika Anda menerapkan node ke wilayah yang jarang.** Jika suatu wilayah pada akhirnya terisi penuh, penjelajah node menunjukkannya dan operator memiliki insentif finansial untuk pindah sebelum batas tersebut memengaruhi mereka. Operator yang tiba lebih dulu mempertahankan hadiah penuh pada node tertua mereka hingga ambang batas. Pendaftaran baru ke dalam klaster yang terlalu terkonsentrasi langsung tidak memperoleh apa-apa, sehingga ekonomi secara alami mendorong penerapan baru ke wilayah yang lebih ringan.

**Masalah spesifik yang diselesaikan HF23** adalah satu penyedia tunggal, NodeHub, yang kini menghosting sekitar separuh jaringan (444 node, 49.7%), dengan Contabo di posisi kedua pada sekitar sepertiga. Jika infrastruktur NodeHub mati atau diperintahkan untuk dimatikan, jaringan macet. Tujuannya adalah membawa klaster mana pun di bawah batas 30%. Setiap operator yang menjalankan pengaturan multi-node yang bertanggung jawab pada penyedia atau fasilitas yang berbeda dan tidak terkonsentrasi justru adalah hal yang paling dibutuhkan lebih banyak oleh jaringan.

---

## Mengapa Hard Fork Dipisahkan

HF22 dirilis setelah pengujian yang berhasil. Deduplikasi kuorum kunci-wallet dan penyatuan periode unbonding tidak memiliki ketergantungan pada Lokinet. Keduanya telah divalidasi di testnet dan menahannya sementara penilaian Lokinet masih tertunda merupakan penundaan yang tidak beralasan. Seorang aktor canggih yang membaca whitepaper sebelum HF22 dirilis dapat mencoba pemecahan wallet (wallet splitting) untuk mendahului kontrol kuorum, tetapi melakukannya dapat terdeteksi melalui korelasi pengaturan waktu uptime proof serta analisis IP/ASN dan menciptakan rekaman terdokumentasi untuk tindakan tata kelola.

Lokinet dirilis terlebih dahulu dalam rilis non-penegakannya sendiri (bersamaan dengan perubahan penyimpanan light-node SQLite), sehingga transport baru tidak dijadikan kritis-konsensus pada saat diperkenalkan. Selama rilis tersebut, pengelompokan proksimitas berjalan secara langsung dan dapat diamati tanpa konsekuensi hadiah, yaitu saat jumlah klaster yang sebenarnya diukur dan ambang batas serta fallback HF23 disetel. HF23 kemudian menyusul dan mengaktifkan penegakan. Memisahkan rilis juga memberikan domain kegagalan yang bersih: jika sesuatu berjalan salah setelah aktivasi HF23, variabel yang perlu diisolasi lebih sedikit. Hingga penegakan HF23 aktif, Grand Est tetap terekspos pada risiko daya tahan penuh di luar deduplikasi kuorum HF22.

---

## Mekanika HF22

### Deduplikasi Kuorum Kunci-Wallet

Algoritma pemilihan kuorum menjalankan satu lintasan deduplikasi atas setiap himpunan kandidat sebelum memfinalisasi. Ketika undian memilih sebuah node kandidat, algoritma memeriksa alamat wallet operatornya terhadap semua node yang sudah dipilih untuk ronde tersebut. Jika ditemukan kecocokan, kandidat digantikan dengan mengundi lagi dari kumpulan yang masih memenuhi syarat, mengecualikan semua alamat yang sudah terwakili.

Undian penggantian tidak berputar kembali melalui kandidat yang sudah ditolak. Undian menarik dari kumpulan yang belum terpilih dalam urutan berbobot-probabilitas yang sama dengan yang digunakan untuk undian awal. Ini mempertahankan properti statistik dari pemilihan kuorum tanpa memperkenalkan bias deterministik terhadap himpunan node tersisa tertentu mana pun.

**Hasil validasi testnet:**
- 20 siklus macet/pemulihan diselesaikan (20/20)
- Tingkat pemulihan 100% di seluruh siklus
- Nol intervensi manual diperlukan dalam siklus mana pun (kesenjangan blok terburuk 83 detik)
- Baseline mainnet pra-HF22: 1,000 blok, 100% Pulse, nol blok GOV_SIGNED
- Analisis timeout R0: tidak ada timeout R0 yang diperkenalkan dalam kondisi produksi. Analisis kepadatan mainnet saat ini mengonfirmasi bahwa setiap klaster IP berkepadatan tinggi adalah satu operator tunggal, yang berarti deduplikasi kunci-wallet sudah memberikan perlindungan penuh terhadap penerapan whale saat ini. Dua penerapan IP-tunggal terbesar (masing-masing 58 node dan 51 node) masing-masing adalah satu operator dan dibatasi menjadi satu kursi kuorum per ronde di bawah HF22.

**Apa arti satu kursi kuorum dalam praktiknya:** Ukuran kuorum dan frekuensi rotasi menentukan seberapa sering sebuah node berpartisipasi. Pada ukuran jaringan saat ini, batas satu kursi berarti pengaruh operator terkonsentrasi dalam sesi oracle, ronde Pulse, dan kuorum kewajiban (obligations) identik dengan pengaruh operator yang memiliki satu node. Pendapatan hadiah blok mereka tidak berubah.

**Celah pemecahan wallet dan deteksi sementaranya:** Seorang operator yang memecah 426 node ke 10 wallet memperoleh hingga 10 kursi kuorum per ronde alih-alih satu. Inilah celah yang diketahui yang ditutup oleh HF23. Untuk sementara, pemecahan wallet dapat terdeteksi melalui dua sinyal yang sudah tersedia tanpa perubahan daemon. Pertama, pengaturan waktu uptime proof: node pada host fisik atau hypervisor yang sama mengirimkan proof dalam hitungan milidetik satu sama lain, terlepas dari kunci wallet. Sekelompok proof yang tiba dalam jendela di bawah 10ms dari node yang terdaftar ke wallet berbeda adalah sinyal kuat infrastruktur bersama. Kedua, korelasi IP dan ASN: node pada wallet berbeda yang berbagi IP, subnet, atau ASN dicatat dan ditandai untuk peninjauan tata kelola. Seorang operator yang memecah wallet tetapi menyimpan semua node di fasilitas Contabo yang sama dapat diidentifikasi melalui kedua sinyal dan dikenai tindakan tata kelola di bawah kebijakan blocklist.

### Penyatuan Periode Unbonding

Periode unbonding deregistrasi paksa berubah dari 10,080 blok (kira-kira 7 hari) menjadi 20,160 blok (kira-kira 14 hari), menyamai periode penarikan sukarela. Ini adalah perubahan konstanta konsensus.

Periode paksa 7 hari yang asli adalah pilihan yang disengaja selama stabilisasi jaringan untuk membatasi penalti pada operator yang mengalami peristiwa infrastruktur di luar kendali mereka. Alasan itu tidak lagi berlaku. Jaringan telah stabil, sistem kredit dekomisioning menyediakan penyangga untuk pemadaman singkat, dan periode 14 hari yang disatukan menghapus asimetri yang tidak lagi memiliki pembenaran tersisa.

Koin XEQM dikunci on-chain selama periode unbonding melalui transaksi registrasi. Tidak ada mekanisme untuk melepaskan kunci lebih awal tanpa perubahan protokol. Untuk kegagalan infrastruktur yang terdokumentasi, tata kelola dapat mengompensasi hadiah yang terlewat dari wallet tata kelola sebagai transfer XEQM, tetapi kunci on-chain berjalan selama durasi penuhnya terlepas dari itu.

---

## Mekanika HF23

### Pengelompokan Proksimitas Lokinet

Lokinet (Low Latency Anonymous Routing Protocol, LLARP) merutekan lalu lintas melalui jaringan service node pada layer 3, mendukung TCP, UDP, dan ICMP. Setiap service node berpartisipasi sebagai relay. Graf routing yang muncul mencerminkan topologi jaringan fisik: node pada fasilitas yang sama merutekan melalui switch upstream yang sama dan backbone pusat data yang sama, menghasilkan pemilihan jalur yang berkorelasi dan latensi antar-node di bawah satu milidetik. Node pada fasilitas berbeda merutekan melalui jalur berbeda dengan latensi yang terukur lebih tinggi.

Algoritma pengelompokan menyerap pengukuran latensi routing Lokinet berpasangan dan tumpang-tindih jalur di seluruh node aktif dan mengelompokkannya ke dalam klaster menggunakan pengukuran ini sebagai sinyal proksimitas. Sebuah klaster bukanlah wilayah geografis yang tetap; ia adalah pengelompokan dinamis dari node yang perilaku routing-nya mengindikasikan infrastruktur fisik bersama. Dua node pada fasilitas Contabo berbeda di negara berbeda mungkin merutekan melalui cukup banyak infrastruktur backbone Contabo bersama sehingga tampak dalam klaster yang sama jika tumpang-tindih jalur mereka cukup tinggi. Dua node pada pusat data yang sama tetapi pada mesin fisik berbeda dengan koneksi upstream berbeda akan tampak dalam klaster berbeda jika tumpang-tindih jalur mereka rendah.

Sinyal pelengkap yang digunakan bersama proksimitas Lokinet:

**Korelasi pengaturan waktu uptime proof.** Jaringan sudah menerima uptime proof dari semua node aktif sesuai jadwal rutin. Distribusi timestamp kedatangan proof dari setiap node dicatat oleh node penerima. Node pada host fisik atau hypervisor VM yang sama mengirimkan proof dalam jendela ketat yang khas, biasanya di bawah 10 milidetik. Mengelompokkan distribusi pengaturan waktu kedatangan ini memberikan sinyal ko-lokasi fisik yang tidak memerlukan perubahan daemon dan bekerja sebelum Lokinet aktif.

**Analisis ASN.** Alamat IP setiap node dipetakan ke Autonomous System Number melalui data BGP publik. Node yang berbagi ASN berbagi infrastruktur routing tingkat-penyedia dan eksposur hukum tingkat-penyedia. Sebuah penyedia yang menerima perintah tingkat-yurisdiksi yang memengaruhi seluruh infrastruktur mereka akan menurunkan semua node ASN mereka secara bersamaan, terlepas dari berapa banyak klaster Lokinet tempat mereka muncul. Konsentrasi ASN dilacak sebagai sinyal pelengkap dan berkontribusi pada peninjauan tata kelola terhadap operator yang mendekati ambang batas klaster.

### Batas Registrasi Klaster

Pada saat registrasi, protokol menjalankan evaluasi proksimitas terhadap semua klaster yang ada. Karakteristik routing Lokinet dari node yang mendaftar diukur terhadap sentroid setiap klaster yang ada. Jika klaster terdekat sudah berisi 30% atau lebih dari node aktif, registrasi ditolak dengan kode error spesifik yang mengindikasikan kapasitas klaster dan jumlah node dari klaster terdekat.

Penolakannya bersifat deterministik: setiap node yang merutekan cukup mirip dengan klaster yang terlalu terkonsentrasi sehingga ditetapkan ke dalamnya akan ditolak, terlepas dari kunci wallet operator, riwayat registrasi, atau jumlah stake. Operator tidak dapat mengajukan banding atas penolakan melalui tata kelola. Satu-satunya jalan ke depan adalah mendaftar pada infrastruktur yang merutekan ke klaster berbeda.

Ambang batas dievaluasi terhadap jumlah node aktif pada saat registrasi. Seiring pertumbuhan jaringan, ambang batas 30% dalam angka absolut tumbuh bersamanya. Seorang operator yang berada pada batas hari ini dapat mendaftarkan node tambahan dalam klaster yang sebelumnya dibatasi seiring pertumbuhan jaringan dan naiknya batas absolut, tanpa memigrasikan node yang ada mana pun.

### Pengubah Hadiah-Nol

Pengubah hadiah-nol diterapkan pada saat perhitungan hadiah blok. Perhitungan hadiah untuk node yang terpilih mencakup pemeriksaan kelayakan klaster. Jika klaster node berisi lebih banyak node daripada ambang batas, dan peringkat registrasi node dalam klaster tersebut berada di atas ambang batas (diperingkat dari tertua ke terbaru), perhitungan hadiah menghasilkan nol.

Peringkat dihitung dari ketinggian blok registrasi node dalam penetapan klasternya. Node terlama terdaftar dalam klaster mendapat peringkat 1, yang paling baru terdaftar mendapat peringkat N. Node dengan peringkat lebih besar dari ambang batas memperoleh nol. Node dengan peringkat pada atau di bawah ambang batas memperoleh hadiah standar penuh. Peringkat dihitung ulang setiap kali penetapan klaster berubah, yang terjadi ketika node bermigrasi keluar dari klaster, ketika node baru bergabung, atau ketika batas klaster bergeser akibat perubahan topologi jaringan.

**Matematika ekonomi untuk Grand Est:** Pada 426 node dengan batas 208 node, 218 node memperoleh nol hadiah blok. Pada harga self-hosted sebesar $0.53 per node per bulan, 218 node tersebut berbiaya $115.54 per bulan dengan nol pendapatan. Pada harga Pecunia sebesar $1.76 per node per bulan, biayanya adalah $383.68 per bulan. Operator memiliki dua respons rasional: memigrasikan node berlebih ke klaster yang tidak terkonsentrasi, memulihkan hadiah mereka segera setelah registrasi baru diterima, atau menderegistrasi node berlebih dan memulihkan XEQM yang di-stake melalui proses unbonding. Salah satu respons mengurangi konsentrasi. Tidak ada dasar rasional untuk mempertahankan node berlebih pada hadiah nol.

**Mekanika masa tenggang (grace period):** Pada blok aktivasi HF23, protokol mengambil snapshot semua klaster aktif dan jumlah node-nya. Setiap klaster yang melampaui ambang batas 30% ditandai sebagai terlalu terkonsentrasi. Selama 30 hari setelah blok aktivasi, pengubah hadiah-nol ditangguhkan untuk semua node, termasuk yang berada di atas ambang batas. Selama masa tenggang, pemilik node dapat mengamati penetapan klaster di penjelajah node, merencanakan migrasi, dan mulai melaksanakannya. Pada blok berakhirnya masa tenggang, pengubah diaktifkan. Node yang telah bermigrasi keluar dari klaster yang terlalu terkonsentrasi pada blok tersebut memperoleh hadiah penuh sejak blok tersebut dan seterusnya. Node yang masih di atas ambang batas memperoleh nol sejak blok tersebut dan seterusnya hingga mereka bermigrasi.

### Deduplikasi Kuorum Klaster Proksimitas

Peningkatan deduplikasi kuorum HF23 menggantikan pemeriksaan alamat wallet dengan pemeriksaan keanggotaan klaster. Ketika undian memilih sebuah node kandidat, algoritma memeriksa penetapan klasternya terhadap semua node yang sudah dipilih untuk ronde tersebut. Jika dua node berbagi penetapan klaster, yang kedua digantikan oleh undian dari kumpulan tersisa, mengecualikan semua klaster yang sudah terwakili.

Dampak praktis pada operator yang memecah wallet: 10 alamat wallet yang tersebar di 426 node yang semuanya di fasilitas Contabo yang sama muncul dalam klaster proksimitas yang sama. Pemeriksaan klaster menangkap kesemuanya sebagai satu unit. Satu node dari klaster tersebut memegang kursi. 425 node lainnya dari klaster tersebut tidak, terlepas dari berapa banyak alamat wallet berbeda tempat mereka terdaftar.

### Persyaratan Jumlah Klaster Minimum dan Aturan Fallback

Ukuran kuorum jaringan EXIOM adalah 12 kursi per ronde. Oleh karena itu, deduplikasi klaster proksimitas memerlukan setidaknya 12 klaster proksimitas berbeda dalam himpunan node aktif untuk menjamin pembentukan kuorum. Jika jaringan menghasilkan kurang dari 12 klaster berbeda, algoritma tidak dapat memenuhi batasan satu-kursi-per-klaster dan pembentukan kuorum gagal.

Distribusi jaringan saat ini, setelah pengelompokan proksimitas Lokinet diterapkan, diperkirakan menghasilkan antara 12 dan 18 klaster berbeda. Ini sangat dekat secara tidak nyaman dengan minimum 12 kursi. Infrastruktur backbone penyedia bersama antara fasilitas yang nominalnya terpisah dapat menyebabkan dua lokasi IP berbeda bergabung menjadi satu klaster proksimitas dalam graf routing Lokinet. Penggabungan semacam itu yang mengurangi jumlah klaster di bawah 12 sepenuhnya mematahkan pembentukan kuorum.

Oleh karena itu, algoritma menerapkan aturan fallback wajib:

1. Algoritma mencoba mengisi semua 12 kursi dengan satu node per klaster berbeda, menelusuri klaster yang tersedia dalam urutan acak.
2. Jika semua klaster berbeda habis sebelum 12 kursi terisi, algoritma memasuki lintasan fallback.
3. Dalam lintasan fallback, ia mengizinkan node kedua dari setiap klaster, dimulai dengan klaster terkecil terlebih dahulu. Klaster yang paling tidak terkonsentrasi menerima kursi kedua sebelum klaster yang paling terkonsentrasi.
4. Algoritma melanjutkan lintasan fallback, menambah jumlah maksimum kursi per klaster sebanyak satu setiap lintasan, hingga 12 kursi terisi.
5. Klaster yang paling terkonsentrasi, seperti Grand Est dalam kondisi saat ini, menerima kursi tambahan hanya setelah semua klaster yang lebih kecil telah diberikan alokasi fallback mereka.

Setiap ronde yang memicu fallback dicatat beserta jumlah klaster yang menyebabkannya. Tata kelola memantau frekuensi fallback sebagai indikator langsung risiko konsentrasi. Jaringan dengan 12 atau lebih klaster berbeda tidak pernah memicu fallback. Jaringan yang secara konsisten memicu fallback menandakan bahwa penegakan konsentrasi HF23 belum mencapai keberagaman fisik yang memadai dan bahwa batas klaster atau penegakan masa tenggang memerlukan perhatian tata kelola.

Log fallback diterbitkan di penjelajah node bersama penetapan klaster sehingga komunitas operator dapat mengamati risiko konsentrasi secara real-time.

---

## Identitas Operator pada Rantai Privasi

Protokol tidak perlu mengidentifikasi operator manusia mana yang memiliki node mana untuk menegakkan batas klaster dan pengubah hadiah-nol. Kedua kontrol beroperasi pada tingkat klaster. Apa yang dapat dan tidak dapat ditentukan adalah konteks yang berguna untuk pemantauan tata kelola tetapi tidak diperlukan untuk penegakan protokol.

**Apa yang deterministik dari data on-chain:** node yang terdaftar di bawah kunci wallet operator yang sama secara pasti adalah operator yang sama. Ini adalah informasi publik dalam transaksi registrasi.

**Apa yang dapat disimpulkan dengan keyakinan tinggi dari data Lokinet dan pengaturan waktu:** jumlah host fisik berbeda yang mendasari sekelompok node, terlepas dari berapa banyak kunci wallet yang mereka gunakan. Lima kunci wallet yang masing-masing menjalankan 85 node, semuanya pada dua server fisik yang sama, menghasilkan dua tanda tangan pengaturan waktu berbeda dan dua sentroid proksimitas Lokinet, bukan lima.

**Apa yang tidak dapat ditentukan pada rantai privasi:** apakah dua kunci wallet berbeda dengan infrastruktur berbeda milik operator manusia yang sama. Sumber pendanaan setiap kunci wallet bersifat privat secara desain. Seorang operator canggih yang menggunakan lima wallet yang didanai dari lima sumber berbeda melalui lapisan transaksi rantai privasi menampilkan lima identitas berbeda pada tingkat protokol.

Untuk penegakan daya tahan, hal ini tidak menjadi masalah. Klaster berisi 426 node. 208 tertua memperoleh hadiah. 218 terbaru memperoleh nol. Identitas operator tidak relevan dengan perhitungan tersebut.

---

## Status Implementasi

| Kontrol | Status |
|---|---|
| Deduplikasi kuorum kunci-wallet operator | HF22, diaktifkan pada blok 219120 |
| Penyatuan periode unbonding, 7 ke 14 hari | HF22, diaktifkan |
| Pemulihan macet Pulse (fallback tanda tangan, snode_revision 1) | Diaktifkan pada blok 236920, 18 Oktober 2026 |
| Aktivasi Lokinet sebagai transport jaringan | Dalam pengembangan; dirilis dalam rilis non-penegakan sebelum HF23 |
| Penyimpanan light-node SQLite | Dalam pengembangan; dirilis bersama rilis Lokinet pra-HF23 |
| Algoritma pengelompokan proksimitas | Fase desain, menunggu penilaian Lokinet |
| Batas registrasi klaster, ambang batas 30% | HF23, fase desain |
| Pengubah hadiah-nol untuk node berlebih | HF23, fase desain |
| Mekanisme masa tenggang | HF23, fase desain |
| Deduplikasi kuorum klaster proksimitas dengan aturan fallback | HF23, fase desain |
| Pemantauan jumlah klaster minimum dan pencatatan fallback | HF23, fase desain |
| Perkakas korelasi pengaturan waktu uptime proof | Tidak memerlukan perubahan daemon, perkakas dalam pengembangan |
| Pelengkap pengelompokan ASN | Tidak memerlukan perubahan daemon, perkakas dalam pengembangan |

---

## Apa yang Tidak Diselesaikan oleh Kontrol Ini

**Konsentrasi hukum tingkat-penyedia.** Sebuah penyedia yang menerima perintah hukum tingkat-yurisdiksi yang memengaruhi seluruh infrastruktur global mereka akan menurunkan semua node mereka secara bersamaan, bahkan jika node-node tersebut muncul dalam beberapa klaster proksimitas Lokinet. Analisis ASN memunculkan risiko ini tetapi protokol tidak dapat menegakkan keberagaman penyedia tanpa mengharuskan operator mengungkapkan identitas penyedia mereka. Sebaran geografis yang secara alami dihasilkan oleh batas klaster secara substansial memitigasi risiko ini dalam praktiknya, karena operator yang terpaksa menyebar ke berbagai klaster pada praktiknya akan menggunakan beberapa penyedia.

**Penentuan identitas operator manusia lintas pemecahan wallet rantai-privasi.** Sebagaimana dijelaskan di atas, seorang operator canggih yang menggunakan beberapa wallet yang didanai melalui rantai privasi tidak dapat diidentifikasi pada tingkat protokol. Batas klaster dan pengubah hadiah-nol mengatasi risiko domain kegagalan terlepas dari identitas. Deduplikasi kuorum menutup celah pengaruh konsensus di HF23. Risiko residualnya adalah bahwa seorang operator canggih menjalankan banyak node di banyak klaster yang benar-benar berbeda, mengakumulasi pendapatan hadiah blok yang proporsional dengan jumlah node mereka sambil berkontribusi secara proporsional terhadap kesehatan jaringan. Ini adalah hasil yang dapat diterima: pengaruh konsensus yang terkonsentrasi dibatasi; partisipasi modal yang terdistribusi diberi hadiah.

Operator yang memiliki pertanyaan tentang penetapan klaster, perencanaan migrasi, atau linimasa HF22/HF23 dianjurkan untuk memposting di saluran Telegram Node Operators atau membuka issue di repositori ini.

---

## Bahasa yang Tersedia

Terjemahan komunitas dari dokumen ini dikelola di repositori whitepaper. Apabila terjadi konflik antara terjemahan dan versi bahasa Inggris, versi bahasa Inggris yang berlaku.

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

*Dokumen ini tidak merupakan nasihat keuangan atau hukum. XEQM adalah koin utilitas untuk platform EXIOM, bukan produk investasi. Klasifikasi token, status sekuritas, dan peraturan yang berlaku bervariasi menurut yurisdiksi. Peserta harus berkonsultasi dengan kerangka hukum dan regulasi lokal mereka sebelum memperoleh atau beroperasi dengan XEQM. XEQM Labs tidak menganjurkan pembelian XEQM atas dasar apresiasi harga spekulatif.*
