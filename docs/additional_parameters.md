# Parameter Tambahan

Parameter/asumsi di luar soal. Setiap kali menambah asumsi di model, tambahkan satu baris di sini.

| Parameter | Nilai | Alasan | Dipakai di model |
|---|---|---|---|
| Target utilisasi desain | <= 85% | Dasar jumlah server: c = ceil(λ·E[S] / 0,85). Hasil: 12 desk Eco, 3 desk Prio, 6 lane Reg, 3 lane Prio, 3 gate | B, C |
| Aturan flex desk Priority | Ambil dari `PrioCheckInQueue` kalau ada antrian; kalau kosong, layani `EcoCheckInQueue` | Memanfaatkan waktu idle desk Priority tanpa menambah server | C |
| Aturan flex lane Priority | Ambil dari `PrioSecurityQueue` kalau ada antrian; kalau kosong, layani `EcoSecurityQueue` | Memanfaatkan waktu idle lane Priority tanpa menambah server | C |
| Durasi run | 4 jam (240 menit) | Sistem terminating | A, B, C |
| Warm-up | 0 (tanpa warm-up) | Sistem terminating, mulai dari kondisi kosong | A, B, C |
| Waktu jalan ke check-in | Triangular(min 1, mode 2, max 3) menit | Sesuai cfg (`WalkToCheckInDist`) | A, B, C |
| Waktu jalan check-in ke security | Triangular(min 1, mode 2, max 4) menit | Sesuai cfg (`WalkToSecurityDist`) | A, B, C |
| Waktu jalan security ke lounge/gate | Triangular(min 2, mode 4, max 6) menit | Sesuai cfg (`WalkToLoungeDist`) | A, B, C |
|  |  |  |  |
