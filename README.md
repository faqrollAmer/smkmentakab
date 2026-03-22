# SMK Mentakab React System

Sistem React + Firebase untuk rekod penghantaran tugasan mingguan staff.

## Fungsi utama

- Landing login sebelum masuk sistem
- Login Staff melalui dropdown nama
- Login Admin dan Pengetua melalui passcode
- Staff hanya boleh akses rekod sendiri
- Admin dan Pengetua boleh akses semua rekod
- Upload fail mingguan
- Pratonton fail imej dan PDF
- Pengesahan tugasan oleh admin/pengetua
- Panel notifikasi
- Ubah logo sekolah dan banner terus dari sistem
- Navigasi minggu 1 hingga 52
- Carta pai ringkas status penghantaran

## Struktur

```bash
smk-mentakab-react/
├─ index.html
├─ package.json
├─ vite.config.js
├─ .env.example
├─ README.md
└─ src/
   ├─ main.jsx
   └─ App.jsx
```

## Cara guna

### 1. Install

```bash
npm install
```

### 2. Buat fail `.env`

Salin `.env.example` jadi `.env`

```bash
cp .env.example .env
```

Isi semua nilai Firebase anda.

### 3. Run local

```bash
npm run dev
```

### 4. Build untuk GitHub / hosting

```bash
npm run build
```

Fail output akan berada dalam folder `dist/`.

## Koleksi Firestore yang digunakan

- `submissions`
- `notifications`
- `settings/branding`

## Peraturan login default

- Staff: pilih nama sendiri
- Admin: passcode `0000`
- Pengetua: passcode `1234`

Passcode ini boleh diubah dalam `.env`.

## Nota penting

Kod ini simpan fail sebagai `data URL` terus dalam Firestore untuk setup cepat.
Untuk projek sebenar yang lebih besar, elok pindah fail ke **Firebase Storage**.
