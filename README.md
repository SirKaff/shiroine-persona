# Shiroine Persona Database 🎭

Koleksi database persona dan karakter AI open-source untuk **Shiroine WhatsApp Bot** dan platform website Shiroine.

Repositori ini memungkinkan siapa saja untuk menambahkan, memperbaiki, atau menyempurnakan gaya bicara, kepribadian, skenario, dan informasi dunia (*world info*) dari karakter AI favorit.

---

## 📌 Struktur Format Persona JSON

Setiap persona didefinisikan dalam format file JSON dengan penamaan:  
`<ID>-<nama-karakter>.json` (contoh: `200303-furina.json`).

### Contoh File JSON:

```json
{
  "id": "200303",
  "name": "Furina",
  "calling": "Furina",
  "description": "Mantan Archon Hydro Fontaine yang dramatis, ekspresif, dan memiliki sisi rapuh.",
  "personality": [
    "Dramatis dan teatrikal",
    "Percaya diri di luar, rapuh di dalam",
    "Sangat peduli pada keadilan dan rakyat Fontaine"
  ],
  "first_message": "Hehe! Selamat datang di hadapanku! Apa yang membawamu kemari?",
  "style": {
    "tone": "theatrical, expressive, charming",
    "language": "id"
  }
}
```

---

## 🏷️ Skema Penomoran ID (6 Digit)

Format: `TTCCNN`
- `TT` = Tipe Karakter:
  - `10` = Anime
  - `20` = Game
  - `30` = AI Assistant
  - `40` = Fun
- `CC` = Kategori Karakter:
  - `01` = Idol
  - `02` = VTuber
  - `03` = Waifu
  - `04` = Male / Husband
- `NN` = Nomor Urut Karakter (01, 02, 03, dst.)

*Contoh:* `200303` = Game (`20`) / Waifu (`03`) / Urutan ke-3 (`03`) -> Furina.

---

## 🤝 Cara Berkontribusi

1. Fork repositori ini.
2. Buat branch baru untuk karakter kamu (`git checkout -b feature/karakter-baru`).
3. Tambahkan file JSON karakter baru mengikuti skema ID yang belum digunakan.
4. Pastikan sintaks JSON valid (bisa cek dengan `jq . <nama-file>.json`).
5. Commit dan buat **Pull Request (PR)**!

Setelah PR disetujui dan di-merge, Shiroine Bot akan otomatis mensinkronisasi karakter baru kamu ke dalam sistem tanpa perlu restart bot! 🚀
