# SIAPK - Sistem Informasi Alat Peraga Kampanye

Aplikasi web untuk pengawasan dan pemetaan sebaran Alat Peraga Kampanye (APK) berbasis GIS dengan hierarki pengguna multi-level.

## 🚀 Fitur Utama

- **Peta Interaktif** - OpenStreetMap + Marker Clustering
- **Multi-Level Pengguna** - Admin/Kabupaten, Kecamatan, Desa
- **Input APK** - Koordinat GPS / klik peta, upload foto
- **Filter & Pencarian** - Per partai, jenis, status, kecamatan
- **Rekap Laporan** - Per kecamatan, per partai, per jenis APK
- **Grafik Statistik** - Chart distribusi dan perbandingan
- **Export CSV** - Laporan bisa diunduh
- **Halaman Publik** - Masyarakat bisa lihat tanpa login
- **Mode Demo** - Bisa dicoba tanpa konfigurasi Supabase

## 👥 Hierarki Pengguna

| Level | Akses |
|-------|-------|
| **Admin/Kabupaten** | Full akses: tambah data, rekap seluruh, manajemen akun, manajemen wilayah |
| **Pengawas Kecamatan** | Input data, rekap kecamatan sendiri |
| **Pengawas Desa** | Input data desa sendiri |
| **Masyarakat** | Peta publik + statistik (tanpa login) |

## ⚙️ Setup Supabase

### 1. Buat Project Supabase
- Daftar di [supabase.com](https://supabase.com)
- Buat project baru
- Catat **Project URL** dan **Anon Key**

### 2. Jalankan SQL Schema
- Buka **SQL Editor** di Supabase Dashboard
- Jalankan semua query dari file: `src/lib/supabaseSchema.sql`

### 3. Buat Storage Bucket
- Buka **Storage** di Supabase Dashboard
- Buat bucket bernama `apk-photos`
- Set sebagai **Public**

### 4. Konfigurasi Environment
Buat file `.env` di root project:
```env
VITE_SUPABASE_URL=https://xxxxxxxxxxxxx.supabase.co
VITE_SUPABASE_ANON_KEY=your-anon-key-here
```

### 5. Buat Admin Pertama
- Di Supabase Dashboard > Authentication > Users
- Tambah user baru (email + password)
- Catat UUID user tersebut
- Jalankan SQL berikut:
```sql
INSERT INTO profiles (id, email, full_name, role, is_active)
VALUES ('UUID-USER-ANDA', 'admin@email.com', 'Nama Admin', 'admin', true);
```

## 🚀 Deploy ke Netlify

1. Push kode ke GitHub
2. Buka [netlify.com](https://netlify.com) > New Site from Git
3. Pilih repository
4. Build command: `npm run build`
5. Publish directory: `dist`
6. Tambah environment variables:
   - `VITE_SUPABASE_URL`
   - `VITE_SUPABASE_ANON_KEY`
7. Deploy!

## 💻 Development

```bash
npm install
npm run dev
```

## 🛠️ Tech Stack

- **Frontend**: React 19 + TypeScript + Vite
- **Styling**: Tailwind CSS
- **Peta**: React-Leaflet + OpenStreetMap
- **Database**: Supabase (PostgreSQL)
- **Auth**: Supabase Auth
- **Storage**: Supabase Storage
- **Charts**: Recharts
- **Icons**: Lucide React
