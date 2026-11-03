---
name: product-knowledge
description: Jawab pertanyaan spesifikasi, fungsi, dan perbandingan produk Advantech, Transcend, Litemax, atau brand lain yang didistribusikan Eforel berdasarkan datasheet resmi, lalu simpan hasilnya ke repo eforel-product-knowledge. Gunakan setiap kali ada part number atau pertanyaan produk.
---

# Product Knowledge Eforel

Skill ini menjawab pertanyaan produk dari sumber resmi dan menyimpan setiap hasilnya ke repo GitHub `eforel-product-knowledge`. Pertanyaan berikutnya untuk produk yang sama dijawab langsung dari repo.

## Prinsip utama

1. **Prioritas sumber**: datasheet > user manual > halaman produk resmi > eforel.com / eforelonline.com. Sumber yang lebih rendah tidak boleh menimpa sumber yang lebih tinggi.
2. **Wajib sitasi**: setiap angka spesifikasi disertai sumbernya (nama file datasheet dan halaman, atau halaman produk).
3. **Tidak menebak**: data yang tidak ada di sumber resmi ditulis `perlu datasheet` atau dijawab "tidak tercantum di datasheet". Jangan mengisi dari pengetahuan umum atau produk serupa.
4. **Konflik dicatat**: jika halaman produk berbeda dengan datasheet, ikuti datasheet dan tulis perbedaannya di bagian "Catatan perbedaan sumber".
5. **Jawaban dalam Bahasa Indonesia**, formal dan ringkas. Istilah teknis dan nama spesifikasi tetap dalam bahasa aslinya.

## Struktur repo

```
eforel-product-knowledge/
├── index.csv
├── _template.md
└── <brand>/<kategori>/<PART-NUMBER>.md
```

- `brand` dan `kategori` ditulis huruf kecil dengan tanda hubung (contoh: `advantech/edge-ai/`).
- Nama file = part number persis seperti di datasheet, huruf besar (contoh: `MIC-711-ON.md`).
- Kategori mengikuti kategori di website brand. Cek dulu kategori yang sudah ada di `index.csv` sebelum membuat yang baru.

## Alur kerja

### 1. Identifikasi produk
- Ambil part number dari pertanyaan. Jika pengguna hanya menyebut deskripsi ("box PC fanless 4 COM"), cari kandidat di `index.csv` dulu, lalu di website brand. Tampilkan maksimal 3 kandidat dan minta pengguna memilih jika ragu.
- Bedakan varian (contoh: MIC-711-ON vs MIC-711-OX). Setiap varian dengan datasheet berbeda = file terpisah.

### 2. Cek repo
- Baca `index.csv`, cari baris part number tersebut.
- **Ada dan `dicek_terakhir` ≤ 90 hari** → buka file produknya, langsung ke langkah 5.
- **Ada tetapi > 90 hari** → lanjut ke langkah 3 untuk pengecekan ulang.
- **Belum ada** → lanjut ke langkah 3.

### 3. Ambil sumber resmi
Sumber per brand:
| Brand | Halaman produk | Datasheet |
|---|---|---|
| Advantech | advantech.com (halaman produk / model) | link "Datasheet" di halaman produk |
| Transcend | transcend-info.com (halaman produk) | tab Specifications / Downloads |
| Litemax | litemax.com (halaman produk) | link datasheet di halaman produk |

- Buka halaman produk, catat link datasheet dan nama filenya (nama file sering memuat kode versi/tanggal).
- Coba baca datasheet PDF. Jika tidak bisa dibaca, minta pengguna mengunggah PDF-nya. Sementara itu, isi file dari halaman produk dan tandai kolom yang belum ada sebagai `perlu datasheet`.

### 4. Ekstrak dan simpan
- Isi file mengikuti `_template.md` secara persis (frontmatter dan urutan bagian).
- Kolom "Sumber" di tabel spesifikasi diisi `DS hal. N` (datasheet halaman N), `Manual hal. N`, atau `Halaman produk`.
- `status_verifikasi` selalu `belum` saat dibuat atau diubah oleh skill. Hanya manusia yang mengubahnya menjadi `terverifikasi`.
- Untuk file yang sudah ada: ubah hanya nilai yang berubah, tambahkan satu baris di "Riwayat", dan jangan hapus catatan yang ditulis manusia.
- Perbarui `index.csv`: tambah baris baru atau perbarui `versi_datasheet`, `dicek_terakhir`, dan `status`.

### 5. Jawab
- Jawab pertanyaan pengguna langsung di kalimat pertama.
- Sertakan sitasi untuk setiap angka.
- Jika file berstatus `belum` terverifikasi, tambahkan satu baris: "Data belum diverifikasi manual."
- Untuk perbandingan produk, gunakan tabel dengan kolom per produk dan baris per spesifikasi.
- Tambah 1 pada kolom `ditanya` di `index.csv` untuk setiap produk yang ditanyakan.

## Menyimpan ke GitHub

- Gunakan tool GitHub yang tersedia di sesi (connector GitHub, `gh` CLI, atau git).
- Pesan commit: `add: <PART-NUMBER>`, `update: <PART-NUMBER> (<apa yang berubah>)`, atau `index: ditanya <PART-NUMBER>`.
- Jika tidak ada akses GitHub di sesi ini, berikan isi file lengkap dan baris `index.csv` yang perlu ditambahkan agar pengguna bisa menyimpannya manual. Sebutkan hal ini dalam satu kalimat.

## Larangan

- Jangan menyimpan PDF datasheet ke repo; simpan link-nya saja.
- Jangan mengisi spesifikasi dari ingatan atau dari produk lain yang mirip.
- Jangan mengubah `status_verifikasi` menjadi `terverifikasi`.
- Jangan menyalin paragraf marketing dari website secara utuh; tulis ringkasan dengan kata sendiri.
