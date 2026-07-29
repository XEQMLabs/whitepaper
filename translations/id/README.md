# XEQM Labs - Platform EXIOM
## Whitepaper Tokenomik
### Draf v11 | 26/07/2026

---

## Layanan yang Sudah Aktif vs. Rencana Mendatang

| Komponen | Status |
|---|---|
| Mainnet EXIOM | Aktif, beroperasi sejak 6 Mei 2026 |
| Layanan jaringan node | Aktif, 693 node aktif, 184 operator (Juli 2026) |
| Lokinet (LLARP) | Hadir dalam basis kode, status aktivasi dalam penilaian rekayasa |
| Pertukaran koin XEQ ke XEQM | Selesai dan ditutup, siklus produksi 35 hari, buku besar publik yang dapat diaudit |
| Dompet GUI | Aktif, github.com/XEQMLabs/XEQMLabs-GUI |
| Penjelajah Node (Node explorer) | Aktif, pemantauan layanan node secara langsung |
| API Pengembang EXIOM | Dalam pengembangan, Fase 2 (AKTIF) |
| Privasi Oracle EXIOM | Dirancang, pra-implementasi, Fase 3 |
| Platform Perdagangan RFQ EXIOM | Dalam pengembangan, Fase 2/3, pasangan pertama XEQM/BTC |
| HF22, dedup kuorum dompet-kunci & unifikasi unbonding | Memasuki testnet, tervalidasi, tanpa ketergantungan Lokinet |
| HF23, batas kluster kedekatan, pengubah hadiah, transport Lokinet | Tahap desain, menunggu penilaian rekayasa Lokinet |
| Tata Kelola On-Chain Formal | Direncanakan, Fase 6 |

---

## 1. Apa Itu XEQM Labs

XEQM Labs adalah perusahaan teknologi privasi. Produk unggulannya, EXIOM, adalah jaringan Proof-of-Stake Layer 1 yang menjaga privasi serta platform pengembang komersial yang dioperasikan oleh kumpulan layanan node global. XEQM adalah koin akses dan penggunaan untuk platform tersebut. Pengembang melakukan staking XEQM untuk membuka tingkatan API. Aplikasi mengonsumsi XEQM saat melakukan panggilan API. Operator layanan node memperoleh XEQM karena mengamankan jaringan. Operator API node memperoleh XEQM karena melayani lalu lintas pengembang.

Proyek ini melanjutkan riwayat komunitas dan operasional yang telah berlangsung lebih dari tujuh tahun. Mainnet EXIOM dibangun untuk memberikan jaringan dengan pasokan yang dapat diverifikasi, jadwal emisi yang dapat diprediksi, konsensus Proof-of-Stake murni tanpa komponen Proof-of-Work, serta mekanika layanan node yang menghargai waktu dan modal operator.

XEQM adalah koin native Layer 1, tidak ditokenisasi di rantai lain mana pun, bukan aset ERC-20 atau wrapped asset, dan tidak menggunakan bridge. Pemegang koin berinteraksi langsung dengan mainnet EXIOM.

### Lini Produk EXIOM

**Layanan jaringan Node EXIOM.** Aktif di mainnet. Kumpulan layanan node global mengamankan rantai, memperoleh hadiah blok, dan membentuk lapisan infrastruktur tempat semua produk EXIOM lainnya berjalan. Terdapat 693 node aktif di 184 operator independen per Juli 2026.

**Pertukaran Koin EXIOM.** Produk komersial yang memungkinkan proyek memigrasikan komunitas pemegang token dari rantai lama ke rantai baru dengan keterauditan kriptografis penuh. Uji coba perdana adalah migrasi pemegang XEQ ke XEQM di mainnet EXIOM, berjalan selama 35 hari dengan setiap pengajuan diproses melalui buku besar terverifikasi secara kriptografis yang memiliki sidik jari SHA256 publik. Produk ini tersedia untuk proyek lain yang memerlukan migrasi rantai terverifikasi.

**API Pengembang Privat EXIOM.** Dalam pengembangan. Platform pengembang yang memaparkan kemampuan privasi jaringan melalui API terstruktur. Pengembang melakukan staking XEQM untuk membuka tingkatan akses. Aplikasi mengonsumsi XEQM saat melakukan panggilan API. Operator API node memperoleh bagian proporsional dari biaya platform. Fase 2, aktif.

**Privasi Oracle EXIOM.** Dirancang, pra-implementasi. Oracle mengutamakan privasi yang membuktikan fakta tentang data web privat tanpa mengekspos sumber mendasar. Baik platform perdagangan RFQ EXIOM maupun aplikasi pihak ketiga yang dibangun di atas API EXIOM dapat mengonsumsi output oracle. Fase 3.

**Platform Perdagangan RFQ EXIOM.** Dalam pengembangan. Platform perdagangan antar individu tanpa konter dengan atestasi penyelesaian kriptografis, dibangun di atas API EXIOM. Pasangan perdagangan pertama adalah XEQM/BTC, keduanya merupakan aset native Layer 1 tanpa tokenisasi, tanpa wrapping, dan tanpa risiko bridge. Oracle menyediakan atestasi harga privat untuk lapisan penetapan harga. Fase 2/3.

XEQM Labs mengoperasikan EXIOM sebagai platform perangkat lunak komersial. Tujuannya adalah pendapatan platform berkelanjutan yang mengurangi ketergantungan pada tata kelola emisi seiring waktu. XEQM Labs tidak mendorong pembelian XEQM atas dasar apresiasi harga spekulatif.

---

## 2. Asal-Usul Pasokan

Migrasi telah selesai. Sebanyak 276.917.604 XEQM diterbitkan di mainnet EXIOM sebagai penukaran dari kepemilikan rantai lama. Angka tersebut merupakan pasokan awal yang terverifikasi pada peluncuran mainnet tanggal 6 Mei 2026. Setiap deposit lama dicatat dalam buku besar publik dengan sidik jari SHA256. Rantai baru dicetak sekali pada akhir proses pertukaran untuk mencocokkan total terverifikasi tersebut secara tepat. Kunci pembelanjaan untuk setiap dompet yang terlibat dalam penukaran telah dipublikasikan, dan siapa pun dapat memverifikasi seluruh riwayat transaksi dari deposit hingga pembayaran.

Di luar pasokan awal, XEQM baru masuk ke dalam sirkulasi melalui dua alur emisi tingkat protokol: hadiah blok layanan node dan tata kelola emisi. Both berjalan berdasarkan jadwal tetap dan terprediksi yang tertulis dalam protokol yang dapat dihitung oleh siapa saja dari parameter publik. Rincian tarif dan operasional ada di Bagian 3. Total pasokan bertambah seiring waktu. XEQM adalah rantai dengan pasokan tak terbatas berdasarkan model emisi ekor seperti Monero. Disiplin pasokan tetap yang dikomitmenkan oleh proyek ini mengacu pada ketiadaan penerbitan diskresional, bukan batas keras pada emisi yang didorong oleh protokol.

**Tidak ada pencetakan diskresional.** Protokol tidak mengizinkan penerbitan ad-hoc, penyesuaian pasokan manual, atau pencetakan di luar jadwal. Setiap XEQM baru yang masuk ke sirkulasi dilakukan melalui dua alur emisi terjadwal di atas.

**Tidak ada pembakaran.** Arsitektur kriptografis yang menjadi landasan jaringan ini tidak mendukung bukti pembakaran sebagaimana istilah tersebut biasa digunakan. Alamat mana pun tempat koin dikirim hanya sebatas tidak dapat dibelanjakan jika kuncinya terbukti dihancurkan secara eksplisit. Kami tidak akan merepresentasikan dompet mana pun sebagai alamat pembakaran. Koin yang tidak ditukarkan selama jendela migrasi tetap berada di rantai lama yang tidak aktif dan bukan bagian dari pasokan XEQM.

---

## 3. Model Tokenomik

### Emisi Blok

Jaringan menghasilkan blok baru setiap 60 detik dan memberikan 8,25 XEQM kepada layanan node yang terpilih, menghasilkan 11.880 XEQM per hari. Pada 700 node aktif, setiap node menghasilkan sekitar 17,0 XEQM per hari, atau 516 XEQM per bulan.

Mulai dari HF21, hadiah blok didistribusikan dalam jadwal pengelompokan mingguan. Sebelum HF21, hadiah diterbitkan setiap 20 blok. hadiah kini diakumulasikan setiap jendela 10.080 blok (sekitar 7 hari) dan dibayarkan pada akhir setiap jendela. Total tingkat emisi tidak berubah; hanya ritme pembayarannya yang bergeser.

### Tata Kelola Emisi

Bendahara Kas menerima sekitar 17.857 XEQM per hari, atau sekitar 124.999 XEQM per minggu. Ini adalah anggaran operasional untuk tim pengembang perangkat lunak komersial yang aktif. Insinyur, peninjau keamanan, operator infrastruktur, dan kontributor ekosistem diberi kompensasi dari emisi ini selama platform berada dalam tahap sebelum menghasilkan pendapatan. Seiring setiap produk EXIOM mencapai status menghasilkan pendapatan, tata kelola emisi ditinjau dan dikurangi secara bertahap. Tujuan jangka panjangnya adalah agar pendapatan platform menggantikan tata kelola emisi sebagai mekanisme pendanaan utama.

### Alokasi Emisi

| Alokasi | Bagian | Tujuan |
|---|---|---|
| Hadiah Layanan Node | 40% | Hadiah blok dibayarkan langsung ke layanan node |
| Pengembangan Protokol Inti | 25% | Blockchain, platform EXIOM, dan layanan jaringan inti |
| Pemasaran dan Kesadaran | 15% | Visibilitas dan adopsi jaringan |
| Ekosistem dan Komunitas | 10% | Hibah, hadiah, hadiah komunitas, dukungan integrasi |
| Keamanan dan Audit | 5% | Audit kode, peninjauan keamanan, pengujian keandalan |
| Cadangan Jangka Panjang | 5% | Stabilitas, kebutuhan darurat, operasional jangka panjang |

### Distribusi Biaya Platform EXIOM

Di luar hadiah blok, platform pengembang EXIOM menghasilkan biaya yang didistribusikan sebagai berikut ini:

| Penerima | Bagian | Catatan |
|---|---|---|
| Operator API Node | 35% | Didistribusikan secara proporsional berdasarkan permintaan yang dilayani |
| Kas XEQM Labs | 35% | Danai pengembangan platform yang berkelanjutan |
| Tata Kelola Komunitas | 30% | Mengalir ke dompet tata kelola |

Setiap operator yang berkemampuan teknis dapat menjalankan API node, mendaftar ke platform, dan mulai memperoleh bagian biaya platform secara proporsional dengan permintaan yang dilayani. Persyaratan perangkat keras dasar: 4 core CPU, RAM 8 GB, SSD 100 GB, koneksi 100 Mbps. Beban kerja Oracle membutuhkan spesifikasi yang lebih tinggi, yang dibahas di Bagian 10.

---

## 4. Struktur Layanan Node

### Parameter Staking

| Parameter | Nilai |
|---|---|
| Persyaratan full node | 200.000 XEQM |
| Staking minimum operator | 100.000 XEQM (50% dari persyaratan penuh) |
| Biaya maksimum operator | 10% |
| Periode unbonding, penarikan sukarela | 14 hari, hadiah tetap berjalan |
| Periode unbonding, deregistrasi paksa | 14 hari, tanpa hadiah (disatukan pada HF22) |
| Slot kontributor maksimum | 11 (termasuk operator) |
| Kontribusi komunitas minimum per slot | 10.000 XEQM |
| Jendela staker komunitas per node | Hingga 100.000 XEQM melalui hingga 10 slot kontributor |

### Ekonomika Node

Banyak penyedia VPS cloud menawarkan tingkat layanan gratis yang dapat mendukung pengoperasian layanan node tanpa biaya bulanan. VPS berbayar dengan harga sekitar $5,28 per bulan dapat menjalankan 10 layanan node, menjadikan biaya hosting per node sekitar $0,53 per bulan. Managed hosting melalui Pecunia tersedia seharga $1,76 per node per bulan.

Pada 700 node aktif, setiap node menghasilkan sekitar 516 XEQM per bulan. Hasil bersih bulanan per node setelah biaya hosting:

| Harga | Kotor/bln | Bersih: Self-hosted ($0,53) | Bersih: Pecunia ($1,76) | APY pada stake 200rb |
|---|---|---|---|---|
| $0,01547 (hari ini) | $0,008 | -$0,52 | -$1,75 | 3,1% |
| $0,05 | $0,026 | -$0,50 | -$1,73 | 3,1% |
| $0,10 | $0,052 | -$0,48 | -$1,71 | 3,1% |
| $0,25 | $0,129 | -$0,40 | -$1,63 | 3,1% |
| $0,50 | $0,258 | -$0,27 | -$1,50 | 3,1% |
| $1,00 | $0,516 | -$0,01 | -$1,24 | 3,1% |
| $2,00 | $1,032 | +$0,50 | -$0,73 | 3,1% |
| $5,00 | $2,580 | +$2,05 | +$0,82 | 3,1% |

APY pada hadiah blok bersifat konstan pada angka 3,1% karena nilai hadiah dan nilai stake berskala bersama dengan harga. Yang berubah mengikuti harga adalah arus kas USD relatif terhadap biaya hosting USD yang tetap. Tugas API node menambahkan alur pendapatan kedua yang berbasis pendapatan dan berskala dengan penggunaan platform secara nyata.

### Ekonomika Kontributor

Operator yang tidak dapat atau memilih untuk tidak menjalankan infrastruktur dapat menyumbangkan stake ke node yang ada melalui hingga 10 slot kontributor. Operator dapat mengenakan biaya 0% hingga 10% dari hadiah blok sebelum sisanya dibagi secara proporsional di antara para kontributor. Kontributor tidak menanggung biaya hosting, sehingga pada setiap titik harga, hasil bersih kontributor melebihi hasil operator self-hosted atau Pecunia.

### Siklus Hidup Node

Node tetap aktif tanpa batas waktu dengan jaminan kolateral dan persyaratan kinerja yang terjaga. Node yang tidak memenuhi kepatuhan dapat diperbaiki tanpa penalti. Jika tidak diperbaiki, deregistrasi paksa memicu periode unbonding 14 hari tanpa hadiah. Keluar secara sukarela membawa periode unbonding 14 hari dengan hadiah yang terus berjalan sepanjang periode tersebut.

---

## 5. Kelangsungan Jaringan dan Serangan Vektor 

### Persyaratan Kelangsungan Hidup

Jaringan EXIOM memberikan komitmen keandalan kepada para pengembang. Jaringan yang dapat dilumpuhkan oleh satu gangguan pusat data tidak dapat memberikan komitmen tersebut. Protokol menerapkan batas ukuran domain kegagalan maksimum: tidak ada satu pun fasilitas fisik, pusat data, atau kluster routing yang boleh menampung lebih dari 30% dari node aktif.

Pada 693 node, 30% adalah sekitar 208 node. Kehilangan satu fasilitas fisik mana pun paling banyak dapat melumpuhkan 208 node secara bersamaan, menyisakan setidaknya 485 node tetap beroperasi, yang cukup untuk mempertahankan produksi blok dan pembentukan kuorum tanpa dekomisi beruntun. Ini adalah persyaratan rekayasa teknis, bukan sekadar preferensi desentralisasi.

### Dua Hard Fork

Penerapan aturan kelangsungan jaringan disampaikan dalam dua tahap yang dipisahkan untuk mengurangi risiko dan mengirimkan hasil kerja yang telah tervalidasi secara langsung.

**HF22, memasuki testnet:** Dedup kuorum dompet-kunci operator dan unifikasi periode unbonding. Tanpa ketergantungan Lokinet. Tervalidasi melalui sembilan siklus terhenti/pemulihan dengan tingkat pemulihan 100% dan tanpa intervensi manual.

**HF23, tahap desain:** Batas pendaftaran kluster kedekatan, pengubah hadiah nol untuk node berlebih, dan peningkatan dedup kuorum dari dompet-kunci ke kluster kedekatan. Ketiganya bergantung pada aktivasi Lokinet sebagai transport jaringan utama. Lini masa bergantung pada penilaian rekayasa Lokinet yang sedang berlangsung.

### Kontrol HF22

**Deduplikasi kuorum dompet-kunci operator.** Paling banyak satu node per alamat dompet operator yang dapat memegang kursi validator dalam setiap putaran Pulse, sesi oracle, atau kuorum kewajiban tertentu. Jika penarikan acak memilih dua node dari alamat operator yang sama, node kedua digantikan oleh node dari operator yang berbeda. Hadiah blok tidak terpengaruh; hadiah dialokasikan berdasarkan urutan waktu tunggu secara independen dari partisipasi kuorum.

Keterbatasan yang diketahui: dapat dilampaui dengan pemisahan dompet. Operator yang menggunakan beberapa alamat dompet menampilkan beberapa kunci operator ke protokol. HF23 menutup celah ini melalui deduplikasi kluster kedekatan.

**Unifikasi periode unbonding.** Unbonding deregistrasi paksa diperpanjang dari 7 hari menjadi 14 hari, menyamakan penarikan sukarela. Kedua kasus kini berdurasi 14 hari.

### Kontrol HF23

Setelah Lokinet aktif sebagai transport jaringan, node yang berlokasi di tempat fisik yang sama akan menunjukkan tanda tangan routing yang khas: latensi mutual di bawah satu milidetik dan tumpang tindih jalur yang tinggi melalui grafik routing Lokinet. Node yang berada di fasilitas yang benar-benar berbeda akan menunjukkan latensi yang lebih tinggi dan tumpang tindih jalur yang lebih rendah. Sinyal pengelompokan ini diturunkan dari perilaku jaringan yang teramati, tanpa mewajibkan operator untuk mengungkapkan penyedia atau lokasi mereka.

**Batas pendaftaran kluster.** Pendaftaran node baru dievaluasi terhadap kedekatan routing Lokinet ke kluster yang ada. Jika kluster sasaran telah berisi 30% atau lebih dari node aktif, pendaftaran ditolak oleh protokol.

**Pengubah hadiah nol.** Node di atas ambang batas batas kluster memperoleh hadiah blok nol hingga dimigrasikan ke kluster yang tidak terkonsentrasi. Node diurutkan dalam setiap kluster berdasarkan usia pendaftaran; node tertua hingga ambang batas batas menerima hadiah penuh. Setiap node di atas ambang batas tersebut memperoleh nol. Hadiah yang dikurangi dapat dirasionalkan terhadap biaya VPS; hadiah nol tidak bisa.

Masa tenggang 30 hari berlaku pada aktivasi HF23. Semua node memperoleh hadiah penuh selama masa tenggang. Setelah berakhir, pengubah hadiah nol diaktifkan pada node yang berlebih.

**Deduplikasi kuorum kluster kedekatan.** Meningkatkan dedup dompet-kunci HF22 menjadi dedup kluster kedekatan. Paling banyak satu node per kluster kedekatan per putaran, tanpa memandang struktur dompet. Menutup celah pemisahan dompet.

Ukuran kuorum adalah 12 kursi per putaran. Oleh karena itu, dedup membutuhkan setidaknya 12 kluster kedekatan yang berbeda agar dapat berfungsi tanpa opsi cadangan. Mengingat topologi jaringan saat ini, jumlah kluster pada aktivasi HF23 mungkin mendekati batas minimum ini. Algoritma mengimplementasikan cadangan wajib: jika semua kluster yang berbeda telah habis sebelum 12 kursi terisi, kursi tambahan dialokasikan mulai dari kluster terkecil (paling tidak terkonsentrasi) terlebih dahulu, sebelum kluster yang paling terkonsentrasi menerima kursi kedua. Frekuensi cadangan dicatat dan dipublikasikan di penjelajah node sebagai indikator risiko konsentrasi waktu nyata. Jaringan yang tidak pernah memicu cadangan telah mencapai keragaman fisik yang memadai.

### Kontrol Tambahan

**Hambatan biaya modal.** Staking minimum operator sebesar 100.000 XEQM memastikan setiap operator berkomitmen pada modal nyata untuk setiap node. Menjalankan N node membutuhkan setidaknya N x 100.000 XEQM yang distake.

**Perlindungan pengambilalihan biaya operator.** EXIOM tidak rentan terhadap serangan pengambilalihan biaya operator yang ada di beberapa jaringan layanan node, di mana operator mendaftarkan node dengan modal minimal dan menetapkan biaya 100% untuk mengambil seluruh hadiah blok tanpa mempedulikan stake kontributor. Biaya maksimum dibatasi pada 10% dan minimum stake operator sebesar 50% membuat hal ini tidak rasional secara ekonomi.

**Analisis waktu bukti uptime.** Node pada host fisik yang sama mengirimkan bukti uptime dalam kluster ketat yang berkorelasi, yang dapat dideteksi dari data penerimaan bukti yang ada tanpa perubahan daemon.

**Analisis ASN.** Node di belakang Autonomous System Number (ASN) yang sama berbagi infrastruktur tingkat penyedia dan paparan hukum. Konsentrasi ASN berkontribusi pada penentuan kluster dan peninjauan tata kelola.

**Daftar blokir tata kelola.** Daftar blokir kunci publik yang dikelola oleh tata kelola mencegah kunci pendaftaran yang masuk daftar hitam untuk mendaftarkan node baru.

**Target koefisien Nakamoto.** Jaringan menargetkan koefisien setidaknya 8. Per Juli 2026, dengan 693 node aktif di 184 operator, koefisien berada di angka 7.

Proposal batas konsentrasi lengkap ada disini [concentration-limits-proposal.md](https://github.com/XEQMLabs/whitepaper/blob/main/concentration-limits-proposal.md). Metodologi ketahanan sybil ada di [XEQMLabs/xeqm-sybil-resistance](https://github.com/XEQMLabs/xeqm-sybil-resistance).

### Lokinet sebagai Transport Jaringan Masa Depan

Infrastruktur pengalamatan jaringan EXIOM direncanakan untuk dimigrasikan dari alamat IP yang diumumkan secara publik ke pengalamatan Lokinet sebagai bagian dari HF23. Lokinet (Low Latency Anonymous Routing Protocol, LLARP) adalah protokol onion routing layer 3 yang mengarahkan lalu lintas berbasis IP apa pun melalui beberapa layanan node via onion routing multi-hop, tanpa ada satu pun node dalam jalur yang mengetahui asal dan tujuan sekaligus.

Setelah Lokinet aktif:

- Layanan node akan dialamatkan oleh pengidentifikasi kriptografis Lokinet mereka, bukan alamat IP yang diumumkan secara publik
- API pengembang EXIOM akan dapat diakses sebagai layanan tersembunyi di alamat `.loki`, menyembunyikan IP asal pengembang dari API node
- Platform perdagangan RFQ akan dapat diakses sebagai layanan tersembunyi, menyembunyikan alamat IP pemohon dan LP dari platform
- Komunikasi sesi oracle antara pembuktian dan kuorum pemeriksa akan diarahkan melalui Lokinet, menghilangkan asumsi kepercayaan koordinator terpusat

Aktivasi Lokinet saat ini sedang dalam penilaian rekayasa. Basis kode LLARP ada di repositori EXIOM. Tim rekayasa sedang mengevaluasi apakah aktivasi hanya memerlukan perubahan konfigurasi atau pekerjaan tambahan. Hasilnya akan menentukan lini masa HF23.

---

## 6. XEQM sebagai Koin Utilitas

XEQM beroperasi melalui empat mekanisme permintaan yang simultan. Staking node mengunci bagian pasokan terbesar, sekitar 50,6% pada 700 node. Staking tingkatan pengembang menciptakan permintaan berkelanjutan karena partisipan pasar baru harus memperoleh dan mengunci XEQM sebelum dapat mengakses platform. Konsumsi panggilan API menciptakan lapisan kecepatan berkelanjutan saat aplikasi memproses permintaan di atas batas tingkatan mereka. Akses Oracle menambahkan lapisan keempat untuk konsumen Production dan Enterprise.

| Tingkatan | Stake yang Dibutuhkan | Panggilan yang Termasuk |
|---|---|---|
| Gratis | Tidak ada | 10.000 panggilan testnet per bulan |
| Pembangun | 1.000 XEQM | 100.000 panggilan mainnet per bulan |
| Produksi | 10.000 XEQM | 1.000.000 panggilan per bulan, webhooks, dukungan prioritas |
| Perusahaan | 50.000 XEQM | Panggilan tak terbatas, batas kecepatan kustom, SLA |

Stake tingkatan pengembang membawa periode unbonding 7 hari, sebuah parameter lapisan aplikasi platform yang tidak memerlukan hard fork. Periode yang lebih singkat mencerminkan bahwa stake tingkatan adalah komitmen akses, bukan stake keamanan jaringan.

---

## 7. Tata Kelola dan Kas Perbendaharaan

Alamat dompet tata kelola dan view key telah dipublikasikan. Siapa pun dapat memverifikasi saldo kapan saja. Tata kelola saat ini dijalankan melalui tim pendiri dengan masukan komunitas melalui saluran Telegram terbuka dan diskusi GitHub.

Alokasi kas, yang ditarik dari tata kelola emisi yang dijelaskan di Bagian 3:

- Pengembangan inti (25%): rekayasa untuk API EXIOM, oracle, dan platform RFQ
- Pemasaran dan kesadaran (15%): pendaftaran bursa, konten, pertumbuhan komunitas
- Ekosistem dan komunitas (10%): hibah, hadiah, dukungan integrasi
- Keamanan dan audit (5%): audit kode, peninjauan keamanan, pengujian penetrasi
- Cadangan jangka panjang (5%): stabilitas operasional dan cadangan darurat

Fase 3 memperkenalkan proses proposal dan komentar formal. Fase 6 memperkenalkan pemungutan suara berbobot di mana operator layanan node dan API node memegang hak formal yang proporsional dengan stake dan masa jabatan.

---

## 8. Ringkasan Parameter

| Parameter | Nilai |
|---|---|
| Mekanisme konsensus | 100% Proof-of-Stake |
| Waktu blok | 60 detik |
| Hadiah blok | 8,25 XEQM per blok |
| Emisi blok harian | 11.880 XEQM |
| Tata kelola emisi | ~17.857 XEQM per hari |
| Persyaratan full node | 200.000 XEQM |
| Staking minimum operator | 100.000 XEQM (50%) |
| Biaya maksimum operator | 10% |
| Slot kontributor maksimum | 11 (termasuk operator) |
| Kontribusi komunitas minimum | 10.000 XEQM per slot |
| Jendela staker komunitas per node | Hingga 100.000 XEQM melalui 10 slot |
| Periode unbonding, penarikan sukarela | 14 hari, hadiah tetap berjalan |
| Periode unbonding, deregistrasi paksa | 14 hari, tanpa hadiah (HF22) |
| Unbonding stake tingkatan pengembang | 7 hari, tanpa hadiah (lapisan platform) |
| Total pasokan | 276.917.604 XEQM saat peluncuran, bertambah melalui emisi terjadwal |
| Pasokan terkunci pada 700 node | 140.000.000 XEQM (~50,6% dari pasokan awal) |
| Beredar bebas pada 700 node | ~137.000.000 XEQM pada pasokan awal, bertambah seiring emisi |
| APY operator solo pada 700 node | ~3,1% (hanya hadiah blok, dibayarkan mingguan via HF21) |
| Biaya self-hosted per node | ~$0,53/bulan ($5,28/bln VPS, 10 node) |
| Biaya managed hosting (Pecunia) | $1,76/node/bulan |
| Koefisien Nakamoto (Juli 2026) | 7 (target: 8; 693 node, 184 operator) |
| Aktivasi eksternal Oracle | Nakamoto >= 6 tercapai; tertahan hingga penyelesaian Fase 3 |
| Ukuran kuorum | 12 kursi per putaran |
| Dedup kuorum, HF22 | Satu alamat dompet operator per kursi kuorum per putaran |
| Dedup kuorum, HF23 | Satu kluster kedekatan per kursi kuorum per putaran (membutuhkan Lokinet) |
| Cadangan dedup kuorum, HF23 | Jika terdapat kurang dari 12 kluster berbeda, kluster terkecil menerima kursi tambahan terlebih dahulu sebelum kluster yang paling terkonsentrasi; frekuensi cadangan dicatat dan dipublikasikan |
| Batas kelangsungan jaringan, HF23 | 30% dari node aktif per kluster kedekatan (~208 node pada jumlah saat ini) |
| Pengubah hadiah nol, HF23 | Hadiah blok nol untuk node di atas batas kluster, diurutkan berdasarkan usia pendaftaran |
| Repositori utama | github.com/XEQMLabs |

---

## 9. Peta Jalan

**Fase 1, Stabilisasi jaringan. TELAH SELESAI.** 693 node aktif di 184 operator, koefisien Nakamoto 7. Pertukaran koin XEQ ke XEQM berjalan dan berhasil ditutup.

**Fase 2, API pengembang EXIOM. TELAH AKTIF.** Rilis publik API pengembang, pendaftaran tingkatan, onboarding API node, dan integrasi produksi pertama. Distribusi biaya API node diaktifkan. Pengembangan platform perdagangan RFQ EXIOM berjalan secara paralel, XEQM/BTC sebagai pasangan perdagangan pertama.

**Fase 3, Privasi Oracle EXIOM dan platform RFQ.** Oracle diluncurkan dalam beberapa tahap: *proof of concept* internal, testnet terfederasi, lalu mainnet dengan konsumen internal. Platform perdagangan RFQ mencapai tahap produksi pada fase ini, menggunakan oracle untuk atestasi harga privat pada pasangan XEQM/BTC. Both dibangun di atas API EXIOM.

**Fase 4, Akses konsumen eksternal Oracle.** Output oracle tersedia untuk pengembang tingkatan Production dan Enterprise serta konsumen eksternal. Ambang batas koefisien Nakamoto sebesar 6 telah tercapai; aktivasi tertahan hingga penyelesaian Fase 3.

**HF22, memasuki testnet.** Dua perubahan konsensus tervalidasi tanpa ketergantungan Lokinet: deduplikasi kuorum dompet-kunci operator (satu alamat operator per kursi kuorum per putaran) dan unifikasi periode unbonding (deregistrasi paksa diperpanjang dari 7 menjadi 14 hari).

**HF23, tahap desain, menunggu penilaian Lokinet.** Setelah Lokinet aktif sebagai transport jaringan: aktivasi Lokinet sebagai transport utama menggantikan alamat IP yang diumumkan secara publik; batas pendaftaran kluster kedekatan (pendaftaran ditolak ketika sebuah kluster melebihi 30% dari node aktif); pengubah hadiah nol untuk node di atas ambang batas batas yang diurutkan berdasarkan usia pendaftaran; peningkatan deduplikasi kuorum dari dompet-kunci ke kluster kedekatan, dengan aturan cadangan wajib yang memastikan pembentukan kuorum selalu memungkinkan meskipun terdapat kurang dari 12 kluster berbeda (kluster terkecil menerima kursi tambahan terlebih dahulu sebelum kluster yang paling terkonsentrasi, dengan frekuensi cadangan dicatat dan dipublikasikan sebagai indikator risiko konsentrasi). Masa tenggang 30 hari berlaku pada aktivasi sebelum pengubah hadiah nol berlaku.

**Fase 6, Tata kelola formal.** Proses proposal terstruktur, pemungutan suara berbobot untuk operator, transisi jangka panjang keluar dari tata kelola tim pendiri.

---

## 10. Privasi Oracle EXIOM

Privasi Oracle EXIOM memungkinkan aplikasi mengonsumsi umpan data privat yang terotentikasi tanpa mengekspos data sumber yang mendasari. Oracle ini menggunakan teknik *zero-knowledge proof* untuk membuktikan asal-usul data dari endpoint HTTPS standar, tanpa memerlukan kerja sama dari sisi server dan tanpa perangkat keras tepercaya. Ini adalah hasil kerja Fase 3, mengikuti stabilisasi platform API Fase 2 dan konsultasi kriptografi sebelum pembangunan penuh dimulai.

Oracle ini bukan umpan data tujuan umum. Ini adalah oracle yang mengutamakan privasi untuk kasus penggunaan di mana data itu sendiri harus tetap rahasia: ambang batas harga tanpa mengungkapkan harga pasti, saldo akun tanpa mengekspos kredensial, atestasi kepatuhan tanpa mengungkapkan catatan yang mendasari. Platform RFQ EXIOM adalah konsumen internal pertama, menggunakannya untuk membuktikan bahwa eksekusi XEQM/BTC terjadi pada atau lebih baik dari harga referensi tanpa mengungkapkan harga pasti kepada platform atau pihak lain.

Setelah Lokinet aktif sebagai transport jaringan, komunikasi sesi oracle antara pembuktian dan kuorum pemeriksa akan diarahkan secara onion-routing melalui jaringan layanan node. Baik asal pembuktian maupun alamat jaringan node kuorum tidak akan terlihat oleh satu pun node relay, menghilangkan asumsi kepercayaan koordinator terpusat.

### Arsitektur

**Lapisan Pembuktian.** Aplikasi atau pengguna yang memegang akses ke sumber data privat berpartisipasi dalam protokol kriptografis yang berkomitmen pada respons TLS tanpa mengesposnya. Kredensial dan data mentah tidak pernah meninggalkan kendali pembuktian.

**Lapisan Pemeriksa.** Kuorum layanan node yang bergilir memverifikasi bahwa data yang dikomitmenkan memenuhi kondisi yang diminta. Node pemeriksa hanya mempelajari hasilnya (benar atau salah, di atas atau di bawah ambang batas) dan tidak pernah melihat data atau kredensial yang mendasarinya.

**Lapisan Konsumen.** Konsumen hanya menerima output minimal: hasil boolean, perbandingan ambang batas, atestasi bertanda tangan, atau nilai turunan kecil. Data sumber mentah tidak pernah dipublikasikan.

### Rencana Pembangunan Bertahap

**Fase 1, Bukti konsep internal.** Tim pendiri memvalidasi protokol kriptografis penuh dari ujung ke ujung terhadap sejumlah kecil sumber yang masuk daftar putih, tanpa konsumen eksternal atau partisipasi layanan node.

**Fase 2, Testnet oracle terfederasi.** Operator layanan node sukarelawan dengan riwayat uptime yang kuat bergabung dengan pool pemeriksa di testnet. Pengujian terintegrasi terhadap integritas atestasi sebelum penempatan mainnet apa pun.

**Fase 3, Oracle mainnet dengan konsumen internal.** Tugas pemeriksa oracle dibuka untuk node mainnet yang memenuhi syarat. Output memberi makan kontrak internal EXIOM dan platform RFQ. Biaya oracle mulai mengalir ke node pemeriksa yang berpartisipasi.

**Fase 4, Akses konsumen eksternal.** Output oracle tersedia untuk pengembang tingkatan Production dan Enterprise serta konsumen eksternal. Tertahan hingga penyelesaian Fase 3.

### Persyaratan Perangkat Keras Pemeriksa

Persyaratan indikatif: 8 core CPU, RAM 16 GB, SSD 200 GB, 500 Mbps dengan latensi rendah. Perangkat keras dasar API node standar tidak cukup untuk tugas pemeriksa oracle.

### Hadiah Pemeriksa

| Sumber Pendapatan | Deskripsi |
|---|---|
| Hadiah blok | Hadiah blok layanan node standar, tidak berubah |
| Bagian biaya API node | Bagian proporsional dari biaya platform untuk operator yang juga menjalankan API node |
| Biaya sesi Oracle | Biaya per sesi dari konsumen oracle, didistribusikan ke kuorum pemeriksa |
| Bonus tugas Oracle | Tata kelola emisi tambahan selama periode volume rendah, berkurang seiring biaya sesi menjadi mandiri |

---

## 11. Platform Perdagangan RFQ EXIOM

Platform RFQ EXIOM adalah sistem perdagangan antar individu tanpa konter dengan atestasi penyelesaian kriptografis, yang dibangun di atas API EXIOM. Pasangan perdagangan pertama adalah XEQM/BTC, keduanya merupakan aset native Layer 1 tanpa tokenisasi, tanpa wrapping, dan tanpa risiko bridge.

Setelah Lokinet aktif, platform RFQ akan dapat diakses sebagai layanan tersembunyi Lokinet. Baik alamat IP pemohon maupun LP tidak akan terlihat oleh platform. Lapisan penetapan harga oracle memungkinkan pihak lawan untuk membuktikan bahwa eksekusi terjadi pada atau lebih baik dari harga referensi dari sumber yang masuk daftar putih, tanpa mengungkapkan harga eksekusi pasti kepada platform atau pihak lain.

Spesifikasi aplikasi RFQ dan model data telah selesai. Pengembangan aktif dilanjutkan pada Fase 2 pada lapisan API. Produksi platform perdagangan penuh adalah hasil kerja Fase 3, bergantung pada API EXIOM yang mencapai tahap produksi dan MVP oracle yang menyelesaikan Bukti dari konsep internalnya.

---

---

## Bahasa yang Tersedia

Terjemahan komunitas dari whitepaper ini dikelola dalam folder `translations`. Jika terjadi konflik antara versi terjemahan dan versi bahasa Inggris, versi bahasa Inggris yang berlaku.

| Bahasa | Whitepaper |
|---|---|
| Español | [translations/es/README.md](./translations/es/README.md) |
| Français | [translations/fr/README.md](./translations/fr/README.md) |
| Deutsch | [translations/de/README.md](./translations/de/README.md) |
| 中文 | [translations/zh/README.md](./translations/zh/README.md) |
| Português | [translations/pt/README.md](./translations/pt/README.md) |
| Türkçe | [translations/tr/README.md](./translations/tr/README.md) |
| Polski | [translations/pl/README.md](./translations/pl/README.md) |

---

*Ini adalah dokumen draf. Parameter, jadwal emisi, dan fase peta jalan yang dijelaskan di sini adalah desain yang dimaksudkan. Pembaruan akan dipublikasikan seiring perkembangan jaringan dan platform.*

*Dokumen ini bukan merupakan nasihat keuangan atau hukum. XEQM adalah koin utilitas untuk platform EXIOM, bukan produk investasi. Klasifikasi token, status sekuritas, dan peraturan yang berlaku bervariasi menurut yurisdiksi. Partisipan harus berkonsultasi dengan kerangka hukum dan peraturan lokal mereka sebelum memperoleh atau beroperasi dengan XEQM. XEQM Labs tidak mendorong pembelian XEQM atas dasar apresiasi harga spekulatif.*
