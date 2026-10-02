CARA MEMPERBARUI DATA KASUS
===========================

1. Salin kasus_terbaru_TEMPLATE.csv.
2. Ubah nama salinan menjadi kasus_terbaru.csv.
3. Isi case_count dengan jumlah kasus sebenarnya untuk empat BULAN KALENDER LENGKAP sampai bulan input model.
   Contoh pada Oktober 2026: Juni, Juli, Agustus, September 2026.
4. Jangan mengubah kode atau nama kecamatan.
5. Simpan sebagai CSV UTF-8.
6. Buka WebGIS > Eksperimental > Perbarui data pemantauan.

Jangan mengisi angka 0 apabila data sebenarnya belum diterima. Angka 0 berarti
telah terverifikasi tidak ada kasus pada kecamatan dan bulan tersebut.


Sistem tidak memakai bulan berjalan yang masih parsial untuk membentuk fitur model.
