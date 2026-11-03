# Eforel Product Knowledge

Sumber pengetahuan produk terpusat PT Eforel Citra Utama (Advantech, Transcend, Litemax, dan brand lain). Datasheet resmi adalah sumber kebenaran; repo ini hanya menyimpan hasil ekstraksi beserta link sumbernya.

## Isi repo

| File / folder | Fungsi |
|---|---|
| `index.csv` | Daftar semua produk yang sudah terdokumentasi |
| `_template.md` | Format baku setiap file produk |
| `SKILL.md` | Aturan kerja skill `product-knowledge` (salinan untuk agent lain) |
| `<brand>/<kategori>/<PART-NUMBER>.md` | Satu file per produk |

## Aturan singkat

- Prioritas sumber: datasheet > user manual > halaman produk > website Eforel.
- Setiap nilai spesifikasi wajib mencantumkan sumbernya.
- Data yang tidak ada di sumber resmi ditulis `perlu datasheet`.
- PDF datasheet tidak disimpan di repo, hanya link-nya.
- `status_verifikasi: terverifikasi` hanya diubah oleh manusia setelah dicek.
- Bagian "Catatan tim Eforel" di file produk diisi tim dan tidak diubah oleh skill.
