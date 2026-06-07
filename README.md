# Terrain of Architectural Discourse
**Datascape Studio Perancangan Arsitektur ITS**

Visualisasi interaktif 3D untuk memetakan lanskap wacana Tugas Akhir mahasiswa Arsitektur ITS. Data dibaca otomatis dari Google Sheets dan dirender sebagai terrain topografis berbasis Kernel Density Estimation.

---

## Struktur Repo

```
repo/
├── index.html        ← Aplikasi utama (file ini yang di-deploy)
└── README.md         ← Dokumentasi ini
```

---

## Deploy ke GitHub Pages

1. Upload `index.html` ke repo GitHub (rename jika perlu)
2. Buka **Settings → Pages**
3. Pilih branch `main`, folder `/ (root)`
4. Klik **Save**
5. Akses di: `https://USERNAME.github.io/NAMA-REPO`

---

## Koneksi Google Sheets

### Format Spreadsheet

Buat Google Sheets dengan header di baris pertama:

| Tahun | ID | Judul | Koordinat | Kuadran |
|---|---|---|---|---|
| 2025 | TA1 | Judul proyek | (-6,+7,+3) | I |
| 2025 | TA2 | Judul proyek | (-7,+4,+2) | I |

**Keterangan kolom:**

| Kolom | Wajib | Keterangan |
|---|---|---|
| `Tahun` atau `Year` | Opsional | Angkatan, mis: `2024`, `2025` — digunakan untuk filter tahun |
| `ID` atau `No` | Ya | Identifikasi unik, mis: `TA1`, `TA2` |
| `Judul` atau `Title` | Ya | Judul lengkap Tugas Akhir |
| `Koordinat` | Ya | Format `(-6,+7,+3)` atau `-6,7,3` |
| `Kuadran` | Opsional | `I`, `II`, `III`, atau `IV` — jika kosong ditentukan otomatis |

**Makna koordinat:**

```
X  →  Sumbu Operasional   : -10 (Sistemis) .. +10 (Spontan/Kontingensi)
Y  →  Sumbu Intensi        : -10 (Teritorial/Ekologi) .. +10 (Somatis/Intim)
Z  →  Sumbu Temporal       : -10 (Masa Lalu) .. +10 (Masa Depan Spekulatif)
```

**Makna Kuadran:**

| Kode | Nama | Karakter |
|---|---|---|
| I | Structured Mind | Sistemis + Somatis |
| II | Experiential Poetics | Spontan + Somatis |
| III | Tactical & Resilient | Spontan + Teritorial |
| IV | Cybernetic Territory | Sistemis + Teritorial |

---

### Setting Google Sheets

1. Buka spreadsheet → klik **Share**
2. Pilih **"Anyone with the link"** → **Viewer**
3. Klik **Done**

> ⚠️ Tanpa setting ini, data tidak bisa dibaca oleh aplikasi.

---

### Menghubungkan ke HTML

Buka `index.html` dengan teks editor, cari baris berikut di bagian atas script:

```javascript
const GSHEET_ID  = '1kte8dUBPLSQjRjyXw1ekSR9IzlphF3KlGK9IrcdmCak';
const GSHEET_GID = '0';
```

- **`GSHEET_ID`** — ambil dari URL spreadsheet Anda:
  ```
  https://docs.google.com/spreadsheets/d/[INI_YANG_DICOPY]/edit
  ```
- **`GSHEET_GID`** — biarkan `'0'` untuk sheet pertama. Jika menggunakan sheet lain, lihat angka `gid=` di URL saat sheet tersebut aktif.

---

## Update Data

Cukup edit isi Google Sheets → simpan. Siapapun yang me-refresh halaman akan otomatis mendapat data terbaru. **Tidak perlu menyentuh file HTML sama sekali.**

---

## Fitur Visualisasi

| Fitur | Keterangan |
|---|---|
| **Density Terrain** | Elevation dari kepadatan proyek (KDE) — area padat jadi pegunungan |
| **Novelty Terrain** | Elevation dari jarak ke tetangga — proyek unik jadi puncak |
| **Hybrid Terrain** | Kombinasi 60% density + 40% novelty |
| **Warna Terrain** | Cyan = masa lalu · Violet = masa kini · Merah = masa depan |
| **Outlier Beacon** | Ikon diamond emas = proyek dengan novelty index tinggi |
| **Filter Tahun** | Muncul otomatis jika data punya kolom Tahun — terrain re-render per angkatan |
| **Sidebar Daftar** | Daftar seluruh proyek, sortable by ID / Kuadran / Tahun, dilengkapi search |

---

## Dependensi

Semua di-load dari CDN — tidak perlu instalasi:

| Library | Versi | Fungsi |
|---|---|---|
| [Plotly.js](https://plotly.com/javascript/) | 2.27.0 | Render terrain 3D interaktif |
| [SheetJS (xlsx)](https://sheetjs.com/) | 0.18.5 | Parse file XLSX lokal (fallback) |
| [Google Fonts — Roboto](https://fonts.google.com/specimen/Roboto) | — | Tipografi |

> Butuh koneksi internet saat pertama dibuka untuk memuat library dan font.

---

## Kredit

Didesain oleh **Nurfahmi Muchlis**  
Departemen Arsitektur — Institut Teknologi Sepuluh Nopember  
2026
