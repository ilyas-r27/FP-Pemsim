# Airport Terminal DES

Simulasi discrete-event terminal keberangkatan bandara dengan **JaamSim** (Final Project Pemodelan dan Simulasi). Penumpang Economy (70%) dan Priority (30%) datang dengan inter-arrival Exponential (mean 12 detik), lalu melewati check-in, security, dan boarding gate. Tiga model dibandingkan lewat utilisasi, antrian, cycle time, dan throughput.

> Anggota tim: baca [CONTRIBUTING.md](CONTRIBUTING.md) sebelum mulai kerja, supaya tidak conflict.

## Ringkasan model

| Model | File cfg | Jumlah server | Keterangan |
|---|---|---|---|
| **A, Existing** | `Existing_System.cfg` | 8 (check-in 1 Eco + 1 Prio, security 2 Reg + 2 Prio, gate 2) | Kondisi awal |
| **B, Proposed 1** | `Proposed_System_1.cfg` | 27 (check-in 12 Eco + 3 Prio, security 6 Reg + 3 Prio, gate 3) | Server dedicated per kelas, target utilisasi <= 85% |
| **C, Proposed 2** | `Proposed_System_2.cfg` | 27 (sama dengan B) | Desk dan lane Priority melayani Economy saat antrian Priority kosong |

Asumsi dan parameter tambahan: [docs/additional_parameters.md](docs/additional_parameters.md).

## Struktur folder

```
airport-terminal-des/
├── README.md
├── CONTRIBUTING.md          # aturan kerja tim (Git)
├── requirements.txt
├── group_members.txt
├── docs/                    # problem statement, parameter tambahan
├── models/
│   ├── A_existing/          # cfg + log + .rep
│   ├── B_proposed_1/
│   └── C_proposed_2/
├── analysis/
│   ├── JaamSim_Log_Analysis.ipynb
│   ├── analytical/          # .xlsx perhitungan teori
│   └── figures/             # grafik per model + comparison
├── report/
├── presentation/
└── submission/              # lokal saja, tidak masuk Git
```

## Menjalankan model di JaamSim

1. Buka cfg langsung dari folder modelnya, misalnya `models/B_proposed_1/Proposed_System_1.cfg` (versi yang dipakai: JaamSim 2026-05).
2. Tekan **Run** sekali dan tunggu sampai selesai (4 jam waktu simulasi).
3. **Jangan reset** setelah selesai. Log dan `.rep` otomatis muncul di folder yang sama dengan cfg.
4. Pastikan di folder model ada 4 file: `<cfg>-ArrivalLogger.log`, `<cfg>-PassengerLogger.log`, `<cfg>-QueueLogger.log`, `<cfg>.rep`.

**Jangan ganti nama cfg**, karena nama log mengikuti nama cfg dan dibaca otomatis oleh notebook.

## Menjalankan notebook

```bash
pip install -r requirements.txt
```

1. Buka `analysis/JaamSim_Log_Analysis.ipynb` di VS Code.
2. Di section 2, pilih `MODEL = 'A_existing'`, `'B_proposed_1'`, atau `'C_proposed_2'`.
3. **Run All**. Grafik tersimpan di `analysis/figures/<MODEL>/`; grafik perbandingan di `analysis/figures/comparison/`.

Di Google Colab: jalankan cell Upload lalu pilih file log dan `.rep`.

## Checklist deliverable FP (deadline **3 Desember 2026**)

- [ ] 3 file cfg: Existing, Proposed 1, Proposed 2
- [ ] Log model A (Existing), `.log` dan `.rep`
- [ ] Log model B (Proposed 1), `.log` dan `.rep`
- [ ] Log model C (Proposed 2), `.log` dan `.rep`
- [ ] Report, maks 15 halaman
- [ ] Slide presentasi, maks 15 halaman
- [ ] File nama anggota (`group_members.txt`)
- [ ] Semua di-zip, satu zip per cluster
