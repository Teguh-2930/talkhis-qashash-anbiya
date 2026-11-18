# Talkhīṣ Qashash al-Anbiyā’ – Panduan Guru (paket publikasi)

Isi folder ini adalah situs yang sama dengan versi di Claude (versi 1.0.0), disiapkan agar dapat diterbitkan di hosting sendiri. **Isi materi, desain, struktur bab, dan fitur tidak diubah.**

| Berkas | Fungsi |
|---|---|
| `index.html` | Seluruh situs (halaman, gaya, skrip, dan seluruh data materi dalam satu berkas, ±3 MB) |
| `fonts/` | Huruf Arab Amiri dan Noto Naskh Arabic (lisensi SIL OFL 1.1, teksnya ada di folder yang sama) dan `fonts.css` |
| `vercel.json` | Pengaturan kecil untuk Vercel (header keamanan dasar). Boleh dibiarkan atau dihapus |
| `SHA256SUMS.txt` | Sidik jari semua berkas untuk memastikan tidak ada yang berubah |

## Perbedaan dari versi di Claude (hanya bagian kepala halaman)
1. Huruf Arab **tidak lagi dimuat dari Google Fonts**, melainkan dari folder `fonts/` di situs sendiri. Hurufnya sama (Amiri dan Noto Naskh Arabic), sehingga tampilan tidak berubah dan situs tidak lagi menghubungi server lain.
2. Ditambahkan keterangan pratinjau tautan (judul dan deskripsi) agar tampil rapi saat tautan dibagikan di WhatsApp dan media sosial, serta ikon tab peramban.
3. Satu aturan gaya kecil ditambahkan agar tanda baca Arab yang tinggi tidak keluar dari kotak ayat. Aturan yang sama juga sudah diterapkan pada versi di Claude.

Berkas dasar (versi Claude, sebelum perubahan nomor 1 dan 2) memiliki sidik jari SHA-256: `782fce18928ca929e57d9299e9fa1ed3a38a8ac9ffa1eb7f3f588f914523da43`.

## Teknologi situs
- **Situs statis satu berkas**: HTML + CSS + JavaScript biasa. **Bukan React, bukan Vite**, tidak ada langkah *build*, tidak ada `package.json`.
- Navigasi memakai alamat berawalan `#` (misalnya `/#/entry/musa`), sehingga **tidak perlu pengaturan server atau pengalihan**.
- Pencarian, penanda, ayat, dan semua fitur lain berjalan **di peramban pengunjung**. **Tidak ada server, basis data, atau akun.**
- Semua berkas dimuat dari situs sendiri; tidak ada permintaan ke layanan pihak lain.

## Cara paling mudah: Vercel lewat GitHub (hanya memakai peramban web)
1. Buat akun di https://github.com (bila belum punya).
2. Klik tanda **+** di kanan atas → **New repository**. Beri nama, misalnya `talkhis-qashash-anbiya`. Pilih **Public** (atau Private), lalu **Create repository**.
3. Pada halaman repositori yang baru, klik tautan **uploading an existing file**. Seret **isi folder ini** (`index.html`, `vercel.json`, dan folder `fonts`) ke area unggah, lalu klik **Commit changes**. Pastikan folder `fonts` ikut terunggah beserta isinya.
4. Buka https://vercel.com → **Sign Up** → pilih **Continue with GitHub**.
5. Di Vercel: **Add New…** → **Project** → pada daftar repositori pilih `talkhis-qashash-anbiya` → **Import**.
6. Pada pengaturan proyek:
   - **Framework Preset**: pilih **Other**.
   - **Build Command**, **Output Directory**, dan **Install Command**: **biarkan kosong**.
7. Klik **Deploy**. Tunggu sekitar satu menit sampai muncul alamat seperti `https://talkhis-qashash-anbiya.vercel.app`.
8. Klik alamat itu. Itulah tautan publik yang dapat dibagikan kepada para guru.

> Bila saat dibuka tanpa akun muncul halaman masuk Vercel, buka proyek di Vercel → **Settings** → **Deployment Protection**, lalu pastikan perlindungan tidak diaktifkan untuk alamat produksi.

> Nama tombol di layar Anda bisa sedikit berbeda dari penjelasan di atas karena tampilan Vercel dapat berubah.

## Cara lain: Vercel CLI (bagi yang sudah memasang Node.js)
```
npm install -g vercel
cd folder-ini
vercel login
vercel          # jawab pertanyaan; Directory: ./ ; jangan ubah pengaturan
vercel --prod   # menerbitkan ke alamat produksi
```

## Cara alternatif tanpa Vercel
Seluruh isi folder ini dapat diunggah apa adanya ke layanan hosting statis lain seperti Netlify (fitur seret-lepas folder), Cloudflare Pages, atau GitHub Pages, termasuk bila ditempatkan di subfolder (misalnya `…/nama-repo/`). Tidak ada yang perlu diubah di dalam `index.html`.

## Setelah terbit: daftar periksa
1. Buka alamat publik di HP, tablet, dan laptop.
2. Buka `…/#/entry/yunus/s4` langsung (harus tembus ke bagian subbab).
3. Buka halaman ayat, misalnya `…/#/ayat/20:17-21`. Huruf Arab harus berbentuk Naskh yang rapi.
4. Cari kata "Qarun", buka satu bab, klik satu tulisan "QS. …", lalu tekan **Kembali ke bacaan**.
5. Beri tanda penanda, muat ulang halaman, dan pastikan penanda masih ada.
6. Di folder ini jalankan `sha256sum -c SHA256SUMS.txt` (Linux dan Mac) untuk memastikan semua berkas utuh; di Windows gunakan `Get-FileHash` dan cocokkan secara manual.

## Fitur yang bergantung pada layanan atau perilaku tertentu
- **Tidak ada backend.** Tidak ada fitur yang memerlukan server, basis data, atau login.
- **Penanda, status "sudah dipelajari", posisi bacaan terakhir, dan pengaturan tampilan** disimpan di *localStorage* peramban masing-masing pengunjung. Itu berarti: tidak dibagikan antar guru, tidak berpindah antar perangkat, dan hilang bila data situs dihapus. Data yang sudah tersimpan di versi Claude **tidak ikut pindah** karena alamatnya berbeda. Bila alamat situs diganti di kemudian hari, data pengunjung di alamat lama juga tidak ikut pindah.
- **Tidak ada statistik pengunjung.** Bila ingin tahu jumlah pembaca, perlu menambahkan layanan analitik (itu perubahan di `index.html`, belum dilakukan).
- **Gambar pratinjau tautan (`og:image`) belum ada.** Pratinjau saat ini memuat judul dan deskripsi saja; gambar memerlukan alamat lengkap situs sehingga baru dapat ditambahkan setelah alamat publiknya diketahui.
- **Pembaruan manual**: setiap perubahan isi harus diterbitkan ulang (ganti berkasnya, lalu commit di GitHub atau jalankan `vercel --prod`).

## Hal yang perlu dipertimbangkan sebelum dibuka untuk semua orang
- Materi ini dirangkum dari buku *Kisah Para Nabi* karya Ibnu Katsir (terjemahan Indonesia dan edisi Arab) dan memuat terjemahan ayat Al-Qur'an Kemenag RI. Sebelum dipublikasikan luas, sebaiknya pastikan izin dari pemegang hak (penerbit atau penerjemah) dan cantumkan sumbernya. Ini bukan nasihat hukum.
- Paket gratis Vercel (Hobby) ditujukan untuk penggunaan pribadi nonkomersial; periksa ketentuan terbaru di situs Vercel, terutama bila situs dipakai atas nama lembaga atau yayasan.
- Situs ini dapat ditemukan mesin pencari bila tautannya dipublikasikan. Bila hanya ingin dibagikan kepada guru, jangan mencantumkan tautannya di tempat umum.
