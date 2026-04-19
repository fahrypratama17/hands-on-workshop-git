# 🛠️ Hands-On: Website Portofolio Tim

**Skenario:** Kamu dan rekanmu (sebut saja "Yuswanto") sedang membangun website portofolio tim bersama. Kamu mengerjakan halaman utama dan blog, sementara Yuswanto mengerjakan halaman tim dan galeri. Di tengah jalan kalian akan mengalami konflik dan harus menyelesaikannya bersama.

---

## Skenario 1: Inisialisasi Repository

1. Buat folder project dan struktur awalnya:
   ```
   📁portfolio-tim
   📄index.html
   ```

2. Jalankan `git init` dari dalam folder tersebut:
   ```bash
   git init
   ```

3. Isi `index.html` dengan konten awal:
   ```html
   <html>
     <head>
       <title>Portfolio Tim</title>
     </head>
     <body>
       <header>
         <h1>Portfolio Tim Kami</h1>
         <nav>
           <a href="index.html">Home</a>
         </nav>
       </header>
     </body>
   </html>
   ```

4. Staging dan commit:
   ```bash
   git add .
   git commit -m "feat: initial commit with homepage skeleton"
   ```

5. Buat file `draft-notes.txt` — ini adalah catatan pribadi yang tidak perlu di-track:
   ```bash
   echo "catatan sementara, jangan di-commit" > draft-notes.txt
   ```

6. Masukkan ke `.gitignore`:
   ```bash
   echo draft-notes.txt > .gitignore
   ```

7. Buat folder `pages` untuk menampung halaman-halaman lain:
   ```bash
   mkdir pages
   ```

8. Buat dua file di dalam folder `pages`: `blog.html` dan `team.html`, isi keduanya dengan struktur HTML kosong terlebih dahulu:
   ```html
   <html>
     <head><title>Placeholder</title></head>
     <body></body>
   </html>
   ```

9. Commit semuanya:
   ```bash
   git add .gitignore index.html pages/blog.html pages/team.html
   git commit -m "feat: add .gitignore and pages folder with blog and team placeholders"
   ```

---

## Skenario 2: Branching — Kamu Mengerjakan Blog

1. Buat branch untuk fitur blog dan langsung pindah ke sana:
   ```bash
   git checkout -b feature/blog
   ```

2. Isi `pages/blog.html` dengan konten:
   ```html
   <html>
     <head>
       <title>Blog</title>
     </head>
     <body>
       <h1>Blog Tim</h1>
       <article>
         <h2>Postingan Pertama</h2>
         <p>Ini adalah postingan pertama kami.</p>
       </article>
     </body>
   </html>
   ```

3. Commit perubahan:
   ```bash
   git add pages/blog.html
   git commit -m "feat(blog): add blog page with first post"
   ```

---

## Skenario 3: Kembali ke Main — Update Navbar

1. Kembali ke branch `master`:
   ```bash
   git checkout master
   ```

2. Update `index.html` — tambahkan link navigasi ke semua halaman:
   ```html
   <html>
     <head>
       <title>Portfolio Tim</title>
     </head>
     <body>
       <header>
         <h1>Portfolio Tim Kami</h1>
         <nav>
           <a href="index.html">Home</a>
           <a href="pages/blog.html">Blog</a>
           <a href="pages/team.html">Team</a>
           <a href="pages/gallery.html">Gallery</a>
         </nav>
       </header>
       <main>
         <p>Selamat datang di website portofolio tim kami.</p>
       </main>
     </body>
   </html>
   ```

3. Commit:
   ```bash
   git add index.html
   git commit -m "feat(nav): add full navigation links to homepage"
   ```

---

## Skenario 4: Merge Branch Blog

1. Pindah dulu ke branch `feature/blog` untuk menambah satu postingan lagi:
   ```bash
   git checkout feature/blog
   ```

2. Update `pages/blog.html`:
   ```html
   <html>
     <head>
       <title>Blog</title>
     </head>
     <body>
       <h1>Blog Tim</h1>
       <article>
         <h2>Postingan Pertama</h2>
         <p>Ini adalah postingan pertama kami.</p>
       </article>
       <article>
         <h2>Postingan Kedua</h2>
         <p>Kami terus berkembang dan belajar hal baru.</p>
       </article>
     </body>
   </html>
   ```

3. Commit:
   ```bash
   git add pages/blog.html
   git commit -m "feat(blog): add second blog post"
   ```

4. Merge ke master:
   ```bash
   git checkout master
   git merge feature/blog
   ```

5. Sekarang update `pages/team.html` — isi dengan data anggota tim:
   ```html
   <html>
     <head>
       <title>Tim Kami</title>
     </head>
     <body>
       <h1>Anggota Tim</h1>
       <div>
         <h2>Kamu — Frontend Developer</h2>
         <p>Bertanggung jawab pada tampilan dan interaksi pengguna.</p>
       </div>
     </body>
   </html>
   ```

   ```bash
   git add pages/team.html
   git commit -m "feat(team): add team page with first member"
   ```

---

## Skenario 5: Git Stash — Simpan Pekerjaan Sementara

Setelah merge branch blog, kamu mulai mengerjakan halaman `pages/faq.html` di `master`. Kamu sudah menulis setengah konten, tapi tiba-tiba Yuswanto menghubungi dan meminta kamu untuk cepat mengecek sesuatu di branch `feature/blog` yang sudah di-merge tadi. Pekerjaan `faq.html` belum layak di-commit, tapi kamu juga tidak mau kehilangan progress yang sudah ada.

Di sinilah `git stash` berguna.

1. Buat dan isi `pages/faq.html` — tapi baru setengah jadi, belum siap di-commit:
   ```html
   <html>
     <head>
       <title>FAQ</title>
     </head>
     <body>
       <h1>Pertanyaan Umum</h1>
       <div>
         <h2>Apa itu portofolio tim?</h2>
         <p>Portofolio tim adalah kumpulan karya...</p>
       </div>
       <!-- masih banyak yang belum selesai -->
     </body>
   </html>
   ```

2. Cek status — Git tahu ada perubahan yang belum di-commit:
   ```bash
   git status
   ```
   Output:
   ```
   On branch master
   Untracked files:
     pages/faq.html
   ```

3. Simpan pekerjaan sementara ke stash:
   ```bash
   git stash -u
   ```

   > Flag `-u` (atau `--include-untracked`) diperlukan agar file baru yang belum pernah di-`add` sebelumnya ikut tersimpan ke stash. Tanpa flag ini, file untracked seperti `faq.html` akan diabaikan oleh stash.

4. Cek status sekarang — working directory bersih:
   ```bash
   git status
   ```
   Output:
   ```
   On branch master
   nothing to commit, working tree clean
   ```

5. Cek isi stash:
   ```bash
   git stash list
   ```
   Output:
   ```
   stash@{0}: WIP on master: 3154e7d feat(team): add team page with first member
   ```

6. Sekarang kamu bisa pindah branch dengan aman untuk mengecek sesuatu:
   ```bash
   git checkout feature/blog
   git checkout master
   ```

7. Setelah selesai, ambil kembali pekerjaan yang tadi disimpan:
   ```bash
   git stash pop
   ```

   `git stash pop` mengambil stash terakhir dan sekaligus menghapusnya dari daftar stash. Jika ingin mengambil tanpa menghapus dari daftar, gunakan `git stash apply`.

8. Cek status — `faq.html` kembali ada:
   ```bash
   git status
   ```
   Output:
   ```
   On branch master
   Untracked files:
     pages/faq.html
   ```

9. Lanjutkan mengisi `faq.html` hingga selesai:
   ```html
   <html>
     <head>
       <title>FAQ</title>
     </head>
     <body>
       <h1>Pertanyaan Umum</h1>
       <div>
         <h2>Apa itu portofolio tim?</h2>
         <p>Portofolio tim adalah kumpulan karya dan proyek yang pernah dikerjakan bersama.</p>
       </div>
       <div>
         <h2>Bagaimana cara bergabung?</h2>
         <p>Hubungi kami melalui halaman kontak untuk informasi lebih lanjut.</p>
       </div>
     </body>
   </html>
   ```

   ```bash
   git add pages/faq.html
   git commit -m "feat(faq): add FAQ page with common questions"
   ```

---

## Skenario 6: Git Reset  

1. Ternyata kamu sadar bahwa deskripsi di `team.html` terlalu umum dan belum sesuai dengan yang diinginkan tim. Kamu ingin kembali ke kondisi sebelum commit tersebut.

2. Cek log untuk menemukan commit target:
   ```bash
   git log --oneline
   ```
   Output akan terlihat seperti:
   ```
   9141c90 (HEAD -> master) feat(faq): add FAQ page with common questions     ← ingin undo ini
   3154e7d feat(team): add team page with first member
   ba62862 Merge branch 'feature/blog' : add article in blog.html
   058689f (feature/blog) feat(blog): add second blog post
   e7ad63b fix(blog): delete typo in index.html
   6259e22 feat(nav): add full navigation links to homepage
   47e52b0 feat(blog): add blog page with first post
   7c9c406 feat: add .gitignore and pages folder with blog and team placeholders
   dd5e704 feat: initial commit with homepage skeleton
   ```

3. Reset ke commit sebelum perubahan `team.html` (gunakan hash commit <`e4f5g6h`> milikmu):
   ```bash
   git reset --hard 9141c90
   ```

   > **⚠️ Perhatian:** `git reset --hard` akan menghapus semua perubahan yang belum di-commit secara permanen. Gunakan dengan hati-hati.

4. Cek log kembali — commit team.html sudah hilang:
   ```bash
   git log --oneline
   ```

5. Isi ulang `pages/team.html` dengan versi yang lebih baik dan commit lagi:
   ```html
   <html>
     <head>
       <title>Tim Kami</title>
     </head>
     <body>
       <h1>Anggota Tim</h1>
       <div>
         <h2>Kamu — Frontend Developer</h2>
         <p>Spesialisasi di React dan Tailwind CSS.</p>
       </div>
       <div>
         <h2>Yuswanto — UI/UX Designer</h2>
         <p>Spesialisasi di Figma dan desain sistem.</p>
       </div>
     </body>
   </html>
   ```

   ```bash
   git add pages/team.html
   git commit -m "feat(team): add team page with proper member descriptions"
   ```

   Jangan lupa karena faq.html terhapus maka harus dibuat lagi:
   Lanjutkan mengisi `faq.html` hingga selesai:
   ```html
   <html>
     <head>
       <title>FAQ</title>
     </head>
     <body>
       <h1>Pertanyaan Umum</h1>
       <div>
         <h2>Apa itu portofolio tim?</h2>
         <p>Portofolio tim adalah kumpulan karya dan proyek yang pernah dikerjakan bersama.</p>
       </div>
       <div>
         <h2>Bagaimana cara bergabung?</h2>
         <p>Hubungi kami melalui halaman kontak untuk informasi lebih lanjut.</p>
       </div>
     </body>
   </html>
   ```

   ```bash
   git add pages/faq.html
   git commit -m "feat(faq): add FAQ page with common questions"
   ```

---

## Skenario 7: Remote Repository

1. Hubungkan repo lokal ke GitHub:
   ```bash
   git remote add origin <url-repo-kamu>
   git push -u origin master
   ```

2. Yuswanto meng-clone repo dan membuat branch untuk mengerjakan halaman galeri:
   ```bash
   git clone <url-repo-kamu>
   cd portfolio-tim
   git checkout -b feature/gallery
   ```

3. Yuswanto membuat file `pages/gallery.html` dan melakukan commit lalu push:
   ```html
   <html>
     <head>
       <title>Galeri</title>
     </head>
     <body>
       <h1>Galeri Proyek</h1>
       <div>
         <h2>Proyek Alpha</h2>
         <p>Website e-commerce untuk klien pertama kami.</p>
       </div>
       <div>
         <h2>Proyek Beta</h2>
         <p>Aplikasi dashboard internal perusahaan.</p>
       </div>
     </body>
   </html>
   ```

   ```bash
   git add pages/gallery.html
   git commit -m "feat(gallery): add gallery page with two projects"
   git push origin feature/gallery
   ```

4. Yuswanto membuat Pull Request di GitHub dengan judul: `feat: add gallery page`.

---

## Skenario 8: Kamu Menambahkan Fitur Baru di Master

Sementara menunggu PR Yuswanto di-review, kamu melanjutkan pekerjaan di `master`.

1. Tambahkan halaman `pages/contact.html`:
   ```html
   <html>
     <head>
       <title>Kontak</title>
     </head>
     <body>
       <h1>Hubungi Kami</h1>
       <p>Email: tim@portfolio.com</p>
     </body>
   </html>
   ```

   ```bash
   git add pages/contact.html
   git commit -m "feat(contact): add contact page with email info"
   git push origin master
   ```

2. Kamu juga update `pages/team.html` — tambahkan satu anggota baru:
   ```html
   <html>
     <head>
       <title>Tim Kami</title>
     </head>
     <body>
       <h1>Anggota Tim</h1>
       <div>
         <h2>Kamu — Frontend Developer</h2>
         <p>Spesialisasi di React dan Tailwind CSS.</p>
       </div>
       <div>
         <h2>Yuswanto — UI/UX Designer</h2>
         <p>Spesialisasi di Figma dan desain sistem.</p>
       </div>
       <div>
         <h2>Budi — Backend Developer</h2>
         <p>Spesialisasi di Node.js dan PostgreSQL.</p>
       </div>
     </body>
   </html>
   ```

   ```bash
   git add pages/team.html
   git commit -m "feat(team): add Budi as backend developer"
   git push origin master
   ```

---

## Skenario 9: Konflik — Yuswanto Juga Edit team.html

Ternyata di branch `feature/gallery`, Yuswanto juga mengedit `pages/team.html` untuk memperbarui deskripsinya sendiri dengan versi yang berbeda:

```html
<html>
  <head>
    <title>Tim Kami</title>
  </head>
  <body>
    <h1>Anggota Tim</h1>
    <div>
      <h2>Kamu — Frontend Developer</h2>
      <p>Spesialisasi di React dan Tailwind CSS.</p>
    </div>
    <div>
      <h2>Yuswanto — UI/UX Designer</h2>
      <p>Berpengalaman 3 tahun di industri desain produk.</p>
    </div>
  </body>
</html>
```

```bash
# Dilakukan oleh Yuswanto di branch feature/gallery
git add pages/team.html
git commit -m "feat(team): update Yuswanto description with experience"
git push origin feature/gallery
```

Ketika PR Yuswanto dicek, terjadi konflik di `pages/team.html` karena kamu dan Yuswanto sama-sama mengubah bagian deskripsi Yuswanto dengan teks yang berbeda, dan kamu sudah menambahkan Budi yang tidak ada di versi Yuswanto.

**Yuswanto menyelesaikan konflik dari sisi branchnya:**

```bash
git checkout feature/gallery
git pull origin master
```

Git akan menandai konflik di `pages/team.html` seperti ini:

```html
<html>
  <head>
    <title>Tim Kami</title>
  </head>
  <body>
    <h1>Anggota Tim</h1>
    <div>
      <h2>Kamu — Frontend Developer</h2>
      <p>Spesialisasi di React dan Tailwind CSS.</p>
    </div>
    <div>
      <h2>Yuswanto — UI/UX Designer</h2>
<<<<<<< HEAD
      <p>Berpengalaman 3 tahun di industri desain produk.</p>
=======
      <p>Spesialisasi di Figma dan desain sistem.</p>
    </div>
    <div>
      <h2>Budi — Backend Developer</h2>
      <p>Spesialisasi di Node.js dan PostgreSQL.</p>
>>>>>>> master
    </div>
  </body>
</html>
```

Yuswanto menyelesaikan konflik secara manual — menggabungkan deskripsinya yang lebih lengkap sekaligus mempertahankan tambahan Budi dari master:

```html
<html>
  <head>
    <title>Tim Kami</title>
  </head>
  <body>
    <h1>Anggota Tim</h1>
    <div>
      <h2>Kamu — Frontend Developer</h2>
      <p>Spesialisasi di React dan Tailwind CSS.</p>
    </div>
    <div>
      <h2>Yuswanto — UI/UX Designer</h2>
      <p>Berpengalaman 3 tahun di industri desain produk.</p>
    </div>
    <div>
      <h2>Budi — Backend Developer</h2>
      <p>Spesialisasi di Node.js dan PostgreSQL.</p>
    </div>
  </body>
</html>
```

```bash
git add pages/team.html
git commit -m "fix(team): resolve conflict by merging member descriptions"
git push origin feature/gallery
```

Setelah push, PR Yuswanto sudah tidak konflik lagi dan siap di-merge. Lakukan merge PR di GitHub, lalu hapus branch `feature/gallery`.

---

## Struktur Akhir Project

Setelah semua skenario selesai, struktur folder project akan terlihat seperti ini:

```
📁portfolio-tim
├── 📁pages
│   ├── 📄blog.html
│   ├── 📄team.html
│   ├── 📄gallery.html
│   ├── 📄contact.html
│   └── 📄faq.html
├── 📄index.html
└── 📄.gitignore
```

> `draft-notes.txt` tidak masuk ke repository karena sudah di-ignore sejak awal.

# EZ LAH YA TEMEN-TEMEN