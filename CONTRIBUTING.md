# Aturan Kerja Tim (biar tidak conflict)

Prinsip utama: **satu file dikerjakan satu orang pada satu waktu**. Git tidak bisa menggabungkan `.xlsx`, `.docx`, `.pptx`, dan log; kalau dua orang mengubahnya bersamaan, salah satu hasil kerja harus dibuang. Cfg dan notebook memang teks, tapi hasil merge-nya mudah rusak.

## Setup (sekali saja, tiap anggota)

```bash
git clone <URL-REPO>
cd airport-terminal-des
git config user.name "Nama Kamu"
git config user.email "email-github-kamu"
pip install -r requirements.txt
```

## Alur kerja harian

```bash
# 1. Mulai dari main terbaru
git switch main
git pull

# 2. Buat branch sendiri (format: nama/tugas)
git switch -c budi/log-model-b

# 3. Kerja, lalu cek apa saja yang berubah
git status

# 4. Commit hanya file yang kamu kerjakan (hindari "git add .")
git add models/B_proposed_1
git commit -m "Tambah log model B"

# 5. Push, lalu buat Pull Request di GitHub
git push -u origin budi/log-model-b
```

Setelah PR dicek satu teman: **Merge**, hapus branch, lalu semua orang `git switch main` dan `git pull`. Buat PR kecil dan sering; jangan menumpuk kerja berhari-hari.

Kalau `main` sudah berubah saat kamu masih kerja: commit dulu, lalu `git pull --no-rebase origin main` di branch kamu.

## Pembagian file (isi nama)

| Bagian | File | PIC |
|---|---|---|
| Model A | `models/A_existing/` | .......... |
| Model B | `models/B_proposed_1/` | .......... |
| Model C | `models/C_proposed_2/` | .......... |
| Notebook dan grafik | `analysis/JaamSim_Log_Analysis.ipynb`, `analysis/figures/` | .......... |
| Perhitungan teori | `analysis/analytical/` | .......... |
| Report | `report/` | .......... |
| Slide | `presentation/` | .......... |

Mau ubah file milik orang lain? Kabari PIC di grup dulu.

## Aturan per jenis file

**`.cfg`**
- Jangan ganti nama file. Hanya PIC yang mengubah dan menyimpan.
- Cuma mau lihat? Boleh, tapi **jangan Save** di JaamSim. Menggeser objek lalu Save juga mengubah cfg.
- Kalau cfg berubah tanpa sengaja (kelihatan di `git status`): `git restore path/ke/file.cfg`. Perhatian: ini membuang perubahan di file itu.

**`.log` dan `.rep`**
- Setiap run menimpa file lama, jadi hanya PIC model yang commit hasil run.
- Commit **keempat file dari run yang sama** (3 log + 1 rep), bersama cfg kalau cfg-nya berubah.
- Tutup JaamSim dulu sebelum `git pull` atau pindah branch, supaya file tidak terkunci.
- Jangan edit manual.

**Notebook `.ipynb`**
- Sebelum commit: **Clear All Outputs**, lalu save.
- Ganti `MODEL` hanya untuk run lokal; kembalikan ke `'A_existing'` sebelum commit.

**Grafik `.png`**
- Hanya PIC notebook yang generate dan commit, setelah semua log final.

**Report, slide, dan Excel**
- Paling aman: kerjakan bareng di Google Docs/Slides/Sheets, lalu PIC export versi final ke repo.
- Kalau tetap pakai Word/PowerPoint/Excel lokal: bilang di grup "lagi edit X" dan "selesai X, sudah push".

**`submission/`** tidak masuk Git. Buat lokal saat mau submit.

## Kalau terlanjur conflict

`git status` menunjukkan file mana yang conflict. Untuk cfg, log, rep, Office, dan png: jangan gabung manual, pilih satu versi utuh. Saat conflict muncul karena `git pull --no-rebase origin main` di branch kamu:

```bash
git checkout --ours path/file     # pakai versi branch kamu
git checkout --theirs path/file   # pakai versi dari main
git add path/file
git commit
```

Pilih sisi yang sama untuk cfg, log, dan rep satu model supaya tetap cocok. Kalau ragu, jalankan ulang modelnya. Bingung? `git merge --abort` untuk batal, lalu tanya di grup.

## Jangan

- Push langsung ke `main`
- `git push --force`
- Commit zip, atau rename/pindah folder tanpa kabar ke grup
