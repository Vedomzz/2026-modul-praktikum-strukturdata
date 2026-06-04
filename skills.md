---
description: Alur Evaluasi Manual Praktikum Struktur Data (Agent Skill/Workflow)
---
# Alur Evaluasi Manual Praktikum Struktur Data

File instruksi ini memandu AI Assistant untuk mengevaluasi repositori mahasiswa kelas Struktur Data secara **manual satu-per-satu**. Pendekatan ini menjamin integritas evaluasi melalui validasi test dan code review individual.

> ⚠️ **DILARANG** menggunakan skrip Python otomatis `generate` kasar untuk evaluasi massal. Setiap mahasiswa harus dievaluasi secara komparatif dengan ketelitian tinggi.

---

## 1. Persiapan Laporan

- Buat direktori `Hasil-Evaluasi-Kelas-X/` (X = A, B, dst).
- Di dalamnya:
  - Satu `README.md` berisi tabel rekapitulasi nilai + catatan khusus.
  - Satu file `Evaluasi_NIM_NamaLengkap_username.md` per mahasiswa.

---

## 2. Pemahaman Soal

- Baca `01-modul.md`, `02-modul.md`, dst. di root project untuk memahami soal tugas setiap modul.
- Identifikasi apa yang seharusnya diimplementasikan mahasiswa (method, output, validasi test case).

---

## 3. Penyusuran Direktori Mahasiswa

- Clone repositori global: `gh classroom clone student-repos` (atau `git pull` jika sudah ada).
- Folder mahasiswa biasanya berada di `strukturdata-{a|b}-submissions/strukturdata-{a|b}-{username}/`.
- Saring folder `.git` dan repositori non-relevan.
- Struktur internal mahasiswa **bervariasi** — bisa `minggu 1/`, `Minggu1/`, `Modul-01/`, `tugas/week-1/`, dll. Jangan asumsikan satu pola.

---

## 4. Verifikasi Isi Folder

- `list_dir` setiap folder mahasiswa per minggu.
- Cek apakah file tugas (`Tugas1_*.py`, `Tugas2_*.py`, `Tugas3_*.py`) ada di lokasi yang diharapkan **atau** folder alternatif (`Tugas/`, `Tugas 2/`, dst.).
- Jika ekstensi `.py` hilang (mis. `tugas1_NIM` tanpa `.py`), tetap test dengan Python interpreter — namun **kenakan penalti -15 per tugas** (lihat bagian 7).

---

## 5. Testing Execution

**Perintah standar:**
```bash
PYTHONIOENCODING=utf-8 python "path/ke/file.py" 2>&1
```

- Selalu set `PYTHONIOENCODING=utf-8` — Windows console default cp1252 sering error untuk emoji/unicode dalam test output.
- Tambahkan `2>&1` untuk capture stderr (error message dari interpreter).

**Kasus khusus — Windows path invalid:**
File/folder dengan karakter invalid di Windows (mis. titik di akhir: `Shafwat Azzah H. L.`) tidak dapat di-checkout. Gunakan:
```bash
git show origin/main:"path/ke/file.py" | python
```

---

## 6. Validasi Hasil — Tidak Cukup Hanya "PASSED"

Wajib cek **3 hal**:

1. **Test case lulus** — semua `✓ Test ... PASSED` dan tidak ada `AssertionError`/exception.
2. **Konten file sesuai tugas** — banyak mahasiswa submit file salah:
   - File praktikum dikumpulkan sebagai tugas (mis. `ArrayStack.py` bukan Browser History).
   - Kode modul lain dicopy ke folder modul ini (mis. M5 Browser History dicopy ke folder M6 sebagai T3 Bank Queue).
   - File template kosong/placeholder (1–2 baris).
3. **Output masuk akal** — bukan cuma PASSED, validasi nilai numerik:
   - Avg waiting time bank queue **harus positif** (negatif = logika salah).
   - Total execution time Round Robin scheduler harus sesuai (mis. 12 detik).
   - Right-associativity `^`: `A^B^C` harus jadi `A B C ^ ^` (bukan `A B ^ C ^`).

---

## 7. Konvensi Penilaian

### Skor per Tugas
| Kondisi | Nilai |
|---|---|
| Test lulus + konten benar | 100 |
| File tidak ada / tidak dikumpul | 0 |
| Test gagal / error fatal | 0 |
| Konten salah (file praktikum, modul lain, placeholder) | 0 |
| Test lulus tapi terlambat | max 50 |
| Test lulus tapi tanpa ekstensi `.py` | -15 (jadi 85) |
| Bug minor (mis. 1 method gagal dari N method) | proportional |

### Skor per Modul
Rata-rata 3 tugas: `(T1 + T2 + T3) / 3`

Contoh: `(100 + 100 + 0) / 3 = 67`

### Skor Rata-Rata
Rata-rata semua modul yang sudah dievaluasi: `(M1 + M2 + ... + Mn) / n`

### Notasi di README
- **`-`** = belum dievaluasi (asisten belum cek)
- **`0`** = sudah dievaluasi, tapi tidak ada submission / error fatal
- **angka lain (1–100)** = sudah dievaluasi dengan nilai tersebut

Jangan campur aduk `-` dan `0`. Setelah dievaluasi, `-` harus diganti `0` jika tidak ada submission.

### Badge Warna
| Nilai | Warna Badge |
|---|---|
| ≥ 90 | `success` (hijau) |
| ≥ 70 | `yellowgreen` |
| ≥ 50 | `orange` |
| < 50 | `red` |

Format: `![Score](https://img.shields.io/badge/Score-XX.XX-{warna})`

---

## 8. Format File `Evaluasi_NIM_NamaLengkap_username.md`

```markdown
# 📝 Laporan Evaluasi Terperinci - Praktikum Struktur Data

---

## 👤 Data Mahasiswa
- **Nama:** {Nama Lengkap}
- **NIM:** {NIM}
- **Kelas:** Struktur Data {A|B}
- **GitHub Username:** `{username}`

---

## 🥇 Hasil Evaluasi Modul 1: {Judul Modul}

### 1. Tugas 1: {Judul Tugas}
- **Pengecekan Kode:** {ringkas, 1–2 kalimat tentang implementasi}
- **Hasil Testing Terminal:** **PASSED** ✅ (100%) / **FAILED** ❌ (0%)

### 2. Tugas 2: ...
### 3. Tugas 3: ...

**✨ NILAI MODUL 1: {nilai} ✨**

---

## (ulang untuk modul lain)

---
### **🏆 NILAI RATA-RATA (Modul 1-N): {avg} 🏆**

*Penilaian dievaluasi secara statis-manual berdasarkan kode program dan divalidasi melalui eksekusi unit test satu per satu.*
```

---

## 9. Format `Hasil-Evaluasi-Kelas-X/README.md`

```markdown
# Laporan Evaluasi Praktikum Struktur Data (Kelas X) - Modul 1, 2, ..., N

| No | Nama Lengkap | NIM | GitHub Username | M1 | M2 | ... | Mn | Nilai Rata-rata | Detail Evaluasi |
|---:|:---|:---|:---|:---:|:---:|:---:|:---:|:---|
| 1 | **{Nama}** | {NIM} | `{user}` | 100 | 100 | ... | ![Score](...) | [Lihat Laporan](Evaluasi_{NIM}_{Nama}_{user}.md) |
...

## 📝 Catatan Khusus Evaluasi
1. **{Nama} ({NIM}):** {penjelasan kasus tidak normal}
...
```

**Catatan khusus** hanya untuk:
- Mahasiswa dengan kasus tidak normal (file salah konten, late submission, dual account GitHub, NIM tidak sesuai, dll.).
- **Jangan** catat mahasiswa dengan nilai penuh — tidak ada yang perlu dijelaskan.

---

## 10. NIM Verification

Jika username GitHub ambigu atau mahasiswa tidak mencantumkan nama (mis. `strukturdata-b-Vedomzz`):
- Cek header file kode (`# NIM: 10251084`) untuk konfirmasi identitas.
- Cross-check dengan daftar mahasiswa resmi jika tersedia.
- Jangan asumsikan NIM dari username — selalu verifikasi.

---

## 11. Handling Feedback Mahasiswa Pasca-Evaluasi

Jika mahasiswa komplain bahwa nilainya salah:
1. **Re-test** file yang dikomplain dengan command yang sama.
2. **Verifikasi root cause** — apakah bug di kode mahasiswa atau kesalahan evaluasi.
3. **Update jika valid**:
   - Bug di kode mahasiswa → nilai **tetap** (kesalahan dia, bukan kita).
   - File ada tapi terlewat saat evaluasi → **koreksi nilai** + update eval file + README + catatan.
   - Data salah (NIM, nama) → **koreksi** + rename file eval jika perlu.
4. **Dokumentasikan** perubahan di catatan khusus README jika kasusnya tidak normal.

---

## 12. Larangan & Best Practices

- ❌ **Jangan** pakai skrip Python otomatis untuk generate nilai massal **per-tugas evaluasi**. Setiap tugas mahasiswa harus dicek manual via execution + validasi konten.
- ❌ **Jangan** asumsikan struktur folder mahasiswa seragam — cek manual per mahasiswa.
- ❌ **Jangan** mark file sebagai "tidak ada submission" tanpa cek folder alternatif (mis. `Tugas/` di root mahasiswa, bukan `Minggu1/Tugas/`).
- ❌ **Jangan** terburu-buru menambahkan catatan khusus untuk semua mahasiswa — hanya yang bermasalah.
- ✅ Selalu validasi konten file, bukan cuma test PASSED.
- ✅ Selalu set `PYTHONIOENCODING=utf-8`.
- ✅ Selalu cross-check NIM dari header kode jika username ambigu.
- ✅ Selalu update `README.md` + file `Evaluasi_*.md` + catatan secara konsisten setelah perubahan nilai.
- ✅ **Boleh** pakai script `compute_final_grades.py` untuk **agregasi nilai final** (lihat section 13–16) — script ini bukan untuk evaluasi per-tugas, tapi untuk hitung nilai akhir berbobot.

---

## 13. Komposisi Nilai Final & Konversi Huruf

### Bobot Nilai Final

| Komponen | Bobot | Sumber Data |
|---|---:|---|
| Praktikum | 30% | Rata-rata semua modul (M1-M7, M9-Mn) dari README evaluasi |
| Kuis | 10% | Excel `PRESENSI PRAKTIKUM STRUKTUR DATA.xlsx` sheet `Kuis dan UTS KELAS X` |
| UTS | 25% | Excel sheet `Kuis dan UTS KELAS X` (atau hasil remedial — lihat section 16) |
| UAS | 25% | Belum ada (placeholder `-`) |
| Kehadiran | 10% | Excel sheet `KELAS X` minggu 1-15 |

### Kehadiran (rumus)

- `HADIR = 1`, `IZIN`/`SAKIT = 0.5`, `TANPA KETERANGAN`/`ALPA = 0`.
- Sel **kosong di minggu yang sudah berjalan** (auto-detect dari kelas) → dianggap **alpa**.
- Sel kosong di minggu yang **belum berjalan** → **skip**.
- Skor kehadiran = `(sum / total minggu sudah berjalan) × 100`.

### Konversi Huruf (batas bawah inklusif)

| Range | Huruf |
|---|:---:|
| ≥ 86 | A |
| 76 ≤ x < 86 | AB |
| 66 ≤ x < 76 | B |
| 56 ≤ x < 66 | BC |
| 51 ≤ x < 56 | C |
| 41 ≤ x < 51 | D |
| < 41 | E |

### Formula Nilai Sementara (saat UAS belum ada)

```
Nilai Sementara = (Praktikum × 0.30 + Kuis × 0.10 + UTS × 0.25 + Hadir × 0.10) / 0.75
```

Normalisasi `/0.75` karena UAS belum dilaksanakan; asumsi UAS = rata-rata komponen lain.

### Formula Nilai Final (saat UAS sudah ada)

```
Nilai Final = Praktikum × 0.30 + Kuis × 0.10 + UTS × 0.25 + UAS × 0.25 + Hadir × 0.10
```

---

## 14. Script `compute_final_grades.py` — Workflow Nilai Final

File ini terletak di root project dan menghasilkan `Hasil-Evaluasi-Kelas-A/Nilai-Final-Kelas-A.md` + `Hasil-Evaluasi-Kelas-B/Nilai-Final-Kelas-B.md`.

### Struktur Script

```python
# 1. Komposisi bobot (jangan diubah kecuali kebijakan berubah)
BOBOT = {'praktikum': 0.30, 'kuis': 0.10, 'uts': 0.25, 'uas': 0.25, 'hadir': 0.10}

# 2. Skor praktikum HARDCODED per NIM (rata-rata semua modul yang sudah dievaluasi)
PRAKTIKUM_A = {10231081: 92.45, 10251002: 94.00, ...}
PRAKTIKUM_B = {10231001: 97.00, ...}

# 3. Override dicts (kondisi khusus yang tidak bisa di-derive dari Excel)
ATTENDANCE_OVERRIDE = {'A': {10251041: 0.0, ...}, 'B': {}}
KUIS_OVERRIDE       = {'A': {}, 'B': {10251115: 60}}     # Excel salah/kosong
UTS_FINAL_OVERRIDE  = {'A': {10251002: 65, ...}, 'B': {...}}  # hasil remedial
```

### Cara Menjalankan

```bash
cd <root project>
PYTHONIOENCODING=utf-8 python compute_final_grades.py
```

Output: regenerate kedua file `Nilai-Final-Kelas-X.md`.

### Sumber Data per Komponen (Prioritas Tinggi → Rendah)

| Komponen | 1. Override Dict | 2. Excel | 3. Praktikum Dict |
|---|---|---|---|
| Praktikum | — | — | `PRAKTIKUM_A` / `PRAKTIKUM_B` |
| Kuis | `KUIS_OVERRIDE` | Excel `Kuis dan UTS KELAS X` | — |
| UTS | `UTS_FINAL_OVERRIDE` | Excel | — |
| Kehadiran | `ATTENDANCE_OVERRIDE` | Excel sheet `KELAS X` | — |

### ⚠️ PENTING — Jangan Edit Langsung File `.md`

File `Nilai-Final-Kelas-X.md` **selalu** diregenerasi oleh script. Edit manual akan **hilang** saat re-run.

Kalau ada koreksi nilai, **masukkan ke override dict di script**, bukan edit file `.md`.

---

## 15. Pola Menambah Data Baru (Modul Lanjutan, Kuis Susulan, UAS)

### Menambah Modul Praktikum Lanjutan (mis. M13, M14, M15)

1. Lakukan **evaluasi per-tugas** (section 1–11) untuk Modul N.
2. Update `README.md` Hasil-Evaluasi-Kelas-X dengan kolom MN baru + nilai per mhs + catatan khusus.
3. Update `Evaluasi_*.md` per mahasiswa dengan section MN + tabel rata-rata baru.
4. Hitung ulang rata-rata praktikum per mhs (skema baru: `(M1+...+Mn)/n_modul`).
5. **Update `PRAKTIKUM_A` / `PRAKTIKUM_B`** di `compute_final_grades.py` dengan nilai rata-rata baru.
6. Re-run `compute_final_grades.py` — `Nilai-Final-Kelas-X.md` otomatis ter-update.

### Menambah Kuis Susulan / Koreksi Kuis

```python
KUIS_OVERRIDE = {
    'B': {
        10251115: 60,    # contoh yang sudah ada
        10251XXX: <nilai>,  # tambah di sini
    },
}
```

Lalu re-run script.

### Input UAS (saat UAS selesai)

1. Tambah dict baru di script:
   ```python
   UAS_SCORES = {
       'A': {10231081: 75, 10251002: 80, ...},
       'B': {...},
   }
   ```
2. Ubah fungsi `compute_nilai_sementara()` jadi `compute_nilai_final()`:
   - Hapus normalisasi `/ 0.75`.
   - Tambah `uas` sebagai parameter.
   - Formula: `(p*0.30 + k*0.10 + u*0.25 + uas*0.25 + h*0.10)`.
3. Di main loop, ambil `uas = UAS_SCORES.get(kelas, {}).get(nim)`. Kalau None, biarkan kolom UAS `-` dan pakai formula sementara (untuk mhs yang tidak ikut UAS).
4. Update teks deskripsi di markdown output: hapus "UAS belum dilaksanakan".
5. Re-run script.

---

## 16. Workflow Remedial UTS

### Kriteria & Kebijakan Default

- **Berhak remedial:** mahasiswa dengan UTS < 66.
- **Cap nilai remedial:** maksimal **65** (jangan ubah tanpa konfirmasi dosen).
- **Formula:** `UTS_final = MAX(UTS_asli, MIN(UTS_remedial, 65))`.
  - Kalau UTS_asli > UTS_remedial → pakai UTS_asli (mahasiswa tidak rugi).
  - Kalau UTS_remedial > UTS_asli → pakai UTS_remedial (max 65).

### Format Submission Mahasiswa

Folder `Remedial-UTS/` di repo classroom mereka, berisi:
```
README.md                 ← identitas + analisis Big-O + jawaban teori
Soal1_<Topik>_<NIM>.py
Soal2_<Topik>_<NIM>.py
Soal3_<Topik>_<NIM>.py
```

### Penalti yang Diterapkan

| Kondisi | Penalti |
|---|---|
| File error fatal (SyntaxError/IndentError/RuntimeError) | Soal terkait dapat 0 |
| File MISSING | Soal terkait dapat 0 |
| File tanpa ekstensi `.py` | -15 per soal |
| README minim/tidak ada | -15 dari nilai total |
| Suspect copy (similarity AST ≥ 0.85) di set sama | Soal terkait dapat 0 untuk **kedua belah pihak** |

### Workflow Pemeriksaan

1. `git pull` semua repo classroom (atau re-clone untuk yang baru).
2. Cek folder `Remedial-UTS/` (variasi nama: `Remedial UTS`, `remedial-uts`, dll).
3. Run setiap `Soal{1,2,3}.py` dengan `PYTHONIOENCODING=utf-8 python ...`.
4. Cek README ada/tidak + isi (identitas, Big-O, jawaban teori).
5. **Similarity check** AST token-based antar mhs di **set sama** (threshold ≥ 0.85 = SUSPECT).
6. Hitung skor per rubrik (S1=25, S2=25, S3=30, README=20).
7. Cap maksimal 65.
8. Tulis **Hasil-Remedial-Kelas-X.md** di folder `Remedial-UTS/` (tabel skor + catatan khusus).
9. Update `UTS_FINAL_OVERRIDE` di `compute_final_grades.py` untuk mhs yang skor naik.
10. Re-run script untuk regenerate Nilai-Final.

### Pola UTS_FINAL_OVERRIDE

```python
UTS_FINAL_OVERRIDE = {
    'A': {
        10251002: 65,  # Dina (asli 30, remedial cap 65)
        # ...
        # Mhs yang remedial-nya < UTS asli TIDAK di-override (biar tetap pakai UTS asli)
    },
}
```

---

## 17. Best Practices Spesifik Nilai Final

- ✅ Pakai `compute_final_grades.py` untuk semua agregasi nilai final.
- ✅ Setiap koreksi nilai → masukkan ke override dict, bukan edit file `.md`.
- ✅ Dokumentasikan alasan di **comment** di sebelah baris override (mis. `# Koreksi: M10 keliru dinilai 0`).
- ✅ Setelah update override → **re-run** script supaya semua file konsisten.
- ❌ Jangan edit langsung `Nilai-Final-Kelas-X.md` (akan hilang saat regenerate).
- ❌ Jangan ubah `BOBOT` dict tanpa konfirmasi dosen.
- ❌ Jangan hapus override yang sudah ada tanpa alasan (mis. `ATTENDANCE_OVERRIDE` untuk mhs nonaktif).

---

*Pendekatan ini berpegang teguh pada integritas analisis manual AI dan mencegah skor buatan otomatis yang tidak bisa diverifikasi silang dengan logika algoritma orisinil tiap mahasiswa.*
