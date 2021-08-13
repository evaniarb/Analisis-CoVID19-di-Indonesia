# Analisis-CoVID19-di-Indonesia
Maraknya CoVID-19 di Indonesia membuatku penasaran akan pergerakan grafik jumlah pasien, korban, dan kasus sembuh. 
Hal ini juga yang melatarbelakangiku bahan sebagai belajar R dalam penerapan riset industri. 
Aku menggunakan API dari website covid resmi pemerintah yakni https://data.covid19.go.id/public/api/update.json dengan fungsi GET() 
sebagai permintaan kepada server dan fungsi status_code(resp) sebagai informasi dari server. resp menunjukkan angka 200 yang berarti permintaan sukses dipenuhi.

aku juga menguji ulang dengan cara lain untuk memastikan apakah server benar-benar mengizinkanku mengakses permintaan datanya atau tidak dengan formula sebagai berikut:
resp$status_code [1] 200
identical(resp$status_code, status_code(resp)) [2] TRUE

kemudian aku juga ingin melihat isi metadata apa saja yang tersedia dalam elemen content-type menggunakan formula headers(resp). dan inilah metadata yang keluar
1. Server: Nginx
2. Tanggal terakhir data diupdate: Jumat, 13 Agustus 2021 08:55 GMT
3. Content Type: Apllication/Json
3. Vary: Accept Encoding
4. etag: W/\"61163311-31f25\
5. Content type options: nosniff
6. XSS Protection: 1; mode=block
7. Strict Transport Security: max-age=31536000; includeSubDomains; preload
8. Content Encoding: gzip

dengan data length 2, aku mendapatkan surface analysis sebagai berikut:
1. Kapan tanggal pembaharuan data penambahan kasus? Jawaban: 2021-08-12
2. Berapa jumlah penambahan kasus sembuh? Jawaban: 36637
3. Berapa jumlah penambahan kasus meninggal? Jawaban: 1466
4. Berapa jumlah total kasus positif hingga saat ini? Jawaban: 3774155
5. Berapa jumlah total kasus meninggal hingga saat ini? Jawaban: 113664

Hal diatas menggunakan formula
lapply(cov_id_update,names)
cov_id_update$penambahan$tanggal
cov_id_update$penambahan$jumlah_sembuh
cov_id_update$penambahan$jumlah_meninggal
cov_id_update$total$jumlah_positif
cov_id_update$total$jumlah_meninggal

NOTE: github hanya berisi source code saja. jika ingin penjelasan berupa storytelling bisa menuju blogku di http://evaniarb.medium.com Thankyou! xoxo
