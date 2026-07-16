# Activity Deck

Kartu bermain berbasis aktivitas untuk pembelajaran dan permainan sosial. Berbeda dari kartu remi atau UNO yang mengandalkan angka dan lambang, setiap kartu di sini menampilkan sebuah gambar kegiatan sebagai inti permainan, dilengkapi lapisan kuis film yang membuat setiap ronde terasa berbeda.

---

## Daftar Isi

- [Konsep Dasar](#konsep-dasar)
- [Anatomi Kartu](#anatomi-kartu)
- [Contoh Tata Letak Kartu](#contoh-tata-letak-kartu)
- [Mekanisme Film Quiz](#mekanisme-film-quiz)
- [Alur Permainan](#alur-permainan)
- [Struktur Data Kartu](#struktur-data-kartu)
- [Struktur Folder Proyek](#struktur-folder-proyek)
- [Referensi Visual](#referensi-visual)
- [Roadmap](#roadmap)

---

## Konsep Dasar

Setiap kartu merepresentasikan satu kegiatan (misalnya memasak, memanah, melukis, mendaki). Pemain tidak membaca angka atau simbol seperti pada kartu remi, melainkan membaca gambar dan menafsirkan aktivitas yang sedang ditampilkan. Nilai strategis kartu ditentukan oleh kombinasi poin, kuis film terkait, dan efek power yang melekat padanya.

Tujuan desain:

1. Melatih daya observasi dan asosiasi visual pemain terhadap suatu kegiatan.
2. Menggabungkan unsur trivia film sebagai lapisan tantangan tambahan.
3. Memberi ruang untuk konsekuensi sosial yang menghibur melalui mekanisme hukuman bergaya karakter film.

---

## Anatomi Kartu

Setiap kartu terdiri dari enam komponen berikut.

| No | Komponen | Fungsi |
|----|----------|--------|
| 1 | Gambar Kartu | Ilustrasi utama yang menggambarkan sebuah kegiatan tanpa teks penjelas tambahan pada gambar itu sendiri. |
| 2 | Nomor Pojok | Angka identitas atau poin yang dikumpulkan sepanjang permainan untuk menentukan pemenang. |
| 3 | Nama Kegiatan | Label singkat di bawah gambar yang menyebutkan nama aktivitas yang ditampilkan. |
| 4 | Film Quiz | Pertanyaan seputar sebuah film yang temanya berkaitan dengan kegiatan pada gambar. |
| 5 | Power | Efek khusus kartu, dapat berupa petunjuk untuk kartu lain, izin melompat ke tahap berikutnya, atau hak mengambil kartu tambahan. |
| 6 | Efek Film | Konsekuensi unik saat Film Quiz dijawab salah, berupa hukuman memerankan adegan atau menjawab kuis lanjutan menggunakan gaya bicara khas karakter dari film terkait. |

---

## Contoh Tata Letak Kartu

Diagram di bawah menunjukkan sketsa posisi setiap komponen pada satu kartu, sebagai acuan awal sebelum masuk tahap desain grafis.

```
+---------------------------------------+
| [2]                                   |
|  07                                   |
|                                       |
|            [ 1. GAMBAR KARTU ]        |
|            (ilustrasi kegiatan)       |
|                                       |
|-----------------------------------   |
|  [3] Memanah                          |
|-----------------------------------    |
|  [4] Film Quiz:                       |
|  "Film apa yang menampilkan           |
|   pemanah sebagai tokoh utama?"       |
|-----------------------------------    |
|  [5] Power:                           |
|  Boleh mengambil 1 kartu tambahan     |
|  jika jawaban benar.                  |
|-----------------------------------    |
|  [6] Efek Film:                       |
|  Jawaban salah -> jawab 1 ronde       |
|  berikutnya dengan gaya bicara        |
|  karakter dari film tersebut.         |
+---------------------------------------+
```

Susunan ini dapat disesuaikan, namun pola umum yang disarankan adalah gambar mendominasi bagian atas kartu, sementara teks pendukung (nama kegiatan, kuis, power, efek) disusun berlapis di bagian bawah agar tetap mudah dibaca saat kartu dipegang dalam genggaman tangan.

Untuk gaya visual pembanding, lihat bagian [Referensi Visual](#referensi-visual) yang menampilkan contoh tata letak kartu edukasi dan flashcard sejenis.

---

## Mekanisme Film Quiz

Bagian ini adalah pembeda utama dek kartu ini dari kartu permainan konvensional.

- Setiap kartu memuat satu pertanyaan seputar film yang temanya berhubungan dengan gambar kegiatan pada kartu tersebut.
- Pemain yang menerima giliran wajib menjawab kuis film sebelum dapat menggunakan efek Power pada kartu.
- Jawaban benar akan mengaktifkan Power kartu secara penuh, misalnya membuka petunjuk untuk kartu lain, melanjutkan ke tahap berikutnya, atau mengambil kartu ekstra.
- Jawaban salah akan memicu Efek Film, yaitu hukuman berupa memerankan sebuah adegan singkat atau menjawab pertanyaan susulan dengan gaya bicara khas karakter dari film yang dimaksud, hingga permainan selesai atau selama sejumlah putaran sesuai kesepakatan pemain.

Kombinasi ini membuat setiap kartu berfungsi ganda, sebagai alat bantu belajar mengenali kegiatan sekaligus sebagai pemicu momen sosial yang menghibur di meja permainan.

---

## Alur Permainan

Alur berikut adalah kerangka dasar yang dapat dimodifikasi sesuai kebutuhan proyek.

1. Setiap pemain menerima sejumlah kartu awal dari dek yang telah dikocok.
2. Pemain yang mendapat giliran mengangkat satu kartu dan menunjukkan gambar kegiatan kepada pemain lain tanpa menyebut namanya.
3. Pemain lain menebak nama kegiatan pada gambar tersebut.
4. Jika tebakan benar, pemain yang memegang kartu membacakan Film Quiz kepada penebak.
5. Penebak menjawab Film Quiz.
   - Jawaban benar mengaktifkan Power kartu.
   - Jawaban salah memicu Efek Film sebagai hukuman.
6. Poin pada Nomor Pojok dikumpulkan oleh pemain yang berhasil menjawab dengan benar.
7. Permainan berlanjut hingga dek habis atau target poin tercapai, dan pemain dengan poin tertinggi dinyatakan sebagai pemenang.

---

## Struktur Data Kartu

Untuk mempermudah proses produksi maupun pengembangan aplikasi pendamping (jika dibutuhkan), setiap kartu dapat direpresentasikan dalam format berikut.

```json
{
  "id": "card_007",
  "activity_name": "Memanah",
  "image_path": "assets/cards/memanah.png",
  "corner_number": 7,
  "film_quiz": {
    "question": "Film apa yang menampilkan pemanah sebagai tokoh utama?",
    "answer": "Contoh Judul Film",
    "difficulty": "medium"
  },
  "power": {
    "type": "draw_extra_card",
    "description": "Boleh mengambil 1 kartu tambahan jika jawaban benar."
  },
  "film_effect": {
    "penalty_type": "roleplay_speech_style",
    "duration": "1_round",
    "description": "Jawaban salah membuat pemain menjawab 1 ronde berikutnya dengan gaya bicara karakter dari film terkait."
  }
}
```

Struktur ini memungkinkan seluruh isi dek disimpan dalam satu berkas `cards.json`, sehingga proses balancing poin, distribusi power, maupun revisi kuis film dapat dilakukan tanpa menyentuh berkas gambar.

---

## Struktur Folder Proyek

Contoh susunan folder yang disarankan untuk memisahkan aset, data, dan dokumentasi.

```
activity-deck/
├── assets/
│   └── cards/
│       ├── memanah.png
│       ├── melukis.png
│       └── mendaki.png
├── data/
│   └── cards.json
├── docs/
│   └── rulebook.md
└── README.md
```

---

## Referensi Visual

Sebagai gambaran awal gaya desain, contoh tata letak kartu edukasi dan flashcard sejenis telah ditampilkan pada percakapan di atas. Referensi tersebut menunjukkan pola umum berupa ilustrasi dominan di bagian atas kartu, judul kegiatan di bawah ilustrasi, serta elemen pendukung seperti nomor dan kotak aturan yang disusun rapi di sisi kartu. Pola ini dapat dijadikan titik awal sebelum menentukan gaya ilustrasi final untuk dek kartu ini.

---

## Roadmap

- [ ] Menentukan daftar lengkap kegiatan yang akan diilustrasikan.
- [ ] Menyusun basis data kuis film untuk setiap kegiatan.
- [ ] Merancang ilustrasi final untuk setiap kartu.
- [ ] Menyusun buku aturan lengkap di `docs/rulebook.md`.
- [ ] Uji coba permainan bersama kelompok kecil untuk menyeimbangkan poin dan efek power.
- [ ] Produksi cetak atau versi digital dek kartu.
