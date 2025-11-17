# 🚀 Panduan Deploy Shadow Finance Frontend

## ⚠️ Masalah Build Error di Windows

### Penyebab Error:
Project ini menggunakan **Yarn Workspaces** (monorepo) yang membutuhkan symlink. Di Windows, symlink memerlukan permission administrator.

Error yang muncul:
```
Error: Can't resolve '@pancakeswap\uikit\package.json'
```

### ✅ Solusi 1: Jalankan sebagai Administrator (RECOMMENDED)

1. **Tutup semua terminal/CMD yang sedang berjalan**

2. **Buka PowerShell atau CMD sebagai Administrator:**
   - Klik kanan pada PowerShell/CMD
   - Pilih "Run as Administrator"

3. **Navigasi ke folder project:**
   ```cmd
   cd C:\MyPC\MyProject\PROJECT-CRYPTO\MEMESWAP\SHADOW-SWAP\Shadow-finance-frontend-good
   ```

4. **Hapus node_modules dan reinstall:**
   ```cmd
   rmdir /s /q node_modules
   yarn install
   ```

5. **Build project:**
   ```cmd
   yarn build
   ```

### ✅ Solusi 2: Enable Developer Mode di Windows 10/11

1. Buka **Settings** → **Update & Security** → **For Developers**
2. Aktifkan **Developer Mode**
3. Restart komputer
4. Jalankan di terminal biasa:
   ```cmd
   rmdir /s /q node_modules
   yarn install
   yarn build
   ```

### ✅ Solusi 3: Gunakan npm workspaces (alternatif)

Jika masih error, coba gunakan npm:
```cmd
rmdir /s /q node_modules
del yarn.lock
npm install
npm run build
```

---

## 🌐 Deploy ke Vercel

### Persiapan:
1. Push code ke GitHub/GitLab
2. Pastikan build berhasil di local

### Langkah Deploy:

1. **Login ke [vercel.com](https://vercel.com)**

2. **Import Project:**
   - Klik "Add New Project"
   - Pilih repository Shadow-finance-frontend-good
   
3. **Konfigurasi Build:**
   - Framework: Next.js (auto-detect)
   - Root Directory: `./`
   - Build Command: `yarn build`
   - Output Directory: `.next`
   - Install Command: `yarn install`

4. **Environment Variables:**
   Tambahkan di Vercel Dashboard:
   ```
   NEXT_PUBLIC_GTAG=GTM-TLF66T4
   NEXT_PUBLIC_GRAPH_API_PROFILE=https://api.thegraph.com/subgraphs/name/pancakeswap/profile
   NEXT_PUBLIC_GRAPH_API_PREDICTION_BNB=https://api.thegraph.com/subgraphs/name/pancakeswap/prediction-v2
   NEXT_PUBLIC_GRAPH_API_PREDICTION_CAKE=https://api.thegraph.com/subgraphs/name/pancakeswap/prediction-cake
   NEXT_PUBLIC_GRAPH_API_LOTTERY=https://api.thegraph.com/subgraphs/name/pancakeswap/lottery
   NEXT_PUBLIC_GRAPH_API_NFT_MARKET=https://api.thegraph.com/subgraphs/name/pancakeswap/nft-market
   NEXT_PUBLIC_GRAPH_API_POTTERY=https://api.thegraph.com/subgraphs/name/pancakeswap/pottery
   NEXT_PUBLIC_SNAPSHOT_BASE_URL=https://hub.snapshot.org
   NEXT_PUBLIC_API_NFT=https://nft.pancakeswap.com/api/v1
   NEXT_PUBLIC_BIT_QUERY_ENDPOINT=https://graphql.bitquery.io
   ```

5. **Deploy:**
   - Klik "Deploy"
   - Tunggu 5-10 menit
   - Dapatkan URL: `https://your-project.vercel.app`

---

## 🌐 Deploy ke Netlify

### Langkah Deploy:

1. **Login ke [netlify.com](https://netlify.com)**

2. **Import Project:**
   - Klik "Add new site" → "Import an existing project"
   - Connect ke Git provider

3. **Build Settings:**
   - Build command: `yarn build`
   - Publish directory: `.next`
   - Base directory: (kosongkan)

4. **Environment Variables:**
   Sama seperti Vercel di atas

5. **Deploy:**
   - Klik "Deploy site"
   - Tunggu build selesai

---

## 🔗 Hubungkan Domain Custom

### Untuk Vercel:

1. **Di Vercel Dashboard:**
   - Buka project → Settings → Domains
   - Klik "Add" → masukkan domain (contoh: shadowfinance.com)

2. **Di DNS Provider (Namecheap/GoDaddy/Cloudflare):**
   
   **Untuk domain root (shadowfinance.com):**
   ```
   Type: A
   Name: @
   Value: 76.76.21.21
   TTL: Automatic
   ```

   **Untuk subdomain (www.shadowfinance.com):**
   ```
   Type: CNAME
   Name: www
   Value: cname.vercel-dns.com
   TTL: Automatic
   ```

3. **Tunggu DNS Propagation:** 5-30 menit
4. **SSL otomatis aktif** setelah domain terverifikasi

### Untuk Netlify:

1. **Di Netlify Dashboard:**
   - Site settings → Domain management → Add custom domain

2. **Di DNS Provider:**
   
   **Untuk domain root:**
   ```
   Type: A
   Name: @
   Value: 75.2.60.5
   TTL: Automatic
   ```

   **Untuk subdomain:**
   ```
   Type: CNAME
   Name: www
   Value: your-site.netlify.app
   TTL: Automatic
   ```

3. **SSL otomatis aktif** via Let's Encrypt

---

## 📝 Checklist Deployment:

- [ ] Build berhasil di local (`yarn build`)
- [ ] Code sudah di-push ke GitHub/GitLab
- [ ] Environment variables sudah dikonfigurasi
- [ ] Deploy ke Vercel/Netlify berhasil
- [ ] Domain sudah dibeli
- [ ] DNS records sudah ditambahkan
- [ ] SSL certificate aktif
- [ ] Website bisa diakses via domain

---

## 🆘 Troubleshooting:

**Build gagal di Vercel/Netlify:**
- Cek logs di dashboard
- Pastikan semua environment variables sudah benar
- Vercel biasanya lebih baik untuk Next.js

**Domain tidak bisa diakses:**
- Tunggu DNS propagation (bisa sampai 48 jam)
- Cek DNS dengan: https://dnschecker.org
- Pastikan DNS records sudah benar

**SSL tidak aktif:**
- Tunggu beberapa menit setelah domain terverifikasi
- Vercel/Netlify akan otomatis provision SSL
