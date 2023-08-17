# NodeJS Tingkat Pemula Part II
Pemateri: Raka Ardhi
Sumber: Course Kode.id (NodeJS Tingkat Pemula)
Tanggal: 17 Agustus 2023
## Kegiatan
- Melanjutkan video materi pada course NodeJS Tingkat Pemula
- Membuat summary dari video yang ditonton
- Menyelesaikan video pembelajaran di course ini
- Membuat aplikasi untuk menampilkan cuaca pada sebuah kota
## Masalah
Tidak ada masalah hari ini. Saya berhasil menyelesaikan seluruh video dalam course tanpa hambatan.
## Hasil
- === Express (Routing, Middleware, dan Porting) ===
- Middleware digunakan untuk menjalankan operasi sebelum dan sesudah menjalankan listener utama
- Middleware dapat digunakan untuk memodifikasi request atau response dan menjalankan operasi tertentu sebelum mengirim response ke client
- Kita menggunakan method use() dengan parameter route name dan listener yang mirip dengan listener biasa bedanya kita menambahkan parameter next yang nantinya dipanggil sebagai fungsi untuk melanjutkan ke listener berikutnya
- Jika kita membuat lebih dari 1 middleware, maka akan dijalankan urut dari atas ke bawah
- Kalau menggunakan GET maka data yg dikirim akan muncul dan terlihat di url
- Kita bisa menggunakan module body-parser untuk memparse data yang dikirimkan dengan POST
- === The Simple Knot ===
- EJS untuk templating engine sehingga bisa membuat html menjadi dinamis karena bisa berinteraksi dengan variabel
- Untuk memasang EJS kita bisa gunakan method set() pada app dengan parameter 'view engine' dan 'ejs'
- EJS otomatis akses folder views
- Untuk expose folder (misal untuk akses file css) maka kita bisa gunakan middleware express.static('\<nama-folder\>'). Dengan begitu maka semua file yang ada di folder tersebut dapat diakses dari web server kita
- Untuk memanggil api lain, kita bisa menggunakan module request. untuk request kita bisa langsung panggil fungsi request setelah diimport dengan parameter api url dan callback untuk hasil requestnya.
- Bracket EJS adalah \<\% \%\>.
- Untuk output data dapat menggunakan \<\%= nama-variabel\%\>
## Tambahan
Hari ini tidak terlalu berbeda dari kemarin. Namun tetap terasa menyenangkan karena hari ini saya mulai membuat sebuah aplikasi yang dapat berjalan dengan baik.
## Lampiran
- [Github](https://github.com/punkestu/code-archive-mbkm/tree/main/170823-jump-to-web)
- [Weather App Project](https://github.com/punkestu/weather-app)