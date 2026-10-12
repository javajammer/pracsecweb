# Practical Security — situs statis

Situs ini menggunakan HTML dan CSS murni untuk GitHub Pages. Tidak ada framework, build step, JavaScript aplikasi, font eksternal, analytics, atau widget pihak ketiga. Domain awal yang dikonfigurasi: `practicalsecurity.web.id`.

## File utama

- `index.html` — halaman utama dan structured data `ProfessionalService`.
- `privasi.html` — kebijakan privasi.
- `404.html` — halaman kesalahan GitHub Pages.
- `assets/style.css` — gaya responsif, mode gelap, fokus keyboard, dan reduced motion.
- `assets/og-image.svg` — sumber vektor gambar Open Graph.
- `assets/og-image.png` — gambar Open Graph 1200 × 630.
- `CNAME`, `robots.txt`, `sitemap.xml` — konfigurasi domain dan crawler.

## Placeholder yang wajib diganti

Cari dan ganti nilai berikut pada seluruh file yang relevan:

- `[ISI_NOMOR_WA]` — nomor WhatsApp format internasional tanpa `+`, misalnya `62...`.
- `[ISI_EMAIL]` — alamat email kontak.
- `[ISI_URL_LINKEDIN]` — URL profil LinkedIn lengkap, misalnya `https://www.linkedin.com/in/...`.
- `[ISI: prosedur penyimpanan, masa retensi, dan penghapusan bukti sebelum situs dipublikasikan.]` — ganti dengan prosedur yang benar-benar diterapkan. Lengkapi juga bagian terkait di `privasi.html`.
- Pastikan domain `practicalsecurity.web.id` tetap menjadi domain final. Jika berubah, perbarui `CNAME`, canonical URL, Open Graph URL, JSON-LD, `robots.txt`, dan `sitemap.xml`.

Profil memakai kata ganti **kami**, sesuai positioning Practical Security yang dapat berkembang menjadi tim. Jangan menambahkan klaim sertifikasi, klien, studi kasus, atau pengalaman yang belum dapat dibuktikan.

### Menyembunyikan harga

Setiap layanan memiliki tepat satu elemen `.price`. Untuk menyembunyikan harga, tambahkan class `hide-price` pada elemen terkait, misalnya:

```html
<p class="price hide-price">Mulai dari Rp7,5 juta...</p>
```

Atau hapus elemen `<p class="price">...</p>` tersebut. Komentar petunjuk sudah ditempatkan di dekat masing-masing elemen harga.

## Deploy ke GitHub Pages

1. Buat repository GitHub baru, misalnya `practical-security-site`.
2. Unggah isi folder ini ke root repository (jangan unggah folder pembungkusnya saja).
3. Buka **Settings → Pages**.
4. Pada **Build and deployment**, pilih **Deploy from a branch**, branch `main`, folder `/(root)`, lalu simpan.
5. Tunggu proses deployment selesai dan periksa URL GitHub Pages sementara sebelum menghubungkan domain.

## Custom domain dan DNS

1. Pada **Settings → Pages → Custom domain**, masukkan `practicalsecurity.web.id` dan simpan.
2. Di penyedia DNS domain, atur record apex (`@`) dan `www` sesuai dokumentasi resmi GitHub Pages: <https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site>.
3. Untuk apex domain, GitHub mendokumentasikan penggunaan record A/AAAA yang sesuai. **Jangan memakai IP dari README lama, tutorial, atau ingatan. Verifikasi nilai IP terkini di dokumentasi resmi GitHub Pages sebelum membuat record DNS.**
4. Buat record `www` sebagai CNAME yang mengarah ke domain GitHub Pages yang benar sesuai dokumentasi resmi. Periksa juga record AAAA lama yang mungkin bertentangan.
5. Tunggu propagasi DNS. Gunakan dokumentasi GitHub untuk memverifikasi konfigurasi yang terdeteksi.

## Verifikasi domain dan HTTPS

1. Buka pengaturan akun/organisasi GitHub dan cari bagian **Pages** untuk **Verify a domain**.
2. Tambahkan domain, lalu buat record TXT pada DNS dengan nilai verifikasi persis seperti yang diberikan GitHub. Jangan menebak atau menggunakan nilai dari domain lain.
3. Setelah GitHub memverifikasi domain, pastikan domain tersebut tercantum pada pengaturan Pages repository yang benar.
4. Setelah sertifikat tersedia, aktifkan **Enforce HTTPS** di **Settings → Pages**.
5. Uji `https://practicalsecurity.web.id`, versi `www` jika dikonfigurasi, dan redirect HTTP ke HTTPS.

Panduan resmi: <https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/verifying-your-custom-domain-for-github-pages> dan <https://docs.github.com/en/pages/getting-started-with-github-pages/securing-your-github-pages-site-with-https>.

## CSP dan batasan header GitHub Pages

Halaman menggunakan CSP melalui `<meta http-equiv>` dan referrer policy melalui `<meta name="referrer">`. GitHub Pages tidak menyediakan konfigurasi header HTTP kustom langsung melalui repository. Karena itu beberapa header tidak dapat diterapkan sebagai response header dari situs GitHub Pages, antara lain `Strict-Transport-Security`, `X-Content-Type-Options`, `X-Frame-Options`, dan `Permissions-Policy`. `frame-ancestors` juga tidak efektif di CSP yang dipasang melalui meta tag. Jangan menganggap meta tag sebagai pengganti penuh header HTTP. Jika header tersebut wajib, gunakan hosting/proxy yang memberi kendali response header.

JSON-LD menggunakan elemen `<script type="application/ld+json">` untuk structured data, bukan JavaScript aplikasi. Situs tidak memakai skrip interaktif.

## Open Graph image

`assets/og-image.svg` adalah sumber vektor 1200 × 630. PNG sudah disediakan. Jika mengubah SVG, ekspor ulang sebagai PNG 1200 × 630 menggunakan editor vektor atau alat konversi yang tepercaya, lalu pastikan teks tetap terbaca pada pratinjau kecil.

## Checklist sebelum go-live

- [ ] Ganti nomor WhatsApp, email, dan URL LinkedIn.
- [ ] Pastikan domain final konsisten di seluruh metadata, `CNAME`, sitemap, dan robots.
- [ ] Lengkapi kebijakan penyimpanan dan penghapusan bukti dengan praktik aktual.
- [ ] Verifikasi harga atau sembunyikan elemen `.price`.
- [ ] Periksa copy, ejaan, dan semua tautan kontak.
- [ ] Pastikan tidak ada placeholder `[ISI: ...]` yang tertinggal kecuali sengaja dipertahankan sebagai pengingat internal.
- [ ] Uji tampilan mobile, desktop, mode gelap, navigasi keyboard, fokus terlihat, dan FAQ.
- [ ] Periksa judul, description, canonical, Open Graph, Twitter Card, dan JSON-LD.
- [ ] Uji `404.html`, `privasi.html`, sitemap, serta robots setelah deploy.
- [ ] Verifikasi domain di GitHub dan aktifkan **Enforce HTTPS**.
- [ ] Ingat bahwa situs statis dan CSP meta tag tidak menggantikan header keamanan HTTP yang tidak didukung GitHub Pages.
