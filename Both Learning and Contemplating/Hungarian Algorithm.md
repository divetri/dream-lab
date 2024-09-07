Metode Munkres Assignment atau yang bisa disebut dengan metode Hungarian adalah sebuah algoritma untuk mencari alokasi penugasan agar beban yang diperlukan menjadi optimal. Metode ini digunakan untuk kasus _assignment_ atau penugasan antar pekerja terhadap beban pekerjaan. 

Contoh kasusnya kita ambil saja dari kisahnya Mawar. Saat istirahat makan siang, Mawar diajak pacarnya _fine dinning_ nanti malam di restoran. Tapi Mawar saat ini merasa sangat kucel dan tidak siap untuk diajak kencan dengan kekasihnya itu, karena hari ini _workload_ di kantor sangat banyak. Jadi, Mawar ingin mempercantik diri dengan reservasi _home care salon_ yaitu _hair do_, _manicure_, dan _make up_.

Permasalahnya adalah, ketiga perawatan ini harus dilakukan dalam satu kali waktu karena Mawar tidak ingin terlambat. Jadi, Mawar kumpulkan tiga salon yang bisa dia reservasi dengan _pricelist_ (satuan ribu rupiah) sebagai berikut:

|          | Salon A | Salon B | Salon C |
| -------- | ------- | ------- | ------- |
| Hair Do  | 30      | 50      | 80      |
| Manicure | 50      | 35      | 75      |
| Make Up  | 25      | 50      | 80      |
Jika kita melakukan pendekatan secara biasa, mungkin yang terlintas di kepala adalah membandingkan jumlah biayanya satu persatu, contoh:

Alokasi 1: _hair do_ di Salon A, _manicure_ di Salon B, _make up_ di Salon C
		30 + 35 + 80 = **145**
Alokasi 2: _hair do_ di Salon B, _manicure_ di Salon C, _make up_ di Salon A
		50 + 75 + 25 = **150**
Alokasi 3: _hair do_ di Salon C, _manicure_ di Salon A, _make up_ di Salon B
		80 + 50 + 50 = **180**
Alokasi 4: _hair do_ di Salon C, _manicure_ di Salon B, _make up_ di Salon A
		80 + 35 + 25 = **140**
Alokasi 5: _hair do_ di Salon B, _manicure_ di Salon A, _make up_ di Salon C
		50 + 50 + 80 = **180**
Alokasi 6: _hair do_ di Salon A, _manicure_ di Salon C, _make up_ di Salon B
		30 + 75 + 50 = **155**

Dengan metode manual ini, didapatkan nilai yang paling efektif yaitu dengan melakukan alokasi penugasan nomor 4. Mawar akan pesan _hair do_ di Salon C, _manicure_ di salon B, dan _make up_ di Salon A, sehingga Mawar hanya perlu mengeluarkan 140 ribu untuk semua perawatan dengan sekali jalan.

Tetapi karena Mawar anaknya suka yang efektif-efektif saja, Mawar menggunakan metode Hungarian, kita akan memanipulasi tabel _pricelist_ diatas untuk menemukan alokasi yang optimal.

1. Reduksi horizontal
Pada setiap baris, kita cari nilai minimalnya untuk kemudian mereduksi setiap barisnya agar ditemukan nilai 0 pada setiap baris.

|          | Salon A | Salon B | Salon C | Min.   |
| -------- | ------- | ------- | ------- | ------ |
| Hair Do  | 30      | 50      | 80      | ==30== |
| Manicure | 50      | 35      | 75      | ==35== |
| Make Up  | 25      | 50      | 80      | ==25== |
Hasilnya setelah dikurangi dengan nilai minimal setiap baris akan menjadi seperti ini:

|          | Salon A | Salon B | Salon C |
| -------- | ------- | ------- | ------- |
| Hair Do  | ==0==   | 20      | 50      |
| Manicure | 15      | ==0==   | 40      |
| Make Up  | ==0==   | 25      | 65      |
Kita bisa lihat di _hair do_, harga di Salon A sudah menjadi 0, begitupun dengan _manicure_ di Salon B dan _hair do_ di Salon C. Reduksi horizontal sudah berhasil.

2. Reduksi vertikal
Pada setiap kolom, kita cari nilai minimalnya untuk kemudian mereduksi setiap kolomnya agar ditemukan nilai 0 pada setiap kolom.

|          | Salon A | Salon B | Salon C |
| -------- | ------- | ------- | ------- |
| Hair Do  | 0       | 20      | 50      |
| Manicure | 15      | 0       | 40      |
| Make Up  | 0       | 25      | 65      |
| **Min**  | ==0==   | ==0==   | ==40==  |
Hasilnya setelah dikurangi dengan nilai minimal setiap kolom akan menjadi seperti ini:

|          | Salon A | Salon B | Salon C |
| -------- | ------- | ------- | ------- |
| Hair Do  | ==0==   | 20      | 10      |
| Manicure | 15      | ==0==   | ==0==   |
| Make Up  | ==0==   | 25      | 25      |
Kita bisa lihat, nilai terkecil di Salon C pada _manicure_ sudah menjadi 0. Reduksi vertikal sudah berhasil.

3. Penandaan nol

Langkah selanjutnya adalah membuat garis imajiner yang menutupi nilai 0. Kita harus menemukan garis imajiner sejumlah penugasan yang dicari. Di kasus Mawar, kita harus menemukan 3 garis imajiner untuk bisa menuju ke langkah penentuan solusi optimal.

|          | Salon A | Salon B | Salon C |
| -------- | ------- | ------- | ------- |
| Hair Do  | ==0==   | 20      | 10      |
| Manicure | ==15==  | ==0==   | ==0==   |
| Make Up  | ==0==   | 25      | 25      |
Namun, hanya terdapat 2 garis imajiner disini. Bagaimana cara mengatasinya? Kita menuju ke langkah ke 4.

4. Penyesuaian matriks

Penyesuaian matriks ini dilakukan dengan mencari nilai terkecil pada nilai yang tidak tertutupi garis imajiner. Jika dilihat, nilai terkecil yang tidak tertutupi adalah 10. Maka, semua nilai yang tidak tertutupi garis imajiner dikurangi 10.

|          | Salon A | Salon B | Salon C |
| -------- | ------- | ------- | ------- |
| Hair Do  | ==0==   | 10      | ==0==   |
| Manicure | ==15==  | ==0==   | ==0==   |
| Make Up  | ==0==   | 15      | 15      |
Sehingga didapatkan 1 lagi garis imajiner. Sekarang garisnya sudah ada 3. Kita bisa lanjut ke langkah terakhir.

|          | Salon A | Salon B | Salon C |
| -------- | ------- | ------- | ------- |
| Hair Do  | ==0==   | 10      | ==0==   |
| Manicure | ==25==  | ==0==   | ==0==   |
| Make Up  | ==0==   | 15      | ==15==  |

5. Penentuan solusi optimal
Setelah mendapatkan 3 garis imajiner penutup nilai 0, maka bisa kita dapatkan:
Pada tugas _make up_, hanya terdapat satu Salon dengan nilai 0, maka bisa diambil penugasan Salon A untuk _make up_.
Di nilai 0 pada Salon A yang lain, terdapat _hair do_, kita bisa pilih Salon lain dengan nilai 0 pada _hair do_ yaitu Salon C.
Sisanya, kita bisa ambil Salon B untuk penugasan _manicure_.

|          | Salon A | Salon B | Salon C |
| -------- | ------- | ------- | ------- |
| Hair Do  | 0       | 10      | ==0==   |
| Manicure | 25      | ==0==   | 0       |
| Make Up  | ==0==   | 15      | 15      |

Sehingga alokasi solusi optimal yang bisa Mawar ambil adalah:
_Hair do_ di Salon C, _manicure_ di Salon B, _make up_ di Salon A
		80 + 35 + 25 = **140**

## Kenapa Pakai Hungarian Algorithm?
