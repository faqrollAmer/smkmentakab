# SMK Mentakab - Sistem Penghantaran Mingguan

Versi GitHub Pages untuk sistem penghantaran mingguan staff, admin dan pengetua.

## Fail utama
- `index.html` — aplikasi penuh
- `.nojekyll` — elak isu build GitHub Pages

## Cara guna di GitHub Pages
1. Cipta repository baru di GitHub.
2. Upload semua fail dalam folder ini.
3. Pastikan fail utama bernama `index.html`.
4. Pergi ke **Settings > Pages**.
5. Di bahagian **Build and deployment**, pilih:
   - **Source:** Deploy from a branch
   - **Branch:** `main` / `(root)`
6. Simpan, kemudian tunggu GitHub Pages siap publish.

## Firebase
Kod ini menggunakan Firebase Auth, Firestore dan Storage.
Bahagian `firebaseConfig` sudah berada dalam `index.html`.

Kalau mahu tukar project Firebase, cari bahagian ini dalam `index.html`:

```js
const firebaseConfig = {
  apiKey: "...",
  authDomain: "...",
  projectId: "...",
  storageBucket: "...",
  messagingSenderId: "...",
  appId: "...",
  measurementId: "..."
};
```

## Kata laluan default
Dalam fail `index.html`, cari:

```js
const PASSWORDS = {
  pengetua: "1234",
  admin: "0000"
};
```

Tukar kepada kata laluan sebenar sebelum deploy.

## Nota penting
- Untuk upload fail berfungsi, Firebase Storage mesti aktif.
- Untuk simpan rekod mingguan, Firestore mesti aktif.
- Untuk login anonymous, Firebase Authentication > Sign-in method > Anonymous mesti dihidupkan.
- Jika GitHub Pages tidak paparkan gaya dengan betul, pastikan semua fail diletakkan di root repo.
