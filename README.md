# Git Workshop: Proyek Website Kolaboratif

## Skenario 1: Inisialisasi Repository

1. Mulailah dengan membuat Git repository di komputer lokal, kemudian buatlah struktur folder berikut:
   ```
   📁project-demo
   📄index.html
   ```

2. Kemudian dari root, jalankan perintah git init pada terminal:
   ```bash
   git init
   ```

3. Selanjutnya, isi file index.html dengan kode:
   ```html
   <html>
     <head>
       <title>Project Demo</title>
     </head>
     <body></body>
   </html>
   ```

4. Lakukan commit dengan pesan "Initial commit" setelah melakukan staging:
   ```bash
   git add .
   git commit -m "feat: initial commit"
   ```

5. Lalu dari root project, buatlah file about.html dan isilah dengan kode:
   ```html
   <html>
     <head>
       <title>About Us</title>
     </head>
     <body></body>
   </html>
   ```

6. Namun, karena file about.html tidak ingin di-commit, masukkan file tersebut ke dalam `.gitignore`:
   ```bash
   echo "about.html" > .gitignore
   ```

7. Buatlah folder baru dalam repository untuk menampung halaman-halaman aplikasi demo ini:
   ```bash
   mkdir content
   ```

8. Di dalam folder content, buatlah dua file: contact.html dan services.html.

9. Lakukan commit yang mencakup file .gitignore dan folder content beserta isinya:
   ```bash
   git add .
   git commit -m "feat: add .gitignore and content folder with contact and services pages"
   ```

## Skenario 2: Branching

1. Buatlah branch baru dengan nama feature/services, kemudian pindah ke branch tersebut:
   ```bash
   git branch feature/services
   git checkout feature/services
   ```
   
   Alternatif dalam satu perintah:
   ```bash
   git checkout -b feature/services
   ```

2. Tambahkan file pricing.html di dalam folder content.
   
   Struktur folder di branch feature/services akan terlihat seperti ini:
   ```
   📁project-demo
   ├── 📁content
   │   ├── 📄contact.html
   │   ├── 📄services.html
   │   └── 📄pricing.html
   ├── 📄index.html
   ├── 📄about.html
   └── 📄.gitignore
   ```

3. Tambahkan kode berikut pada file pricing.html:
   ```html
   <html>
     <head>
       <title>Pricing</title>
     </head>
     <body>
       <div>Service 1: $10</div>
       <div>Service 2: $20</div>
     </body>
   </html>
   ```

4. Lakukan commit pada file pricing.html:
   ```bash
   git add content/pricing.html
   git commit -m "feat: add pricing page with initial services"
   ```

## Skenario 3: Bekerja di Branch Utama

1. Kembali ke branch utama (master):
   ```bash
   git checkout master
   ```

2. Lanjutkan dengan mengerjakan file services.html, dan tambahkan beberapa elemen:
   ```html
   <html>
     <head>
       <title>Services</title>
     </head>
     <body>
       <div>
         <h2>Our Services</h2>
       </div>
       <div>
         <ul>
           <li>Service A</li>
           <li>Service B</li>
         </ul>
       </div>
     </body>
   </html>
   ```

3. Lakukan commit untuk file services.html:
   ```bash
   git add content/services.html
   git commit -m "feat: update services page with list of services"
   ```

## Skenario 4: Merge Branch

1. Dari branch master, pindah kembali ke branch feature/services:
   ```bash
   git checkout feature/services
   ```

2. Lanjutkan untuk mengerjakan file pricing.html dan tambahkan elemen lain:
   ```html
   <html>
     <head>
       <title>Pricing</title>
     </head>
     <body>
       <div>Service 1: $10</div>
       <div>Service 2: $20</div>
       <div>Service 3: $30</div>
     </body>
   </html>
   ```

3. Lakukan commit:
   ```bash
   git add content/pricing.html
   git commit -m "feat: add service 3 to pricing page"
   ```

4. Setelah pekerjaan selesai, gabungkan branch feature/services ke branch master:
   ```bash
   git checkout master
   git merge feature/services
   ```

5. Lakukan commit pada perubahan yang terjadi di file contact.html dan tambahkan elemen baru:
   ```bash
   # Edit file content/contact.html untuk menambahkan elemen baru
   git add content/contact.html
   git commit -m "feat: update contact page with form elements"
   ```

## Skenario 5: Git Reset

1. Setelah melakukan beberapa feature, sadar bahwa beberapa halaman di services.html masih perlu penyesuaian.

2. Karena deadline aplikasi semakin dekat, kita akan bekerja sama dengan partner.

3. Lakukan reset pada commit tertentu dengan perintah berikut untuk menghapus perubahan yang tidak diinginkan:
   ```bash
   git reset --hard <commitID_target>
   ```

   > **Catatan**: Ganti `<commitID_target>` dengan ID commit yang ingin Anda kembali. Perintah ini akan menghapus semua perubahan yang belum di-commit, jadi gunakan dengan hati-hati.

## Skenario 6: Remote Repository

1. Sekarang kita akan menghubungkan repository lokal ke remote repository di GitHub agar teman kerja bisa mengaksesnya:
```bash
git remote add origin <remote-repository-url>
git push -u origin master
```

2. John akan meng-clone repository dan membuat branch baru bernama feature/landing-page:
```bash
git clone <remote-repository-url>
cd project-demo
git checkout -b feature/landing-page
```

3. John akan menambahkan kode halaman landing page di file landing.html dan melakukan commit serta push:
```bash
# Buat dan edit file landing.html
git add landing.html
git commit -m "feat: add landing page"
git push origin feature/landing-page
```

4. Setelah itu, John membuat Pull Request dengan judul PR: "feat: Add Landing Page" melalui GitHub.

## Skenario 7: Menambahkan Fitur Baru

1. Setelah bekerja di branch master, kita menambahkan halaman faq.html dengan pertanyaan dan jawaban di dalamnya:
```bash
# Buat dan edit file faq.html
git add faq.html
git commit -m "feat: add FAQ page"
git push origin master
```

2. Selain itu, kita juga mengupdate file pricing.html untuk menambahkan lebih banyak layanan:
```bash# Edit file content/pricing.html untuk menambahkan layanan baru
# Ubah konten menjadi:
html<html>
  <head>
    <title>Pricing</title>
  </head>
  <body>
    <div>Service 1: $10</div>
    <div>Service 2: $20</div>
    <div>Service 3: $30</div>
    <div>Service 7: $70</div>
    <div>Service 8: $80</div>
    <div>Service 9: $90</div>
  </body>
</html>
```
```bashgit add content/pricing.html
git commit -m "feat: add more premium services to pricing page"
git push origin master
```

## Skenario 8: Menyelesaikan Konflik
1. Sementara itu, John telah bekerja di branch feature/landing-page dan juga melakukan perubahan pada file pricing.html:
```bash
# John mengedit file content/pricing.html di branchnya
# Mengubah konten menjadi:
html<html>
  <head>
    <title>Pricing</title>
  </head>
  <body>
    <div>Service 1: $10</div>
    <div>Service 2: $20</div>
    <div>Service 3: $30</div>
    <div>Service 4: $40</div>
    <div>Service 5: $50</div>
    <div>Service 6: $60</div>
  </body>
</html>
```
```bash
git add content/pricing.html
git commit -m "feat: add medium-tier services to pricing page"
git push origin feature/landing-page
```

2. John mengonfirmasi bahwa landing page dan perubahan pricing.html sudah selesai dan siap digabungkan.
3. Namun, setelah check PR, terjadi konflik antara branch master dan feature/landing-page pada file pricing.html.
4. Untuk menyelesaikan konflik:
```bash
git checkout feature/landing-page
git pull origin master
```

5. Git akan menandai konflik di file pricing.html seperti ini:
```html
<html>
  <head>
    <title>Pricing</title>
  </head>
  <body>
    <div>Service 1: $10</div>
    <div>Service 2: $20</div>
    <div>Service 3: $30</div>
<<<<<<< HEAD
    <div>Service 4: $40</div>
    <div>Service 5: $50</div>
    <div>Service 6: $60</div>
=======
    <div>Service 7: $70</div>
    <div>Service 8: $80</div>
    <div>Service 9: $90</div>
>>>>>>> master
  </body>
</html>
```

6. Selesaikan konflik dengan menggabungkan kedua perubahan secara manual di editor. Hasilnya seharusnya seperti:
```html
<html>
  <head>
    <title>Pricing</title>
  </head>
  <body>
    <div>Service 1: $10</div>
    <div>Service 2: $20</div>
    <div>Service 3: $30</div>
    <div>Service 4: $40</div>
    <div>Service 5: $50</div>
    <div>Service 6: $60</div>
    <div>Service 7: $70</div>
    <div>Service 8: $80</div>
    <div>Service 9: $90</div>
  </body>
</html>
```

7. Setelah menyelesaikan konflik:
```bash
git add content/pricing.html
git commit -m "fix: resolve pricing page conflicts by merging all services"
git push origin feature/landing-page
```

8. Setelah berhasil, lakukan merge pull request di GitHub dan hapus branch feature/landing-page.

# GAMPANG LAH YA TEMEN - TEMEN