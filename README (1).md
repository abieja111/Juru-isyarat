# Juru Isyarat

Aplikasi web yang membaca bentuk tangan lewat kamera HP dan mengubahnya jadi teks. Isyarat dilatih sendiri oleh pemakai, jadi bisa dipakai untuk BISINDO, SIBI, atau isyarat buatan sendiri.

## Cara pakai

1. Buka halaman ini di Chrome lewat alamat `https://` dan izinkan kamera.
2. Buka tab **Latih**, ketik nama isyarat (misalnya "Halo" atau "A"), lalu tekan **Rekam**. Peragakan isyaratnya sampai penuh (sekitar 50 sampel). Ulangi untuk tiap isyarat.
3. Buka tab **Terjemah**, peragakan isyarat, dan tahan sekitar 1 detik. Hasilnya masuk ke kalimat dan bisa diucapkan dengan tombol **Ucapkan**.

Tips merekam: putar tangan sedikit dan ubah jaraknya ke kamera selama merekam. Isyarat yang bentuknya mirip butuh lebih banyak sampel. Kalau sering salah baca atau tidak dikenali, atur slider **Toleransi** di tab Terjemah.

## Batasan

- Hanya mengenali bentuk tangan yang diam (huruf atau kata statis). Isyarat yang bergerak belum didukung.
- Satu tangan sekaligus.
- Tidak membaca ekspresi wajah dan gerakan badan, jadi belum bisa menerjemahkan percakapan utuh.
- Perlu internet saat pertama kali dibuka untuk mengunduh model tangan (sekitar 8 MB).

## Privasi

Video diproses di perangkat dan tidak dikirim ke server. Data latihan disimpan di browser (localStorage). Tombol **Simpan cadangan** mengunduhnya sebagai file JSON, dan **Muat cadangan** memasukkannya kembali.

## Cara kerja

1. [MediaPipe Hand Landmarker](https://ai.google.dev/edge/mediapipe/solutions/vision/hand_landmarker) mendeteksi 21 titik tangan.
2. Titik-titik itu dinormalisasi supaya tidak bergantung pada posisi dan ukuran tangan.
3. Pengklasifikasi k-nearest-neighbors (k = 5) mencocokkannya dengan sampel latihan.
4. Hasil dihaluskan beberapa frame, lalu masuk ke kalimat setelah ditahan sekitar 0,9 detik.

Seluruh aplikasi ada di satu file, `index.html`, tanpa proses build.

## Menjalankan di komputer sendiri

Kamera butuh konteks aman, jadi jalankan lewat server lokal:

```
python3 -m http.server 8000
```

Lalu buka `http://localhost:8000`.
