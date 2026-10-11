## Analisis Perbandingan Algoritma A*, Branch and Bound, dan Time-Dependent Customized A* untuk Optimasi Rute Evakuasi Banjir Rob di Kota Semarang

Muhammad Fikri - 24060124130069

Departemen Informatika Universitas Diponegoro Semarang, Indonesia

muhffikri@students.undip.ac.id

naiknya air laut inilah yang memicu terjadinya bencana banjir pasang air laut (rob) yang kini menjadi fenomena permanen di pesisir Semarang.

Meskipun rob menjadi ancaman fisik yang nyata, sifat genangan air yang bergerak perlahan dan terjadi secara berulang justru memicu bias psikologis di tengah masyarakat terdampak [2], [8]. Warga lokal cenderung meremehkan eskalasi bahaya karena menganggap rob sebagai rutinitas harian biasa, sehingga mereka memilih untuk tetap bertahan di dalam rumah masing-masing [8]. Akibatnya, keputusan untuk melakukan evakuasi mandiri sering kali diambil secara mendadak dan tidak terencana ketika ketinggian air telah naik secara ekstrem hingga merendam utilitas domestik. Kondisi evakuasi yang reaktif dan serentak pada titik kritis inilah yang memicu kepanikan massal serta membebani koridor transportasi yang ada di zona pesisir Semarang.

Masalah penataan rute dalam evakuasi mandiri saat ini masih berpaku pada pemanfaatan sistem navigasi konvensional komersial seperti Google Maps [5], [9]. Aplikasi navigasi tersebut memiliki kelemahan fatal dalam konteks manajemen bencana perkotaan karena arsitektur algoritmanya bersifat statis dan buta terhadap data fluktuasi genangan air dari jam ke jam [5], [6]. Navigasi komersial murni menghitung hambatan berdasarkan volume kendaraan, tanpa mengetahui apakah suatu ruas jalan masih dapat dilalui secara aman atau tidak. Akibat keterbatasan mendasar ini, armada penyelamat seperti truk BPBD dan ambulans, maupun kendaraan roda empat milik warga yang sedang menyelamatkan diri, sangat rentan terjebak di dalam jalur buntu yang telah tenggelam [6], [7]. Fenomena salah pilih rute ini memicu keterlambatan penyelamatan yang krusial dan meningkatkan risiko korban di tengah banjir pasang.

Guna mencegah risiko kelumpuhan navigasi tersebut, penelitian ini mengusulkan penerapan strategi pencarian lintasan yang adaptif terhadap dimensi waktu melalui pendekatan Time-Dependent Shortest Path (TDSP) [5], [6]. Dalam model transportasi dinamis ini, fungsi biaya aktual (g) tidak lagi bersifat konstan berdasarkan jarak geografis semata, melainkan dimodifikasi secara dinamis mengikuti estimasi waktu ketibaan kendaraan di suatu persimpangan jalan [5]. Pembaruan bobot graf jalan raya ini dilakukan secara kontinu dengan menyuntikkan kurva pasang surut air laut sinusoidal [1], [2], lalu dikonversikan menjadi fungsi penalti hambatan kendaraan (w) berbasis integrasi data spasial kontur bumi [8], [10]. Melalui skema ini, sistem secara cerdas dapat mengarahkan agen evakuasi kendaraan untuk memutar menjauhi ruas jalan sebelum air laut mencapai ketinggian kritis yang melumpuhkan mesin kendaraan.

## Abstract

Banjir rob di pesisir Kota Semarang secara kontras menurunkan keandalan jaringan jalan darat dan mengancam keselamatan mobilisasi evakuasi. Penelitian ini mengusulkan model rute evakuasi dinamis dependen-waktu menggunakan algoritma Custom Time-Dependent A-star (TD-A*). Metode ini mengintegrasikan graf jalan berarah, data elevasi, serta data temporal pasang surut air laut. Dampak genangan banjir terhadap ketahanan mekanis mobil dimodelkan dengan fungsi penalti non-linier dengan batas kritis lumpuh mesin >0.40 m. Eksperimen komputasional berbasis agen tunggal acak bersyarat dijalankan dari wilayah rawan Semarang Utara menuju Posko Balai Desa Rejomulyo. Hasil pengujian menunjukkan bahwa A-star (A*) gagal (Success Rate = 0.00%) akibat buta temporal sehingga melewati banjir sedalam 2.1209 m. Algoritma Branch and Bound (B&B) berhasil lolos (100.00%) namun kinerjanya menurun akibat ledakan kombinatorial yang mengeksplorasi 219.530 simpul graf dan membengkakkan latensi hingga 68.631,04 ms. Sebaliknya, algoritma usulan Custom TD-A* terbukti paling unggul secara signifikan dengan memotong 99.75% ruang pencarian cabang B&B menjadi hanya 559 simpul, serta mengunci latensi eksekusi sebesar 174.52 ms yang 99.75% lebih cepat dibandingkan B&B dengan paparan banjir minimum 0.0830 m sepanjang lintasan 5.94 km. Temuan ini memvalidasi bahwa Custom TD-A* dan fungsi bobot kustom dapat meningkatkan performa pencarian rute evakuasi banjir yang kompleks.

## Keywords

Evakuasi Dinamis, Banjir Rob, Time-Dependent A*, Branch and Bound, Pemodelan Spasio-Temporal.

## I. PENDAHULUAN

Intensifikasi perubahan iklim global dalam beberapa dekade terakhir telah memicu anomali cuaca dan meningkatkan frekuensi cuaca ekstrem, yang secara konsisten memperburuk ancaman bencana banjir di berbagai kawasan perkotaan dan pesisir di seluruh dunia [6]. Sebagai negara kepulauan, Indonesia menghadapi ancaman fisik yang sangat berbahaya pada wilayah pesisir tropis. Kawasan Pantai Utara Jawa (Pantura) menjadi salah satu titik dengan tingkat kerentanan tertinggi terhadap degradasi lingkungan [1], [2]. Secara spesifik, karakteristik fisik wilayah Pantura Kota Semarang, khususnya Kecamatan Genuk, Gayamsari, dan Semarang Utara menunjukkan kondisi penurunan daya dukung lingkungan yang kritis [1]. Wilayah-wilayah ini mengalami kombinasi destruktif antara topografi daratan yang sangat landai yang bersinggungan langsung dengan Laut Jawa, serta laju penurunan tanah yang masif [1], [2]. Ketidakseimbangan antara penurunan permukaan tanah dan


Tujuan utama dari penelitian ini adalah membangun

hambatan fisik kendaraan yang disimbolkan dengan fungsionalitas komputasi, didefinisikan sebuah fungsi penalti 𝑤(𝑑).

sebuah kerangka eksperimen komputasional yang komprehensif untuk membandingkan secara ketat performa efisiensi internal dan kualitas rute dari tiga strategi algoritma, yaitu A-star standar (A*) [4], Branch and Bound (B&B) [3], dan Time-Dependent A* (Custom TD-A*) [5]. Ketiga algoritma ini akan diuji di dalam skenario Agen Tunggal Mobil Acak Bersyarat melintasi objek graf transportasi berarah tiga kecamatan pesisir kritis Kota Semarang, yaitu Semarang Utara, Semarang Timur, dan Gayamsari [1]. Kontribusi utama dari penelitian ini meliputi: (1) Implementasi fungsi penalti spasio-temporal (w) yang secara dinamis memberikan bobot statis ruas jalan dengan mengintegrasikan model elevasi digital berbasis grid dengan data laut sinusoidal waktu nyata; (2) Analisis komparatif mendalam terhadap metrik performa komputasi; (3) Evaluasi keberhasilan mitigasi kasus lapangan untuk mencegah risiko kerusakan mekanis kendaraan mobil konvensional di wilayah pesisir berisiko tinggi

Fungsi 𝑤(𝑑) bertindak sebagai faktor pengali beban non-

linier terhadap jarak asli jalan. Pengaruh fisik genangan air terhadap kemampuan mekanis armada kendaraan roda empat dimodelkan secara bertingkat berdasarkan ambang batas knalpot kendaraan (0.40 meter) sebagai berikut [6], [8]:

1.0,

𝑑 < 0.20 m

∞,

𝑑 > 0.40 m

𝑤(𝑑) secara otomatis

mendegradasi kecepatan kendaraan aktual Adanya faktor penalti

(𝑉aktual) saat

melintasi area bencana. Hubungan matematis degradasi kecepatan ini berbanding terbalik dengan nilai beban penalti, yang dirumuskan melalui [6]:

𝑉aktual(𝑑) = 𝑉normal 𝑤(𝑑)

## II. BATASAN MASALAH

Penelitian ini dibatasi oleh parameter-parameter berikut:

(1) Evaluasi perilaku agen murni dialokasikan pada karakteristik skenario kendaraan mobil kecil; (2) Atribut sosial lalu lintas, seperti titik kemacetan akibat penumpukan volume kendaraan dan waktu tundaan di lampu lalu lintas diabaikan; (3) Jaringan transportasi dibatasi hanya untuk tipe jalan yang dapat diakses oleh kendaraan roda empat konvensional; (4) Kerapatan titik persimpangan pada graf jalan raya bersifat renggang dibanding kontinuitas piksel grid yang padat. Sehingga, terdapat variasi topografi pada ruas jalan di antara dua persimpangan yang berpotensi tidak terekam pada sistem graf.

Di mana 𝑉normal merupakan batas kecepatan maksimum

kendaraan aman di area perkotaan (8.33 m/s atau ≈ 30

km/jam). Ketika ketinggian air melebihi batas retensi fisik

berhingga ( mesin (d > 0.40 m), nilai ∞ ), yang secara fisik memutus akses busur w(d) melompat menuju tak tersebut dari jaringan graf karena kecepatan kendaraan jatuh ke titik nol [7].

## C. Formulasi Biaya Perjalanan Dependen-Waktu (Time- Dependent Cost Function)

Pada permasalahan TDSP, fungsi biaya perjalanan total untuk melintasi suatu lintasan merupakan fungsi dari waktu keberangkatan atau waktu ketibaan agen pada simpul tertentu [5]. Bobot perjalanan dinamis pada busur (u,v) saat agen berada pada waktu t, yang dinotasikan sebagai W(u,v,t), didefinisikan sebagai hasil perkalian antara panjang fisik ruas jalan dan faktor penalti yang bergantung pada kedalaman genangan:

𝑊(𝑢, 𝑣, 𝑡) = 𝐿(𝑢,𝑣) × 𝑤(𝑑(𝑣, 𝑡))

dengan

waktu menyatakan kedalaman genangan pada simpul tujuan

t, dan

Waktu ketibaan pada simpul tujuan (

simpul saat ini secara rekursif berdasarkan waktu keberadaan agen pada

(𝑡curr) ditambah waktu tempuh untuk melintasi

busur tersebut [5], [6]:

𝑡arrive = 𝑡curr + 𝑉aktual(𝑑) 𝐿(𝑢,𝑣) =

di mana 𝑉normal adalah kecepatan kendaraan pada kondisi

normal tanpa genangan, sedangkan

kecepatan kendaraan aktual yang telah dipengaruhi oleh kedalaman genangan d.

Model ini memenuhi properti First-In-First-Out (FIFO),

yang menjamin bahwa agen yang memasuki suatu ruas jalan lebih awal tidak akan tiba lebih lambat dibandingkan agen yang memasuki ruas jalan yang sama pada waktu yang lebih akhir [5].

## III. DASAR TEORI

## A. Graf dan Pemodelan Jaringan Jalan Raya

Jaringan transportasi darat pada wilayah perkotaan secara melambangkan himpunan simpul berbobot yang disimbolkan dengan matematis direpresentasikan sebagai graf berarah dan (nodes G = (V, E). atau vertices) Komponen yang 𝑉 busur koordinat geodetik. Komponen merepresentasikan titik persimpangan fisik jalan raya atau (edges atau arcs) berarah yang merepresentasikan ruas 𝐸 melambangkan himpunan jalan penghubung antar-persimpangan, di mana ruas jalan tersebut memiliki orientasi satu arah atau dua arah.

(𝑢, 𝑣) ∈ 𝐸

Pada pemodelan sistem statis konvensional, setiap busur

tetangga 𝑣 diasosiasikan dengan sebuah bobot skalar konstan

𝐿(𝑢,𝑣) ∈ ℝ+

jalan dalam satuan meter. Namun, untuk menangani skenario spasio-temporal akibat dinamika bencana alam, representasi busur diperluas dengan menyuntikkan fungsi biaya dinamis berbasis dimensi waktu perjalanan [5].

Dalam kondisi kebencanaan akibat banjir rob, kelayakan suatu ruas jalan dipengaruhi langsung oleh ketinggian

v genangan air di atas permukaan aspal. Ketinggian air simpul

pada waktu t, yang disimbolkan dengan 𝐾𝑒𝑑𝑎𝑙𝑎𝑚𝑎𝑛(𝑣, 𝑡),

ditentukan oleh fluktuasi pasang surut sinusoidal [1], [6]. Untuk memetakan dampak fisik genangan tersebut ke dalam

𝐿(𝑢,𝑣)

menyatakan panjang busur

(u,v), d(v,t)

v pada

𝑤(d)

merupakan fungsi penalti genangan.

𝑡arrive ) dihitung

yang menghubungkan simpul asal

𝑢 ke simpul

yang mencerminkan panjang geometris asli ruas

𝑡curr + 𝐿(𝑢,𝑣)×𝑤(𝑑(𝑣,𝑡curr)) 𝑉normal

## B. Fungsi Penalti Hambatan Banjir dan Degradasi Kecepatan (𝑤 )

𝑉aktual(𝑑) adalah


usulan Custom TD-A* diperbarui secara adaptif menggunakan formulasi berikut:

## D. Algoritma A* Standar

Algoritma A* merupakan metode pencarian berbasis heuristik menguntungkan yang digunakan untuk menemukan rute terpendek pada graf spasial dengan meminimalkan total perkiraan biaya evakuasi [4]. Algoritma ini mengevaluasi setiap simpul n menggunakan fungsi evaluasi matematis

baku:

Di mana g(n) adalah biaya aktual yang dikeluarkan dari simpul awal menuju simpul saat ini n. Sementara h(n) adalah nilai fungsi heuristik perkiraan biaya tersisa dari simpul n menuju simpul tujuan. Agar algoritma A* dijamin mampu menghasilkan solusi rute yang optimal mutlak (admissible), fungsi heuristik h(n) tidak boleh memberikan estimasi yang berlebihan terhadap jarak asli tersisa [4]. Dalam penelitian ini, fungsi h(n) dihitung menggunakan jarak garis lurus (Euclidean distance) dari koordinat simpul n langsung menuju koordinat titik aman posko pengungsian:

Kelemahan utama dari A* Standar adalah dalam konteks ini adalah sifatnya yang buta lingkungan, karena fungsi g(n) hanya mengakumulasikan jarak fisik statis 𝐿(𝑢,𝑣) tanpa mampu mengasimilasi perubahan parameter waktu bencana (t) [5].

di mana fungsi akumulasi biaya perjalanan aktual (g) diperbarui secara adaptif mengikuti estimasi waktu ketibaan menit demi menit dengan melibatkan fungsi penalti w:

Melalui formulasi kustomisasi ini, fungsi evaluasi f(n) bertindak sebagai filter cerdas spasio-temporal. Ketika suatu koridor jalan lokal mulai terendam air pasang seiring bertambahnya durasi simulasi (t), nilai fungsi penalti w pada simpul tersebut akan melonjak secara otomatis. Kondisi ini secara instan mendongkrak nilai f(n) menjadi sangat tinggi atau tak berhingga, sehingga memotivasi mesin algoritma untuk memindahkan prioritas antrean pencarian keluar dari area genangan bahaya [5], [8]. Hasil akhirnya adalah pembentukan rute evakuasi yang secara dinamis meliuk menjauhi rob sebelum bencana pasang mencapai titik puncaknya.

## IV. METODOLOGI

## E. Algoritma Branch and Bound

Algoritma Branch and Bound (B&B) merupakan metode optimasi kombinatorial berbasis penelusuran pohon status (state-space tree) secara sistematis untuk menemukan solusi optimal eksak [3]. Algoritma ini bekerja dengan memecah permasalahan besar menjadi sub-problem melalui mekanisme pencabangan (branching), yang dikombinasikan dengan mekanisme pemangkasan kaku (pruning) untuk mengeliminasi cabang pohon yang tidak menjanjikan solusi terbaik [3].

Dalam konteks penataan rute evakuasi, B&B melacak semua kemungkinan kombinasi jalur persimpangan jalan secara mendalam. Sebuah cabang penelusuran jalan akan dipangkas secara permanen jika memenuhi salah satu dari dua kondisi batasan kaku berikut: (1) nilai akumulasi biaya sementara pada jalur tersebut telah melebihi nilai batas atas (upper bound) dari rute terbaik yang sudah ditemukan sebelumnya oleh sistem; (2) jalur tersebut melanggar batasan fisik lingkungan, yakni ketika mengevaluasi simpul yang memiliki nilai kedalaman air di atas ambang toleransi mesin mobil (d > 0.40 m) [3], [6].

Meskipun menjamin akurasi solusi eksak, B&B memiliki kelemahan inheren berupa pertumbuhan eksponensial pada kompleksitas ruang pencarian simpul dan konsumsi memori ketika dipaksa beroperasi pada graf berskala makro [3].

## F. Algoritma Time-Dependent A*

Algoritma Custom TD-A* merupakan modifikasi tingkat lanjut dari arsitektur A* standar yang dirancang khusus untuk menangani graf dinamis yang berubah terhadap sumbu waktu [5]. Perbedaan fundamental terletak pada mekanisme ekspansi simpul pada daftar terbuka. Fungsi evaluasi untuk algoritma

*Fig. 1. Kerangka Penelitian*


## A. Dataset

Dataset utama yang digunakan dalam penelitian ini mengintegrasikan data graf jaringan jalan raya, data elevasi digital, dan data temporal pasang surut air laut untuk merekonstruksi simulasi evakuasi mandiri kendaraan roda empat secara dinamis. Jaringan jalan raya diperoleh dari pustaka OSMnx dengan membatasi ruang lingkup pada tiga kecamatan kritis di Kota Semarang, yaitu Semarang Utara, Semarang Timur, dan Gayamsari, yang dikunci pada tipe network_type='drive' agar murni mengevaluasi jalur yang dapat dilalui mobil. Informasi elevasi tanah pada simpul graf diintegrasikan dengan data raster DEM Nasional (DEMNAS) dari portal resmi Ina-Geoportal Badan Informasi Geospasial (BIG) yang memiliki resolusi spasial 0.27-arcsecond di mana proses sampling dibatasi pada grid koordinat 110.25∘E hingga 110.5∘E Batas Bujur dan −7.0∘S hingga −6.75∘S Batas Lintang.

*Fig. 2. Komponen Pemodelan Spasio-Temporal Kebencanaan Wilayah Pesisir Kota Semarang: (a) Topologi graf berarah berbobot; (b) File model elevasi digital; (c) Peta sebaran spasial nilai ketinggian tanah persimpangan hasil operasi spatial point-sampling join; (d) Simulasi spasial penetrasi sebaran kedalaman genangan banjir rob saat mencapai grafik air pasang*

*tertinggi*

Seluruh dataset ini ditransformasikan ke dalam sampel pembelajaran graf terarah yang saling bertetangga menggunakan operasi spatial point-sampling join, di mana koordinat geodetik dari setiap simpul graf diekstraksi untuk mengambil nilai piksel ketinggian tanah yang bersinggungan langsung pada raster DEMNAS. Parameter dinamika temporal banjir rob bersumber dari data prakiraan cuaca maritim resmi BMKG (maritim.bmkg.go.id) berupa estimasi ketinggian muka air laut berkala (kolom Estimated Tide / EST) pada tanggal 7 Juni 2026 yang disusun ke dalam deret waktu diskret per interval 10 menit. Nilai pasang surut BMKG tersebut kemudian dikurangi dengan elevasi DEMNAS hasil operasi spatial join secara sekuensial berdasarkan estimasi waktu ketibaan agen untuk menghitung fungsi penalti hambatan fisik w Simulasi penataan rute ini dievaluasi dari titik asal acak bersyarat di wilayah Semarang Utara dengan kriteria tanah rendah (< 1.0 m) menuju target shelter tunggal Posko Balai Desa Rejomulyo di koordinat (110.4349, -

6.9643) [2]. Hasil penggabungan dataset ini menghasilkan 4412 simpul dan 11933 busur (edges)

## B. Desain Skenario

Penelitian ini menerapkan desain eksperimen komputasional berbasis pergerakan agen kendaraan, di mana skenario pengujian difokuskan secara spesifik untuk karakteristik pergerakan kendaraan mobil konvensional. Parameter fisik yang mengunci karakteristik agen mobil dalam simulasi ini meliputi batas kecepatan mengemudi normal di dalam koridor perkotaan (𝑉normal) sebesar 8.33 m/s atau setara dengan ≈ 30 km/jam [10]. Batas ketahanan mekanis kendaraan terhadap media air ditetapkan pada ambang batas ketinggian genangan ℎthreshold = 0.40 meter, di mana jika air di atas permukaan jalan melampaui angka tersebut, kendaraan dinyatakan mengalami lumpuh total akibat risiko kemasukan air pada komponen elektrikal bawah mesin dan pipa knalpot (water hammer) [6]. Mekanisme simulasi diinisialisasi dengan menempatkan agen pada titik asal keberangkatan (source node) yang dipilih menggunakan penarikan sampel acak terikat (constrained random sampling) di dalam wilayah Semarang Utara dengan kriteria elevasi tanah rendah (< 1.0 meter). Agen kendaraan kemudian disimulasikan bergerak mulai pada menit ke-60 (t=60), bertepatan dengan fase naiknya grafik air pasang rob harian tanggal 7 Juni 2026 dari data BMKG Maritim, dengan rute yang diarahkan menuju target shelter tunggal Posko Balai Desa Rejomulyo [2].

## C. Metrik Evaluasi

Evaluasi algoritma menggunakan 6 metrik evaluasi untuk mengukur performa, efisiensi, serta tingkat keselamatan rute yang dihasilkan oleh masing masing algoritma. Metrik yang digunakan adalah sebagai berikut:

- Latensi Waktu Eksekusi (Running Time Latency) yang diukur dalam satuan milidetik (ms). Metrik ini mengevaluasi kecepatan respon komputasi sistem dalam merumuskan rute evakuasi dari titik asal ke titik tujuan.

- Kerapatan Simpul Terekspansi (Explored Nodes Density) yang dibuka dan dievaluasi di dalam memori kerja selama proses pencarian lintasan berlangsung. Metrik ini merepresentasikan efisiensi ruang jelajah dari masing-masing arsitektur algoritma.

- Kapasitas Memori Puncak (Peak Memory Bound) dalam satuan Kilobyte (KB). Metrik ini merekam batas konsumsi RAM tertinggi yang dibutuhkan oleh struktur data internal algoritma saat melakukan ekspansi simpul graf.

- Panjang Lintasan Fisik (Path Length) yaitu akumulasi total dari panjang geometris nyata dari segmen-segmen jalan yang membentuk rute evakuasi final, dihitung dalam satuan kilometer (km).

- Skor Paparan Banjir (Flood Exposure Mean) yaitu nilai rata-rata akumulatif dari ketinggian genangan air banjir rob (meter) yang menyentuh bodi kendaraan di sepanjang simpul jalan yang dilewati, dihitung secara dinamis paralel terhadap pergerakan sumbu waktu perjalanan agen.


- Rasio Keberhasilan Evakuasi (Success Rate) yaitu nilai evaluasi biner untuk menentukan validitas keselamatan fisik rute. Agen dinyatakan sukses (100%) jika berhasil mencapai Posko tanpa pernah sekalipun melewati simpul jalan dengan kedalaman air yang melanggar batas kritis fisik knalpot mobil (> 0.40 m), dan dinyatakan gagal (0\%) jika kendaraan mogok/tenggelam di tengah jalan.

## V. HASIL DAN PEMBAHASAN

## A. Analisis Metrik Efisiensi Komputasi

Fase pertama pengujian difokuskan pada audit metrik performa internal kode untuk mengevaluasi efisiensi penggunaan sumber daya komputasi serta luas ruang eksplorasi graf oleh masing-masing arsitektur algoritma. Evaluasi ini dihitung secara objektif melalui tiga parameter utama yaitu latensi waktu eksekusi, jumlah simpul terekspansi, dan konsumsi memori RAM puncak (peak memory). Berdasarkan hasil pengujian empiris satu agen mobil yang dikunci dari titik asal darurat acak di Semarang Utara menuju target shelter tunggal Posko Balai Desa Rejomulyo, ringkasan data numerik internal kode disajikan pada Tabel I.

*TABLE I.*

*RINGKASAN METRIK PERFORMA KOMPARATIF SUMBER DAYA KOMPUTASI INTERNAL KODE*

| Algoritma | Running Time | Explored Nodes | Peak Memory (Max) |
| --- | --- | --- | --- |
| Standard A* | 31.61 ms | 576 nodes | 307.79 KB |
| Branch and Bound | 68631.04 ms | 219530 nodes | 363.02 KB |
| Custom TD-A* 174.52 ms |   | 559 nodes | 306.26 KB |

Berdasarkan data pada Tabel I, A* Standar mencatatkan latensi eksekusi yang sangat cepat yaitu hanya 31.61 ms dengan konsumsi memori RAM dasar sebesar 307.79 KB dan mengeksplorasi 576 simpul. Karakteristik akselerasi ini terjadi karena struktur kode A* Standar bekerja secara statis; ia hanya mengalkulasi bobot jarak geometris murni satu kali lurus ke depan tanpa melakukan komputasi perhitungan temporal berulang terhadap data pasang surut air laut harian. Namun, minimnya ruang pencarian ini tidak memiliki kontribusi fungsional terhadap mitigasi bencana karena mengabaikan rintangan banjir rob di lapangan.

Sebaliknya, algoritma B&B sebagai metode optimasi eksak murni mengalami degradasi performa internal kode yang sangat signifikan akibat fenomena ledakan kombinatorial. Menggunakan strategi penelusuran mendalam (Depth-First Search) tanpa bimbingan fungsi heuristik arah sasaran, kode B&B terpaksa membuka dan mengevaluasi hingga 219.530 simpul unik demi membuktikan validitas nilai batas atas secara mutlak. Akibat dari masifnya pencabangan status tersebut, latensi waktu eksekusi kode membengkak drastis mencapai 68.631,04 ms (setara dengan ≈1.14 menit) serta menarik kapasitas memori RAM puncak tertinggi sebesar 363.02 KB untuk menampung tumpukan status (memory stack) graf transportasi tiga kecamatan.

Keunggulan arsitektur usulan diperlihatkan secara nyata melalui efisiensi algoritma Custom TD-A*. Melalui perpaduan fungsi penalti dinamis ke dalam komponen biaya

perjalanan aktual (g), algoritma proposal ini mampu memotong ruang pencarian simpul secara ekstrem menjadi hanya 559 simpul, bahkan lebih sedikit daripada jumlah simpul yang dieksplorasi oleh A* Standar. Pemangkasan ruang pohon keputusan yang sangat ketat ini berhasil mengunci latensi waktu eksekusi pada angka yang sangat instan, yaitu 174.52 ms, dengan alokasi RAM puncak paling ringan sebesar 306.26 KB. Hasil empiris ini membuktikan bahwa bimbingan fungsi heuristik admissible h(n) sukses mengeliminasi ratusan ribu cabang buntu pada graf transportasi dependen-waktu secara instan.

## B. Analisis Metrik Keberhasilan Kasus Mitigasi Bencana

Fase kedua evaluasi dilakukan untuk menguji efektivitas fisik dari rute yang dihasilkan dalam memitigasi risiko keselamatan armada evakuasi berdasarkan data pasang surut riil BMKG Maritim tanggal 7 Juni 2026. Data deskriptif geografis simulasi diinisialisasi pada titik asal kritis wilayah Semarang Utara dengan elevasi tanah ekstrem rendah, yaitu hanya 0.64 meter di atas permukaan laut (Latitude -6.957556, Longitude 110.413543). Target penyelamatan dikunci pada Posko Balai Desa Rejomulyo di wilayah Semarang Timur dengan elevasi aman sebesar 2.41 meter di atas permukaan laut (Latitude -6.964804, Longitude 110.434811). Ringkasan metrik keselamatan fisik kasus evakuasi lapangan disajikan pada Tabel II.

*TABLE II. RINGKASAN METRIK EVALUASI KESELAMATAN FISIK KASUS EVAKUASI LAPANGAN TERHADAP RISIKO GENANGAN BANJIR ROB*

*PESISIR SEMARANG.*

| Algoritma | Path Length | Flood Exposure | Success Rate |
| --- | --- | --- | --- |
| Standard A* | 3.17 km | 2.1209 m | 0.00% |
| Branch and Bound | 5.88 km | 0.4781 m | 100.00% |
| Custom TD-A* 5.94 km |   | 0.0830 m | 100.00% |

Data pada Tabel II memperlihatkan kegagalan fisik yang sangat fatal pada rute rekomendasi A* Standar. Algoritma tersebut merekomendasikan lintasan terpendek secara geografis sejauh 3.17 km. Namun, ketiadaan parameter peka- waktu kebencanaan membuat rute tersebut mengarahkan mobil langsung menembus jantung genangan rob terdalam di pesisir Semarang, sehingga memaparkan kendaraan pada skor rata-rata paparan banjir yang sangat tinggi sebesar 2.1209 meter. Ketinggian air ini secara mekanis menenggelamkan bodi mobil melampaui batas knalpot (0.40 m), memicu kerusakan dan menjatuhkan nilai Success Rate ke angka mutlak 0.00%.

Komparasi yang sangat kontras ditunjukkan oleh kedua algoritma dependen-waktu. B&B dan Custom TD-A* sukses mencatatkan Success Rate 100.00% dengan menolak jalur terpendek dan mengalihkan trajektori memutar ke arah selatan melintasi koridor jalan yang lebih tinggi. Custom TD- A* menghasilkan lintasan sepanjang 5.94 km, sedikit lebih panjang dibandingkan lintasan B&B (5.88 km), namun berhasil menekan skor Flood Exposure hingga ke titik terendah, yaitu hanya 0.0830 meter (sekitar 8.3 cm), jauh lebih aman dibanding rute B&B yang masih menyentuh angka 0.4781 meter.


*Fig. 3. Matriks Spasial Integrasi Trajektori Lintasan Evakuasi Akhir dan Densitas Sebaran Ruang Jelajah Simpul Terbuka pada Jaringan Jalan 3 Kecamatan*

*Pesisir Kota Semarang:*

(a) Rute fisik statis rekomendasi A* yang memotong zona genangan banjir;

(b) Kerapatan ruang pencarian minimum dari A*;

(c) Rute fisik memutar hasil optimasi eksak B&B;

(d) Ledakan kombinatorial ruang pencarian B&B yang memenuhi topologi graf;

(e) Rute adaptif dinamis hasil rancangan algoritma Custom TD-A* yang berhasil menyamai akurasi rute eksak;

(f) Efisiensi ruang jelajah simpul terbuka dari algoritma Custom TD-A*

## C. Analisis Lintasan

Berdasarkan pelacakan kronologi runtun waktu pada grafik Figure 4(a), terlihat profil kedalaman air banjir rob yang dihadapi oleh kendaraan per menit di sepanjang lintasan. A* menunjukkan tren kenaikan genangan air yang langsung melesat tajam menerobos batas kritis ketahanan mekanis mobil (0.40 meter) sejak menit-menit awal keberangkatan. Profil ini membuktikan secara ilmiah bahwa kendaraan dipastikan mengalami kelumpuhan total (mati mesin) di dalam genangan air sebelum mampu keluar dari perbatasan administratif kecamatan Semarang Utara.

Sebaliknya, grafik linier milik algoritma Custom TD-A* menampilkan profil pergerakan yang sangat aman dan stabil. Sepanjang sumbu durasi waktu perjalanan agen dari titik

awal, kurva ketinggian air rob secara konsisten bergerak landai mendekati angka nol dan bertahan jauh di bawah ambang batas bahaya 0.40 meter. Hal ini memvalidasi bahwa penambahan jarak tempuh sekitar 2.7 km ke arah timur secara spasial memberikan kompensasi proteksi fisik yang sempurna bagi keselamatan bodi kendaraan armada.

Mekanisme penghindaran banjir secara otomatis dikendalikan oleh fluktuasi nilai pengali fungsi penalti bobot (w) yang terekam pada grafik Figure 4(b). Ketika rute A* memaksa melintasi simpul-simpul jalan yang terendam parah, fungsi internal matriks langsung menetapkan nilai penalti bobot ke titik tak berhingga (∞), namun kondisi tersebut tidak dapat diantisipasi oleh mesin pencari yang menggunakan bobot statis.


Pada implementasi Custom TD-A*, kalkulasi fungsi penalti dilakukan secara dinamis dan sekuensial berdasarkan estimasi waktu ketibaan agen pada simpul tetangga. Begitu waktu simulasi bergerak menjauhi menit ke-60 dan kurva pasang air laut mulai meningkat sehingga menggenangi ruas- ruas jalan dengan elevasi rendah di wilayah Semarang Utara (sekitar 0,64 meter di atas datum referensi), nilai variabel penalti w pada simpul yang terdampak berubah dari bobot normal 1,0 menjadi penalti perlambatan 2,5, bahkan mencapai nilai tak berhingga ketika kedalaman genangan melampaui ambang batas yang dapat dilalui kendaraan. Kemunculan nilai tak berhingga tersebut secara langsung

meningkatkan nilai fungsi evaluasi total pada cabang jalan yang terdampak sehingga jalur tersebut menjadi sangat tidak menarik untuk dipilih selama proses pencarian.

Akibatnya, struktur antrean prioritas yang digunakan pada Open List secara otomatis mengurangi prioritas eksplorasi koridor jalan yang tergenang dan mengarahkan proses pencarian menuju ruas-ruas jalan alternatif yang masih kering dengan nilai penalti tetap 1,0. Mekanisme ini memungkinkan kendaraan menghindari area genangan secara proaktif dan mempertahankan jalur evakuasi yang aman menuju Posko P tanpa harus bergantung pada intervensi eksternal atau pembaruan rute secara manual.

*Fig. 4. Grafik Analisis Karakteristik Lintasan Spasio-Temporal Mobil:*

*(a) Komparasi runtun waktu kedalaman air banjir rob yang menghadang bodi kendaraan terhadap garis ambang batas kritis knalpot mobil (0.40 m);*

*(b) Fluktuasi nilai pengali fungsi penalti hambatan fisik (w) yang memengaruhi bobot dinamis ruas jalan sepanjang sumbu durasi simulasi evakuasi.*

i

## VI. KESIMPULAN DAN SARAN

## A. Kesimpulan

Berdasarkan hasil eksperimen komputasional dan analisis komparatif spasio-temporal yang telah dilakukan pada jaringan jalan tiga kecamatan pesisir Kota Semarang, dapat ditarik beberapa kesimpulan utama sebagai berikut:

- Algoritma usulan Custom TD-A* terbukti secara empiris mampu menyelesaikan permasalahan pencarian rute evakuasi dinamis dengan tingkat efisiensi internal kode yang tinggi. Algoritma ini berhasil memangkas ruang pencarian secara radikal menjadi hanya 559.0 simpul, menghasilkan latensi waktu eksekusi yang sangat instan sebesar 174.52 ms, dan menjaga konsumsi RAM puncak tetap ringan pada angka 306.26 KB.

- Dari dimensi keselamatan fisik mitigasi bencana, algoritma Custom TD-A* berhasil mencapai Success Rate 100.00% dengan mengunci lintasan memutar aman banjir sejauh 5.94 km dan menekan skor rata- rata paparan banjir (Flood Exposure) hingga ke titik terendah, yaitu hanya 0.0830 meter (8.3 cm). Karakteristik rute ini terbukti jauh lebih aman dari risiko mati mesin jika dibandingkan dengan algoritma kontrol eksak Branch and Bound yang masih menyentuh angka paparan 0.4781 m.

- Metode konvensional A* Standar mencatatkan kegagalan total dalam penanganan kasus kebencanaan dinamis (Success Rate = 0.00%). Meskipun kodenya mengeksplorasi graf secara cepat (31.61 ms), ketiadaan parameter peka-waktu membuat rute sepanjang 3.17 km tersebut nekat menerobos titik genangan terdalam Semarang Utara, sehingga memaparkan bodi mobil pada genangan air

kritis setinggi 2.1209 meter yang melumpuhkan kendaraan sejak menit awal keberangkatan.

- Metode eksak Branch and Bound berhasil menemukan rute yang aman dari rob (5.88 km, Success Rate = 100.00\%), namun performa internal kodenya lumpuh akibat fenomena ledakan kombinatorial. Ketiadaan fungsi heuristik arah sasaran memaksa kode B&B mengeksplorasi hingga 219.530.0 simpul unik yang mengakibatkan latensi membengkak drastis menjadi 68.631.04 ms (≈1.14 menit), sehingga tidak layak diimplementasikan untuk sistem navigasi darurat waktu nyata (real-time).

## B. Saran

Beberapa aspek dapat dieksplorasi guna menyempurnakan pengembangan dan perluasan implementasi sistem pemodelan rute evakuasi dinamis ini pada masa mendatang. Penelitian selanjutnya dapat mengeksplorasi scenario multi agen skala makro untuk menguji ketahanan performa algoritma ketika dihadapkan dengan ribuan pergerakan mobil secara parallel, sekaligus memetakan perilaku pergerakan massa darurat yang lebih realistis. Selain itu, integrasi dinamika kemacetan lalu lintas dapat menjadi variabel yang sangat berpengaruh untuk dieksplorasi. Hal ini dapat digunakan untuk memperkokoh system agar tidak hanya adaptif terhadap hambatan alam, tetapi juga mampu menghindari penundaan akibat kemacetan massal. Variasi agen juga dapat diterapkan untuk menguji apakah algoritma Custom TD-A* mampu diterapkan ke semua agen yang memiliki kecepatan pergerakan yang berbeda-beda.

## LAMPIRAN


Kode simulasi eksperimen mesin komputer dan visualisasi trajektori evakuasi kebencanaan pesisir Semarang dalam penelitian ini tersedia secara daring dalam repositori berikut https://github.com/muhffikkri/spatio-temporal-rob- evacuation-routing. Video Penjelasan makalah dapat diakses

pada link berikut https://youtu.be/5ID1cmRQ0YQ.

## REFERENCES

- [1] [1] BPBD Kota Semarang, Dokumen Kajian Risiko Bencana Kota Semarang Provinsi Jawa Tengah Tahun 2023 - 2027. Semarang, Indonesia: BPBD Kota Semarang, 2023.

- [2] [2] BPBD Kota Semarang, Dokumen Rencana Kontinjensi Banjir Kota Semarang 2024-2029. Semarang, Indonesia: BPBD Kota Semarang, 2024.

- [3] [3] D. R. Morrison, S. H. Jacobson, J. J. Sauppe, dan E. C. Sewell, "Branch-and-bound algorithms: A survey of recent advances in searching, branching, and pruning," Discrete Optimization, vol. 19, hal. 79–102, 2016.

- [4] [4] D. Foead, A. Ghifari, M. B. Kusuma, N. Hanafiah, dan E. Gunawan, "A Systematic Literature Review of A* Pathfinding," Procedia Computer Science, vol. 179, hal. 507–514, 2021.

- [5] [5] J. Jao, I. Hameed, M. Era, E. Vallar, dan Y. Liu, "FLOAT: Flood- Aware Trajectories for Modeling the Time-Dependent Evacuation Routing with Risk Consideration," dalam 2025 International Conference on Networking, Sensing and Control (ICNSC), 2025, hal. 267–273.

- [6] [6] S. Cao et al., "Dynamic evacuation route planning for urban residents in flood disasters," Simulation Modelling Practice and Theory, vol. 147, hal. 103250, 2026.

- [7] [7] J. Liang, M. Liu, Z. Zhang, dan L. Yang, "Shortest path planning and dynamic rescue forces dispatching for urban flood disasters," Scientific Reports, vol. 15, hal. 23643, 2025.

- [8] [8] H. Chebika, G. Shen, H. Han, M. Mabrouk, dan B. Nouibat, "Simulating optimal flood evacuation using heuristic algorithms and path-choice behaviors," Simulation Modelling Practice and Theory, vol. 144, hal. 103167, 2025.

- [9] [9] C. Daniel dan M. A. Romli, "Application of the A-Star Method for Evacuation Routes Using the Long-Range Wide Area Network

8

- (LoRaWAN)," J-INTECH (Journal of Information and Technology), vol. 13, no. 1, 2025.

- [10] [10] H. Nirwana, W. Firgiawan, S. Cokrowibowo, dan Z. Zainuddin, "An Intelligent Optimization Method for Evacuation Route Planning in the Occurrence of Natural Disasters," Engineering, Technology & Applied Science Research, vol. 14, no. 6, hal. 17696–17703, 2024.

## PERNYATAAN

Dengan ini saya menyatakan bahwa makalah yang saya susun merupakan hasil karya saya sendiri dan tidak merupakan saduran, terjemahan, maupun plagiasi dari karya orang lain. Seluruh sumber yang digunakan telah

dicantumkan secara benar sesuai dengan kaidah penulisan ilmiah.

Terkait penggunaan teknologi kecerdasan buatan (Artificial Intelligence), saya menyatakan bahwa: Saya menggunakan alat bantu AI sebagai pendukung dalam

- penyusunan makalah ini dengan rincian sebagai berikut:

- Nama alat AI: Gemini

- Tujuan penggunaan: Mengumpulkan ide, menyusun skenario penelitian yang optimal dan realistis, pengembangan visualisasi dan penyempurnaan struktur draf naskah.

- Ruang lingkup penggunaan: (1) Membantu penyusunan kode pemrograman untuk fungsionalitas visualisasi dan optimasi kode inti penelitian; (2) Membantu konversi dan penyelarasan kalimat naratif dan eksplorasi ide alur narasi naskah; (3) Membantu memastikan kerangka penelitian sudah terstruktur sebelum memulai penelitian.

Penggunaan AI, apabila ada, hanya bersifat sebagai alat bantu dan tidak menggantikan peran saya sebagai penulis utama. Seluruh isi, analisis, serta kesimpulan dalam makalah ini tetap merupakan tanggung jawab saya

sepenuhnya

Semarang, 07 Juni 2026

Muhammad Fikri

24060124130069
