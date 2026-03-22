# Sistem Penghantaran Mingguan – SMK Mentakab

Repo ini ialah versi **siap untuk GitHub Pages** bagi sistem penghantaran mingguan staf SMK Mentakab.

## Kandungan
- `index.html` — fail utama aplikasi
- `.nojekyll` — memastikan GitHub Pages hidang fail statik tanpa proses Jekyll

## Cara guna di GitHub
1. Cipta repo baharu di GitHub.
2. Upload semua fail dalam folder ini ke root repo.
3. Pergi ke **Settings > Pages**.
4. Di bahagian **Build and deployment**, pilih:
   - **Source**: `Deploy from a branch`
   - **Branch**: `main`
   - **Folder**: `/ (root)`
5. Simpan tetapan dan tunggu GitHub Pages siap deploy.

## Firebase
Dalam `index.html`, cari bahagian ini:

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

Gantikan semua nilai `PASTE_*` dengan konfigurasi Firebase sebenar.

## Nota penting
- Sistem ini menggunakan **Firebase Auth**, **Firestore**, dan **Storage**.
- Fail dibina sebagai **single-file app** supaya mudah upload ke GitHub Pages.
- Jika logo atau banner tidak keluar, semak URL / Firebase Storage Rules.

## Cadangan struktur ringkas

```text
smk-mentakab-github-repo/
├── index.html
├── README.md
└── .nojekyll
```
