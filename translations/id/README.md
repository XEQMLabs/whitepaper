# XEQM Labs - Platform EXIOM
## Whitepaper Tokenomics
### Draft v12 | 09/27/2026

---

## Apa yang Sudah Aktif Hari Ini vs. Apa yang Direncanakan

| Komponen | Status |
|---|---|
| EXIOM mainnet | Aktif, beroperasi sejak 6 Mei 2026 |
| Jaringan service node | Aktif — 943 service node aktif per 27 September 2026 |
| Lokinet (LLARP) | Dirilis dalam rilis non-penegakan sebelum HF23 (transport aktif, pengelompokan kedekatan dapat diamati); HF23 mengaktifkan penegakan. Implementasi dimulai Q4 2026 |
| Penyimpanan light-node SQLite | Dalam pengembangan; dirilis bersama rilis Lokinet pra-HF23, untuk memori dan disk node yang lebih rendah, dengan light node jendela-terkini opsional |
| Swap koin XEQ ke XEQM | Terkirim dan ditutup, masa produksi 35 hari, ledger publik yang dapat diaudit |
| Wallet GUI | Aktif, github.com/XEQMLabs/XEQMLabs-GUI |
| Node explorer | Aktif, pemantauan service node aktif |
| EXIOM Oracle | Aktif di mainnet (Robinhood Chain, chainId 4663); komite operator beranggotakan 12 orang per 28 September 2026 |
| EXIOM developer API | Aktif dalam beta — kunci swalayan, klaim kepatuhan bertanda tangan dan mesin verifikasi, OpenAPI di /docs; gratis untuk membangun dengan penggunaan prabayar per-panggilan yang sedang diluncurkan (27 September 2026) |
| EXIOM Privacy Oracle (TLSNotary / ZK) | Fondasi aktif (mesin verifikasi, sesi oracle); oracle data-web-privat penuh pada Fase 3 |
| Platform trading RFQ EXIOM | Dalam pengembangan, Fase 2/3, pasangan XEQM/BTC pertama |
| HF22, dedup kuorum kunci-wallet, unifikasi unbonding, pemulihan stall Pulse | Diaktifkan pada blok mainnet 219120. Revisi pemulihan stall Pulse (snode_revision 1, fallback berbasis tanda tangan) diaktifkan pada blok 236920 pada 18 Oktober 2026 |
| HF23, batas cluster kedekatan dan modifier reward (penegakan) | Dalam desain; mengaktifkan batas konsentrasi setelah rilis non-penegakan Lokinet + light-node selesai diuji; ditargetkan Q4 2026 |
| Tata kelola on-chain formal | Direncanakan, Fase 6 |

---

## 1. Apa Itu XEQM Labs

XEQM Labs adalah perusahaan teknologi privasi. Produk andalannya, EXIOM, adalah jaringan Layer 1 Proof-of-Stake yang menjaga privasi dan platform developer komersial yang dioperasikan oleh sekumpulan service node global. XEQM adalah koin akses dan penggunaan untuk platform tersebut. Developer membangun secara gratis dan membayar penggunaan produksi dalam XEQM, yang dikonsumsi saat mereka memanggil API. Operator service node memperoleh XEQM untuk mengamankan jaringan, dan operator yang sama dapat memperoleh pendapatan tambahan dengan menjalankan sidecar oracle yang melayani produk oracle platform.

Proyek ini meneruskan riwayat komunitas dan operasional yang berjalan lebih dari tujuh tahun. EXIOM mainnet dibangun untuk memberi komunitas tersebut sebuah jaringan dengan pasokan yang dapat diverifikasi, jadwal emisi yang dapat diprediksi, konsensus Proof-of-Stake murni tanpa komponen Proof-of-Work, dan mekanika service node yang menghormati waktu dan modal operator.

XEQM adalah koin Layer 1 native, tidak ditokenisasi di chain lain mana pun, bukan ERC-20 atau aset terbungkus, dan tidak di-bridge. Pemegang berinteraksi langsung dengan EXIOM mainnet.

### Keluarga Produk EXIOM

**EXIOM Service Node Network.** Aktif di mainnet. Sekumpulan service node global mengamankan chain, memperoleh block reward, dan membentuk lapisan infrastruktur tempat semua produk EXIOM lainnya berjalan. 943 service node aktif per 27 September 2026.

**EXIOM Coin Swap.** Produk komersial yang memungkinkan proyek memigrasikan komunitas pemegangnya dari chain lama ke chain baru dengan auditabilitas kriptografis penuh. Proyek percontohan adalah migrasi pemegang XEQ ke XEQM di EXIOM mainnet, berjalan selama 35 hari dengan setiap pengajuan diproses melalui ledger yang diverifikasi secara kriptografis dengan sidik jari SHA256 publik. Produk ini tersedia untuk proyek lain yang membutuhkan migrasi chain yang dapat diverifikasi.

**EXIOM Oracle.** Aktif di mainnet. Produk oracle pertama platform: sebuah komite operator service-node XEQM — masing-masing menjalankan sidecar oracle yang ringan — yang menghasilkan atestasi kepatuhan BLS-agregat bertanda tangan EIP-712 (misalnya, bahwa suatu alamat memenuhi syarat untuk yurisdiksi tertentu) yang dikonsumsi aplikasi melalui developer API. Ini di-deploy di Robinhood Chain (chainId 4663) dan menjalankan komite operator beranggotakan 12 orang per 28 September 2026. Menjalankan sidecar adalah cara seorang operator service-node memperoleh pendapatan tambahan berbasis-penggunaan di atas block reward.

**EXIOM Developer API.** Aktif dalam beta. Sebuah API terstruktur yang mengekspos kemampuan kepatuhan dan verifikasi platform — klaim kepatuhan bertanda tangan dan mesin verifikasi (mekanisme signed-claims, TLSNotary, dan zero-knowledge) — dengan akses swalayan (sebuah DID plus API key), spesifikasi OpenAPI 3.1, webhook, dan permintaan idempoten. Developer membangun secara gratis dengan jatah bulanan yang murah hati dan membayar penggunaan produksi dalam XEQM, yang dikonsumsi per panggilan. Fase 2, aktif.

**EXIOM Privacy Oracle.** Dirancang, fondasi sudah ada. Evolusi oracle yang lebih luas: membuktikan fakta tentang data web privat (melalui TLSNotary dan teknik zero-knowledge) tanpa mengekspos sumber yang mendasarinya. Mesin verifikasi dan endpoint oracle-session yang mendasarinya sudah aktif; oracle data-web-privat penuh adalah deliverable Fase 3. Baik platform EXIOM RFQ maupun aplikasi pihak ketiga dapat mengonsumsi output oracle.

**EXIOM RFQ Trading Platform.** Dalam pengembangan. Platform trading over-the-counter peer-to-peer dengan atestasi penyelesaian kriptografis, dibangun di atas EXIOM API. Pasangan trading pertama adalah XEQM/BTC, keduanya aset Layer 1 native tanpa tokenisasi, tanpa pembungkusan, dan tanpa risiko bridge. Oracle menyediakan atestasi harga privat untuk lapisan harga. Fase 2/3.

XEQM Labs mengoperasikan EXIOM sebagai platform perangkat lunak komersial. Tujuannya adalah pendapatan platform yang berkelanjutan yang mengurangi ketergantungan pada emisi tata kelola dari waktu ke waktu. XEQM Labs tidak mendorong pembelian XEQM atas dasar apresiasi harga spekulatif.

---

## 2. Asal-Usul Pasokan

Migrasi telah selesai. 276,917,604 XEQM diterbitkan di EXIOM mainnet sebagai penukaran atas kepemilikan lama. Angka itu adalah pasokan awal terverifikasi saat peluncuran mainnet pada 6 Mei 2026. Setiap setoran lama dicatat dalam ledger publik dengan sidik jari SHA256. Chain baru dicetak sekali pada akhir swap untuk menyamai total terverifikasi yang persis itu. Spend key untuk setiap wallet yang terlibat dalam swap telah dipublikasikan, dan siapa pun dapat memverifikasi riwayat transaksi lengkap dari setoran hingga pembayaran.

Di luar pasokan awal, XEQM baru memasuki sirkulasi melalui dua aliran emisi tingkat-protokol: block reward service node dan emisi tata kelola. Keduanya berjalan pada jadwal yang tetap dan dapat diprediksi yang tertulis dalam protokol yang dapat dihitung siapa pun dari parameter publik. Tarif dan detail operasional ada di Bagian 3. Total pasokan tumbuh dari waktu ke waktu. XEQM adalah chain dengan pasokan tanpa batas pada model yang sama dengan tail emission Monero. Disiplin pasokan-tetap yang menjadi komitmen proyek mengacu pada ketiadaan penerbitan diskresioner, bukan batas keras pada emisi yang didorong protokol.

**Tanpa pencetakan diskresioner.** Protokol tidak mengizinkan penerbitan ad-hoc, penyesuaian pasokan manual, atau pencetakan di luar jadwal. Setiap XEQM baru yang memasuki sirkulasi melakukannya melalui dua aliran emisi terjadwal di atas.

**Tanpa pembakaran.** Arsitektur kriptografis tempat jaringan ini dibangun tidak mendukung pembakaran yang dapat dibuktikan dengan cara istilah tersebut biasanya digunakan. Alamat mana pun yang menjadi tujuan pengiriman koin hanya tidak-dapat-dibelanjakan sejauh kuncinya terbukti dimusnahkan. Kami tidak akan merepresentasikan wallet mana pun sebagai alamat pembakaran. Koin yang tidak di-swap selama jendela migrasi tetap berada di chain lama yang tidak aktif dan bukan bagian dari pasokan XEQM.

---

## 3. Model Tokenomics

### Emisi Blok

Jaringan menghasilkan blok baru setiap 60 detik dan memberikan 8.25 XEQM kepada service node yang terpilih, menghasilkan 11,880 XEQM per hari. Pada 943 node aktif (27 September 2026), setiap node memperoleh sekitar 12.6 XEQM per hari, atau sekitar 380 XEQM per bulan.

Dimulai dengan HF21, block reward didistribusikan pada jadwal batching mingguan. Sebelum HF21, reward diterbitkan setiap 20 blok. Reward kini terakumulasi selama setiap jendela 10,080-blok (sekitar 7 hari) dan dibayarkan pada akhir setiap jendela. Total tingkat emisi tidak berubah; hanya irama pembayaran yang bergeser.

### Emisi Tata Kelola

Treasury menerima sekitar 17,857 XEQM per hari, atau kira-kira 124,999 XEQM per minggu. Ini adalah anggaran operasional untuk tim pengembangan perangkat lunak komersial yang aktif. Engineer, peninjau keamanan, operator infrastruktur, dan kontributor ekosistem dikompensasi dari emisi ini selama platform belum menghasilkan pendapatan. Saat setiap produk EXIOM mencapai status menghasilkan-pendapatan, emisi tata kelola ditinjau dan dikurangi sesuai dengannya. Tujuan jangka panjangnya adalah agar pendapatan platform menggantikan emisi tata kelola sebagai mekanisme pendanaan utama.

### Alokasi Emisi

| Alokasi | Bagian | Tujuan |
|---|---|---|
| Reward Service Node | 40% | Block reward dibayarkan langsung ke service node |
| Pengembangan Protokol Inti | 25% | Blockchain, platform EXIOM, dan layanan jaringan inti |
| Pemasaran dan Kesadaran | 15% | Visibilitas dan adopsi jaringan |
| Ekosistem dan Komunitas | 10% | Hibah, bounty, reward komunitas, dukungan integrasi |
| Keamanan dan Audit | 5% | Audit, peninjauan keamanan, pengujian keandalan |
| Cadangan Jangka Panjang | 5% | Stabilitas, kebutuhan darurat, operasi jangka panjang |

### Pendapatan dan Distribusi Platform EXIOM

Di luar block reward, platform memperoleh pendapatan dari penggunaan developer. Akses bersifat prabayar: developer mendanai akun mereka dengan menyetor XEQM (tidak dapat dikembalikan), dan saldo itu ditarik saat mereka mengonsumsi API produksi, dengan harga per panggilan. Pengembangan dan evaluasi pada jatah gratis tidak dikenai biaya.

XEQM yang dikonsumsi diakui sebagai pendapatan platform dan didistribusikan antara operator yang melayani oracle dan operasi platform:

| Penerima | Bagian | Tujuan |
|---|---|---|
| Operator sidecar oracle | 70% | Operator service-node yang menjalankan sidecar oracle, diberi reward sebanding dengan tugas oracle yang mereka bantu layani |
| Operasi dan pengembangan platform | 30% | Mendanai operasi dan pengembangan yang berkelanjutan, mengurangi ketergantungan pada emisi tata kelola dari waktu ke waktu |

Operator mengambil mayoritas karena mereka menjalankan infrastruktur yang melayani oracle. Rasio 70/30 adalah nilai awal dan dapat disesuaikan melalui tata kelola. Pendapatan diakui dan didistribusikan pada irama mingguan yang sama dengan block reward — setiap jendela 10,080-blok (sekitar 7 hari), selaras dengan batching reward HF21 — sehingga operator menerima block reward dan bagian pendapatan-penggunaan dalam satu irama. Bagian pendapatan ini adalah mekanisme yang membuat reward sidecar operator yang dijelaskan dalam Bagian 4 didanai dari penggunaan nyata alih-alih emisi.

Perangkat keras dasar untuk menjalankan service node (dan sidecar oracle-nya): 4 CPU core, 8 GB RAM, 100 GB SSD, koneksi 100 Mbps. Beban kerja privacy-oracle yang lebih berat membutuhkan spesifikasi yang lebih tinggi, dibahas dalam Bagian 10.

---

## 4. Struktur Service Node

### Parameter Staking

| Parameter | Nilai |
|---|---|
| Persyaratan full node | 200,000 XEQM |
| Stake operator minimum | 100,000 XEQM (50% dari persyaratan penuh) |
| Fee operator maksimum | 10% |
| Periode unbonding, penarikan sukarela | 14 hari, reward berlanjut |
| Periode unbonding, deregistrasi paksa | 14 hari, tanpa reward (diunifikasi di HF22) |
| Slot kontributor maksimum | 11 (termasuk operator) |
| Kontribusi komunitas minimum per slot | 10,000 XEQM |
| Jendela staker komunitas per node | Hingga 100,000 XEQM di seluruh hingga 10 slot kontributor |

### Ekonomi Node

Banyak penyedia cloud VPS menawarkan tier layanan gratis yang dapat mendukung operasi service node tanpa biaya bulanan. VPS berbayar sekitar $5.28 per bulan dapat menjalankan 10 service node, membawa biaya hosting per-node menjadi kira-kira $0.53 per bulan. Hosting terkelola melalui Pecunia tersedia seharga $1.76 per node per bulan.

Block reward per-node berskala terbalik dengan jumlah node aktif: pada 943 service node aktif (27 September 2026), emisi harian 11,880 XEQM jaringan menghasilkan kira-kira 12.6 XEQM per node per hari, sekitar 380 XEQM per bulan. Karena baik reward maupun stake didenominasi dalam XEQM, APY block-reward adalah sekitar 2.3% terlepas dari harga; hosting adalah satu-satunya biaya berulang yang material, sekitar $0.53 per node per bulan self-hosted atau $1.76 melalui Pecunia. Menjalankan sidecar oracle (Bagian 10) menambahkan aliran pendapatan kedua yang berbasis-pendapatan dan berskala dengan penggunaan platform aktual, didanai dari konsumsi developer alih-alih emisi.

### Ekonomi Kontributor

Operator yang tidak dapat atau memilih untuk tidak menjalankan infrastruktur dapat menyumbang stake ke node yang sudah ada di seluruh hingga 10 slot kontributor. Operator dapat membebankan 0% hingga 10% dari block reward sebelum sisanya dibagi secara proporsional di antara kontributor. Kontributor tidak menanggung biaya hosting, sehingga pada setiap titik harga hasil bersih seorang kontributor melebihi hasil operator self-hosted atau yang di-host Pecunia.

### Siklus Hidup Node

Node tetap aktif tanpa batas waktu dengan persyaratan kolateral dan kinerja yang dipertahankan. Node yang tidak lagi patuh dapat diperbaiki tanpa penalti. Jika tidak diperbaiki, deregistrasi paksa memicu periode unbonding 14 hari tanpa reward. Keluar secara sukarela membawa periode unbonding 14 hari dengan reward berlanjut sepanjang waktu.

---

## 5. Daya Tahan Jaringan dan Vektor Serangan

### Persyaratan Daya Tahan

Jaringan EXIOM membuat komitmen keandalan kepada developer. Jaringan yang dapat dibawa offline oleh satu pemadaman datacenter tidak dapat membuat komitmen tersebut. Protokol menegakkan ukuran failure domain maksimum: tidak ada satu fasilitas fisik, datacenter, atau routing cluster yang boleh menampung lebih dari 30% node aktif.

Pada 943 node (27 September 2026), 30% adalah sekitar 283 node. Kehilangan satu fasilitas mana pun paling banyak dapat membawa 283 node offline secara bersamaan, menyisakan setidaknya 660 node yang beroperasi, cukup untuk mempertahankan produksi blok dan pembentukan kuorum tanpa decommission berantai. Ini adalah persyaratan rekayasa, bukan preferensi desentralisasi.

### Dua Hard Fork

Penegakan daya tahan dikirim dalam dua tahap, dipisahkan untuk mengurangi risiko dan mengirim pekerjaan tervalidasi segera.

**HF22, diaktifkan:** Deduplikasi kuorum kunci-wallet operator dan unifikasi periode unbonding, plus revisi pemulihan stall Pulse (snode_revision 1) yang menggantikan fallback pemulihan Proof-of-Work sebelumnya dengan yang berbasis tanda tangan. Tanpa ketergantungan Lokinet. Tervalidasi melalui 20 siklus stall/pemulihan dengan tingkat pemulihan 100%, tanpa intervensi, dan gap blok terburuk 83 detik. HF22 diaktifkan pada blok mainnet 219120; revisi pemulihan stall diaktifkan pada blok 236920 pada 18 Oktober 2026.

**HF23, dalam desain, ditargetkan Q4 2026:** Batas registrasi cluster kedekatan, modifier reward-nol untuk node berlebih, dan peningkatan deduplikasi kuorum dari kunci-wallet ke cluster kedekatan. Ketiganya mengandalkan routing graph Lokinet sebagai sinyal kedekatan. Untuk menghindari membuat transport baru menjadi kritis-konsensus saat ia baru diperkenalkan, Lokinet dirilis lebih dulu dalam rilis non-penegakan terpisah (bersama perubahan penyimpanan light-node SQLite), di mana pengelompokan kedekatan aktif dan dapat diamati tetapi tidak memiliki konsekuensi reward. HF23 kemudian mengaktifkan penegakan, setelah rilis itu diuji dan jumlah cluster riil diukur serta ambang batas dan fallback disetel.

### Kontrol HF22

**Deduplikasi kuorum kunci-wallet operator.** Paling banyak satu node per alamat wallet operator yang boleh memegang kursi validator dalam ronde Pulse, sesi oracle, atau kuorum kewajiban tertentu. Jika pengundian acak memilih dua node dari alamat operator yang sama, yang kedua diganti dengan node dari operator yang berbeda. Block reward tidak terpengaruh; mereka ditetapkan berdasarkan pengurutan waktu-tunggu secara independen dari partisipasi kuorum.

Keterbatasan yang diketahui: dapat dikalahkan dengan pemecahan wallet. Operator yang menggunakan beberapa alamat wallet menyajikan beberapa kunci operator ke protokol. HF23 menutup celah ini melalui deduplikasi cluster kedekatan.

**Unifikasi periode unbonding.** Unbonding deregistrasi paksa diperpanjang dari 7 hari menjadi 14 hari, menyamai penarikan sukarela. Kedua kasus kini 14 hari.

### Kontrol HF23

Begitu Lokinet aktif sebagai transport jaringan, node yang secara fisik berkolokasi akan menunjukkan tanda tangan routing yang khas: latensi mutual sub-milidetik dan tumpang tindih jalur yang tinggi melalui routing graph Lokinet. Node di fasilitas yang benar-benar berbeda akan menunjukkan latensi lebih tinggi dan tumpang tindih jalur lebih rendah. Sinyal pengelompokan ini diturunkan dari perilaku jaringan yang dapat diamati, tanpa persyaratan bagi operator untuk mengungkapkan penyedia atau lokasi mereka.

**Batas registrasi cluster.** Registrasi node baru dievaluasi terhadap kedekatan routing Lokinet ke cluster yang sudah ada. Jika cluster target sudah berisi 30% atau lebih dari node aktif, registrasi ditolak oleh protokol.

**Modifier reward-nol.** Node di atas ambang batas cap cluster memperoleh block reward nol hingga dimigrasikan ke cluster yang tidak terkonsentrasi. Node diperingkat dalam setiap cluster berdasarkan usia registrasi; node tertua hingga ambang cap memperoleh reward penuh. Setiap node di atas ambang itu memperoleh nol. Tarif yang dikurangi dapat dirasionalisasi terhadap biaya VPS; nol tidak bisa.

Periode tenggang 30 hari berlaku pada aktivasi HF23. Semua node memperoleh reward penuh selama periode tenggang. Saat berakhir, modifier reward-nol aktif pada node berlebih.

**Deduplikasi kuorum cluster kedekatan.** Meningkatkan dedup kunci-wallet HF22 menjadi dedup cluster kedekatan. Paling banyak satu node per cluster kedekatan per ronde, terlepas dari struktur wallet. Menutup celah pemecahan-wallet.

Ukuran kuorum adalah 12 kursi per ronde. Oleh karena itu dedup memerlukan setidaknya 12 cluster kedekatan yang berbeda untuk berfungsi tanpa fallback. Mengingat topologi jaringan saat ini, jumlah cluster pada aktivasi HF23 mungkin mendekati minimum ini. Algoritme mengimplementasikan fallback wajib: jika semua cluster berbeda telah habis sebelum 12 kursi terisi, kursi tambahan dialokasikan mulai dari cluster terkecil (paling tidak terkonsentrasi) terlebih dahulu, sebelum cluster paling terkonsentrasi menerima kursi kedua. Frekuensi fallback dicatat dan dipublikasikan di node explorer sebagai indikator risiko konsentrasi real-time. Jaringan yang tidak pernah memicu fallback telah mencapai keragaman fisik yang memadai.

### Kontrol Tambahan

**Penghalang biaya modal.** Stake operator minimum 100,000 XEQM memastikan setiap operator menyerahkan modal nyata ke setiap node. Menjalankan N node memerlukan setidaknya N x 100,000 XEQM yang di-stake.

**Perlindungan penangkapan fee operator.** EXIOM tidak tunduk pada serangan penangkapan fee operator yang ada di beberapa jaringan service node, di mana operator meregistrasi node dengan modal minimal dan menetapkan fee 100% untuk menangkap seluruh block reward terlepas dari stake kontributor. Fee maksimum dibatasi pada 10% dan stake operator minimum 50% membuat ini tidak rasional secara ekonomi.

**Analisis timing bukti uptime.** Node pada host fisik yang sama mengirimkan bukti uptime dalam cluster berkorelasi yang rapat, dapat dideteksi dari data penerimaan bukti yang ada tanpa perubahan daemon.

**Analisis ASN.** Node di balik Autonomous System Number yang sama berbagi infrastruktur tingkat-penyedia dan eksposur hukum. Konsentrasi ASN berkontribusi pada penetapan cluster dan peninjauan tata kelola.

**Blocklist tata kelola.** Blocklist kunci publik yang dikelola tata kelola mencegah kunci registrasi yang di-blocklist meregistrasi node baru.

**Target koefisien Nakamoto.** Jaringan menargetkan koefisien operator setidaknya 8. Per 27 September 2026, di seluruh 943 service node aktif dan 204 operator, koefisien Nakamoto operator — jumlah minimum operator yang mengendalikan mayoritas node aktif — adalah 9, memenuhi target (naik dari 7 di seluruh 184 operator pada Juli 2026). Konsentrasi fasilitas-fisik adalah masalah yang terpisah dan lebih akut: satu region datacenter masih menampung mayoritas node, yang persis merupakan konsentrasi yang dirancang untuk dipecah oleh cap cluster-kedekatan HF23.

Proposal batas konsentrasi lengkap ada di [concentration-limits-proposal.md](https://github.com/XEQMLabs/whitepaper/blob/main/concentration-limits-proposal.md). Metodologi ketahanan sybil ada di [XEQMLabs/xeqm-sybil-resistance](https://github.com/XEQMLabs/xeqm-sybil-resistance).

### Lokinet sebagai Transport Jaringan Masa Depan

Infrastruktur pengalamatan jaringan EXIOM akan bermigrasi dari alamat IP yang diumumkan publik ke pengalamatan Lokinet. Lokinet dirilis lebih dulu dalam rilis non-penegakan sebelum HF23 (ditargetkan Q4 2026); HF23 kemudian menambahkan penegakan konsentrasi yang menggunakan routing graph Lokinet. Lokinet (Low Latency Anonymous Routing Protocol, LLARP) adalah protokol onion routing layer 3 yang merutekan lalu lintas berbasis IP apa pun melalui beberapa service node via multi-hop onion routing, tanpa satu node pun dalam jalur mengetahui baik asal maupun tujuan.

Begitu Lokinet aktif:

- Service node akan dialamatkan oleh identifier kriptografis Lokinet mereka alih-alih alamat IP yang diumumkan publik
- EXIOM developer API akan dapat diakses sebagai hidden service di alamat `.loki`, menyembunyikan IP asal developer dari node API
- Platform trading RFQ akan dapat diakses sebagai hidden service, menyembunyikan alamat IP pemohon dan LP dari platform
- Komunikasi sesi oracle antara prover dan kuorum verifier akan dirutekan melalui Lokinet, menghilangkan asumsi kepercayaan koordinator terpusat

Lokinet dirilis dalam rilis non-penegakan menjelang HF23, ditargetkan Q4 2026, dengan HF23 menyusul setelah diuji. Basis kode LLARP hadir dalam repositori EXIOM; implementasi Lokinet sebagai transport jaringan utama dimulai Q4 2026.

---

## 6. XEQM sebagai Koin Utilitas

Permintaan XEQM berasal dari tiga sumber. Staking node mengunci bagian pasokan terbesar, sekitar 68% pada 943 node aktif saat ini (27 September 2026). Konsumsi developer menciptakan lapisan velositas yang berkelanjutan: aplikasi membayar penggunaan API produksi dalam XEQM, sehingga adopsi platform langsung dikonversi menjadi permintaan berulang untuk koin. Akses oracle menambahkan lapisan ketiga untuk konsumen bervolume lebih tinggi.

Akses mengikuti model prabayar berbasis-penggunaan alih-alih gerbang stake-untuk-membuka — developer tidak harus memperoleh dan mengunci stake tetap untuk membangun:

| Tier | Model akses |
|---|---|
| Gratis | Bangun dan evaluasi tanpa biaya: jatah panggilan bulanan yang murah hati, tanpa setoran yang diperlukan |
| Produksi | Penggunaan prabayar: setor XEQM dan bayar per panggilan; webhook dan batas lebih tinggi |
| Enterprise | Batas kustom, SLA, dan dukungan; ketentuan volume |

Penggunaan produksi diukur per panggilan API dan ditarik dari saldo XEQM prabayar developer. Setoran tidak dapat dikembalikan dan diakui sebagai pendapatan platform saat dikonsumsi (lihat Bagian 3). Desain sebelumnya menggerbang tier di balik stake XEQM tetap; itu telah diganti dengan model prabayar ini, yang lebih sederhana bagi developer dan standar untuk API komersial.

---

## 7. Tata Kelola dan Treasury

Alamat wallet tata kelola dan view key dipublikasikan. Siapa pun dapat memverifikasi saldo kapan saja. Tata kelola saat ini berjalan melalui tim pendiri dengan masukan komunitas melalui kanal Telegram terbuka dan diskusi GitHub.

Alokasi treasury, ditarik dari emisi tata kelola yang dijelaskan dalam Bagian 3:

- Pengembangan inti (25%): rekayasa untuk EXIOM API, oracle, dan platform RFQ
- Pemasaran dan kesadaran (15%): listing exchange, konten, pertumbuhan komunitas
- Ekosistem dan komunitas (10%): hibah, bounty, dukungan integrasi
- Keamanan dan audit (5%): audit kode, peninjauan keamanan, pengujian penetrasi
- Cadangan jangka panjang (5%): stabilitas operasional dan cadangan darurat

Fase 3 memperkenalkan proses proposal dan komentar formal. Fase 6 memperkenalkan pemungutan suara berbobot di mana operator service node dan API node memegang hak formal sebanding dengan stake dan masa jabatan.

---

## 8. Ringkasan Parameter

| Parameter | Nilai |
|---|---|
| Mekanisme konsensus | 100% Proof-of-Stake |
| Waktu blok | 60 detik |
| Block reward | 8.25 XEQM per blok |
| Emisi blok harian | 11,880 XEQM |
| Emisi tata kelola | ~17,857 XEQM per hari |
| Persyaratan full node | 200,000 XEQM |
| Stake operator minimum | 100,000 XEQM (50%) |
| Fee operator maksimum | 10% |
| Slot kontributor maksimum | 11 (termasuk operator) |
| Kontribusi komunitas minimum | 10,000 XEQM per slot |
| Jendela staker komunitas per node | Hingga 100,000 XEQM di seluruh 10 slot |
| Periode unbonding, penarikan sukarela | 14 hari, reward berlanjut |
| Periode unbonding, deregistrasi paksa | 14 hari, tanpa reward (HF22) |
| Total pasokan | 276,917,604 XEQM saat peluncuran, tumbuh melalui emisi terjadwal |
| Pasokan terkunci pada 943 node (27 Sep 2026) | ~188,600,000 XEQM (~68% dari pasokan awal) |
| Bersirkulasi bebas pada 943 node | ~88,300,000 XEQM pada pasokan awal, tumbuh dengan emisi |
| APY operator solo pada 943 node | ~2.3% (hanya block reward, dibayar mingguan via HF21) |
| Biaya self-hosted per node | ~$0.53/bulan ($5.28/bln VPS, 10 node) |
| Biaya hosting terkelola (Pecunia) | $1.76/node/bulan |
| Service node aktif (27 September 2026) | 943 |
| Koefisien Nakamoto operator (27 Sep 2026) | 9 — kendali mayoritas; target >= 8; 943 node, 204 operator |
| Aktivasi eksternal oracle | Nakamoto >= 6 tercapai; digerbang pada penyelesaian Fase 3 |
| Ukuran kuorum | 12 kursi per ronde |
| Dedup kuorum, HF22 | Satu alamat wallet operator per kursi kuorum per ronde |
| Dedup kuorum, HF23 | Satu cluster kedekatan per kursi kuorum per ronde (membutuhkan Lokinet) |
| Fallback dedup kuorum, HF23 | Jika ada kurang dari 12 cluster berbeda, cluster terkecil menerima kursi tambahan terlebih dahulu sebelum cluster paling terkonsentrasi; frekuensi fallback dicatat dan dipublikasikan |
| Cap daya tahan jaringan, HF23 | 30% node aktif per cluster kedekatan (~283 node pada jumlah saat ini) |
| Modifier reward-nol, HF23 | Block reward nol untuk node di atas cap cluster, diperingkat berdasarkan usia registrasi |
| Repo inti | github.com/XEQMLabs |

---

## 9. Roadmap

**Fase 1, Stabilisasi jaringan. SELESAI.** Jaringan service node tumbuh menjadi 943 service node aktif per 27 September 2026 (dari 693 di seluruh 184 operator pada Juli 2026, koefisien Nakamoto 7). Swap koin XEQ ke XEQM berjalan dan ditutup dengan sukses.

**Fase 2, EXIOM developer API dan EXIOM Oracle. AKTIF.** EXIOM Oracle aktif di mainnet dengan komite operator, dan developer API aktif dalam beta (kredensial swalayan, endpoint kepatuhan dan verifikasi, OpenAPI). Pekerjaan Fase 2 yang tersisa: penagihan konsumsi prabayar, bagian pendapatan operator, dan integrasi produksi pertama. Pengembangan platform trading RFQ EXIOM berlanjut secara paralel, XEQM/BTC sebagai pasangan trading pertama.

**Fase 3, EXIOM Privacy Oracle dan platform RFQ.** Oracle diluncurkan dalam beberapa fase: proof of concept internal, testnet terfederasi, lalu mainnet dengan konsumen internal. Platform trading RFQ mencapai produksi pada fase ini, menggunakan oracle untuk atestasi harga privat pada pasangan XEQM/BTC. Keduanya dibangun di atas EXIOM API.

**Fase 4, Akses konsumen oracle eksternal.** Output oracle tersedia untuk developer tier Produksi dan Enterprise serta konsumen eksternal. Ambang koefisien Nakamoto 6 sudah tercapai; aktivasi digerbang pada penyelesaian Fase 3.

**HF22, diaktifkan (blok mainnet 219120).** Dua perubahan konsensus tanpa ketergantungan Lokinet, deduplikasi kuorum kunci-wallet operator (satu alamat operator per kursi kuorum per ronde) dan unifikasi periode unbonding (deregistrasi paksa diperpanjang dari 7 menjadi 14 hari), plus revisi pemulihan stall Pulse (snode_revision 1) yang diaktifkan pada blok 236920 pada 18 Oktober 2026, menggantikan pemulihan Proof-of-Work dengan fallback berbasis tanda tangan. Tervalidasi di seluruh 20 siklus stall/pemulihan (pemulihan 100%, gap blok terburuk 83 detik).

**Rilis Lokinet dan light-node, sebelum HF23.** Rilis non-penegakan yang membawa Lokinet online sebagai transport jaringan (pengelompokan kedekatan aktif dan dapat diamati di node explorer, tanpa konsekuensi reward) dan memperkenalkan penyimpanan light-node SQLite (memori dan disk per-node lebih rendah, dengan light node jendela-terkini opsional). Rilis ini diuji sehingga jumlah cluster-kedekatan riil dapat diukur dan ambang batas serta fallback HF23 disetel sebelum penegakan apa pun berlaku.

**HF23, dalam desain, ditargetkan Q4 2026.** Mengaktifkan penegakan setelah rilis non-penegakan Lokinet dan light-node di atas selesai diuji: batas registrasi cluster kedekatan (registrasi ditolak saat cluster melebihi 30% node aktif); modifier reward-nol untuk node di atas ambang cap diperingkat berdasarkan usia registrasi; peningkatan deduplikasi kuorum dari kunci-wallet ke cluster kedekatan, dengan aturan fallback wajib yang memastikan pembentukan kuorum selalu mungkin bahkan saat ada kurang dari 12 cluster berbeda (cluster terkecil menerima kursi tambahan terlebih dahulu sebelum cluster paling terkonsentrasi, dengan frekuensi fallback dicatat dan dipublikasikan sebagai indikator risiko konsentrasi). Periode tenggang 30 hari berlaku saat aktivasi sebelum modifier reward-nol berlaku.

**Fase 6, Tata kelola formal.** Proses proposal terstruktur, pemungutan suara berbobot untuk operator, transisi jangka panjang menjauh dari tata kelola tim-pendiri.

---

## 10. EXIOM Oracle

### Oracle aktif pertama: EXIOM Oracle

Produk oracle pertama platform aktif di mainnet. EXIOM Oracle adalah komite operator service-node XEQM — masing-masing menjalankan sidecar oracle yang ringan di samping node mereka — yang secara kolektif menghasilkan atestasi BLS-agregat bertanda tangan EIP-712 tentang fakta kepatuhan, paling langsung apakah suatu alamat memenuhi syarat untuk yurisdiksi tertentu. Aplikasi mengonsumsi atestasi ini melalui developer API dan dapat mengirimkan hasil bertanda tangan secara on-chain. Komite di-deploy di Robinhood Chain (chainId 4663) dan menjalankan komite operator beranggotakan 12 orang per 28 September 2026, dengan ambang penandatanganan dua-pertiga (8-dari-12).

**Model keamanan: himpunan terdaftar versus ambang batas.** EXIOM Oracle tidak mengambil sampel komite per-ronde. Karena agregat BLS membebani gate biaya yang sama untuk memverifikasi apakah delapan anggota atau delapan ratus yang menandatangani, setiap anggota terdaftar menandatangani setiap ronde; mengambil sampel subhimpunan tidak akan membeli apa pun dan akan memperkenalkan kembali risiko bahwa pengundian yang kurang beruntung kebetulan memegang cukup anggota yang berkolusi untuk memalsukan. Oleh karena itu keamanan tereduksi menjadi dua properti dari himpunan anggota terdaftar berukuran N, pada ambang dua-pertiga k = ceil(2N/3) yang ditegakkan gate:

- **Pemalsuan** mengharuskan adversary mengendalikan setidaknya k anggota terdaftar — sebuah kolusi, dan karena itu pertanyaan tentang konsentrasi **operator**.
- **Halt** (kegagalan liveness) mengharuskan setidaknya N - k + 1 = floor(N/3) + 1 anggota terdaftar mati sekaligus — pemadaman berkorelasi, dan karena itu pertanyaan tentang konsentrasi **infrastruktur**.

Ini adalah dua koefisien Nakamoto, dan keduanya adalah properti dari himpunan terdaftar, bukan dari armada service-node yang lebih luas: distribusi armada membatasi konsensus, sementara ketahanan pemalsuan dan liveness oracle hanya bergantung pada siapa yang memegang kursi terdaftar.

**Realisasi saat ini.** Per 28 September 2026 anggota terdaftar semuanya dioperasikan oleh operator proyek, sehingga koefisien operator oracle adalah 1: hari ini ketahanan pemalsuannya bertumpu pada kepercayaan pada satu operator, bukan pada kriptografi terdistribusi. Ini adalah keadaan awal yang jujur. Model keamanannya adalah k-dari-N di seluruh operator independen; realisasinya mengeras saat pihak independen mendaftar, yang merupakan tujuan dari onboarding operator service-node tambahan sebagai anggota sidecar. Jumlah node saja tidak membantu — anggota tambahan menaikkan kedua koefisien hanya sejauh mereka adalah operator independen di fasilitas yang berbeda.

**Bagaimana keragaman ditegakkan.** Karena tidak ada seleksi per-ronde, keragaman diputuskan pada **penerimaan**: anggota didaftarkan hanya jika itu menjaga bagian setiap operator di bawah k dan bagian setiap fasilitas pada atau di bawah floor(N/3), dan k dinaikkan untuk melacak ceil(2N/3) seiring himpunan tumbuh. Konsentrasi himpunan terdaftar dipantau terus-menerus dan dipublikasikan sebagai margin pemalsuan (k dikurangi bagian operator terbesar) dan margin liveness (floor(N/3) + 1 dikurangi bagian fasilitas terbesar); margin yang tidak-positif adalah alarm. Sinyal fasilitas adalah ASN dan arrival-timing bukti-uptime hari ini, dipertajam di HF23 menjadi kedekatan routing Lokinet, yang mendeteksi kolokasi fisik bahkan di seluruh ASN yang berbeda. Fakta distribusi tersebut itu sendiri dapat diatestasi melalui antarmuka typed-fact oracle, sehingga metrik konsentrasi adalah nilai yang ditandatangani-komite alih-alih output dari satu skrip tepercaya.

Sidecar sengaja dibuat ringan: ia hanya memegang signing key-nya sendiri, membaca identitas node-nya secara lokal, dan tidak pernah menangani spend key operator. Menjalankannya adalah mekanisme yang membuat operator service-node memperoleh pendapatan tambahan yang didanai-penggunaan yang dijelaskan dalam Bagian 3 dan 4.

### Visi yang lebih luas: EXIOM Privacy Oracle

EXIOM Privacy Oracle memungkinkan aplikasi mengonsumsi feed data privat terautentikasi tanpa mengekspos data sumber yang mendasarinya. Ia menggunakan teknik zero-knowledge proof untuk membuktikan asal-usul data dari endpoint HTTPS standar, tanpa memerlukan kerja sama sisi-server dan tanpa perangkat keras tepercaya. Ini adalah deliverable Fase 3, mengikuti stabilisasi platform API Fase 2 dan konsultasi kriptografi sebelum pembangunan penuh dimulai.

Oracle bukanlah feed data serbaguna. Ia adalah oracle yang mengutamakan-privasi untuk kasus penggunaan di mana data itu sendiri harus tetap rahasia: ambang harga tanpa mengungkapkan harga pasti, saldo akun tanpa mengekspos kredensial, atestasi kepatuhan tanpa mengungkapkan catatan yang mendasarinya. Platform EXIOM RFQ adalah konsumen internal pertama, menggunakannya untuk membuktikan bahwa fill XEQM/BTC terjadi pada atau lebih baik dari harga referensi tanpa mengungkapkan harga pasti kepada platform atau pihak lain.

Begitu Lokinet aktif sebagai transport jaringan, komunikasi sesi oracle antara prover dan kuorum verifier akan di-onion-route melalui jaringan service node. Baik asal prover maupun alamat jaringan node kuorum tidak akan terlihat oleh satu node relay pun, menghilangkan asumsi kepercayaan koordinator terpusat.

### Arsitektur

**Lapisan prover.** Aplikasi atau pengguna yang memegang akses ke sumber data privat berpartisipasi dalam protokol kriptografis yang berkomitmen pada respons TLS tanpa mengungkapkannya. Kredensial dan data mentah tidak pernah meninggalkan kendali prover.

**Lapisan verifier.** Kuorum berputar dari service node memverifikasi bahwa data yang dikomitmen memenuhi kondisi yang diminta. Node verifier hanya mempelajari hasil (benar atau salah, di atas atau di bawah ambang batas) dan tidak pernah melihat data atau kredensial yang mendasarinya.

**Lapisan konsumen.** Konsumen hanya menerima output minimal: hasil boolean, perbandingan ambang batas, atestasi bertanda tangan, atau nilai turunan kecil. Data sumber mentah tidak pernah dipublikasikan.

### Rencana Pembangunan Bertahap

**Fase 1, Proof of concept internal.** Tim pendiri memvalidasi protokol kriptografis penuh dari ujung ke ujung terhadap sekumpulan kecil sumber yang masuk whitelist, tanpa konsumen eksternal atau partisipasi service node.

**Fase 2, Testnet oracle terfederasi.** Operator service node sukarelawan dengan riwayat uptime kuat bergabung dengan pool verifier di testnet. Pengujian adversarial terhadap integritas atestasi sebelum deployment mainnet apa pun.

**Fase 3, Oracle mainnet dengan konsumen internal.** Tugas verifier oracle terbuka untuk node mainnet yang memenuhi syarat. Output memberi makan kontrak EXIOM internal dan platform RFQ. Fee oracle mulai mengalir ke node verifier yang berpartisipasi.

**Fase 4, Akses konsumen eksternal.** Output oracle tersedia untuk developer tier Produksi dan Enterprise serta konsumen eksternal. Digerbang pada penyelesaian Fase 3.

### Persyaratan Perangkat Keras Verifier

Persyaratan indikatif: 8 CPU core, 16 GB RAM, 200 GB SSD, 500 Mbps dengan latensi rendah. Perangkat keras dasar API node standar tidak cukup untuk tugas verifier oracle.

### Reward Verifier

| Sumber Pendapatan | Deskripsi |
|---|---|
| Block reward | Block reward service node standar, tidak berubah |
| Bagian pendapatan platform | Bagian proporsional dari pendapatan konsumsi-developer untuk operator yang menjalankan sidecar oracle |
| Fee sesi oracle | Fee per-sesi dari konsumen oracle, didistribusikan ke kuorum verifier |
| Bonus tugas oracle | Emisi tata kelola suplemental selama periode volume-rendah, dikurangi saat fee sesi menjadi swasembada |

---

## 11. EXIOM RFQ Trading Platform

Platform EXIOM RFQ adalah sistem trading over-the-counter peer-to-peer dengan atestasi penyelesaian kriptografis, dibangun di atas EXIOM API. Pasangan trading pertama adalah XEQM/BTC, keduanya aset Layer 1 native tanpa tokenisasi, tanpa pembungkusan, dan tanpa risiko bridge.

Begitu Lokinet aktif, platform RFQ akan dapat diakses sebagai hidden service Lokinet. Baik alamat IP pemohon maupun LP tidak akan terlihat oleh platform. Lapisan harga oracle memungkinkan pihak lawan membuktikan bahwa fill terjadi pada atau lebih baik dari harga referensi dari sumber yang masuk whitelist, tanpa mengungkapkan harga fill pasti kepada platform atau pihak lain.

Spesifikasi aplikasi RFQ dan model data telah selesai. Pengembangan aktif berlanjut di Fase 2 pada lapisan API. Produksi platform trading penuh adalah deliverable Fase 3, bergantung pada EXIOM API mencapai produksi dan MVP oracle menyelesaikan proof of concept internalnya.

---

---

## Bahasa yang Tersedia

Terjemahan komunitas atas whitepaper ini dipelihara dalam folder translations untuk kemudahan. **Versi bahasa Inggris adalah satu-satunya dokumen otoritatif setiap saat.** Terjemahan mungkin tertinggal di belakang revisi bahasa Inggris saat ini dan tidak dijamin mutakhir; jika terjadi konflik, ambiguitas, atau perbedaan apa pun, versi bahasa Inggris yang berlaku.

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

*Ini adalah dokumen draft. Parameter, jadwal emisi, dan fase roadmap yang dijelaskan di sini adalah desain yang dimaksudkan. Pembaruan akan dipublikasikan seiring jaringan dan platform berkembang.*

*Dokumen ini bukan merupakan nasihat keuangan atau hukum. XEQM adalah koin utilitas untuk platform EXIOM, bukan produk investasi. Klasifikasi token, status sekuritas, dan regulasi yang berlaku bervariasi menurut yurisdiksi. Peserta harus berkonsultasi dengan kerangka hukum dan regulasi lokal mereka sebelum memperoleh atau beroperasi dengan XEQM. XEQM Labs tidak mendorong pembelian XEQM atas dasar apresiasi harga spekulatif.*
