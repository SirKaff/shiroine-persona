# Open AI Persona Database

> **Koleksi Database Karakter & Persona AI Open-Source Terbuka untuk Semua Pengembang, Chatbot, Agen AI, dan Aplikasi LLM.**

Repositori ini menyediakan database persona karakter terstruktur dalam format JSON berstandar tinggi. Dirancang agar dapat langsung diintegrasikan dan **digunakan secara bebas oleh siapa pun**—baik untuk bot WhatsApp, bot Discord, asisten virtual, aplikasi roleplay web, agen otonom, maupun penelitian Large Language Model (LLM).

Setiap persona dilengkapi dengan deskripsi karakter mendalam, sifat kepribadian (*personality*), ciri fisik (*appearance*), aturan aksi-reaksi (*behavior*), data lore (*world info / RAG*), relasi antartokoh, dan contoh dialog interaktif (*few-shot learning*).

---

## 🌟 Fitur Utama

- 🌐 **Universal & Bebas Digunakan Siapa Saja:** Format JSON standar tanpa dependensi khusus platform tertentu. Siapa pun dapat mengimpor, melakukan *fork*, atau menyematkan database ini sebagai *git submodule*.
- 🎭 **114+ Karakter Siap Pakai:** Mencakup Anime, Game, VTuber, Virtual Singer, dan Smart Assistant.
- 🧠 **Optimasi Khusus LLM / Prompt Engineering:** Struktur data dirancang khusus untuk menghasilkan *system prompt* yang konsisten, tidak mudah *out-of-character*, dan ekspresif.
- 📂 **Struktur Folder Terorganisir (Maks 100 File per Folder):** Direktori dikelompokkan berdasarkan kategori dan rentang batch ID yang rapi sehingga cepat dijelajahi di GitHub.
- 🛡️ **Validasi CI Otomatis & JSON Schema:** Dilengkapi dengan schema resmi dan GitHub Actions validator untuk menjamin integritas data dan kualitas format.

---

## 📁 Struktur Direktori

Karakter dikelompokkan ke dalam folder `personas/` berdasarkan kode kategori numerik:

```text
personas/
├── 1001-vocaloid/             # Karakter Virtual Singer / Vocaloid (Miku, Teto, dll.)
├── 1002-vtuber/               # VTuber Hololive, Nijisanji, dll. (Gura, Fubuki, Zeta, dll.)
├── 1003-anime-female/         # Karakter Anime Wanita (Waifu)
│   ├── 001-099/               # Batch 1 (ID 100301 s/d 100399)
│   └── 100-199/               # Batch 2 (ID 1003100 s/d 1003199)
├── 1004-anime-male/           # Karakter Anime Pria / Protagonis (Gojo, Anos, Cid, dll.)
├── 2003-game/                 # Karakter Game Populer (Genshin, Star Rail, Blue Archive, dll.)
└── 3001-assistant/            # AI Assistant Cerdas (Jarvis, TARS, Kurisu, Cortana, dll.)
```

---

## 🔢 Skema ID Karakter (Open-Ended)

Setiap persona memiliki pengenal numerik unik dengan format open-ended:

$$\text{ID} = \text{TT} \, \text{CC} \, \text{NN...}$$

- **`TT` (Tipe Utama):** `10` (Anime/Manga), `20` (Game/Virtual), `30` (Asisten/Utilitas), `40` (Orisinal/Fun).
- **`CC` (Sub-Kategori):** `01` (Vocaloid), `02` (VTuber), `03` (Karakter Wanita), `04` (Karakter Pria).
- **`NN...` (Nomor Urut):** Dimulai dari `01` s/d `99`. Ketika suatu kategori mencapai karakter ke-100, nomor otomatis bertambah menjadi 3 digit (`100`, `101`, dst.) tanpa batas dan tanpa mengubah ID yang sudah ada sebelumnya.

---

## 🚀 Cara Menggunakan Database Ini di Proyek Anda

### 1. Langsung Clone atau Download
```bash
git clone https://github.com/suhwr/shiroine-persona.git
```

### 2. Gunakan Sebagai Git Submodule di Proyek Anda
```bash
git submodule add https://github.com/suhwr/shiroine-persona.git personas
```

### 3. Membaca Persona Menggunakan Node.js
```javascript
const fs = require('fs');
const path = require('path');

// Contoh membaca Hatsune Miku
const mikuPath = path.join(__dirname, 'personas/1001-vocaloid/100101-hatsune-miku.json');
const miku = JSON.parse(fs.readFileSync(mikuPath, 'utf8'));

console.log(`Loaded character: ${miku.name} (@${miku.calling})`);
console.log(`First message: "${miku.first_message}"`);
```

### 4. Membaca Persona Menggunakan Python
```python
import json
from pathlib import Path

# Membaca seluruh persona secara rekursif
personas_dir = Path("personas")
all_personas = {}

for json_file in personas_dir.glob("**/*.json"):
    with open(json_file, "r", encoding="utf-8") as f:
        data = json.load(f)
        all_personas[data["id"]] = data

print(f"Total persona berhasil dimuat: {len(all_personas)}")
```

### 5. Membaca Persona Menggunakan Golang (Recursive Walker)
```go
package main

import (
	"encoding/json"
	"fmt"
	"io/fs"
	"os"
	"path/filepath"
)

type Persona struct {
	ID          string `json:"id"`
	Name        string `json:"name"`
	Calling     string `json:"calling"`
	Description string `json:"description"`
}

func main() {
	personas := make(map[string]Persona)

	_ = filepath.WalkDir("personas", func(path string, d fs.DirEntry, err error) error {
		if err == nil && !d.IsDir() && filepath.Ext(d.Name()) == ".json" {
			data, _ := os.ReadFile(path)
			var p Persona
			if json.Unmarshal(data, &p) == nil && p.ID != "" {
				personas[p.ID] = p
			}
		}
		return nil
	})

	fmt.Printf("Total persona dimuat: %d\n", len(personas))
}
```

---

## 🤝 Berkontribusi Menambahkan Karakter Baru

Kami menyambut kontribusi dari siapa pun! Anda dapat menambahkan karakter favorit Anda dengan membuka Pull Request.

Silakan baca panduan lengkap dan contoh template pada **[CONTRIBUTING.md](CONTRIBUTING.md)**.

### Uji Coba Validasi Lokal:
Sebelum mengirimkan Pull Request, pastikan file Anda lolos uji validasi otomatis:
```bash
node scripts/validate.js
```

---

## 📄 Lisensi

Proyek ini dirilis di bawah lisensi **[MIT License](LICENSE)**. Anda bebas menggunakan, memodifikasi, mendistribusikan, dan mengintegrasikannya ke proyek personal maupun komersial.
