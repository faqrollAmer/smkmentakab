# SMK Mentakab – Sistem Penghantaran Mingguan

Versi ini sudah disediakan untuk **GitHub Pages** dan mempunyai:

- muka depan log masuk untuk **Staff / Admin / Pengetua**
- tema **Canvas Cloud + Electric Blue**
- sokongan **Firebase Auth, Firestore, dan Storage**
- upload fail mingguan, semakan, pengesahan, laporan, banner, dan logo

## Struktur repo

```
.
├── index.html
├── .nojekyll
└── README.md
```

## Cara guna di GitHub Pages

1. Buat repository baru di GitHub.
2. Upload semua fail dalam folder ini ke branch `main`.
3. Pergi ke **Settings > Pages**.
4. Pada **Build and deployment**, pilih:
   - **Source:** Deploy from a branch
   - **Branch:** `main`
   - **Folder:** `/ (root)`
5. Simpan dan tunggu GitHub Pages siap deploy.

## Penting sebelum guna

Buka fail `index.html` dan cari bahagian ini:

```js
const firebaseConfig = {
  apiKey: "PASTE_API_KEY",
  authDomain: "PASTE_AUTH_DOMAIN",
  projectId: "PASTE_PROJECT_ID",
  storageBucket: "PASTE_STORAGE_BUCKET",
  messagingSenderId: "PASTE_MESSAGING_SENDER_ID",
  appId: "PASTE_APP_ID"
};
```

Gantikan semua nilai `PASTE_*` dengan config Firebase sebenar.

## Kata laluan default

Dalam `index.html`, cari blok ini:

```js
const PASSWORDS = {
  pengetua: "1234",
  admin: "0000"
};
```

Tukar kepada kata laluan sebenar sebelum digunakan.

## Login sistem

- **Staff**: pilih nama staff pada muka depan, kemudian masuk ke sistem.
- **Admin**: guna kata laluan admin.
- **Pengetua**: guna kata laluan pengetua.

## Nota

- Jika Firebase belum lengkap, sistem akan papar status config belum lengkap.
- Untuk GitHub Pages, fail ini sudah sesuai digunakan terus tanpa Jekyll.
