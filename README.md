# Analisis Sistem Antrian Pembayaran Registrasi Mahasiswa dengan Model Antrian Single Channel-Single Phase Pola M/M/s

Penelitian ini menganalisis sistem antrian pada loket pembayaran registrasi
mahasiswa di Universitas Nusa Nipa (UNIPA) menggunakan model antrian M/M/s
(multiserver), untuk menentukan jumlah petugas loket yang paling efisien
dengan mempertimbangkan keseimbangan antara waktu tunggu mahasiswa dan biaya
pelayanan yang dikeluarkan.

## Metode

- Observasi data lapangan (jumlah kedatangan & jumlah pelayanan per jam,
  selama periode registrasi Desember 2021)
- Perhitungan parameter dasar laju kedatangan (λ) dan laju pelayanan (μ)
- Simulasi model antrian M/M/s dengan variasi jumlah server s = 1 hingga s = 4
- Perhitungan performa sistem (Erlang-C): tingkat kesibukan (ρ), probabilitas
  sistem kosong (P0), panjang antrian (Lq), jumlah pelanggan dalam sistem (L),
  waktu tunggu rata-rata (Wq), waktu rata-rata dalam sistem (W)
- Pendekatan finite horizon untuk kondisi sistem tidak stabil (ρ ≥ 1), guna
  tetap dapat memperkirakan kondisi antrian dalam jangka waktu tertentu
- Analisis biaya: biaya pelayanan (service cost) dan biaya menunggu
  (waiting cost) untuk menilai efisiensi biaya operasional
- Interpretasi otomatis kondisi sistem (longgar, efisien, atau overload)
  berdasarkan nilai ρ dan Wq

## Data

- Sumber: hasil observasi langsung di loket pembayaran UNIPA
- Cakupan: data kedatangan & pelayanan selama 3 hari, pada 3 interval waktu
  per hari (10.00–11.00, 11.00–12.00, 12.00–13.00)
- Rata-rata kedatangan tertinggi terjadi pada interval 10.00–11.00 (>160
  mahasiswa/jam), sementara kapasitas pelayanan per petugas hanya sekitar
  55–60 orang/jam

## Tools

Python (pandas, math)

## Tujuan

- Menganalisis dan mengoptimalkan sistem antrian pada loket pembayaran
  registrasi mahasiswa
- Menentukan jumlah petugas loket (server) yang paling optimal
- Menyeimbangkan waktu tunggu mahasiswa dengan biaya pelayanan yang
  dikeluarkan

## Hasil Utama

### Perbandingan Simulasi Tiap Konfigurasi Loket

| Hasil            | M/M/1    | M/M/2    | M/M/3   | M/M/4   |
|-------------------|----------|----------|---------|---------|
| P0                | 0        | 0        | 0.0567  | 0.0834  |
| Lq (orang)        | 77       | 22       | 3       | 4       |
| L (orang)         | 79       | 24       | 5       | 3       |
| Wq (menit)        | 34.97    | 9.93     | 1.17    | 0.20    |
| W (menit)         | 96.06    | 11.03    | 2.26    | 1.29    |
| Biaya pelayanan (Cs) | Rp30.000 | Rp60.000 | Rp90.000 | Rp120.000 |
| Biaya menunggu (Cw)  | Rp766.667 | Rp217.778 | Rp25.664 | Rp4.276 |

- M/M/1 dan M/M/2 berada pada kondisi tidak stabil (ρ ≥ 1), sehingga
  dihitung menggunakan pendekatan finite horizon
- M/M/3 berada pada kondisi stabil dan efisien (ρ = 0.7989), dengan waktu
  tunggu rendah dan total biaya per jam paling seimbang (Rp115.644)
- M/M/4 berada pada kondisi longgar (ρ = 0.5992), petugas cenderung idle
  dengan biaya pelayanan relatif lebih tinggi (Rp124.276)

## Implikasi

Konfigurasi M/M/3 dinilai paling optimal untuk operasi loket registrasi
harian karena menyeimbangkan kinerja antrian dan biaya pelayanan — menjaga
utilisasi pada rentang aman, meningkatkan peluang sistem kosong, serta
menurunkan panjang antrian dan waktu tunggu sehingga penumpukan pada jam
normal dapat terkendali. Konfigurasi M/M/4 dapat dipertimbangkan secara
situasional pada periode sangat sibuk (misalnya awal semester atau batas
akhir administrasi) saat target waktu tunggu sangat ketat, atau ketika
kapasitas tiga loket menurun. Di luar kondisi tersebut, sistem menjadi
terlalu longgar dan biaya operasional relatif lebih tinggi.

## Struktur Folder

- `Code/` - Code Penyelesaian
- `Kasus/` - Studi Kasus
- `Slide/` - Slide PPT
