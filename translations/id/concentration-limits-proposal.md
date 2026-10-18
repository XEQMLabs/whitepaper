# Batas Konsentrasi Node - Penegakan Daya Tahan Jaringan
## Pendamping Teknis untuk Whitepaper Tokenomics EXIOM
### 07/26/2026

> **Catatan cakupan (diperbarui Oktober 2026).** Unit yang ditegakkan adalah *cluster kedekatan* (sekelompok node yang berbagi infrastruktur fisik atau routing, dideteksi via kedekatan routing Lokinet, timing bukti-uptime, dan ASN), **bukan negara**. Negara dengan beberapa fasilitas independen tidak terpengaruh. Angka negara di bawah adalah proksi geografis kasar untuk di mana konsentrasi saat ini berada, bukan hal yang dibatasi protokol. Jumlah node dalam pendamping ini adalah snapshot Juli 2026 (~672 node); lihat whitepaper untuk total jaringan saat ini (943 node per 27 September 2026). Lokinet dirilis dalam rilis non-penegakan sebelum HF23, dan HF23 mengaktifkan penegakan.

Dokumen ini adalah pendamping untuk Whitepaper Tokenomics EXIOM dan mengasumsikan whitepaper tersebut telah dibaca. Whitepaper mencakup apa kontrol konsentrasi itu dan mengapa mereka ada. Dokumen ini mencakup detail mekanis tentang bagaimana setiap kontrol bekerja, data validasi testnet di balik HF22, matematika ekonomi yang presisi di balik modifier reward-nol, pertanyaan identitas operator pada chain privasi, dan risiko residual yang tidak sepenuhnya diselesaikan protokol.

---

## Data Konsentrasi Saat Ini

| Negara | Node aktif |
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

France menampung 492 dari 672 node dalam snapshot ini (sekitar 73% dari jaringan), dan konsentrasi itu hampir seluruhnya adalah satu fasilitas Contabo di Grand Est yang menampung kira-kira 426 node (sekitar 63% dari jaringan). Total negara bukanlah yang dibatasi protokol; **cluster** Grand Est lah yang dibatasi. Ambang daya tahan adalah 30% node aktif per cluster kedekatan (sekitar 202 node pada snapshot 672 ini, dan sekitar 283 pada 943 node dalam whitepaper saat ini), dihitung ulang terus-menerus seiring jaringan tumbuh. Grand Est pada kira-kira 426 node lebih dari dua kali lipat cap itu.

---

## Apa Artinya Ini bagi Operator Node

Bagian ini menjawab pertanyaan secara langsung: bagaimana HF23 memengaruhi cara Anda menjalankan node Anda?

**HF23 tidak membatasi berdasarkan negara, dan tidak mengharuskan satu node per IP, satu node per VPS, atau satu node per wallet.** Cap-nya adalah 30% dari jaringan aktif per *cluster kedekatan* (node yang berbagi infrastruktur fisik atau routing). Operator yang menjalankan 10, 50, atau bahkan 100 node pada infrastruktur bersama sama sekali tidak terpengaruh oleh HF23 selama cluster mereka tetap di bawah ambang batas itu. Anda dapat menjalankan beberapa node pada satu mesin, satu akun VPS, dan satu wallet. Tidak ada dalam HF23 yang mengubah itu.

**Modifier reward-nol hanya berlaku untuk node di atas cap per-cluster (30% node aktif).** Node terdaftar tertua dalam sebuah cluster memperoleh reward penuh hingga ambang batas itu. Hanya node yang diperingkat di atasnya dalam cluster yang terlalu-terkonsentrasi memperoleh nol, dan hanya sampai mereka dimigrasikan ke cluster yang kurang terkonsentrasi.

**Deduplikasi kuorum membatasi pengaruh konsensus per ronde, bukan jumlah node atau pendapatan.** Operator yang menjalankan 50 node pada satu VPS memperoleh block reward pada semua 50 dan mengelola infrastruktur mereka persis seperti yang mereka lakukan hari ini. Mereka menerima satu kursi kuorum per cluster per ronde alih-alih berpotensi banyak, yang merupakan hasil yang dimaksudkan.

**Pendekatan yang tepat untuk operator baru** adalah memeriksa node explorer, melihat di mana cluster yang ada terkonsentrasi, dan men-deploy ke cluster yang padat-ringan. Sepuluh node pada satu server dengan routing-nya sendiri yang berbeda bekerja dengan sangat baik di bawah HF23 karena cluster itu sama sekali tidak mendekati ambang batas 30%. Reward penuh, partisipasi kuorum penuh, tanpa masalah.

**Dinamikanya bekerja menguntungkan Anda jika Anda men-deploy ke region yang jarang.** Jika suatu region akhirnya terisi penuh, node explorer menunjukkannya dan operator memiliki insentif finansial untuk pindah sebelum cap memengaruhi mereka. Operator yang sampai di sana lebih dulu mempertahankan reward penuh pada node tertua mereka hingga ambang batas. Registrasi baru ke cluster yang terlalu-terkonsentrasi memperoleh nol segera, sehingga ekonomi secara alami mendorong deployment baru ke region yang lebih ringan.

**Masalah spesifik yang diselesaikan HF23** adalah satu fasilitas di France (cluster Contabo Grand Est) yang menampung kira-kira 426 node, sekitar 63% dari jaringan dalam snapshot ini. Jika fasilitas itu offline jaringan macet. Tujuannya adalah membawa cluster itu di bawah cap 30%. Setiap operator lain yang menjalankan setup multi-node yang bertanggung jawab di cluster yang tidak terkonsentrasi adalah persis apa yang lebih dibutuhkan jaringan.

---

## Mengapa Hard Fork Dipisahkan

HF22 dirilis setelah pengujian yang sukses. Deduplikasi kuorum kunci-wallet dan unifikasi periode unbonding tidak memiliki ketergantungan pada Lokinet. Keduanya telah divalidasi di testnet dan menahannya sementara penilaian Lokinet tertunda adalah penundaan yang tidak dapat dibenarkan. Aktor canggih yang membaca whitepaper sebelum HF22 dirilis dapat mencoba pemecahan wallet untuk mendahului kontrol kuorum, tetapi melakukannya dapat dideteksi melalui korelasi timing bukti uptime dan analisis IP/ASN serta menciptakan catatan terdokumentasi untuk tindakan tata kelola.

Lokinet dirilis lebih dulu dalam rilis non-penegakannya sendiri (bersama perubahan penyimpanan light-node SQLite), sehingga transport baru tidak dibuat kritis-konsensus saat ia baru diperkenalkan. Selama rilis itu pengelompokan kedekatan berjalan aktif dan dapat diamati tanpa konsekuensi reward, yang merupakan saat jumlah cluster riil diukur dan ambang batas serta fallback HF23 disetel. HF23 kemudian menyusul dan mengaktifkan penegakan. Memisahkan rilis juga memberikan failure domain yang bersih: jika terjadi kesalahan setelah aktivasi HF23 ada lebih sedikit variabel untuk diisolasi. Sampai penegakan HF23 aktif, Grand Est tetap terekspos pada risiko daya tahan penuh di luar dedup kuorum HF22.

---

## Mekanika HF22

### Deduplikasi Kuorum Kunci-Wallet

Algoritme seleksi kuorum menjalankan pass deduplikasi atas setiap himpunan kandidat sebelum finalisasi. Ketika pengundian memilih node kandidat, algoritme memeriksa alamat wallet operatornya terhadap semua node yang sudah dipilih untuk ronde tersebut. Jika kecocokan ditemukan, kandidat diganti dengan mengundi lagi dari pool yang memenuhi syarat yang tersisa, mengecualikan semua alamat yang sudah terwakili.

Pengundian pengganti tidak berputar kembali melalui kandidat yang sudah ditolak. Ia mengundi dari pool tak-terpilih yang tersisa dalam urutan terbobot-probabilitas yang sama yang digunakan untuk pengundian awal. Ini menjaga properti statistik dari seleksi kuorum tanpa memperkenalkan bias deterministik ke arah himpunan node tersisa tertentu.

**Hasil validasi testnet:**
- 20 siklus stall/pemulihan selesai (20/20)
- Tingkat pemulihan 100% di seluruh siklus
- Nol intervensi manual diperlukan dalam siklus mana pun (gap blok terburuk 83 detik)
- Baseline mainnet pra-HF22: 1,000 blok, 100% Pulse, nol blok GOV_SIGNED
- Analisis timeout R0: tidak ada timeout R0 yang diperkenalkan dalam kondisi produksi. Analisis kepadatan mainnet saat ini mengonfirmasi setiap cluster IP berkepadatan-tinggi adalah satu operator, yang berarti dedup kunci-wallet sudah memberikan perlindungan penuh terhadap deployment whale saat ini. Dua deployment IP-tunggal terbesar (masing-masing 58 node dan 51 node) masing-masing adalah satu operator dan dibatasi pada satu kursi kuorum per ronde di bawah HF22.

**Apa arti satu kursi kuorum dalam praktik:** Ukuran kuorum dan frekuensi rotasi menentukan seberapa sering sebuah node berpartisipasi. Pada ukuran jaringan saat ini, cap kursi-tunggal berarti pengaruh operator terkonsentrasi dalam sesi oracle, ronde Pulse, dan kuorum kewajiban identik dengan pengaruh operator yang memiliki satu node. Pendapatan block reward mereka tidak berubah.

**Celah pemecahan-wallet dan deteksi interimnya:** Operator yang memecah 426 node di seluruh 10 wallet mendapatkan hingga 10 kursi kuorum per ronde alih-alih satu. Ini adalah celah yang diketahui yang ditutup HF23. Sementara itu, pemecahan wallet dapat dideteksi melalui dua sinyal yang sudah tersedia tanpa perubahan daemon. Pertama, timing bukti uptime: node pada host fisik atau hypervisor yang sama mengirimkan bukti dalam milidetik satu sama lain, terlepas dari kunci wallet. Cluster bukti yang tiba dalam jendela sub-10ms dari node yang terdaftar ke wallet berbeda adalah sinyal kuat infrastruktur bersama. Kedua, korelasi IP dan ASN: node pada wallet berbeda yang berbagi IP, subnet, atau ASN dicatat dan ditandai untuk peninjauan tata kelola. Operator yang memecah-wallet tetapi menjaga semua node di fasilitas Contabo yang sama dapat diidentifikasi melalui kedua sinyal dan tunduk pada tindakan tata kelola di bawah kebijakan blocklist.

### Unifikasi Periode Unbonding

Periode unbonding deregistrasi paksa berubah dari 10,080 blok (sekitar 7 hari) menjadi 20,160 blok (sekitar 14 hari), menyamai periode penarikan sukarela. Ini adalah perubahan konstanta konsensus.

Periode paksa 7-hari asli adalah pilihan yang disengaja selama stabilisasi jaringan untuk membatasi penalti pada operator yang mengalami peristiwa infrastruktur di luar kendali mereka. Rasional itu tidak lagi berlaku. Jaringan stabil, sistem kredit decommission menyediakan buffer untuk pemadaman singkat, dan periode terunifikasi 14-hari menghapus asimetri yang tidak memiliki justifikasi tersisa.

Koin XEQM terkunci on-chain selama periode unbonding via transaksi registrasi. Tidak ada mekanisme untuk melepaskan kunci lebih awal tanpa perubahan protokol. Untuk kegagalan infrastruktur terdokumentasi, tata kelola dapat mengompensasi reward yang terlewat dari wallet tata kelola sebagai transfer XEQM, tetapi kunci on-chain berjalan durasi penuhnya terlepas.

---

## Mekanika HF23

### Pengelompokan Kedekatan Lokinet

Lokinet (Low Latency Anonymous Routing Protocol, LLARP) merutekan lalu lintas melalui jaringan service node pada layer 3, mendukung TCP, UDP, dan ICMP. Setiap service node berpartisipasi sebagai relay. Routing graph yang muncul mencerminkan topologi jaringan fisik: node di fasilitas yang sama merutekan melalui switch upstream yang sama dan backbone datacenter yang sama, menghasilkan pemilihan jalur berkorelasi dan latensi antar-node sub-milidetik. Node di fasilitas berbeda merutekan melalui jalur berbeda dengan latensi yang terukur lebih tinggi.

Algoritme pengelompokan menyerap pengukuran latensi routing Lokinet berpasangan dan tumpang tindih jalur di seluruh node aktif dan mengelompokkan mereka ke dalam cluster menggunakan pengukuran ini sebagai sinyal kedekatan. Sebuah cluster bukanlah region geografis tetap; ia adalah pengelompokan dinamis node yang perilaku routing-nya mengindikasikan infrastruktur fisik bersama. Dua node di fasilitas Contabo berbeda di negara berbeda mungkin merutekan melalui cukup banyak infrastruktur backbone Contabo bersama untuk muncul dalam cluster yang sama jika tumpang tindih jalur mereka cukup tinggi. Dua node di datacenter yang sama tetapi pada mesin fisik berbeda dengan koneksi upstream berbeda akan muncul dalam cluster berbeda jika tumpang tindih jalur mereka rendah.

Sinyal suplemental yang digunakan bersama kedekatan Lokinet:

**Korelasi timing bukti uptime.** Jaringan sudah menerima bukti uptime dari semua node aktif pada jadwal reguler. Distribusi timestamp kedatangan bukti dari setiap node dicatat oleh node penerima. Node pada host fisik atau hypervisor VM yang sama mengirimkan bukti dalam jendela rapat yang khas, biasanya di bawah 10 milidetik. Mengelompokkan distribusi timing kedatangan ini menyediakan sinyal kolokasi fisik yang tidak memerlukan perubahan daemon dan bekerja sebelum Lokinet aktif.

**Analisis ASN.** Alamat IP setiap node dipetakan ke Autonomous System Number via data BGP publik. Node yang berbagi ASN berbagi infrastruktur routing tingkat-penyedia dan eksposur hukum tingkat-penyedia. Penyedia yang menerima perintah tingkat-yurisdiksi yang memengaruhi semua infrastruktur mereka menjatuhkan semua node ASN mereka secara bersamaan, terlepas dari berapa banyak cluster Lokinet tempat mereka muncul. Konsentrasi ASN dilacak sebagai sinyal suplemental dan berkontribusi pada peninjauan tata kelola operator yang dekat ambang cluster.

### Batas Registrasi Cluster

Pada saat registrasi, protokol menjalankan evaluasi kedekatan terhadap semua cluster yang ada. Karakteristik routing Lokinet node yang meregistrasi diukur terhadap centroid setiap cluster yang ada. Jika cluster terdekat sudah berisi 30% atau lebih dari node aktif, registrasi ditolak dengan kode error spesifik yang mengindikasikan kapasitas cluster dan jumlah node dari cluster terdekat.

Penolakan bersifat deterministik: node mana pun yang merutekan cukup mirip dengan cluster yang terlalu-terkonsentrasi untuk ditetapkan kepadanya ditolak, terlepas dari kunci wallet operator, riwayat registrasi, atau jumlah stake. Operator tidak dapat mengajukan banding atas penolakan melalui tata kelola. Satu-satunya jalan ke depan adalah meregistrasi pada infrastruktur yang merutekan ke cluster berbeda.

Ambang batas dievaluasi terhadap jumlah node aktif pada saat registrasi. Seiring jaringan tumbuh, ambang 30% dalam istilah absolut tumbuh bersamanya. Operator pada cap hari ini dapat meregistrasi node tambahan dalam cluster yang sebelumnya di-cap seiring jaringan tumbuh dan cap absolut naik, tanpa memigrasikan node yang ada mana pun.

### Modifier Reward-Nol

Modifier reward-nol diterapkan pada saat kalkulasi block reward. Kalkulasi reward untuk node yang terpilih mencakup pemeriksaan kelayakan cluster. Jika cluster node berisi lebih banyak node daripada ambang cap, dan peringkat registrasi node dalam cluster itu di atas ambang batas (diperingkat tertua ke terbaru), kalkulasi reward mengembalikan nol.

Peringkat dihitung dari tinggi blok registrasi node dalam penetapan cluster-nya. Node terdaftar tertua dalam cluster mendapat peringkat 1, yang paling baru terdaftar mendapat peringkat N. Node dengan peringkat lebih besar dari ambang cap memperoleh nol. Node dengan peringkat pada atau di bawah ambang cap memperoleh reward standar penuh. Peringkat dihitung ulang setiap kali penetapan cluster berubah, yang terjadi ketika node bermigrasi keluar dari cluster, ketika node baru bergabung, atau ketika batas cluster bergeser karena perubahan topologi jaringan.

**Matematika ekonomi untuk Grand Est:** Pada 426 node dengan cap 208-node, 218 node memperoleh block reward nol. Pada harga self-hosted $0.53 per node per bulan, 218 node itu menelan biaya $115.54 per bulan tanpa pendapatan. Pada harga Pecunia $1.76 per node per bulan, biayanya $383.68 per bulan. Operator memiliki dua respons rasional: memigrasikan node berlebih ke cluster yang tidak terkonsentrasi, memulihkan reward mereka segera setelah registrasi baru diterima, atau men-deregistrasi node berlebih dan memulihkan XEQM yang di-stake melalui proses unbonding. Respons mana pun mengurangi konsentrasi. Tidak ada dasar rasional untuk mempertahankan node berlebih pada reward nol.

**Mekanika periode tenggang:** Pada blok aktivasi HF23, protokol mengambil snapshot semua cluster aktif dan jumlah node mereka. Cluster mana pun yang melebihi ambang 30% ditandai sebagai terlalu-terkonsentrasi. Selama 30 hari setelah blok aktivasi, modifier reward-nol ditangguhkan untuk semua node, termasuk yang di atas ambang cap. Selama periode tenggang, pemilik node dapat mengamati penetapan cluster node explorer, merencanakan migrasi, dan mulai mengeksekusinya. Pada blok berakhirnya periode tenggang, modifier aktif. Node yang telah bermigrasi keluar dari cluster yang terlalu-terkonsentrasi pada blok itu memperoleh reward penuh dari blok itu ke depan. Node yang masih di atas ambang batas memperoleh nol dari blok itu ke depan sampai mereka bermigrasi.

### Deduplikasi Kuorum Cluster Kedekatan

Peningkatan deduplikasi kuorum HF23 menggantikan pemeriksaan alamat wallet dengan pemeriksaan keanggotaan cluster. Ketika pengundian memilih node kandidat, algoritme memeriksa penetapan cluster-nya terhadap semua node yang sudah dipilih untuk ronde tersebut. Jika dua node berbagi penetapan cluster, yang kedua diganti dengan pengundian dari pool yang tersisa, mengecualikan semua cluster yang sudah terwakili.

Efek praktis pada operator pemecah-wallet: 10 alamat wallet di seluruh 426 node semuanya di fasilitas Contabo yang sama muncul dalam cluster kedekatan yang sama. Pemeriksaan cluster menangkap mereka semua sebagai satu unit. Satu node dari cluster itu memegang kursi. 425 node lainnya dari cluster itu tidak, terlepas dari berapa banyak alamat wallet berbeda yang menjadi tempat mereka terdaftar.

### Persyaratan Jumlah Cluster Minimum dan Aturan Fallback

Ukuran kuorum jaringan EXIOM adalah 12 kursi per ronde. Oleh karena itu deduplikasi cluster kedekatan memerlukan setidaknya 12 cluster kedekatan yang berbeda dalam himpunan node aktif untuk menjamin pembentukan kuorum. Jika jaringan menghasilkan kurang dari 12 cluster berbeda, algoritme tidak dapat memenuhi batasan satu-kursi-per-cluster dan pembentukan kuorum gagal.

Distribusi jaringan saat ini, begitu pengelompokan kedekatan Lokinet diterapkan, diperkirakan menghasilkan antara 12 dan 18 cluster berbeda. Ini sangat dekat secara tidak nyaman dengan minimum 12-kursi. Infrastruktur backbone penyedia bersama antara fasilitas yang secara nominal terpisah dapat menyebabkan dua lokasi IP berbeda menyatu menjadi satu cluster kedekatan dalam routing graph Lokinet. Penggabungan semacam itu yang mengurangi jumlah cluster di bawah 12 sepenuhnya merusak pembentukan kuorum.

Oleh karena itu algoritme mengimplementasikan aturan fallback wajib:

1. Algoritme mencoba mengisi semua 12 kursi dengan satu node per cluster berbeda, bekerja melalui cluster yang tersedia dalam urutan acak.
2. Jika semua cluster berbeda habis sebelum 12 kursi terisi, algoritme memasuki pass fallback.
3. Dalam pass fallback, ia mengizinkan node kedua dari setiap cluster, dimulai dengan cluster terkecil terlebih dahulu. Cluster yang paling tidak terkonsentrasi menerima kursi kedua sebelum yang paling terkonsentrasi.
4. Algoritme melanjutkan pass fallback, menaikkan kursi maksimum per cluster satu per pass, sampai 12 kursi terisi.
5. Cluster paling terkonsentrasi, seperti Grand Est di bawah kondisi saat ini, menerima kursi tambahan hanya setelah semua cluster yang lebih kecil diberi alokasi fallback mereka.

Setiap ronde yang memicu fallback dicatat dengan jumlah cluster yang menyebabkannya. Tata kelola memantau frekuensi fallback sebagai indikator risiko konsentrasi langsung. Jaringan dengan 12 atau lebih cluster berbeda tidak pernah memicu fallback. Jaringan yang secara konsisten memicu fallback memberi sinyal bahwa penegakan konsentrasi HF23 belum mencapai keragaman fisik yang memadai dan bahwa cap cluster atau penegakan periode tenggang memerlukan perhatian tata kelola.

Log fallback dipublikasikan di node explorer bersama penetapan cluster sehingga komunitas operator dapat mengamati risiko konsentrasi secara real time.

---

## Identitas Operator pada Chain Privasi

Protokol tidak perlu mengidentifikasi operator manusia mana yang memiliki node mana untuk menegakkan cap cluster dan modifier reward-nol. Kedua kontrol beroperasi pada tingkat cluster. Apa yang dapat dan tidak dapat ditentukan adalah konteks berguna untuk pemantauan tata kelola tetapi tidak diperlukan untuk penegakan protokol.

**Apa yang deterministik dari data on-chain:** node yang terdaftar di bawah kunci wallet operator yang sama secara definitif adalah operator yang sama. Ini adalah informasi publik dalam transaksi registrasi.

**Apa yang dapat disimpulkan dengan keyakinan tinggi dari data Lokinet dan timing:** jumlah host fisik berbeda yang mendasari cluster node, terlepas dari berapa banyak kunci wallet yang mereka gunakan. Lima kunci wallet yang masing-masing menjalankan 85 node, semuanya pada dua server fisik yang sama, menghasilkan dua tanda tangan timing berbeda dan dua centroid kedekatan Lokinet, bukan lima.

**Apa yang tidak dapat ditentukan pada chain privasi:** apakah dua kunci wallet berbeda dengan infrastruktur berbeda milik operator manusia yang sama. Sumber pendanaan setiap kunci wallet bersifat privat secara desain. Operator canggih yang menggunakan lima wallet yang didanai dari lima sumber berbeda melalui lapisan transaksi chain privasi menyajikan lima identitas berbeda pada tingkat protokol.

Untuk penegakan daya tahan, ini tidak penting. Cluster berisi 426 node. 208 tertua memperoleh reward. 218 terbaru memperoleh nol. Identitas operator tidak relevan dengan kalkulasi itu.

---

## Status Implementasi

| Kontrol | Status |
|---|---|
| Dedup kuorum kunci-wallet operator | HF22, diaktifkan pada blok 219120 |
| Unifikasi periode unbonding, 7 ke 14 hari | HF22, diaktifkan |
| Pemulihan stall Pulse (fallback tanda tangan, snode_revision 1) | Diaktifkan pada blok 236920, 18 Oktober 2026 |
| Aktivasi Lokinet sebagai transport jaringan | Dalam pengembangan; dirilis dalam rilis non-penegakan sebelum HF23 |
| Penyimpanan light-node SQLite | Dalam pengembangan; dirilis bersama rilis Lokinet pra-HF23 |
| Algoritme pengelompokan kedekatan | Fase desain, menunggu penilaian Lokinet |
| Batas registrasi cluster, ambang 30% | HF23, fase desain |
| Modifier reward-nol untuk node berlebih | HF23, fase desain |
| Mekanisme periode tenggang | HF23, fase desain |
| Dedup kuorum cluster kedekatan dengan aturan fallback | HF23, fase desain |
| Pemantauan jumlah cluster minimum dan logging fallback | HF23, fase desain |
| Perkakas korelasi timing bukti uptime | Tanpa perubahan daemon diperlukan, perkakas dalam pengembangan |
| Suplemen pengelompokan ASN | Tanpa perubahan daemon diperlukan, perkakas dalam pengembangan |

---

## Apa yang Tidak Diselesaikan Kontrol Ini

**Konsentrasi hukum tingkat-penyedia.** Penyedia yang menerima perintah hukum tingkat-yurisdiksi yang memengaruhi semua infrastruktur global mereka menjatuhkan semua node mereka secara bersamaan, bahkan jika node tersebut muncul dalam beberapa cluster kedekatan Lokinet. Analisis ASN memunculkan risiko ini tetapi protokol tidak dapat menegakkan keragaman penyedia tanpa mengharuskan pengungkapan operator atas identitas penyedia mereka. Sebaran geografis yang secara alami dihasilkan oleh cap cluster secara substansial memitigasi risiko ini dalam praktik, karena operator yang terpaksa mendistribusikan di seluruh cluster dalam praktik akan menggunakan beberapa penyedia.

**Penentuan identitas operator manusia di seluruh pemecahan wallet chain-privasi.** Seperti dijelaskan di atas, operator canggih yang menggunakan beberapa wallet yang didanai melalui chain privasi tidak dapat diidentifikasi pada tingkat protokol. Cap cluster dan modifier reward-nol mengatasi risiko failure domain terlepas dari identitas. Dedup kuorum menutup celah pengaruh konsensus di HF23. Risiko residualnya adalah bahwa operator canggih menjalankan banyak node di seluruh banyak cluster yang benar-benar berbeda, mengakumulasi pendapatan block reward sebanding dengan jumlah node mereka sambil berkontribusi secara proporsional pada kesehatan jaringan. Ini adalah hasil yang dapat diterima: pengaruh konsensus terkonsentrasi dibatasi; partisipasi modal terdistribusi diberi reward.

Operator dengan pertanyaan tentang penetapan cluster, perencanaan migrasi, atau timeline HF22/HF23 didorong untuk memposting di kanal Telegram Node Operators atau membuka issue di repositori ini.

---

## Bahasa yang Tersedia

Terjemahan komunitas atas dokumen ini dipelihara dalam repositori whitepaper. Jika terjadi konflik apa pun antara terjemahan dan versi bahasa Inggris, versi bahasa Inggris yang berlaku.

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

*Dokumen ini bukan merupakan nasihat keuangan atau hukum. XEQM adalah koin utilitas untuk platform EXIOM, bukan produk investasi. Klasifikasi token, status sekuritas, dan regulasi yang berlaku bervariasi menurut yurisdiksi. Peserta harus berkonsultasi dengan kerangka hukum dan regulasi lokal mereka sebelum memperoleh atau beroperasi dengan XEQM. XEQM Labs tidak mendorong pembelian XEQM atas dasar apresiasi harga spekulatif.*
