# NodeJS Tingkat Pemula Part I
Pemateri: Raka Ardhi
Sumber: Course Kode.id (NodeJS Tingkat Pemula)
Tanggal: 16 Agustus 2023
## Kegiatan
- Melihat video materi pada course NodeJS Tingkat Pemula
- Membuat summary dari video yang ditonton
- Sudah selesai menonton 13 video yang membahas dasar penggunaan javascript dan sedikit tentang http server
## Masalah
- Ada sedikit distraksi dari teman sehingga hari ini belum bisa menyelesaikan seluruh video dari course
## Hasil
- === Hello World ===
- NodeJS adalah bahasa yang single thread namun asynchronous. Oleh karena itu maka NodeJS tidak perlu membuat thread baru setiap ada request baru, namun tetap bisa berjalan secara non-blocking sehingga NodeJS bisa jadi relatif lebih cepat daripada bahasa lain karena tidak perlu membuat thread baru setiap kali ada event atau request
- NodeJS adalah js runtime non-blocking IO
- Command 'node' untuk menjalankan REPL nodejs dan 'node -v' untuk melihat versi nodejs
- Variabel bisa dideklarasikan dengan 'var' dan 'let'
- Untuk membuat fungsi kita bisa menggunakan keyword 'function' lalu diikuti nama fungsi dan parameter untuk fungsi yang diapit dengan kurung. Lalu untuk bodynya menggunakan kurung kurawal setelah menuliskan kurung milik parameter dan diisi dengan body fungsi
- Untuk memanggil fungsi sama dengan bahasa lain pada umumnya
- Command '.exit' untuk keluar dari REPL
- Command 'node <nama-file.js>' untuk menjalankan file js
- === Module ===
- 'built in module' sudah terinstall saat kita menginstall nodejs; 'user defined module' adalah module yang kita buat sendiri; 'third party module' adalah module yang bisa didownload menggunakan 'npm'
- Untuk menambahkan module ke kode kita bisa menggunakan keyword 'require(\<nama-module\>)'
- Untuk membuat module, kita harus melakukan export agar operasi yang kita inginkan bisa dipakai di luar module. (misal: 'exports.add=function (a,b){return a+b}')
- Untuk memanggil operasi yang ada di dalam module, kita bisa mengaksesnya setelah melakukan require()
- Jika kita menyimpan hasil require ke dalam variabel, maka untuk mengaksesnya kita harus memanggil dari variabel tersebut. (misal: var a = require(modul); a.operasi())
- === Event ===
- Event dapat digunakan sebagai metode asynchronous di nodejs
- Sebuah listener akan dipersiapkan terlebih dahulu dengan event tertentu. Jadi jika event tersebut diemmit, maka listener tersebut akan terpanggil secara asynchronous
- Untuk membuat listener kita menggunakan method on() dan menentukan nama event dan fungsi yang akan dijalankan ketika event tersebut diemmit. Misal '.on('nama-event', function(param){})'
- Untuk mentrigger event kita menggunakan method emmit() dengan argumen nama event dan parameter dari event tersebut jika perlu. Misal '.emmit('nama-event', params)'
- === Buffer ===
- Buffer digunakan untuk handle binary data pada js. Diletakkan di RAM
- Untuk membuat buffer menggunakan Buffer.allocUnsafe(\<panjang-buffer\>)
- Untuk menulis kita bisa menggunakan method write() dan akan mereturn banyaknya byte yang berhasil ditulis. Kita juga bisa menggunakan metode array biasa untuk assign byte kedalam buffer
- Untuk membaca buffer sebagai string kita bisa menggunakan method toString(). Sedangkan jika ingin membaca sebagai int atau nilai raw nya, kita bisa mengakses seperti mengakses array
- Streams adalah sequence data yang dipindah. jadi nanti data akan dipecah jadi kecil dan dipindah 1 per 1
- === Stream ===
- Stream bisa ditulis dan dibaca
- Untuk membaca kita perlu membuat reader stream dan listen di event 'data' dimana kita akan mendapat parameter chunk yang akan berisi potongan data dari stream yang kita baca. Lalu listen di event 'end' untuk cek apakah kita sudah diakhir stream
- Untuk menulis kita perlu membuat writer stream lalu memanggil method write() untuk menuliskan data yang ingin kita input ke stream lalu kita panggil method end() untuk memberi info kalau proses write sudah selesai. Setelah itu kita bisa listen event 'finish' untuk memeriksa apakah proses writing sudah selesai
- Pipe dapat digunakan untuk pass data dari sebuah reader stream secara langsung. Misal jika kita membaca sebuah stream dan ingin menulis ke stream yang lain berdasarkan data dari stream yang kita baca, maka kita bisa menggunakan pipe dari reader stream ke writer stream.
- Kita juga bisa melakukan operasi pipe secara berantai (chain pipe). Misal sebelum kita write ke stream kita bisa melakukan operasi terlebih dahulu pada data yang dibaca sehingga data yang di write ke stream nanti sudah terproses.
- Untuk cek error kita bisa listen dari event 'error' yang akan memberi parameter error message
- === Reading File ===
- Untuk read file kita bisa menggunakan module fs dan memanggil method readFile() untuk async dan readFileSync() untuk sync
- Pada read file async, kita perlu pass path dari file yang ingin dibaca, data option, dan callback dengan parameter error dan data. Perlu digaris bawahi kalau data yang didapatkan berbentuk buffer sehingga jika kita ingin membaca sebagai string, kita bisa konversi dulu atau bisa dengan menambahkan opsi encoding di data option
- Pada read file sync, parameter yang diperlukan mirip dengan async tapi tanpa callback dan data akan direturn sehingga kita harus menyiapkan variabel untuk menampung.
- === Watching File ===
- Watch file digunakan untuk memonitor event yang terjadi pada sebuah file atau folder. untuk menggunakannya kita hanya perlu membuat variabel dengan method fs.Watch lalu lakukan monitor pada event 'change' dengan parameter event type dan nama file yang terjadi perubahan.
- === Writing File ===
- Write file mirip dengan read file. Keduanya sama-sama memiliki method yang sync dan async dengan method writeFileSync() dan writeFile().
- Untuk menulis secara async, kita harus pass path ke file yang ingin ditulis, data yang ingin ditulis, dan callback ketika terjadi error
- Untuk menulis secara sync, kita tidak perlu menambahkan callback dan tidak akan mereturn apa-apa. Oleh karena itu untuk handle error kita bisa menggunakan try catch.
- Untuk menulis dalam bentuk binary, kita bisa mengirimkan data dalam bentuk buffer
- === Simple HTTP Server ===
- Import http module, Lalu buat http server dengan createServer() dengan parameter fungsi listener yang memiliki parameter request dan response. Lalu kita panggil method listen() dengan parameter port dari http server yang kita inginkan.
- Untuk mempersiapkan response header kita bisa melakukan writeHead() dan response body dengan write() pada stream response
- Setelah kita run, maka kita bisa mengakses http server kita dengan localhost:port
- === Express (Routing, Middleware, dan Porting) ===
- Mulai menggunakan express. Untuk install express kita bisa mengunakan 'npm install express' dan setelah install maka akan muncul folder node_modules yang akan menampung semau third party module yang kita install
- Kita juga butuh body-parser untuk menghandle request body kita agar bisa dibaca sebagai JSON, cookie-parser untuk menghandle cookie, dan multer untuk menghandle form request
- Untuk membuat server kita perlu menginisialisasi app express terlebih dahulu. Lalu kita membuat satu route dengan memanggil method yang kita inginkan (.get, .post, dll) lalu kita simpan endpoint route nya dan listener dari route tersebut dengan parameter req dan res. Pada listener kita bisa kirim response dengan menggunakan parameter res dan membaca request dengan parameter req.
- Lalu kita lakukan listen pada port yang kita inginkan untuk menjalankan server
## Tambahan
Hari ini cukup menyenangkan karena saya sudah mulai praktik koding walaupun mulai dari dasar
## Lampiran
- [Github](https://github.com/punkestu/code-archive-mbkm-mbkm/tree/main/160823-get-started)