# SOAL REMEDIAL UJIAN AKHIR SEMESTER
# STRUKTUR DATA

---

**Program Studi:** Sistem Informasi - Institut Teknologi Kalimantan
**Cakupan:** Modul 9 – Modul 15 (Tree, BST, Graph, Searching, Sorting)
**Sifat:** Take-Home, Individu
**Estimasi Waktu Pengerjaan:** ~6–8 jam total
**Durasi:** 3 hari — **batas akhir Jumat, 19 Juni 2026 pukul 14.00 WITA**

---

## INFORMASI PENTING

| Item | Keterangan |
|------|------------|
| **Deadline** | **Jumat, 19 Juni 2026 pukul 14.00 WITA** (3 hari sejak diumumkan, 16 Juni 2026) |
| **Format submission** | Folder `Remedial-UAS/` di repo GitHub Classroom masing-masing |
| **Cap nilai maksimal** | **65** (lihat formula di bawah) |
| **Plagiat / AI** | Dilarang. Tools allowed: dokumentasi Python, modul kuliah, catatan pribadi. **DILARANG:** copy dari teman, copy dari ChatGPT/AI tanpa modifikasi & pemahaman, copy dari GitHub orang lain |

**Formula nilai akhir UAS:**
```
UAS_final = MAX(UAS_asli, MIN(UAS_remedial, 65))
```

Artinya: kalau nilai remedial > UAS awal, dipakai nilai remedial (max 65). Kalau remedial < UAS awal, dipakai UAS awal.

---

## ALUR PENGERJAAN

1. **Cek set kamu** di file `Daftar-Mahasiswa-Remedial.md` (Set A / B / C).
2. **Kerjakan 3 soal** di set kamu, masing-masing di file `.py` terpisah.
3. **Tulis README** berisi identitas, refleksi, jawaban teori, dan analisis kompleksitas.
4. **Push ke repo Classroom** kamu dalam folder `Remedial-UAS/`.
5. **Jangan push sekaligus di akhir** — commit bertahap supaya history kerjamu terlihat (anti-plagiat check via `git log`).

---

## STRUKTUR FOLDER YANG HARUS DI-SUBMIT

```
Remedial-UAS/
├── README.md                            ← identitas + jawaban teori + analisis
├── Soal1_<Topik>_<NIM>.py
├── Soal2_<Topik>_<NIM>.py
└── Soal3_<Topik>_<NIM>.py
```

Contoh untuk mhs Set A, NIM 10251002:
```
Remedial-UAS/
├── README.md
├── Soal1_ProductBST_10251002.py
├── Soal2_DeliveryGraph_10251002.py
└── Soal3_ProductSearch_10251002.py
```

---

## RUBRIK PENILAIAN (Total 100, dicap maks 65)

| Komponen | Bobot | Penjelasan |
|----------|------:|------------|
| Soal 1 (Tree / BST) | 25 | Implementasi + test PASSED + traversal benar |
| Soal 2 (Graph BFS/DFS) | 25 | Implementasi + test PASSED + traversal order benar |
| Soal 3 (Sorting + Searching integrasi) | 30 | Implementasi algoritma sort MANUAL + binary search + test PASSED |
| README teori & refleksi | 20 | Jawaban benar, analisis akurat, refleksi jelas |

**Penalti otomatis:**
- File `.py` tidak bisa di-execute (Syntax/Runtime error fatal): -50% per soal
- File salah konten (mis. submit Praktikum copy modul): 0 untuk soal tsb
- **Soal 3 pakai `list.sort()` / `sorted()` bawaan** (bukan implementasi sendiri): -50% Soal 3
- 1 commit besar di akhir tanpa history bertahap: investigasi plagiat, -20% nilai total
- README kosong / tanpa analisis Big-O: -15

---

## TEMPLATE README.md (WAJIB DIIKUTI)

```markdown
# Remedial UAS - Struktur Data

## Identitas
- Nama: ___________________
- NIM: ___________________
- Kelas: A / B
- Set Remedial: A / B / C
- Tanggal Submit: ___________________

## Refleksi Singkat (3-5 kalimat)
Apa kesalahan/kelemahan saya di UAS sebelumnya, dan apa yang akan saya
perbaiki sekarang?

___________________________________________________________________
___________________________________________________________________

## Penjelasan per Soal

### Soal 1: <Judul>
Penjelasan implementasi (3-5 kalimat):
___________________________________________________________________

Analisis kompleksitas Big-O per method utama:
| Method | Best | Average | Worst | Alasan singkat |
|--------|------|---------|-------|----------------|
| ...    | ...  | ...     | ...   | ...            |

### Soal 2: <Judul>
(format sama)

### Soal 3: <Judul>
(format sama)

## Jawaban Soal Teori (semua set sama, WAJIB)

### Teori 1 — Tracing Traversal BST
Diberikan BST hasil insert berurutan: 50, 30, 70, 20, 40, 60, 80.
Tuliskan hasil traversal:
- Inorder (LNR)
- Preorder (NLR)
- Postorder (LRN)
Lalu jelaskan: traversal mana yang menghasilkan data terurut menaik, dan kenapa.

Jawaban:
___________________________________________________________________

### Teori 2 — BFS vs DFS
Jelaskan perbedaan utama BFS dan DFS pada graph (struktur bantu yang dipakai +
urutan kunjungan), masing-masing minimal 1 contoh use case di dunia nyata
(selain yang sudah ada di modul).

Jawaban:
___________________________________________________________________

### Teori 3 — Perbandingan Algoritma Sorting & Searching
(a) Bandingkan Big-O Worst Case dari: Bubble Sort, Selection Sort, Insertion
    Sort, Merge Sort, dan Quick Sort.
(b) Jelaskan kenapa Binary Search hanya bisa dipakai pada data yang SUDAH
    terurut, dan apa Big-O-nya dibanding Linear Search.

Jawaban:
___________________________________________________________________
```

---

---

# SET A — E-Commerce "TokoBerkah Online"

> **Skenario:** Kamu membangun backend untuk toko online "TokoBerkah". Sistem
> mengelola katalog produk (dengan BST), jaringan pengiriman antar kota
> (dengan Graph), serta fitur pencarian & pengurutan produk.

---

## SET A — Soal 1: ProductBST (Binary Search Tree)

Implementasikan class `Node` dan `ProductBST`. BST di-key berdasarkan `product_id` (integer). Tiap node menyimpan dict produk `{"id", "nama", "harga", "stok"}`.

### Spesifikasi `ProductBST`
| Method | Deskripsi |
|--------|-----------|
| `insert(product_id, nama, harga, stok)` | Sisip produk ke posisi BST yang benar (kiri < parent < kanan) |
| `search(product_id)` | Return dict produk atau `None` |
| `delete(product_id)` | Hapus node (tangani 3 kasus: leaf, 1 anak, 2 anak — pakai successor inorder) |
| `inorder()` | Return list `product_id` urut menaik |
| `find_min()` / `find_max()` | Return `product_id` terkecil / terbesar |
| `height()` | Tinggi tree dalam jumlah edge (tree kosong = -1, 1 node = 0) |
| `count()` | Jumlah node |

### Test Case Wajib (taruh di `if __name__ == "__main__":`)
```python
bst = ProductBST()
data = [(50,"Beras",65000,20),(30,"Minyak",18000,50),(70,"Gula",14000,5),
        (20,"Telur",28000,8),(40,"Tepung",12000,15),(60,"Garam",5000,30),
        (80,"Kopi",25000,12)]
for pid, nama, harga, stok in data:
    bst.insert(pid, nama, harga, stok)

assert bst.count() == 7
assert bst.search(40)["nama"] == "Tepung"
assert bst.search(99) is None
assert bst.inorder() == [20,30,40,50,60,70,80]
assert bst.find_min() == 20
assert bst.find_max() == 80
assert bst.height() == 2     # root 50, level1 {30,70}, level2 {20,40,60,80}

bst.delete(30)               # node dengan 2 anak
assert bst.search(30) is None
assert bst.inorder() == [20,40,50,60,70,80]
assert bst.count() == 6
print("Semua test Soal 1 PASSED")
```

---

## SET A — Soal 2: DeliveryGraph (Graph BFS/DFS)

Implementasikan `DeliveryGraph` (graph **tak berarah**, adjacency list) untuk jaringan pengiriman antar kota.

> **Catatan deterministik:** saat BFS/DFS, kunjungi tetangga dalam urutan **alfabet (sorted)** supaya hasil bisa diuji.

### Spesifikasi `DeliveryGraph`
| Method | Deskripsi |
|--------|-----------|
| `add_city(name)` | Tambah simpul kota |
| `add_route(a, b)` | Tambah sisi tak berarah antara kota a dan b |
| `neighbors(city)` | Return list tetangga (sorted) |
| `bfs(start)` | Return list kota urut kunjungan BFS (tetangga sorted) |
| `dfs(start)` | Return list kota urut kunjungan DFS (tetangga sorted) |
| `has_path(a, b)` | Return `True/False` apakah ada jalur a→b |
| `shortest_hops(a, b)` | **(khusus Set A)** jumlah edge jalur terpendek (BFS), `-1` jika tak terhubung |

### Test Case Wajib
```python
g = DeliveryGraph()
for c in ["Jakarta","Bandung","Surabaya","Bali","Medan"]:
    g.add_city(c)
g.add_route("Jakarta","Bandung")
g.add_route("Jakarta","Surabaya")
g.add_route("Bandung","Surabaya")
g.add_route("Surabaya","Bali")
# Medan sengaja terisolasi

assert g.neighbors("Jakarta") == ["Bandung","Surabaya"]
assert g.bfs("Jakarta") == ["Jakarta","Bandung","Surabaya","Bali"]
assert g.dfs("Jakarta") == ["Jakarta","Bandung","Surabaya","Bali"]
assert g.has_path("Jakarta","Bali") is True
assert g.has_path("Jakarta","Medan") is False
assert g.shortest_hops("Jakarta","Bali") == 2   # Jakarta->Surabaya->Bali
assert g.shortest_hops("Jakarta","Medan") == -1
print("Semua test Soal 2 PASSED")
```

---

## SET A — Soal 3: ProductSearchEngine (Sorting + Binary Search)

Buat `ProductSearchEngine` yang mengurutkan produk dengan **Merge Sort buatan sendiri** (DILARANG `sorted()` / `list.sort()`), lalu mencari dengan **Binary Search**.

### Spesifikasi
| Method | Deskripsi |
|--------|-----------|
| `add_product(nama, harga)` | Tambah produk |
| `sort_by_price()` | Return list produk urut **harga menaik** — WAJIB pakai Merge Sort manual |
| `find_by_price(target)` | Binary Search pada list terurut, return dict produk berharga `target` atau `None` |
| `top_k_expensive(k)` | Return `k` produk termahal (list of dict, termahal dulu) |
| `price_range(low, high)` | Return list produk dengan `low <= harga <= high` (urut menaik) |

### Test Case Wajib
```python
eng = ProductSearchEngine()
for nama, harga in [("Beras",65000),("Minyak",18000),("Gula",14000),
                    ("Telur",28000),("Kopi",25000)]:
    eng.add_product(nama, harga)

sorted_list = eng.sort_by_price()
assert [p["harga"] for p in sorted_list] == [14000,18000,25000,28000,65000]
assert eng.find_by_price(25000)["nama"] == "Kopi"
assert eng.find_by_price(99999) is None
assert [p["nama"] for p in eng.top_k_expensive(2)] == ["Beras","Telur"]
assert [p["nama"] for p in eng.price_range(15000,30000)] == ["Minyak","Kopi","Telur"]
print("Semua test Soal 3 PASSED")
```

---

---

# SET B — Telekomunikasi "TelkomFiber"

> **Skenario:** Kamu membangun sistem operasional ISP "TelkomFiber". Sistem
> mengelola data pelanggan (BST), topologi jaringan tower (Graph), serta
> pengurutan & pencarian keluhan pelanggan.

---

## SET B — Soal 1: CustomerBST (Binary Search Tree)

Implementasikan `Node` dan `CustomerBST`, di-key berdasarkan `customer_id` (integer). Tiap node menyimpan `{"id", "nama", "paket", "tagihan"}`.

### Spesifikasi `CustomerBST`
| Method | Deskripsi |
|--------|-----------|
| `insert(customer_id, nama, paket, tagihan)` | Sisip pelanggan ke posisi BST yang benar |
| `search(customer_id)` | Return dict pelanggan atau `None` |
| `delete(customer_id)` | Hapus node (tangani leaf / 1 anak / 2 anak dengan successor inorder) |
| `inorder()` | Return list `customer_id` urut menaik |
| `find_min()` / `find_max()` | Return id terkecil / terbesar |
| `height()` | Tinggi tree (edge; kosong = -1, 1 node = 0) |
| `count()` | Jumlah node |

### Test Case Wajib
```python
bst = CustomerBST()
data = [(50,"Andi","Premium",350000),(30,"Budi","Basic",150000),
        (70,"Citra","VIP",500000),(20,"Dewi","Basic",150000),
        (40,"Eko","Premium",350000),(60,"Fani","Basic",150000),
        (80,"Gita","VIP",500000)]
for cid, nama, paket, tagihan in data:
    bst.insert(cid, nama, paket, tagihan)

assert bst.count() == 7
assert bst.search(40)["nama"] == "Eko"
assert bst.search(99) is None
assert bst.inorder() == [20,30,40,50,60,70,80]
assert bst.find_min() == 20
assert bst.find_max() == 80
assert bst.height() == 2

bst.delete(30)               # node dengan 2 anak
assert bst.search(30) is None
assert bst.inorder() == [20,40,50,60,70,80]
assert bst.count() == 6
print("Semua test Soal 1 PASSED")
```

---

## SET B — Soal 2: NetworkGraph (Graph BFS/DFS)

Implementasikan `NetworkGraph` (graph **tak berarah**, adjacency list) untuk topologi tower jaringan.

> **Catatan deterministik:** kunjungi tetangga dalam urutan **alfabet (sorted)**.

### Spesifikasi `NetworkGraph`
| Method | Deskripsi |
|--------|-----------|
| `add_tower(name)` | Tambah simpul tower |
| `add_link(a, b)` | Tambah sisi tak berarah antar tower |
| `neighbors(tower)` | Return list tetangga (sorted) |
| `bfs(start)` | Return list tower urut BFS |
| `dfs(start)` | Return list tower urut DFS |
| `has_path(a, b)` | Return `True/False` |
| `count_reachable(start)` | **(khusus Set B)** jumlah tower yang bisa dicapai dari `start` (TERMASUK start sendiri) |

### Test Case Wajib
```python
g = NetworkGraph()
for t in ["T-A","T-B","T-C","T-D","T-E"]:
    g.add_tower(t)
g.add_link("T-A","T-B")
g.add_link("T-A","T-C")
g.add_link("T-B","T-C")
g.add_link("T-C","T-D")
# T-E sengaja terisolasi

assert g.neighbors("T-A") == ["T-B","T-C"]
assert g.bfs("T-A") == ["T-A","T-B","T-C","T-D"]
assert g.dfs("T-A") == ["T-A","T-B","T-C","T-D"]
assert g.has_path("T-A","T-D") is True
assert g.has_path("T-A","T-E") is False
assert g.count_reachable("T-A") == 4   # A,B,C,D
assert g.count_reachable("T-E") == 1   # hanya dirinya sendiri
print("Semua test Soal 2 PASSED")
```

---

## SET B — Soal 3: ComplaintSearchEngine (Sorting + Binary Search)

Buat `ComplaintSearchEngine` yang mengurutkan keluhan berdasarkan `urgency` dengan **Quick Sort buatan sendiri** (DILARANG `sorted()` / `list.sort()`), lalu mencari dengan **Binary Search**.

### Spesifikasi
| Method | Deskripsi |
|--------|-----------|
| `add_complaint(customer, isi, urgency)` | Tambah keluhan (`urgency` integer, makin besar makin urgent) |
| `sort_by_urgency()` | Return list keluhan urut **urgency menaik** — WAJIB pakai Quick Sort manual |
| `find_by_urgency(target)` | Binary Search pada list terurut, return **list** keluhan dengan urgency `target` (boleh lebih dari satu), `[]` jika tak ada |
| `top_k_urgent(k)` | Return `k` keluhan paling urgent (urgency tertinggi dulu) |
| `urgency_range(low, high)` | Return list keluhan dengan `low <= urgency <= high` (urut menaik) |

### Test Case Wajib
```python
eng = ComplaintSearchEngine()
data = [("Andi","Internet lambat",2),("Budi","Tidak bisa nelpon",5),
        ("Citra","Tagihan salah",1),("Dewi","Service mati total",5),
        ("Eko","Modem rusak",3)]
for cust, isi, urg in data:
    eng.add_complaint(cust, isi, urg)

assert [c["urgency"] for c in eng.sort_by_urgency()] == [1,2,3,5,5]
hasil5 = eng.find_by_urgency(5)
assert len(hasil5) == 2
assert {c["customer"] for c in hasil5} == {"Budi","Dewi"}
assert eng.find_by_urgency(4) == []
assert [c["customer"] for c in eng.top_k_urgent(2)] == ["Budi","Dewi"] \
    or [c["customer"] for c in eng.top_k_urgent(2)] == ["Dewi","Budi"]
assert [c["customer"] for c in eng.urgency_range(2,3)] == ["Andi","Eko"]
print("Semua test Soal 3 PASSED")
```

---

---

# SET C — Project Tracker "DevBoard"

> **Skenario:** Kamu membangun aplikasi manajemen proyek "DevBoard" untuk tim
> developer. Sistem mengelola task (BST berdasar prioritas), jaringan
> kolaborasi antar anggota (Graph), serta pengurutan & pencarian task.

---

## SET C — Soal 1: TaskBST (Binary Search Tree)

Implementasikan `Node` dan `TaskBST`, di-key berdasarkan `task_id` (integer). Tiap node menyimpan `{"id", "judul", "priority", "deadline"}`.

### Spesifikasi `TaskBST`
| Method | Deskripsi |
|--------|-----------|
| `insert(task_id, judul, priority, deadline)` | Sisip task ke posisi BST yang benar |
| `search(task_id)` | Return dict task atau `None` |
| `delete(task_id)` | Hapus node (tangani leaf / 1 anak / 2 anak dengan successor inorder) |
| `inorder()` | Return list `task_id` urut menaik |
| `find_min()` / `find_max()` | Return id terkecil / terbesar |
| `height()` | Tinggi tree (edge; kosong = -1, 1 node = 0) |
| `count()` | Jumlah node |

### Test Case Wajib
```python
bst = TaskBST()
data = [(50,"Setup DB",3,5),(30,"Login",2,3),(70,"Build UI",1,7),
        (20,"Fix bug",3,-2),(40,"Write docs",1,7),(60,"Deploy",2,5),
        (80,"Code review",3,-1)]
for tid, judul, prio, dl in data:
    bst.insert(tid, judul, prio, dl)

assert bst.count() == 7
assert bst.search(40)["judul"] == "Write docs"
assert bst.search(99) is None
assert bst.inorder() == [20,30,40,50,60,70,80]
assert bst.find_min() == 20
assert bst.find_max() == 80
assert bst.height() == 2

bst.delete(30)               # node dengan 2 anak
assert bst.search(30) is None
assert bst.inorder() == [20,40,50,60,70,80]
assert bst.count() == 6
print("Semua test Soal 1 PASSED")
```

---

## SET C — Soal 2: CollabGraph (Graph BFS/DFS)

Implementasikan `CollabGraph` (graph **tak berarah**, adjacency list) untuk jaringan kolaborasi antar anggota tim.

> **Catatan deterministik:** kunjungi tetangga dalam urutan **alfabet (sorted)**.

### Spesifikasi `CollabGraph`
| Method | Deskripsi |
|--------|-----------|
| `add_member(name)` | Tambah simpul anggota |
| `add_collab(a, b)` | Tambah sisi tak berarah antar anggota |
| `neighbors(member)` | Return list tetangga (sorted) |
| `bfs(start)` | Return list anggota urut BFS |
| `dfs(start)` | Return list anggota urut DFS |
| `has_path(a, b)` | Return `True/False` |
| `count_components()` | **(khusus Set C)** jumlah komponen terhubung (connected components) di seluruh graph |

### Test Case Wajib
```python
g = CollabGraph()
for m in ["Alice","Bob","Charlie","Diana","Evan"]:
    g.add_member(m)
g.add_collab("Alice","Bob")
g.add_collab("Alice","Charlie")
g.add_collab("Bob","Charlie")
g.add_collab("Charlie","Diana")
# Evan sengaja sendiri (komponen terpisah)

assert g.neighbors("Alice") == ["Bob","Charlie"]
assert g.bfs("Alice") == ["Alice","Bob","Charlie","Diana"]
assert g.dfs("Alice") == ["Alice","Bob","Charlie","Diana"]
assert g.has_path("Alice","Diana") is True
assert g.has_path("Alice","Evan") is False
assert g.count_components() == 2   # {Alice,Bob,Charlie,Diana} dan {Evan}
print("Semua test Soal 2 PASSED")
```

---

## SET C — Soal 3: TaskSearchEngine (Sorting + Binary Search)

Buat `TaskSearchEngine` yang mengurutkan task berdasarkan `deadline` dengan **Insertion Sort buatan sendiri** (DILARANG `sorted()` / `list.sort()`), lalu mencari dengan **Binary Search**.

### Spesifikasi
| Method | Deskripsi |
|--------|-----------|
| `add_task(judul, deadline)` | Tambah task (`deadline` integer = hari tersisa, boleh negatif) |
| `sort_by_deadline()` | Return list task urut **deadline menaik** — WAJIB pakai Insertion Sort manual |
| `find_by_deadline(target)` | Binary Search pada list terurut, return **list** task dengan deadline `target`, `[]` jika tak ada |
| `most_urgent(k)` | Return `k` task dengan deadline terkecil (paling mepet dulu) |
| `deadline_range(low, high)` | Return list task dengan `low <= deadline <= high` (urut menaik) |

### Test Case Wajib
```python
eng = TaskSearchEngine()
data = [("Setup DB",5),("Login",3),("Build UI",7),("Fix bug",-2),
        ("Write docs",7),("Deploy",5)]
for judul, dl in data:
    eng.add_task(judul, dl)

assert [t["deadline"] for t in eng.sort_by_deadline()] == [-2,3,5,5,7,7]
hasil7 = eng.find_by_deadline(7)
assert len(hasil7) == 2
assert {t["judul"] for t in hasil7} == {"Build UI","Write docs"}
assert eng.find_by_deadline(100) == []
assert eng.most_urgent(1)[0]["judul"] == "Fix bug"
assert [t["judul"] for t in eng.deadline_range(3,5)] == ["Login","Setup DB","Deploy"] \
    or [t["judul"] for t in eng.deadline_range(3,5)] == ["Login","Deploy","Setup DB"]
print("Semua test Soal 3 PASSED")
```

---

---

# CATATAN PENTING UNTUK PENGUMPULAN

1. **Setiap file `.py` HARUS bisa dijalankan langsung** dengan `python Soal1_*.py` dan menampilkan "Semua test Soal X PASSED" (atau pesan error yang jelas kalau gagal).

2. **Identitas di header file `.py`** wajib:
   ```python
   """
   Remedial UAS Struktur Data - Set <X>
   Soal <N>: <Judul>

   Nama : ___________________
   NIM  : ___________________
   Kelas: ___________________
   """
   ```

3. **Soal 3 WAJIB implementasi algoritma sorting sendiri** (Merge/Quick/Insertion sesuai set). Pakai `sorted()` atau `list.sort()` bawaan = penalti -50% Soal 3.

4. **Commit bertahap** — minimal 3 commit per soal (initial, progress, final). Jangan satu commit besar di akhir. History `git log` akan diperiksa.

5. **README.md WAJIB diisi lengkap** sesuai template di atas. Tanpa README atau README kosong = -15 dari nilai total.

6. **Pertanyaan / klarifikasi** soal: hubungi dosen via channel yang disepakati. **JANGAN tanya jawaban ke teman**.

---

*Soal ini disusun sebagai remedial UAS Praktikum Struktur Data, Program Studi Sistem Informasi - Institut Teknologi Kalimantan. Cakupan materi: Modul 9–15 (Tree, Binary Search Tree, Graph, Searching, Sorting).*
