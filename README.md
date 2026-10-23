# Open AI Persona Database

Koleksi database karakter dan persona AI open-source terstruktur dalam format JSON standar. Dirancang agar dapat langsung diintegrasikan dan digunakan secara bebas oleh siapa pun—baik untuk bot WhatsApp, bot Discord, asisten virtual, aplikasi roleplay web, agen otonom, maupun eksperimen Large Language Model (LLM).

Setiap persona dilengkapi deskripsi karakter, kepribadian (*personality*), ciri fisik (*appearance*), aturan aksi-reaksi (*behavior*), data lore (*world info* / RAG), relasi antartokoh, dan contoh percakapan (*few-shot learning*).

---

## Fitur

- **Universal & Portabel:** Format JSON standar tanpa keterikatan pada platform atau pustaka tertentu. Dapat diimpor, di-fork, atau disematkan sebagai submodule.
- **114+ Karakter Terkurasi:** Meliputi kategori Anime, Game, VTuber, Vocaloid, dan Smart Assistant.
- **Optimasi Khusus LLM:** Struktur data dirancang untuk menghasilkan *system prompt* yang konsisten dan menjaga karakter tetap *in-character*.
- **Struktur Direktori Modular:** Dikelompokkan berdasarkan kategori dengan batas maksimal 100 file per folder.
- **Skema ID Open-Ended:** Penomoran ID bertambah secara dinamis tanpa mengubah ID yang sudah ada sebelumnya.
- **Validasi CI Otomatis:** Dilengkapi skrip validator dan GitHub Actions workflow untuk menjamin integritas data dan kepatuhan format.

---

## Struktur Direktori

File persona disimpan di dalam direktori `personas/` berdasarkan kode kategori:

```text
personas/
├── 1001-vocaloid/             # Virtual Singer / Vocaloid
├── 1002-vtuber/               # VTuber
├── 1003-anime-female/         # Karakter Anime Wanita
│   ├── 001-099/               # Batch 1 (ID 100301 s/d 100399)
│   └── 100-199/               # Batch 2 (ID 1003100 s/d 1003199)
├── 1004-anime-male/           # Karakter Anime Pria / Protagonis
├── 2003-game/                 # Karakter Game
└── 3001-assistant/            # Smart Assistant
```

---

## Skema ID Karakter (Open-Ended)

Setiap persona memiliki pengenal numerik unik dengan format:

$$\text{ID} = \text{TT} \, \text{CC} \, \text{NN...}$$

- **TT (Tipe Utama):** `10` (Anime/Manga), `20` (Game/Virtual), `30` (Asisten/Utilitas), `40` (Orisinal/Fun).
- **CC (Sub-Kategori):** `01` (Vocaloid), `02` (VTuber), `03` (Karakter Wanita), `04` (Karakter Pria).
- **NN... (Nomor Urut):** Dimulai dari `01` s/d `99`. Ketika nomor urut melampaui 99, digit bertambah secara alami menjadi 3 digit (`100`, `101`, dst.) dan ditempatkan pada folder batch baru (`100-199/`).

---

## Struktur Data JSON

Setiap file persona `{id}-{slug}.json` mengikuti spesifikasi berikut:

| Field | Tipe | Status | Keterangan |
| :--- | :--- | :---: | :--- |
| `id` | `string` | Wajib | Nomor pengenal unik (minimal 6 digit angka). |
| `name` | `string` | Wajib | Nama lengkap karakter. |
| `calling` | `string` | Wajib | Panggilan alias / trigger singkat dalam satu kata huruf kecil. |
| `description` | `string` | Wajib | Ringkasan identitas dan latar belakang karakter. |
| `personality` | `string[]` | Wajib | Daftar sifat kepribadian karakter. |
| `appearance` | `string[]` | Wajib | Ciri-ciri visual dan fisik. |
| `features` | `string[]` | Wajib | Kemampuan khusus, senjata, atau trivia penting. |
| `behavior` | `string[]` | Wajib | Pola kondisi -> respon emosi -> tindakan fisik -> ucapan. |
| `scenario` | `string` | Wajib | Latar situasi awal interaksi antara user dan karakter. |
| `first_message` | `string` | Wajib | Pesan pembuka saat percakapan dimulai. |
| `world_info` | `object[]` | Wajib | Pengetahuan lorebook / RAG (`keywords` dan `content`). |
| `relationships` | `object[]` | Wajib | Hubungan karakter dengan tokoh lain (`name` dan `content`). |
| `example_dialogues` | `object[]` | Wajib | Contoh percakapan few-shot (`user` dan `char`). |
| `speech_patterns` | `string` | Opsional | Gaya bicara, intonasi, atau verbal tics khas karakter. |

---

## Panduan Kontribusi

Jika Anda ingin menambahkan karakter baru, silakan baca panduan lengkap dan contoh format pada [CONTRIBUTING.md](CONTRIBUTING.md).

Uji validasi lokal sebelum membuat Pull Request:

```bash
node scripts/validate.js
```

---

## Lisensi

Proyek ini dirilis di bawah [MIT License](LICENSE).
