LoveStudio Firebase Cloud Starter

SETUP
1. Firebase Console > Project settings > Your apps > LoveStudio > Config.
2. Edit index.html. Cari const firebaseConfig di awal script type=module dan ganti placeholder dengan config Web App.
3. Authentication > Sign-in method > aktifkan Email/Password.
4. Firestore Database > Rules, pasang rules berikut. Ganti YOUR_UID dengan UID akun admin yang kamu izinkan.

rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{userId}/{document=**} {
      allow read, write: if request.auth != null && request.auth.uid == userId
        && userId == "YOUR_UID";
    }
  }
}

5. Deploy folder lovestudio ke hosting HTTPS (mis. GitHub Pages). Jangan buka dengan file://.
6. Daftar akun melalui aplikasi atau buat user di Authentication, lalu login.

CATATAN
- Versi ini benar-benar memakai Firebase Authentication dan Cloud Firestore untuk template/project.
- Firestore menyimpan tiap item sebagai dokumen; batas dokumen 1 MiB. Aplikasi menolak data di atas sekitar 850 KB.
- Tidak memakai Firebase Storage. Firebase Storage dapat memerlukan paket Blaze/billing. Media besar/ZIP penuh tidak disimpan di cloud oleh versi ini.
- Import ZIP hanya mengambil index.html utama; tidak mengonversi semua CSS/JS/aset menjadi elemen editor. Export menghasilkan website dasar dari field editor.
- Fitur multipage, music player, embed, drag-and-drop, dan penyimpanan media cloud belum termasuk dalam starter ini.
- Firebase SDK, JSZip, dan Google Fonts memerlukan internet.
- Data lama di localStorage tidak dimigrasikan otomatis.
