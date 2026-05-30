# XEQM Labs
## Whitepaper Tokenomics
### Draf v8 | 14/05/2026

---

## 1. Apa Itu XEQM Labs

XEQM Labs adalah jaringan Proof-of-Stake yang menjaga privasi sekaligus platform developer untuk membangun aplikasi di atasnya. Jaringan ini dioperasikan oleh serangkaian node layanan global yang mendapatkan XEQM karena telah mengamankan rantai (*chain*). Platform developer mengekspos kapabilitas privasi jaringan melalui API yang bersih dan merupakan mekanisme utama di mana XEQM menemukan utilitas praktis yang berkelanjutan.

Proyek ini meneruskan sejarah komunitas dan operasional yang telah berjalan lebih dari tujuh tahun. Mainnet XEQM Labs adalah fondasi teknis yang kami bangun untuk memberikan jaringan dengan pasokan yang dapat diverifikasi, jadwal emisi yang dapat diprediksi, model konsensus Proof-of-Stake tanpa komponen Proof-of-Work, serta mekanika node layanan yang menghormati waktu dan modal operator kepada komunitas tersebut.

XEQM is the access and usage token for the platform. Developers stake XEQM to unlock API tiers. Applications consume XEQM as they make calls. Service node operators earn XEQM for securing the network. API node operators earn XEQM for serving developer traffic. These four roles, with a fifth oracle role described in Section 10, form the economic backbone of the network.

XEQM adalah token akses dan penggunaan untuk platform ini. Developer melakukan *staking* XEQM untuk membuka tingkatan API. Aplikasi mengonsumsi XEQM saat mereka melakukan pemanggilan API. Operator node layanan mendapatkan XEQM karena mengamankan jaringan. Operator node API mendapatkan XEQM karena melayani lalu lintas (*traffic*) developer. Keempat peran ini, bersama dengan peran oracle kelima yang dijelaskan dalam Bagian 10, membentuk tulang punggung ekonomi jaringan.

Whitepaper ini mendokumentasikan tokenomics, struktur node layanan, model keamanan, dan peta jalan (*roadmap*) platform. Angka-angka dalam dokumen ini mencerminkan migrasi yang telah selesai ke mainnet XEQM Labs dan pasokan yang diterbitkan melalui penukaran (*swap-issued*) yang telah diverifikasi.

---

## 2. Asal-Usul Pasokan

Migrasi telah selesai. Sebanyak 276.917.604 XEQM diterbitkan di mainnet XEQM Labs sebagai Hadiah atas kepemilikan warisan, dan angka tersebut merupakan pasokan awal terverifikasi dari jaringan saat peluncuran mainnet pada 6 Mei 2026.

Setiap deposit warisan dicatat dalam buku besar publik dengan sidik jari SHA256. Rantai baru dicetak sekali pada akhir proses penukaran agar cocok dengan total terverifikasi yang tepat tersebut. Kunci pengeluaran (*spend keys*) untuk setiap dompet yang terlibat dalam proses penukaran telah dipublikasikan, dan siapa pun dapat membuka dompet tersebut serta memverifikasi riwayat transaksi lengkap dari deposit hingga pembayaran.

### Emisi Berkelanjutan

Di luar pasokan awal, XEQM baru masuk ke dalam sirkulasi melalui dua aliran emisi tingkat protokol, di mana keduanya berjalan pada jadwal yang tetap dan dapat diprediksi:

- **Hadiah blok node layanan.** Protokol mencetak 8,25 XEQM per blok 60 detik sebagai Hadiah bagi node layanan yang dipilih, menghasilkan sekitar 11.880 XEQM per hari dalam emisi blok.
- **Emisi tata kelola.** Protokol mencetak sekitar 17.857 XEQM per hari ke dompet tata kelola untuk pengembangan, program ekosistem, audit keamanan, dan cadangan jangka panjang.

Emisi ini ditulis ke dalam protokol dan mengikuti jadwal yang diketahui yang dapat dihitung oleh siapa saja dari parameter publik. Akibatnya, total pasokan tumbuh seiring waktu, dan oleh karena itu XEQM adalah rantai pasokan tak terbatas dengan model yang sama seperti emisi ekor milik Monero. "Disiplin pasokan tetap" yang dipegang teguh oleh proyek ini mengacu pada tidak adanya penerbitan diskresioner, bukan batas mutlak pada emisi yang didorong oleh protokol.

### Tidak Ada Pencetakan Diskresioner, Tidak Ada Pembakaran

XEQM Labs berkomitmen pada dua aturan manajemen pasokan yang membatasi bagaimana total pasokan dapat berubah di luar emisi terjadwal yang dijelaskan di atas.

Tidak ada pencetakan diskresioner. Protokol tidak mengizinkan penerbitan ad-hoc, penyesuaian pasokan manual, atau pencetakan di luar jadwal. Setiap XEQM baru yang masuk ke sirkulasi dilakukan melalui dua aliran emisi yang dijelaskan di atas, dengan jadwal yang tertulis dalam protokol dan dapat diverifikasi oleh siapa saja dengan menghitungnya dari parameter publik.

Tidak ada pembakaran. Arsitektur kriptografi tempat jaringan ini dibangun tidak mendukung pembakaran yang dapat dibuktikan (*provable burns*) sebagaimana istilah tersebut biasanya digunakan. Alamat mana pun yang dikirimi koin hanya akan menjadi tidak dapat dibelanjakan jika kuncinya terbukti dihancurkan secara nyata, dan kami tidak akan merepresentasikan dompet mana pun sebagai alamat pembakaran. Koin yang tidak ditukarkan selama jendela migrasi tetap berada di rantai warisan yang tidak aktif dan bukan merupakan bagian dari pasokan XEQM.

Kurva pasokan yang dievaluasi oleh developer, bursa (*exchange*), atau operator hari ini—yaitu pasokan awal yang terverifikasi ditambah jadwal emisi yang dipublikasikan—adalah kurva pasokan yang dapat mereka andalkan di masa mendatang.

---

## 3. Model Tokenomics

### Emisi Blok

Jaringan memproduksi blok baru setiap 60 detik dan memberikan 8,25 XEQM kepada node layanan yang terpilih. Ini menghasilkan 11.880 XEQM per hari di seluruh jaringan.

### Emisi Tata Kelola

Protokol mengalokasikan emisi tata kelola yang terpisah ke dompet kas. Kas menerima sekitar 17.857 XEQM per hari, atau kira-kira 124.999 XEQM per minggu. Ini mendanai pengembangan, platform XEQM Labs, dukungan ekosistem, pekerjaan keamanan, dan cadangan jangka panjang pada jadwal yang stabil dan dapat diprediksi.

### Model Distribusi

Semua XEQM yang baru diterbitkan mengikuti alokasi yang lugas. Ini adalah persentase target yang memandu perencanaan jangka panjang. Protokol tidak mengodekannya secara kaku (*hardcode*), dan tata kelola dapat menyesuaikannya.

| Alokasi | Pangsa | Tujuan |
|---|---|---|
| Hadiah Node Layanan | 40% | Dibayarkan langsung ke node layanan sebagai kompensasi atas pengamanan jaringan |
| Pengembangan Protokol Inti | 25% | Mendukung pengembangan blockchain, platform XEQM Labs, dan layanan jaringan inti |
| Pemasaran dan Kesadaran (*Awareness*) | 15% | Meningkatkan visibilitas jaringan dan mendukung adopsi |
| Ekosistem dan Komunitas | 10% | Hibah, *bounties*, Hadiah komunitas, dan dukungan integrasi |
| Keamanan dan Audit | 5% | Mencakup audit, tinjauan keamanan, dan pengujian keandalan |
| Cadangan Jangka Panjang | 5% | Disimpan untuk stabilitas, kebutuhan darurat, atau operasional jangka panjang |

### Distribusi Biaya Platform XEQM Labs

Di luar Hadiah blok, platform developer XEQM Labs menghasilkan biaya yang menguntungkan ekosistem yang lebih luas. Platform mendistribusikan semua pendapatan sebagai berikut:

| Penerima | Pangsa | Catatan |
|---|---|---|
| Operator Node API | 35% | Didistribusikan secara proporsional berdasarkan permintaan yang dilayani kepada operator yang menjalankan node API XEQM Labs |
| Kas XEQM Labs | 35% | Mendanai pengembangan platform yang sedang berjalan |
| Tata Kelola Komunitas | 30% | Mengalir ke dompet tata kelola untuk alokasi yang diarahkan oleh komunitas |

Node API adalah infrastruktur independen. Mereka tidak perlu berjalan di mesin yang sama dengan node layanan, dan menjalankannya tidak memerlukan latar belakang operator node layanan. Operator mana pun yang memiliki kemampuan teknis dapat menjalankan node API, mendaftar ke platform, dan mulai mendapatkan pangsa biaya platform yang proporsional dengan permintaan yang mereka layani. Persyaratan perangkat keras dasar saat ini tergolong standar: 4 inti CPU, RAM 8 GB, penyimpanan SSD 100 GB, dan koneksi jaringan 100 Mbps. Aplikasi Privasi XEQM dan beban kerja oracle di masa mendatang akan memerlukan spesifikasi yang lebih tinggi, dan operator didorong untuk merencanakan penskalaan vertikal (*vertical scaling*) saat tugas oracle mulai tersedia. VPS standar diperkirakan memakan biaya $20 hingga $40 per bulan pada persyaratan dasar saat ini.

Operator node layanan yang juga menjalankan node API mendapatkan Hadiah blok dari partisipasi konsensus sekaligus pangsa proporsional biaya platform dari lalu lintas API. Ini adalah dua aliran pendapatan yang terpisah dan saling menambah. Operator yang tidak menjalankan node API tetap mendapatkan Hadiah blok seperti biasa. Operator yang juga mengambil tugas verifikator oracle mendapatkan aliran Hadiah tambahan ketiga dari biaya oracle, yang dijelaskan dalam Bagian 10.

### Strategi Inflasi Jangka Panjang

Mainnet berjalan pada emisi yang stabil dan dapat diprediksi, tetapi level ini tidak dimaksudkan untuk tetap permanen. Seiring dengan platform XEQM Labs menghasilkan pendapatan yang berkelanjutan, jaringan akan berupaya mengurangi emisi tata kelola dan mengurangi ketergantungan pada penerbitan token untuk pendanaan operasional. Inflasi menurun seiring meningkatnya pendapatan protokol. Operator node layanan, pemegang token, dan kontributor ekosistem semuanya diuntungkan oleh hasil tersebut.

---

## 4. Struktur Node Layanan

### Parameter Staking

Parameter berikut berlaku untuk node layanan di jaringan XEQM Labs.

| Parameter | Nilai |
|---|---|
| Persyaratan node penuh (*full node*) | 200.000 XEQM |
| *Stake* minimum operator | 100.000 XEQM (50% dari persyaratan penuh) |
| Biaya (*fee*) maksimum operator | 10% |
| Periode pelepasan (*unbonding period*) | 14 hari |
| Slot kontributor maksimum | 11 (termasuk operator) |
| Kontribusi komunitas minimum per slot | 10.000 XEQM |
| Jendela staker komunitas per node | Hingga 100.000 XEQM di maksimum 10 slot kontributor |

### Mengapa 200.000 XEQM Per Node

Persyaratan node penuh sebesar 200.000 XEQM dikalibrasi terhadap pasokan awal terverifikasi sebesar 276.917.604 XEQM. Ukuran ini ditentukan untuk mengunci pangsa pasokan yang berarti dalam keamanan jaringan aktif, sembari menyisakan ambang bebas (*free float*) yang cukup untuk likuiditas bursa, orientasi (*onboarding*) developer, dan konsumsi API yang berkelanjutan.

Pada angka 200.000 XEQM per node penuh, 700 node akan mengunci 140.000,000 XEQM, yang merupakan sekitar 50,6% dari pasokan awal. Menghapus pangsa tersebut dari sirkulasi aktif meredam volatilitas spekulatif dan menciptakan permintaan yang berkelanjutan untuk token tersebut. Sisa sekitar 137.000.000 XEQM dalam ambang bebas memberikan kedalaman yang dibutuhkan oleh pasar bursa dan jalur orientasi developer. Seiring emisi menumbuhkan total pasokan dari waktu ke waktu, pangsa yang dikunci akan menurun sebagai persentase pasokan, yang mana memang merupakan lintasan yang ditargetkan: jaringan menjadi lebih likuid secara proporsional seiring matangnya jaringan dan seiring aktivitas platform menciptakan permintaan tambahan untuk XEQM ambang bebas.

### Mengapa Batas Minimum Stake Kontributor 10.000 XEQM

Setiap node layanan mendukung hingga 11 slot kontributor, termasuk operator. Operator menempati satu slot dan berkontribusi 100.000 XEQM, menyisakan 10 slot yang berbagi hingga 100.000 XEQM dari *stake* komunitas. Batas minimum 10.000 XEQM per slot kontributor menyaring kontribusi sepele atau debu (*dust*) yang tidak memiliki tujuan jaringan, serta memberikan kontributor taruhan ekonomi yang nyata dalam kinerja node. Ini juga menjaga agar *staking* komunitas tetap dapat diakses oleh para pemegang token yang tidak dapat menjalankan node penuh sendiri.

### Mengapa Stake Minimum Operator 50%

*Stake* minimum operator ditetapkan sebesar 50% dari persyaratan node penuh, atau 100.000 XEQM. Bagian vektor serangan di bawah ini menjelaskan hal ini secara terperinci. Singkatnya, *stake* minimum yang rendah memberikan insentif ekonomi bagi aktor jahat untuk membuka node dengan modal minimal dan meraup Hadiah yang tidak proporsional. Menetapkan batas minimum pada 50% menghapus insentif tersebut sembari tetap memungkinkan anggota komunitas untuk berkontribusi pada sisa *stake* di slot kontributor yang tersedia.

### Siklus Hidup Node Layanan

Node layanan di jaringan XEQM Labs beroperasi dengan ketentuan berkelanjutan, bukan periode tetap.

- Node tetap aktif tanpa batas waktu selama operator mempertahankan kolateral yang di-*stake* dan memenuhi persyaratan kinerja. Tidak ada jangka waktu tetap dan tidak diperlukan pembaruan.
- Jika sebuah node tidak lagi patuh, operator dapat memperbaiki masalah tersebut dan kembali mendapatkan Hadiah tanpa kehilangan sisa periode tetap. Jika operator tidak memperbaiki masalah tersebut, node layanan akan dilepas (*unbond*) setelah 7 hari dan tidak menerima Hadiah selama periode pelepasan tersebut.
- Operator dapat keluar kapan saja. Periode pelepasan 14 hari hanya berlaku ketika operator memilih untuk pergi.
- Kontributor komunitas dapat menyediakan antara 10.000 XEQM hingga porsi yang belum terpenuhi dari persyaratan node, di maksimum 10 slot kontributor yang tersedia.

---

## 5. Vektor Serangan dan Perlindungan

### Serangan Pengambilalihan Biaya Operator

Serangan ini ada di dalam basis kode asal fork mainnet XEQM Labs dan memerlukan perubahan kode untuk memperbaikinya. Kami mengungkapkannya di sini karena para staker komunitas perlu memahami risiko serta mitigasi yang diterapkan.

Jaringan mendistribusikan Hadiah node layanan dalam dua langkah. Pertama, jaringan menghitung persentase biaya operator dari total Hadiah blok sebelum distribusi apa pun terjadi. Kedua, jaringan membagi sisa Hadiah secara proporsional di antara semua kontributor berdasarkan pangsa *stake* mereka.

Smisal tanpa kontrol yang dijelaskan di bawah ini, seorang operator dapat membuka node dengan modal minimal dan menetapkan biaya hingga 100%. Pada biaya 100%, operator akan menerima seluruh Hadiah blok terlepas dari berapa banyak yang di-*stake* oleh orang lain. Kontributor yang menaruh sisa *stake* tidak akan mendapatkan apa-apa. Operator akan meraup 100% Hadiah menggunakan sebagian kecil dari kolateral yang disyaratkan.

Dua kontrol yang saling tumpang tindih dalam parameter XEQM Labs mengatasi serangan ini.

Pertama, biaya maksimum operator dibatasi sebesar 10%. Pada biaya 10%, operator yang menaruh tepat batas minimum 100.000 XEQM mendapatkan 10% dari Hadiah blok sebagai biaya, ditambah 50% dari sisa 90% tersebut, sehingga totalnya menjadi 55% dari Hadiah blok. Kontributor komunitas yang menaruh 100.000 XEQM lainnya mendapatkan 45% dari Hadiah blok. Itu adalah hasil yang proporsional dan masuk akal.

Kedua, *stake* minimum operator sebesar 50% mengharuskan operator untuk berkomitmen pada modal yang besar sebelum membuka node. Aktor jahat tidak lagi memiliki jalur untuk meraup 100% Hadiah dengan modal minimal. Bersama-sama, batas atas biaya dan *stake* minimum yang lebih tinggi membuat serangan ini tidak rasional secara ekonomi.

Staker komunitas tetap harus menggunakan penilaian yang bijak saat memilih node. Penjelajah node (*node explorer*) menampilkan biaya, persentase *stake* operator, dan jumlah kontributor saat ini sebelum staker membuat komitmen.

### Tindakan Anti-Sybil

Dalam konteks ini, serangan Sybil berarti satu aktor mengoperasikan sejumlah besar node untuk mendapatkan pengaruh yang tidak proporsional atas jaringan. Kekhawatiran ini nyata. Buku besar penukaran menunjukkan bahwa 10 dompet teratas dalam migrasi memegang konsentrasi XEQM yang sangat besar, dan beberapa dompet tampaknya sengaja dipecah menjadi saldo yang hampir identik.

Pemisahan dompet tidak selalu menunjukkan niat jahat. Pemegang besar umumnya mendistribusikan kepemilikan ke beberapa alamat untuk alasan keamanan dan operasional. Terlepas dari itu, kami mencatat dan memantau pola ini.

Perlindungan berikut telah diterapkan atau ditegakkan melalui kebijakan tata kelola.

**Penghalang biaya modal.** *Stake* minimum operator sebesar 100.000 XEQM secara signifikan meningkatkan biaya menjalankan setiap node dan membatasi secara berarti berapa banyak node yang dapat dioperasikan oleh satu dompet.

**Batas konsentrasi node tata kelola.** Kebijakan yang ditegakkan oleh tata kelola membatasi operator yang dapat diidentifikasi hingga sekitar 50 node, kira-kira 7% dari jaringan dengan 700 node. Penjelajah node secara publik mencantumkan setiap node layanan aktif bersama dengan kunci publik registrasinya dan alamat IP yang diumumkan. Tim dan komunitas memantau daftar tersebut untuk melihat pola yang menunjukkan jika satu operator mengendalikan lebih dari batas maksimal. Ketika kami mengidentifikasi suatu pola, kami akan menghubungi operator tersebut dan memberi mereka kesempatan untuk mengurangi jumlah node mereka secara sukarela. Operator yang tidak patuh akan menghadapi identifikasi publik dan tindakan tata kelola, yang minimal berarti kami menambahkan kunci registrasi mereka ke daftar blok protokol guna mencegah registrasi node di masa mendatang.

**Daftar blok kunci publik.** Daftar blok kunci publik registrasinya dikelola oleh tata kelola, dan jaringan akan menolak kunci-kunci tersebut untuk registrasi node di masa mendatang. Ketika aktor jahat dihapus registrasinya karena perilaku buruk, kunci publik mereka akan ditambahkan secara permanen ke daftar tersebut. Menghasilkan pasangan kunci baru tidak memakan biaya, tetapi beroperasi di bawah kunci baru sementara kunci asli berada di daftar blok akan terlihat oleh alat pemantau dan menciptakan catatan penghindaran yang terdokumentasi, di mana hal ini memperkuat alasan untuk tindakan tata kelola lebih lanjut.

**Pemantauan alamat IP.** Node layanan harus mengumumkan alamat IP mereka secara publik untuk berpartisipasi dalam jaringan. Ini adalah persyaratan fungsional, bukan opsional. Beberapa node yang berjalan dari alamat IP atau subnet yang sama hampir pasti milik operator yang sama. Beberapa node yang berjalan dari penyedia hosting dan blok pusat data (*datacenter*) yang sama sangat menunjukkan satu operator tunggal bahkan di alamat IP yang berbeda. Kami menandai node yang muncul dari rentang IP terkait sesaat setelah peristiwa deregistrasi untuk ditinjau. Operator canggih yang menggunakan penyedia VPS berbeda di berbagai wilayah menambahkan biaya dan kompleksitas pada operasi mereka tanpa menghilangkan visibilitas mereka, karena pola perilaku di seluruh kunci, alamat, dan waktu masih menghasilkan catatan yang dapat dilacak.

**Analisis grafik slot kontributor.** Setiap node layanan mendukung hingga 11 slot kontributor, dan setiap kontributor mendaftarkan alamat dompet terhadap node tersebut. Operator yang menjalankan beberapa node dan menggunakan alamat kontributor sekunder yang sama di seluruh node tersebut, atau yang mendanai slot kontributor dari dompet yang memiliki hubungan yang dapat diamati dengan dompet operator, menciptakan grafik yang dapat dianalisis oleh alat pemantau. Pada rantai yang menjaga privasi, analisis ini kurang begitu lugas dibandingkan pada rantai transparan, tetapi registrasi kontributor membawa data yang dapat diamati yang melengkapi pemantauan IP dan kunci.

**Target koefisien Nakamoto.** Jaringan menargetkan koefisien Nakamoto minimal 8, yang berarti setidaknya 8 operator independen harus bekerja sama untuk mengendalikan 51% node aktif. Distribusi dompet saat ini menghasilkan koefisien Nakamoto sekitar 4 pada saat peluncuran. Batas node tata kelola dan pertumbuhan alami dari himpunan operator adalah mekanisme utama yang akan meningkatkan angka tersebut seiring waktu.

Koefisien Nakamoto sekitar 4 saat peluncuran lebih rendah dari target 8. Kami menyatakan hal ini di sini karena pengungkapan yang jujur mengenai kelemahan yang diketahui lebih berharga daripada diam. Kesenjangan ini akan menutup seiring dengan lebih banyak operator bergabung dengan jaringan dan seiring batas konsentrasi tata kelola ditegakkan. Pemilihan kuorum oracle, yang dijelaskan dalam Bagian 10, tidak akan dibuka untuk konsumen kontrak eksternal sampai koefisien Nakamoto mencapai setidaknya 6, memberikan batas integritas yang berarti sebelum output oracle membawa bobot kepercayaan yang nyata.

---

## 6. XEQM sebagai Token Utilitas

XEQM adalah token akses dan penggunaan untuk platform developer, dan perbedaan itu penting ketika memikirkan dinamika pasokan.

Platform developer XEQM Labs memerlukan XEQM di setiap tingkat interaksi. Developer melakukan *stake* XEQM untuk membuka tingkatan akses API. Ketika mereka pergi, mereka mendapatkan kembali *stake* tersebut; ini adalah mekanisme komitmen, bukan biaya. Aplikasi mengonsumsi XEQM ketika mereka melakukan panggilan API di atas batas tingkatan mereka. Operator mendapatkan XEQM untuk infrastruktur yang mereka kontribusikan.

| Tingkatan | Stake yang Diperlukan | Panggilan yang Disertakan |
|---|---|---|
| Gratis | Tidak ada | 10.000 panggilan testnet per bulan |
| Builder | 1.000 XEQM | 100.000 panggilan mainnet per bulan |
| Produksi | 10.000 XEQM | 1.000.000 panggilan per bulan, webhooks, dukungan prioritas |
| Enterprise | 50,000 XEQM | Panggilan tak terbatas, batas tarif khusus, SLA |

Akses umpan data (*data feed*) oracle selaras dengan struktur tingkatan yang ada. Developer tingkat Produksi dan Enterprise mendapatkan akses ke output oracle sebagai bagian dari kapabilitas yang disertakan. Beban kerja berat oracle yang melebihi batas tarif standar mengonsumsi XEQM pada model per panggilan yang sama seperti lalu lintas API lainnya. Ini menciptakan lapisan permintaan keempat di atas tiga penampung (*sinks*) yang telah dijelaskan: *staking* node, *staking* tingkatan developer, dan konsumsi panggilan API. Konsumen oracle harus memegang dan membelanjakan XEQM untuk mengakses umpan data privat terautentikasi.

Tiga penampung permintaan yang berbeda beroperasi secara bersamaan. *Staking* node layanan mengunci pangsa pasokan terbesar. *Staking* tingkatan developer menciptakan tekanan beli yang berkelanjutan dari partisipan pasar baru yang harus memperoleh XEQM sebelum mereka dapat mengakses platform. Konsumsi panggilan API menciptakan lapisan kecepatan yang berkelanjutan saat aplikasi memproses permintaan di atas batas tingkatan mereka.

Parameter pasokan dalam dokumen ini dirancang dengan mempertimbangkan semua penampung tersebut. Ambang bebas yang beredar sekitar 137 juta XEQM pada pasokan awal, setelah 700 node di-*stake* penuh, memberikan likuiditas yang cukup bagi pasar bursa, orientasi developer, dan konsumsi API yang berkelanjutan agar dapat berfungsi. Likuiditas ambang bebas tumbuh seiring waktu karena emisi menambah total pasokan. Persyaratan node yang lebih ketat akan menyusutkan ambang bebas ke tingkat yang akan membuat orientasi developer menjadi sulit dan penganggaran biaya API menjadi tidak andal, di mana hal ini akan langsung merusak proposisi nilai platform.

---

## 7. Tata Kelola dan Kas (*Treasury*)

Model kas XEQM Labs mengonsolidasikan semua pendanaan tata kelola ke dalam satu jadwal emisi tunggal yang dapat diprediksi.

Tata kelola saat ini dijalankan melalui tim pendiri. Tim membuat keputusan dengan masukan dari komunitas melalui saluran Telegram terbuka dan diskusi GitHub. Ini adalah deskripsi jujur tentang bagaimana hal-hal bekerja hari ini. Belum ada mekanisme pemungutan suara (*voting*) on-chain, dan tidak ada cara untuk memverifikasi secara kriptografis bahwa peserta dalam diskusi komunitas benar-benar memegang XEQM. Proses tata kelola apa pun harus memperhitungkan realitas tersebut daripada mengasumsikan partisipasi dengan niat baik dari setiap suara di setiap saluran.

Fase peta jalan di masa mendatang akan bergerak menuju model tata kelola yang lebih terstruktur. Fase 3 memperkenalkan proses proposal dan komentar formal. Fase 4 memperkenalkan pemungutan suara berbobot (*weighted voting*) di mana operator node layanan dan node API memegang hak formal yang proporsional dengan *stake* dan masa jabatan mereka. Operator yang memiliki andil langsung dalam permainan (*skin in the game*) melalui kolateral yang di-*stake* adalah konstituensi paling berarti untuk keputusan tata kelola, dan model berbobot mencerminkan hal tersebut.

Alokasi 40/25/15/10/5/5 yang dijelaskan dalam Bagian 3 memandu perencanaan sebagai target. Tim pendiri akan mengusulkan perubahan secara publik, mendiskusikannya secara terbuka, dan memutuskannya melalui konsultasi dengan komunitas operator sampai mekanisme tata kelola yang lebih formal diterapkan.

---

## 8. Parameter Ringkasan

| Parameter | Nilai |
|---|---|
| Mekanisme konsensus | 100% Proof-of-Stake |
| Waktu blok | 60 detik |
| Hadiah blok | 8,25 XEQM per blok |
| Emisi blok harian | 11.880 XEQM |
| Emisi tata kelola | ~17.857 XEQM per hari |
| Persyaratan node penuh | 200.000 XEQM |
| *Stake* minimum operator | 100.000 XEQM (50%) |
| Biaya maksimum operator | 10% |
| Slot kontributor maksimum | 11 (termasuk operator) |
| Kontribusi komunitas minimum | 10.000 XEQM per slot |
| Jendela staker komunitas per node | Hingga 100.000 XEQM di 10 slot |
| Periode pelepasan (*unbonding*) | 14 hari |
| Total pasokan | Pasokan awal terverifikasi: 276.917.604 XEQM. Tumbuh seiring waktu melalui emisi terjadwal. |
| Pasokan dikunci pada 700 node | 140.000.000 XEQM (kira-kira 50,6% dari pasokan awal, menurun sebagai pangsa seiring waktu) |
| Sisa beredar bebas pada 700 node | Sekitar 137.000.000 XEQM pada pasokan awal, tumbuh seiring emisi |
| APY operator solo pada 700 node | ~3,1% (hanya Hadiah blok) |
| Koefisien Nakamoto saat peluncuran | ~4 (target: 8, meningkat seiring waktu) |
| Aktivasi eksternal kuorum oracle | Koefisien Nakamoto ≥ 6 |

---

## 9. Peta Jalan

Mainnet XEQM Labs telah aktif. Peta jalan berikut menjelaskan pekerjaan ke depan.

**Fase 1: Stabilisasi jaringan.** Pemantauan berkelanjutan terhadap produksi blok, waktu aktif (*uptime*) node layanan, dan kesehatan jaringan. Dukungan orientasi operator. Penyelesaian fitur penjelajah node.

**Fase 2: Peluncuran produksi platform API XEQM Labs.** Rilis publik API developer, registrasi tingkatan, orientasi node API, dan integrasi produksi pertama. Distribusi biaya node API mulai aktif.

**Fase 3: Peluncuran bertahap Oracle Privasi.** Bukti konsep internal, testnet terfederasi, dan oracle mainnet dengan konsumen internal, sebagaimana dijelaskan dalam Bagian 10.

**Fase 4: Akses konsumen oracle eksternal.** Output oracle menjadi tersedia untuk konsumen kontrak pintar eksternal dan developer XEQM Labs tingkat Produksi dan Enterprise. Fase ini hanya aktif setelah koefisien Nakamoto mencapai setidaknya 6.

**Fase 5: Tata kelola formal.** Proses proposal terstruktur, pemungutan suara berbobot untuk operator, dan transisi jangka panjang melepaskan diri dari tata kelola tim pendiri.

---

## 10. Oracle Privasi XEQM

### Gambaran Umum

Oracle Privasi XEQM adalah kapabilitas terencana dari platform XEQM Labs yang memungkinkan kontrak pintar dan aplikasi eksternal untuk mengonsumsi umpan data privat terautentikasi tanpa mengekspos data sumber yang mendasarinya. Ini dibangun di atas protokol oracle terdesentralisasi untuk TLS yang membuktikan asal-usul data dari titik akhir (*endpoints*) HTTPS standar menggunakan pembuktian tanpa pengetahuan, tanpa memerlukan kerja sama dari sisi server dan tanpa perangkat keras tepercaya.

Oracle ini bukan bagian dari rangkaian fitur awal mainnet. Ini adalah kapabilitas platform fase berikutnya, yang dikembangkan setelah mainnet XEQM Labs stabil dan platform API XEQM Labs telah mencapai tahap produksi. Bagian ini menjelaskan arsitektur, rencana pembangunan bertahap, dan bagaimana partisipasi oracle berintegrasi dengan model Hadiah node layanan dan node API yang sudah ada.

### Mengapa Ini Cocok untuk XEQM

Proposisi nilai inti XEQM adalah privasi. Oracle memperluas proposisi nilai tersebut melampaui rantai itu sendiri ke dalam ekonomi data yang lebih luas. Aplikasi yang dibangun di atas XEQM Labs dapat menggunakan oracle untuk membuktikan fakta tentang data web privat, seperti ambang batas harga, saldo akun, atribut kredensial, dan kondisi kepatuhan, tanpa mengungkapkan data yang mendasarinya ke jaringan oracle, aplikasi, atau blockchain.

Ini bukan oracle tujuan umum yang bersaing dengan penyedia umpan data yang ada. Ini adalah oracle yang mengutamakan privasi yang dirancang khusus untuk kasus penggunaan di mana data itu sendiri harus tetap rahasia. Itu adalah ceruk (*niche*) yang sempit dan dapat dipertahankan yang selaras dengan apa yang sudah dilakukan XEQM.

### Arsitektur

Oracle beroperasi sebagai sistem tiga lapisan yang berada di atas infrastruktur node layanan yang ada.

**Lapisan pembukti.** Aplikasi atau pengguna yang memegang akses ke sumber data privat bertindak sebagai pembukti. Pembukti mengambil data dari titik akhir TLS standar, seperti API harga, portal akun, atau umpan kepatuhan, dan berpartisipasi dalam protokol kriptografi yang berkomitmen pada respons tanpa mengungkapkannya.

**Lapisan verifikator.** Kuorum berputar dari node layanan bertindak sebagai verifikator. Node verifikator membantu pembukti dalam menghasilkan komitmen yang tidak dapat dipalsukan terhadap data sesi TLS menggunakan protokol jabat tangan tiga pihak (*three-party handshake*), kemudian memverifikasi bahwa data yang berkomitmen memenuhi kondisi yang diminta. Node verifikator hanya mempelajari hasil dari kondisi tersebut, benar atau salah, di atas atau di bawah ambang batas, dan tidak pernah melihat data yang mendasari atau kredensial pembukti.

**Lapisan konsumen.** Kontrak pintar atau konsumen API XEQM Labs hanya menerima output minimal: hasil boolean, perbandingan ambang batas, atestasi bertanda tangan, atau nilai turunan kecil. Data sumber mentah tidak pernah dipublikasikan ke konsumen mana pun.

Node verifikator dipercaya untuk integritasnya, bukan untuk privasinya. Bahkan jika semua node verifikator dalam suatu kuorum disusupi secara bersamaan, desain protokol tetap menjaga privasi data pembukti. Beberapa verifikator dapat diwajibkan untuk mencapai kesepakatan kuorum sebelum output apa pun ditandatangani, di mana hal ini membatasi dampak dari satu node tidak jujur terhadap integritas.

### Rencana Pembangunan Bertahap

**Fase 1, Bukti konsep internal.** Seorang pembukti tunggal dan sebuah node verifikator tunggal yang dioperasikan oleh tim pendiri memvalidasi protokol kriptografi penuh dari ujung ke ujung (*end to end*) terhadap sejumlah kecil sumber data yang masuk daftar putih (*whitelist*). Tidak ada konsumen eksternal. Tidak ada partisipasi node layanan. Tujuannya adalah memastikan protokol berfungsi terhadap titik akhir TLS nyata dalam kondisi jaringan produksi sebelum melibatkan komunitas operator yang lebih luas.

**Fase 2, Testnet oracle terfederasi.** Sekelompok kecil operator node layanan sukarela, yang dipilih dari node dengan riwayat waktu aktif yang kuat dan memenuhi spesifikasi perangkat keras yang ditingkatkan, bergabung dengan kumpulan verifikator di testnet. Tugas oracle berputar melalui kelompok ini menggunakan adaptasi dari logika pemilihan kuorum yang ada. Kondisi pemotongan (*slashing conditions*) untuk atestasi yang terbukti salah diuji dalam kondisi musuh (*adversarial*) sebelum peluncuran mainnet apa pun. Fase ini tidak membuka output oracle untuk konsumen kontrak eksternal.

**Fase 3, Oracle mainnet dengan konsumen internal.** Tugas verifikator oracle dibuka untuk kelompok node layanan yang lebih luas yang memenuhi syarat di mainnet. Output hanya masuk ke kontrak internal XEQM Labs. Ukuran kuorum, parameter rotasi, dan kondisi pemotongan difinalisasi berdasarkan pengamatan testnet. Biaya oracle mulai mengalir ke node verifikator yang berpartisipasi sebagai aliran Hadiah tambahan.

**Fase 4, Akses konsumen eksternal.** Output oracle menjadi tersedia untuk developer XEQM Labs tingkat Produksi dan Enterprise serta konsumen kontrak pintar eksternal. Fase ini tidak akan aktif sampai koefisien Nakamoto jaringan mencapai setidaknya 6. Aktivasi eksternal sebelum ambang batas tersebut akan mengekspos output oracle ke risiko konsentrasi yang tidak dapat diterima.

### Persyaratan Perangkat Keras Verifikator Oracle

Tugas verifikator oracle membutuhkan komputasi yang intensif. Protokol jabat tangan tiga pihak dan komputasi dua pihak yang mendasari oracle melibatkan beberapa putaran kriptografi interaktif yang secara signifikan lebih menuntut daripada operasi node layanan standar.

Node yang memilih untuk berpartisipasi dalam tugas verifikator oracle harus memenuhi spesifikasi perangkat keras yang ditingkatkan pada saat spesifikasi tersebut difinalisasi. Persyaratan indikatif saat ini adalah minimal 8 inti CPU, RAM 16 GB, penyimpanan SSD 200 GB, dan koneksi jaringan 500 Mbps dengan latensi rendah. Angka-angka ini mencerminkan tolok ukur terhadap implementasi protokol yang sebanding dan akan dikonfirmasi sebelum Fase 2 dimulai. Perangkat keras dasar node API standar tidak cukup untuk tugas verifikator oracle.

Operator yang memenuhi spesifikasi yang ditingkatkan dan ikut serta (*opt-in*) ke dalam tugas oracle akan diidentifikasi di penjelajah node. Pemilihan kuorum untuk sesi oracle ditarik secara eksklusif dari kumpulan opt-in ini.

### Hadiah Verifikator Oracle

Node verifikator oracle mendapatkan kompensasi di luar Hadiah blok standar. Struktur Hadiah untuk partisipasi oracle adalah sebagai berikut.

| Sumber Pendapatan | Deskripsi |
|---|---|
| Hadiah blok | Hadiah blok node layanan standar, tidak berubah |
| Biaya node API | Pangsa proporsional dari biaya platform XEQM Labs untuk operator yang juga menjalankan node API |
| Biaya sesi oracle | Biaya per sesi yang dibayarkan oleh konsumen oracle, didistribusikan ke kuorum verifikator yang memproses sesi tersebut |
| Bonus tugas oracle | Emisi tambahan yang dialokasikan dari dompet tata kelola ke node yang memenuhi syarat oracle selama periode volume konsumen rendah, memastikan node verifikator tetap layak secara ekonomi sebelum permintaan oracle mencapai tingkat yang mandiri |

Bonus tugas oracle adalah mekanisme pengisian daya awal (*bootstrapping*). Seiring pertumbuhan volume konsumen oracle dan biaya sesi menjadi sumber pendapatan utama bagi node verifikator, komponen emisi tata kelola akan dikurangi secara proporsional. Model jangka panjangnya adalah keberlanjutan biaya sesi tanpa subsidi tata kelola yang berkelanjutan.

### Pengelolaan Sumber Data

Tidak semua sumber data sesuai untuk konsumsi oracle. Oracle mempertahankan registri sumber bertingkat yang dikelola oleh tata kelola.

**Tingkat 1, Sumber produksi yang masuk daftar putih.** Sumber yang ditinjau dan disetujui untuk penggunaan oracle mainnet. Ini adalah satu-satunya sumber yang tersedia untuk konsumen eksternal di Fase 4.

**Tingkat 2, Sumber validasi silang.** Sumber yang digunakan secara internal untuk memvalidasi output Tingkat 1 tetapi tidak diekspos secara langsung kepada konsumen. Umpan harga Tingkat 1 yang menyimpang secara material dari semua sumber Tingkat 2 yang tersedia akan memicu penahanan pada output sesi tersebut sembari menunggu peninjauan manual.

**Tingkat 3, Sumber yang dikecualikan.** Sumber yang menimbulkan kekhawatiran hukum, kepatuhan, atau keandalan. Node oracle tidak akan memproses sesi yang menargetkan sumber yang dikecualikan. Tata kelola memelihara dan memublikasikan daftar yang dikecualikan.

Baik operator oracle maupun pengguna memikul tanggung jawab hukum atas sumber data yang mereka akses. Protokol oracle tidak memberikan izin untuk mengakses data yang dilarang oleh ketentuan layanan. Pemeriksaan tata kelola terhadap sumber Tingkat 1 mencakup peninjauan terhadap ketentuan layanan yang berlaku dan paparan hukum apa pun yang diketahui. Operator diinformasikan tentang peninjauan ini sebelum sumber dimasukkan ke daftar putih.

### Cakupan MVP

Produk Minimum Viable Product (MVP) menargetkan satu kasus penggunaan tunggal: atestasi ambang batas harga privat. Seorang pembukti mengambil harga dari sumber Tingkat 1 yang masuk daftar putih dan membuktikan kepada kuorum verifikator bahwa harga tersebut berada di atas atau di bawah nilai yang ditentukan, tanpa mengungkapkan harga persisnya atau kredensial API pembukti. Kuorum verifikator menandatangani hasil boolean tersebut. Atestasi yang ditandatangani dikirimkan ke kontrak atau aplikasi yang meminta.

Cakupan ini sengaja dibuat sempit. Ini memvalidasi seluruh tumpukan protokol—jabat tangan tiga pihak, eksekusi kueri komputasi dua pihak, pembuatan bukti tanpa pengetahuan, penandatanganan kuorum, dan pengiriman output—tanpa memerlukan integritas konteks yang lebih luas dan kapabilitas agregasi multi-sumber yang akan ditambahkan oleh fase-fase berikutnya. Perluasan MVP ke kasus penggunaan tambahan akan menyusul setelah protokol inti stabil dalam produksi.

---

*Ini adalah dokumen draf. Parameter, jadwal emisi, dan fase peta jalan yang dijelaskan di sini adalah desain yang dimaksudkan. Pembaruan untuk whitepaper ini akan dipublikasikan seiring perkembangan jaringan dan platform.*
