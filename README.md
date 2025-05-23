# **SakuraCloudID Web Platform – Powered by Next.js**  
## **Dokumentasi Teknis Komprehensif**

---

## **Memulai**  
Panduan langkah demi langkah untuk menyiapkan proyek secara lokal untuk pengembangan.

### **1. Kloning Repositori**  
```bash
git clone https://github.com/sakuracloudid/web.git
cd web
```  
- **Tujuan**: Membuat salinan lokal dari repositori proyek dan masuk ke direktori proyek.  
- **Praktik Terbaik**:  
  - Gunakan kunci SSH untuk autentikasi GitHub jika Anda sering melakukan kloning repositori.  
  - Pastikan Anda memiliki `git` yang terinstal di sistem Anda (versi minimum yang disarankan adalah 2.25 atau lebih tinggi).  

### **2. Instal Dependensi**  
```bash
npm install  # atau yarn
```  
- **Tujuan**: Menginstal semua dependensi proyek yang tercantum dalam file `package.json`.  
- **Dependensi Utama**:  
  - **`next`**: Kerangka kerja inti untuk rendering sisi server (SSR) dan manajemen routing.  
  - **`react` & `react-dom`**: Pustaka untuk membangun antarmuka pengguna (UI) dan integrasi dengan DOM.  
  - **`tailwindcss`**: Kerangka kerja CSS berbasis utilitas untuk pengembangan UI yang cepat.  
  - **`typescript`**: Menambahkan pemeriksaan tipe statis untuk meningkatkan kualitas kode.  

### **3. Jalankan Server Pengembangan**  
```bash
npm run dev  # atau yarn dev
```  
- **Tujuan**: Memulai server pengembangan lokal dengan fitur *hot-reloading* untuk mempercepat proses pengembangan.  
- **Akses**: Buka `http://localhost:3000` di peramban Anda untuk melihat aplikasi berjalan.  
- **Alat Pengembangan**:  
  - Mode pengembangan Next.js menyediakan overlay kesalahan langsung dan refresh cepat saat ada perubahan kode.  
  - Gunakan Chrome DevTools untuk debugging komponen React dan memantau permintaan jaringan.  

---

## **Struktur Proyek**  
Berikut adalah rincian lengkap hierarki direktori dan tanggung jawab masing-masing file atau folder.

### **Direktori Inti**  
1. **`/app`**  
   - **Tujuan**: Menggunakan **App Router** dari Next.js versi 13+ untuk mengatur routing dan struktur halaman.  
   - **File Utama**:  
     - **`layout.tsx`**: Layout utama yang diterapkan ke semua halaman untuk konsistensi tata letak.  
     - **`page.tsx`**: Titik masuk untuk halaman beranda, yang dapat diakses melalui rute `/`.  
     - **Subdirektori**: Misalnya, `/dashboard` digunakan untuk mendefinisikan rute bersarang seperti `/dashboard/settings`.  

2. **`/components`**  
   - **Tujuan**: Menyimpan komponen UI yang dapat digunakan kembali, seperti `Navbar.tsx` atau `Footer.tsx`.  
   - **Praktik Terbaik**:  
     - Kelompokkan komponen terkait ke dalam subfolder, misalnya `/auth/LoginForm.tsx`.  
     - Gunakan antarmuka TypeScript untuk memvalidasi *props* yang diterima komponen.  

3. **`/styles`**  
   - **File Utama**:  
     - **`globals.css`**: Berisi variabel CSS global dan gaya dasar yang diterapkan ke seluruh aplikasi.  
     - **`light.css` & `dark.css`**: Gaya khusus untuk tema terang dan gelap, yang dimuat secara dinamis.  
   - **Pendekatan Gaya**:  
     - **Tailwind CSS**: Menggunakan kelas utilitas untuk membangun UI secara cepat dan konsisten.  
     - **CSS Modules**: Digunakan untuk gaya spesifik komponen dengan *scoping* lokal.  

4. **`/public`**  
   - **Aset**: Menyimpan file statis seperti gambar (`/images/logo.svg`), ikon, atau dokumen PDF.  
   - **Optimisasi**: Gunakan komponen `Image` dari Next.js untuk mendukung *lazy loading* dan meningkatkan performa.  

5. **`/utils`**  
   - **Tujuan**: Menyimpan fungsi utilitas yang dibagikan di seluruh proyek, seperti `formatCurrency.ts` atau `apiClient.ts`.  
   - **Contoh**:  
     - **`auth.ts`**: Fungsi pembantu untuk validasi token JWT.  
     - **`email.ts`**: Konfigurasi SMTP dan integrasi dengan Nodemailer untuk pengiriman email.  

### **File Konfigurasi**  
- **`next.config.js`**: Digunakan untuk menyesuaikan perilaku Next.js, seperti pengaturan pengalihan (*redirects*) atau header kustom.  
- **`.env.local`**: Menyimpan variabel lingkungan sensitif (pastikan file ini tidak di-*commit* ke Git).  
- **`tsconfig.json`**: Pengaturan kompiler TypeScript, dengan mode ketat (*strict mode*) diaktifkan untuk keandalan kode.  

---

## **Skrip**  
Berikut adalah daftar skrip yang tersedia dalam `package.json` beserta deskripsinya:

| **Skrip** | **Perintah**      | **Deskripsi**                                                                 |
|-----------|-------------------|-------------------------------------------------------------------------------|
| `dev`     | `npm run dev`     | Memulai server pengembangan dengan *hot-reloading* untuk pengujian lokal.     |
| `build`   | `npm run build`   | Menghasilkan build produksi yang dioptimalkan, disimpan di folder `/.next`.   |
| `start`   | `npm run start`   | Menjalankan aplikasi dari build produksi (harus menjalankan `build` dulu).    |
| `lint`    | `npm run lint`    | Menjalankan ESLint dengan aturan bawaan Next.js untuk memastikan kualitas kode. |

---

## **Font dan Gaya**  
### **Font**  
- **Geist (oleh Vercel)**: Font default yang dioptimalkan untuk performa dan dimuat melalui `next/font`.  
  ```tsx
  // app/layout.tsx
  import { GeistSans } from 'next/font/google';
  const geist = GeistSans({ subsets: ['latin'] });
  ```  
- **Optimisasi**: Font di-*host* secara lokal untuk menghindari permintaan ke server pihak ketiga, sehingga mengurangi latensi dan mencegah pergeseran tata letak (*layout shift*).  

### **Arsitektur CSS**  
- **Gaya Global**: Didefinisikan dalam `globals.css`, termasuk variabel `:root` untuk mendukung tema.  
- **Tema**:  
  ```css
  /* styles/light.css */
  :root {
    --primary: #2563eb;
    --background: #ffffff;
  }
  ```  
  - Tema dimuat secara dinamis menggunakan komponen `Script` dari Next.js atau konteks React untuk fleksibilitas.  

---

## **Variabel Lingkungan**  
### **Konfigurasi**  
1. Buat file `.env.local` berdasarkan template yang disediakan di `.env.example`.  
2. Gunakan awalan `NEXT_PUBLIC_` untuk variabel yang perlu diakses di sisi klien (terbuka untuk browser).  

### **Contoh**  
```env
NEXT_PUBLIC_API_URL=https://api.sakuracloudid.id
SMTP_HOST=smtp.mailersakura.com  # Hanya untuk sisi server
```  

### **Keamanan**  
- Jangan pernah mengekspos rahasia seperti `SMTP_PASS` ke sisi klien.  
- Akses variabel sisi server melalui `getServerSideProps` atau rute API untuk menjaga keamanan.  

---

## **Deployment**  
### **Vercel (Disarankan)**  
1. **Langkah-langkah**:  
   - Hubungkan repositori GitHub Anda ke platform Vercel.  
   - Tambahkan variabel lingkungan melalui dashboard Vercel.  
   - Aktifkan deployment otomatis setiap kali ada *push* ke branch `main`.  

2. **Keuntungan**:  
   - Dukungan penuh untuk fitur Next.js seperti Incremental Static Regeneration (ISR), Server-Side Rendering (SSR), dan rute API.  
   - Dilengkapi CDN bawaan dan perlindungan DDoS untuk performa dan keamanan optimal.  

### **Deployment Manual**  
```bash
npm run build && npm run start  # Untuk server Node.js (contoh: AWS EC2)
```  
- Cocok untuk lingkungan server kustom, tetapi memerlukan konfigurasi tambahan seperti reverse proxy (misalnya, Nginx).  

---

## **Gambaran Fitur**  
### **1. Situs Publik**  
- **Desain Mobile-First**:  
  - Tata letak responsif dibangun dengan utilitas breakpoint Tailwind (contoh: `md:flex-row`).  
  - Gambar dioptimalkan menggunakan komponen `next/image` untuk waktu muat yang lebih cepat.  
- **Dukungan Multi-Bahasa**:  
  - Widget Google Translate diintegrasikan melalui `<script>` di `_document.tsx`.  
  - Rencana masa depan: Implementasi lokalisasi manual dengan `next-i18next`.  

### **2. Autentikasi**  
- **Alur JWT**:  
  1. Pengguna login melalui endpoint `/api/auth/login`.  
  2. Server mengembalikan token JWT yang disimpan dalam cookie `HttpOnly` untuk keamanan.  
  3. Status autentikasi di sisi klien dikelola menggunakan konteks React atau pustaka Zustand.  
- **Login Sosial**:  
  - Integrasi opsional dengan NextAuth.js untuk mendukung OAuth (contoh: Google, GitHub).  

### **3. Panel Admin (Direncanakan)**  
- **Fitur**:  
  - Operasi CRUD untuk manajemen pengguna (contoh: blokir pengguna, tetapkan peran).  
  - Antarmuka konfigurasi SMTP untuk memperbarui pengaturan email secara langsung.  
  - **Pengumuman**: Hanya satu pengumuman aktif yang ditampilkan, disimpan di basis data.  
- **Otomatisasi**:  
  - Pengingat invoice otomatis dikirim 7 hari sebelum tanggal jatuh tempo melalui *cron job*.  

### **4. Integrasi API**  
- **Gerbang Pembayaran**:  
  ```ts
  // utils/duitku.ts
  const createPayment = async (amount: number) => {
    await fetch('https://api.duitku.com/transaction', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({ apiKey: process.env.DUITKU_KEY, amount }),
    });
  };
  ```  
- **API Eksternal**:  
  - Data katalog produk diambil dari `NEXT_PUBLIC_API_URL/products`.  

### **5. Sistem Tambahan**  
- **Generasi Invoice**:  
  - Dokumen PDF dibuat menggunakan `@react-pdf/renderer` dan dikirim melalui email.  
- **Optimisasi SEO**:  
  - Rendering sisi server diimplementasikan untuk halaman seperti `/pricing` dan `/features` menggunakan `getServerSideProps`.  

---

## **Tumpukan Teknologi**  
| **Kategori**       | **Teknologi**    | **Kasus Penggunaan**                          |
|---------------------|------------------|-----------------------------------------------|
| Frontend           | Next.js 13+      | Routing, SSR, rute API                        |
| Gaya               | Tailwind CSS     | Pengembangan UI cepat dan responsif           |
| Manajemen State    | Zustand          | Manajemen state sisi klien yang ringan        |
| Autentikasi        | JWT/NextAuth     | Sesi pengguna dan manajemen peran             |
| Pembayaran         | Duitku API       | Pemrosesan pembayaran lokal (Indonesia)       |
| Email              | Nodemailer       | Email transaksional (pengingat invoice)       |

---

## **Pelajari Lebih Lanjut**  
- **[Dokumentasi Next.js](https://nextjs.org/docs)**: Panduan tentang App Router, rute API, dan optimisasi.  
- **[Tailwind CSS](https://tailwindcss.com/docs)**: Referensi kelas utilitas dan desain responsif.  
- **[Dokumentasi Duitku API](https://docs.duitku.com)**: Petunjuk integrasi gerbang pembayaran.  
- **[Nodemailer](https://nodemailer.com)**: Konfigurasi SMTP dan pembuatan templat email.  
