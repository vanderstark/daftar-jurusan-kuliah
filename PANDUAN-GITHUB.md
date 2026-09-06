# 📚 Panduan Push ke GitHub Repo Baru & Cara Menggunakan

Dokumentasi ini menjelaskan cara membuat repo baru, push file ke GitHub, dan menggunakan repositori yang sudah dibuat.

---

## 📋 **Daftar Isi**

1. [Syarat Awal](#1-syarat-awal)
2. [Langkah-langkah Membuat Repo Baru & Push](#2-langkah-langkah-membuat-repo-baru--push)
3. [Mengakses Repo di GitHub](#3-mengakses-repo-di-github)
4. [Menggunakan Repo untuk Riset](#4-menggunakan-repo-untuk-riset)
5. [Memperbarui Repo](#5-memperbarui-repo)
6. [Pertanyaan Umum](#6-pertanyaan-umum)

---

## 1. Syarat Awal

Sebelum memulai, pastikan:

### ✅ **GitHub CLI Terinstal**
```bash
gh --version
```
Jika belum terinstal:
```bash
sudo apt update && sudo apt install gh -y
```

### ✅ **Login ke GitHub**
```bash
gh auth login
```
- Pilih `HTTPS` sebagai protokol.
- Login dengan username dan personal access token (PAT).
- Verifikasi dengan: `gh auth status`

### ✅ **Git Terinstal**
```bash
git --version
```
Jika belum:
```bash
sudo apt install git -y
```

---

## 2. Langkah-langkah Membuat Repo Baru & Push

### **Langkah 1: Buat Direktori Kerja**
```bash
mkdir -p /opt/data/nama-repo-baru
cd /opt/data/nama-repo-baru
git init
```

### **Langkah 2: Buat atau Tambahkan File**
```bash
# Contoh: Buat README.md
cat > README.md << 'EOF'
# 📚 Nama Repo
Deskripsi dari repo ini.
EOF
```

### **Langkah 3: Buat Repo di GitHub**
```bash
gh repo create vanderstark/nama-repo-baru --public --description "Deskripsi repo" 2>&1
```

### **Langkah 4: Tambahkan Remote & Push**
```bash
# Set remote URL
git remote add origin https://github.com/vanderstark/nama-repo-baru.git

# Commit semua file
git add .
git commit -m "Initial commit: Deskripsi repo"

# Rename branch ke main
git branch -m main

# Push ke GitHub
git push -u origin main
```

### **Langkah 5: Verifikasi Push**
```bash
git push https://$(gh auth token)@github.com/vanderstark/nama-repo-baru.git main 2>&1
```

---

## 3. Mengakses Repo di GitHub

### **Opsi 1: Melalui Browser**
1. Buka browser.
2. Kunjungi: `https://github.com/vanderstark/nama-repo-baru`
3. Lihat file, README, commit history, dll.

### **Opsi 2: Melalui GitHub CLI**
```bash
# Lihat info repo
gh repo view vanderstark/nama-repo-baru --json name,description,url

# Clone repo ke lokal
gh repo clone vanderstark/nama-repo-baru /opt/data/nama-repo-baru

# Lihat list file
gh api repos/vanderstark/nama-repo-baru/contents --jq '.[].name'
```

### **Opsi 3: Melalui Git Clone**
```bash
git clone https://github.com/vanderstark/nama-repo-baru.git /opt/data/nama-repo-baru
```

---

## 4. Menggunakan Repo untuk Riset

### **Kasus: Repo "daftar-jurusan-kuliah"**

Repositori yang sudah dibuat berisi daftar jurusan kuliah di Indonesia dengan kelebihan dan kekurangan.

#### 📖 **Mengakses Repo**
- **Link:** https://github.com/vanderstark/daftar-jurusan-kuliah
- **File utama:** `README.md` (berisi seluruh daftar jurusan)

#### 🔍 **Cara Menggunakan**
1. **Baca langsung di GitHub:**
   - Kunjungi link di atas.
   - Scroll ke bawah untuk melihat daftar lengkap.

2. **Clone ke lokal:**
   ```bash
   git clone https://github.com/vanderstark/daftar-jurusan-kuliah.git /opt/data/daftar-jurusan-kuliah
   ```
   - Edit file lokal.
   - Commit dan push perubahan:
     ```bash
     cd /opt/data/daftar-jurusan-kuliah
     git add .
     git commit -m "Update: Tambah jurusan baru"
     git push origin main
     ```

3. **Gunakan sebagai referensi:**
   - File `README.md` bisa dijadikan template untuk proyek lain.
   - Tambahkan kategori baru, perbarui data, atau terapkan struktur ini ke repo lain.

---

## 5. Memperbarui Repo

### **Langkah-langkah Update**
```bash
# 1. Navigasi ke direktori repo
cd /opt/data/nama-repo-baru

# 2. Pull perubahan terbaru dari GitHub
git pull origin main

# 3. Edit file
nano README.md  # atau gunakan editor lain

# 4. Commit dan push
git add .
git commit -m "Update: Deskripsi perubahan"
git push origin main
```

### **Menambahkan File Baru**
```bash
# Buat file baru
echo "Konten file baru" > file-baru.md

# Commit dan push
git add file-baru.md
git commit -m "Add: file-baru.md"
git push origin main
```

---

## 6. Pertanyaan Umum

### **Q1: Error "could not read Username" saat push?**
Gunakan token GitHub:
```bash
git push https://$(gh auth token)@github.com/vanderstark/nama-repo-baru.git main
```

### **Q2: Repo tidak muncul di GitHub?**
Pastikan push berhasil dan tidak ada error:
```bash
gh repo list vanderstark --limit 100 --json name
```

### **Q3: Bagaimana cara fork repo orang lain?**
```bash
gh repo fork vanderstark/nama-repo --clone
```

### **Q4: Bagaimana cara delete repo?**
```bash
gh repo delete vanderstark/nama-repo --yes
```

### **Q5: Bagaimana cara menjadikan repo private?**
```bash
gh repo edit vanderstark/nama-repo --visibility=private
```

---

## 📋 **Ringkasan Perintah Esensial**

| Perintah | Fungsi |
|----------|--------|
| `gh auth login` | Login ke GitHub |
| `gh auth status` | Cek status login |
| `gh repo create <repo> --public` | Buat repo baru |
| `gh repo list vanderstark` | Daftar repo milik user |
| `gh repo clone <repo> <path>` | Clone repo ke lokal |
| `git add .` | Tambahkan semua file ke staging |
| `git commit -m "msg"` | Commit file |
| `git push origin main` | Push ke GitHub |
| `git pull origin main` | Pull perubahan dari GitHub |

---

## 🧪 **Verifikasi Repo "daftar-jurusan-kuliah"**

Repo yang sudah dibuat:
- **Nama:** `daftar-jurusan-kuliah`
- **Owner:** `vanderstark`
- **Visibilitas:** Public
- **Link:** https://github.com/vanderstark/daftar-jurusan-kuliah
- **File:** `README.md` (576 baris, berisi daftar lengkap jurusan kuliah)
- **Status:** ✅ Sudah di-push dan terverifikasi

---

**Dokumentasi ini dibuat oleh [vanderstark](https://github.com/vanderstark) untuk keperluan edukasi.**

*Terakhir diperbarui: September 2025*
