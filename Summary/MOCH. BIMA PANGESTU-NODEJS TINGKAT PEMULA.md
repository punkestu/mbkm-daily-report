# Moch. Bima Pangestu
## Program: Node JS For Back End Web Developer

### Pengertian
NodeJS adalah runtime javascript non-blocking IO. Nodejs berjalan secara single thread namun bisa asynchronous. Oleh karena itu NodeJS tidak perlu membuat thread baru setiap ada request baru, namun tetap bisa berjalan secara non-blocking sehingga menjadi relatif lebih cepat daripada bahasa lain.
### Hello NodeJS
- Kita bisa menggunakan command 'node' untuk menjalankan REPL dan perintah-perintah pada NodeJS. Gunakan command '.exit' untuk keluar dari REPL
- Jika ingin menjalankan file javascript gunakan command 'node <nama-file.js>'
- Variabel bisa dideklarasikan dengan 'var' dan 'let' serta 'const' untuk mendifinisikan konstanta.
- Untuk membuat fungsi kita bisa menggunakan keyword 'function' lalu diikuti nama fungsi dan parameter untuk fungsi yang diapit dengan kurung. Lalu untuk bodynya menggunakan kurung kurawal setelah menuliskan kurung milik parameter dan diisi dengan body fungsi. Contoh :
```
function nama_fungsi(parameter1, parameter2) {
	// operasi
}
```
- Untuk memanggil fungsi sama dengan bahasa lain pada umumnya dengan menulis nama fungsi dan diikuti argumennya jika perlu. Contoh :
```
nama_fungsi(argumen1, argumen2);
```
### Modules
- Ada 3 macam module 1.) 'built in module' sudah terinstall saat kita menginstall nodejs, 2.) 'user defined module' adalah module yang kita buat sendiri, dan 3.) 'third party module' adalah module yang bisa didownload menggunakan 'npm'.
- Untuk mengimport module ke kode kita bisa menggunakan `require(\<nama-module\>)`. Contoh:
```
require("nama-module");
```
- Untuk membuat module, kita harus melakukan export agar operasi yang kita inginkan bisa dipakai di luar module. Contoh: 
```
exports.add = function (a,b) {
	return a+b
}
```
- Kita hanya bisa mengakses operasi yang ada di dalam module setelah melakukan import
- Jika kita menyimpan hasil require ke dalam variabel, maka untuk mengaksesnya kita harus memanggil dari variabel tersebut. Contoh: 
```
const modul = require("nama-module");
modul.operasi();
```
### Events
- Event dapat digunakan sebagai implementasi asynchronous di javascript dimana sebuah listener akan dipersiapkan dengan event tertentu. Lalu jika event tersebut diemmit, maka listener tersebut akan terpanggil secara asynchronous. 
- Untuk membuat listener kita menggunakan method on() dengan argumen nama event dan fungsi yang akan dijalankan.
- Untuk mentrigger event kita menggunakan method emmit() dengan argumen nama event dan parameter dari event tersebut jika perlu.
- Contoh:
```
event.on("event1", function(parameter1) {
	// operasi
});
event.emmit("event1", arg1); // memanggil listener event1 dengan parameter arg1
```
### Buffers
- Buffer digunakan untuk menghandle binary atau raw data pada javascript.
- Untuk membuat buffer menggunakan Buffer.allocUnsafe(\<panjang-buffer\>). Contoh:
```
const buff1 = Buffer.allocUnsafe(100);
```
- Untuk menulis kita bisa menggunakan method write() yang akan mereturn banyaknya byte yang berhasil ditulis. Kita juga bisa menggunakan metode array biasa untuk assign byte kedalam buffer. Contoh:
```
buff1.write("hello nodejs");
// atau bisa akses per elemen
buff1[0] = 'h';
buff1[1] = 'e';
// ...dst
```
- Untuk membaca buffer sebagai string kita bisa menggunakan method toString(). Sedangkan jika ingin membaca sebagai int atau nilai raw nya, kita bisa mengakses seperti mengakses array. Contoh:
```
console.log(buff1.toString());
```
### Streams
- Stream adalah sequence dari data yang dipindah dimana nantinya data akan dipecah menjadi bagian kecil dan ditransfer satu per satu.
- Stream bisa ditulis dan dibaca. Untuk membaca kita perlu membuat reader stream dan listen pada event 'data' dimana kita akan mendapat parameter chunk yang akan berisi potongan data dari stream yang kita baca. Lalu listen di event 'end' untuk cek apakah kita sudah diakhir stream. Contoh:
```
const reader = fs.createReadStream("sumber data");
reader.on("data", function (chunk) {
	data += chunk;
});
reader.on("end", function () {
	// operasi
});
```
- Untuk menulis kita perlu membuat writer stream lalu memanggil method write() untuk menuliskan data yang ingin kita input ke stream lalu kita panggil method end() untuk mentrigger event 'end'. Setelah itu kita bisa listen event 'finish' untuk memeriksa apakah proses writing sudah selesai. Contoh:
```
const writer = fs.createWriteStream("tujuan");
writer.write("hello nodejs", "utf8");
writer.end();
writer.on("finish", function () {
	// operasi
});
```
- Pipe dapat digunakan untuk pass data dari sebuah reader stream ke stream lain secara langsung. Misal jika kita membaca sebuah stream dan ingin menulis ke stream yang lain berdasarkan data dari stream yang kita baca, maka kita bisa menggunakan pipe dari reader stream ke writer stream. Kita juga bisa melakukan operasi pipe secara berantai (chain pipe). Misal sebelum kita write ke stream kita bisa melakukan operasi terlebih dahulu pada data yang dibaca sehingga data yang di write ke stream nanti sudah terproses. Contoh:
```
const chainReader = fs.createReadStream("sumber");
const chainOps = operation();
chainReader.pipe(chainOps).pipe(fs.createWriteStream("tujuan"));
```
- Untuk cek error kita bisa listen dari event 'error' yang akan mengirim parameter error message. Contoh:
```
streamer.on("error", function (err) {
	// operasi
});
```
### File Handle
#### Read file
- Untuk read file kita bisa menggunakan module fs dan memanggil method readFile() untuk async dan readFileSync() untuk sync. Pada read file async, kita perlu pass path dari file yang ingin dibaca, data option, dan callback dengan parameter error dan data. Pada read file sync, parameter yang diperlukan mirip dengan async tapi tanpa callback dan data akan direturn sehingga kita harus menyiapkan variabel untuk menampung. Perlu digaris bawahi kalau data yang didapatkan berbentuk buffer sehingga jika kita ingin membaca sebagai string, kita bisa konversi dulu atau bisa dengan menambahkan opsi encoding di argumen option. Contoh:
```
// asynchronous
fs.readFile("file sumber", {encoding:"utf8"}, function(err, data){
	if(err){return console.error(err);}
	// operasi
});
// synchronous
const data = fs.readFileSync("file sumber",{encoding:"utf8"});
```
#### Watch file
- Watch file digunakan untuk memonitor event yang terjadi pada sebuah file atau folder. untuk menggunakannya kita hanya perlu membuat variabel dengan method fs.Watch lalu lakukan monitor pada event 'change' dengan parameter event type dan nama file yang terjadi perubahan. Contoh:
```
const watcher = fs.watch("path yang diwatch");
watcher.on("change", function(event, fname){
	// operasi
});
```
#### Write file
- Write file mirip dengan read file. Keduanya sama-sama memiliki method yang sync dan async dengan method writeFileSync() dan writeFile(). Untuk menulis secara async, kita harus pass path file yang ingin ditulis, data yang ingin ditulis, dan callback ketika terjadi error. Untuk menulis secara sync, kita tidak perlu menambahkan callback dan tidak akan mereturn apa-apa. Oleh karena itu untuk handle error kita bisa menggunakan try catch. Contoh:
```
// asynchronous
fs.writeFile("file tujuan","hello nodejs",
	function (err) {
		if (err) return console.error(err);
	}
);
// synchronous
try {
	fs.writeFileSync("file tujuan","hello nodejs");
} catch (err) {
	console.error(err);
}
```
- Untuk menulis dalam bentuk binary, kita bisa mengirimkan data dalam bentuk buffer. Contoh:
```
fs.writeFile("file tujuan",Buffer.from([16, 17, 18]),
	function (err) {
		if (err) return console.error(err);
	}
);
```
### HTTP Server
- Untuk membuat http server, Import http module lalu buat http server dengan createServer() dengan parameter fungsi listener yang memiliki parameter request dan response. Lalu kita panggil method listen() dengan parameter port dari http server yang kita inginkan. Contoh:
```
const http = require("http");
http.createServer(function (request, response) {
	// operasi
}).listen(8080);
```
- Untuk mempersiapkan response header kita bisa melakukan writeHead() dan response body dengan write() pada stream response. Contoh:
```
http.createServer(function (req, res) {
	res.writeHead(200, {"Content-Type": "text/html"});
	res.write("Hello nodejs");
	res.end();
}).listen(8080);
```
- Setelah kita run, maka kita bisa mengakses http server kita dengan address localhost:port
### Express
#### Get Started
- Untuk menginstall express (atau module third party lainnya) kita bisa mengunakan 'npm install express' ('express' bisa diganti dengan nama module yang ingin diinstall) dan setelah install maka akan muncul folder node_modules yang akan menampung semua third party module yang kita install.
- Kita juga butuh module body-parser untuk menghandle request body kita agar bisa dibaca sebagai JSON, cookie-parser untuk menghandle cookie, dan multer untuk menghandle form request.
- Untuk membuat server kita perlu menginisialisasi app express terlebih dahulu. Lalu kita membuat satu route dengan memanggil method yang kita inginkan (.get, .post, dll) lalu kita simpan endpoint route nya dan listener dari route tersebut dengan parameter req dan res. Pada listener kita bisa kirim response dengan menggunakan parameter res dan membaca request dengan parameter req.
- Lalu kita lakukan listen pada port yang kita inginkan untuk menjalankan server.
- Contoh:
```
const express = require("express");
const app = express();
app.get("/", function(req, res){
	res.send("Hello from express http");
});
app.listen(8080);
```
#### Middleware
- Middleware digunakan untuk menjalankan operasi sebelum dan sesudah menjalankan listener utama sehingga dapat digunakan untuk memodifikasi request atau response dan menjalankan operasi tertentu sebelum mengirim response ke client
- Untuk membuat middleware, kita menggunakan method use() dengan parameter route name dan listener yang mirip dengan listener biasa bedanya kita perlu parameter next untuk memanggil listener berikutnya.
- Jika kita membuat lebih dari 1 middleware, maka akan dijalankan urut dari atas ke bawah
- Contoh:
```
app.use("/", function (req, res, next) { // dijalankan pertama
	// operasi
	next();
});
app.get("/", function (req, res, next) { // dijalankan kedua
	// operasi
	next();
});
app.use("/", function (req, res) { // dijalankan terakhir
	// operasi
});
```
- Middleware juga bisa untuk mengexpose sebuah folder (misal untuk mengakses file css) dengan menggunakan middleware express.static('\<nama-folder\>'). Dengan begitu maka semua file yang ada di folder tersebut dapat diakses dari web server kita. Contoh:
```
app.use("/public", express.static(__dirname + "/public"));
```
#### Route
- Route akan mengatur jalur dari request yang dikirim ke server kita. Pengaturannya akan berdasarkan endpoint (misal: '/' atau '/user') dan method (GET, POST, dll).
- Jika menggunakan GET maka data yang dikirim akan muncul dan terlihat di url. Sedangkan jika menggunakan method yang lain, maka semua data akan dikirim melalui body request sehingga tidak muncul di url.
- Kita bisa menggunakan module body-parser untuk memparse body request yang dikirimkan dengan POST.
- Contoh:
```
const bodyParser = require("body-parser");
app.use(bodyParser.urlencoded({extended: false}));
app.use(bodyParser.json());
app.post("/user", function(req,res){ // route ke endpoint '/user' dan method POST
	res.end(JSON.stringify(req.body)); // akses dengan .body
});
```
### EJS dan templating engine
 - Templating engine dapat digunakan untuk membuat html berinteraksi dengan variabel sehingga menjadi lebih dinamis. Salah satu templating engine di javascript adalah EJS.
 - Untuk memasang EJS pada server kita harus install ejs dan mengunakan method set() pada app dengan parameter 'view engine' dan 'ejs'. Contoh:
```
app.set("view engine", "ejs"); 
```
 - EJS akan otomatis mengakses folder views untuk mendapatkan semua template htmlnya.
 - Untuk mengenerate html menggunakan EJS, kita harus menggunakan method render() dan mengirimkan semua variabel yang diperlukan pada template tersebut (jika datanya kosong maka kirimkan null). Contoh:
```
app.get("/", function (req, res) {
	res.render("index", {weather:null, error:null});
});
```
 - Bracket EJS adalah \<\% \%\>.
 - Untuk output data dapat menggunakan \<\%= nama-variabel\%\>
 - Contoh EJS:
```
<fieldset>
	<% if (weather !== null){ %>
		<p><%= weather %></p>
	<% } %>
	<% if (error !== null){ %>
		<p><%= error %></p>
	<% } %>
</fieldset>
```
### Fetch API lain
 - Untuk memanggil api lain, kita bisa menggunakan module request. untuk request kita bisa langsung panggil fungsi request setelah diimport dengan parameter api url dan callback untuk hasil requestnya. Contoh:
```
request(url, function (err, resp, body) {
	if (err) {
		// operasi jika ada error
	} else {
		// operasi jika tidak ada error
	}
});
```