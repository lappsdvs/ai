# PROJECT PLAN — Claude AI @ DVS (claude-ai presentation site)

> Letak file ni dalam `C:\Users\burnk\OneDrive\Documents-assets\Present\PROJECT_PLAN.md`
> lepas tu buka Claude Code dalam folder tu dan suruh dia baca + execute step demi step.
> Boleh copy satu "Bahagian" sekali gus sebagai prompt untuk Claude Code.

---

## 0. Konteks Projek

- **Site sedia ada:** https://lappsdvs.github.io/claude-ai/ (deploy via GitHub Pages, repo `claude-ai`)
- **File utama:** `index.html` (single-file HTML, struktur: Intro / Setup / Integrasi / Skill / Debug / Deploy)
- **Audien:** 35 peserta PM & PPS, 2-3 tahun bekerja, makmal/sains DVS
- **Tujuan baru:**
  1. Tukar tema visual jadi **3D Clay** + warna **Jabatan Perkhidmatan Veterinar (DVS)**
  2. Tambah elemen interaktif (QR, cheat sheet, FAQ, "Cuba Sendiri")
  3. Bina **modul hands-on** berasingan — peserta belajar tukar nota kelas jadi bahan interaktif, dan main dengan Claude guna data sendiri

---

## 1. Design Brief — Tema "3D Clay" + Warna DVS

### Palette (asaskan bendera Malaysia — rujukan rasmi logo DVS: merah, biru, putih, kuning)

| Token | Hex (cadangan) | Guna untuk |
|---|---|---|
| `--clay-blue` | `#1E4FA0` | Warna utama (header, nav, accent utama) |
| `--clay-blue-deep` | `#0F3576` | Shadow / depth untuk elemen biru |
| `--clay-red` | `#D32F2F` | Accent kedua (CTA, highlight penting) |
| `--clay-yellow` | `#FFC72C` | Accent ceria (badge, icon, hover) |
| `--clay-cream` | `#FFF8EC` | Background utama (lembut, bukan putih keras) |
| `--clay-white` | `#FFFFFF` | Card surface |
| `--ink` | `#27314A` | Teks utama |

### "3D Clay" look — checklist visual

- [ ] Card/button guna **border-radius besar** (16–28px) + **double shadow** (soft ambient shadow + tighter contact shadow di bawah) supaya nampak "timbul" macam objek tanah liat
- [ ] Button ada **state "pressed"**: bila klik, shadow mengecil + element turun 2px (`transform: translateY(2px)`) — bagi rasa tactile
- [ ] Icon/illustration guna gaya **soft 3D / claymorphism** (gradient lembut + highlight di satu sudut)
- [ ] Animasi masuk (`fade-up` / `scale-in`) bila section masuk viewport — guna `IntersectionObserver`, ringan je
- [ ] Hover pada card: sedikit `scale(1.02)` + shadow lebih besar
- [ ] Nav bar sticky, button nav pun bergaya clay (rounded + shadow)
- [ ] Jangan overdo animasi — 1 signature motion (contoh: hero icon float perlahan / bounce halus) + transition konsisten untuk hover/click je

### Typography
- Display: `Baloo 2` atau `Fredoka` (rounded, friendly — match clay style)
- Body: `Inter` atau `Plus Jakarta Sans`

---

## 2. Struktur Site (Updated)

```
index.html              ← Presentation utama (theme 3D Clay + DVS)
hands-on.html           ← Page baru: Workshop Hands-On
assets/
  qr-claude.png         ← QR code daftar claude.ai
  cheatsheet.pdf        ← Senarai prompt siap-pakai (A4)
  img/ ...
```

---

## 3. Tambahan kat `index.html`

### 3.1 QR Code Section (dalam "Setup")
- Generate QR code yang link ke `https://claude.ai`
- Letak dalam card clay-style, label: "Scan untuk daftar sekarang"

### 3.2 "Cuba Sendiri" Exercise Card (dalam "Integrasi" / "Skill")
- Card khas dengan 1 prompt contoh yang peserta boleh **copy terus**
- Tambah butang "📋 Copy Prompt" (guna `navigator.clipboard.writeText`)
- Contoh prompt: *"Tukar ayat ni jadi bahasa rasmi untuk surat rasmi: '[ayat peserta]'"*

### 3.3 FAQ / Myth-Busting (dalam "Debug")
- Accordion style (klik untuk expand) — clay card yang "buka" dengan animasi height
- Soalan cadangan:
  - "AI akan gantikan kerja kita ke?"
  - "Data yang kita taip selamat ke?"
  - "Perlu bayar ke untuk guna Claude?"
  - "Macam mana kalau jawapan AI salah?"

### 3.4 Before/After Comparison (dalam "Integrasi")
- Dua card side-by-side: "Sebelum" (nota mentah) vs "Selepas" (output Claude yang dikemas)
- Guna contoh sebenar dari kerja makmal DVS

---

## 4. Page Baru: `hands-on.html` — Workshop Interaktif

Tujuan: peserta **belajar buat sendiri**, bukan tengok je. 3 bahagian:

### Bahagian A — "Nota Kelas → Interaktif"
Tunjuk macam mana tukar nota mentah (txt/markdown) jadi bahan menarik guna Claude:
- Step 1: Tulis nota biasa (contoh nota SOP/prosedur dalam bullet point)
- Step 2: Minta Claude tukar jadi:
  - Infografik ringkas (guna Artifact/HTML)
  - Flashcard untuk revision
  - Quiz/soalan ujian kefahaman
- Sediakan **template prompt** untuk setiap output di atas, siap untuk copy

### Bahagian B — "Main dengan Data Sendiri"
- Setiap peserta bawa 1 sample data (Excel/CSV ringkas — boleh data dummy)
- Live exercise: upload ke Claude, minta:
  1. Ringkaskan / cari trend
  2. Highlight anomali
  3. Jana carta ringkas
- Sediakan 1 **sample dataset dummy** (CSV kecil, contoh rekod sampel makmal palsu) untuk peserta yang tak bawa data sendiri

### Bahagian C — "Self-Challenge"
- Senarai 5 mini-challenge (tingkat kesukaran rendah → tinggi) peserta boleh cuba lepas sesi:
  1. Tukar 1 emel jadi versi formal
  2. Ringkaskan 1 PDF panjang
  3. Buat jadual perbandingan dari nota
  4. Analisis 1 dataset kecil
  5. Bina 1 mini-tool (Google Sheet automation) dengan bantuan Claude

> Layout `hands-on.html` ikut design system sama dengan `index.html` (3D Clay + warna DVS), tapi struktur lebih "workbook" — banyak ruang kosong untuk peserta isi/tulis (jika dicetak) atau interaktif (jika digital).

---

## 5. Cheat Sheet PDF (`assets/cheatsheet.pdf`)

A4, satu muka, senarai 6-8 prompt siap pakai untuk tugasan harian PM/PPS:
1. Draf surat rasmi
2. Ringkaskan dokumen
3. Terjemah EN→BM
4. Analisis data Excel
5. Buat carta dari data
6. Semak/perbaiki ayat
7. Buat senarai semak (checklist) dari SOP
8. Bina automasi Google Sheets

---

## 6. Urutan Kerja (untuk Claude Code)

1. **Redesign `index.html`** — tukar CSS variables ikut palette DVS + tambah 3D clay styling (shadow, radius, animasi)
2. **Tambah komponen interaktif** dalam `index.html`: QR section, Cuba Sendiri card, FAQ accordion, Before/After
3. **Generate QR code** (boleh guna library JS ringan macam `qrcode.js` dari CDN, atau pre-generate PNG)
4. **Bina `hands-on.html`** ikut struktur Bahagian A/B/C di atas, guna design system sama
5. **Sediakan `assets/cheatsheet.pdf`** dan `assets/dummy-data.csv`
6. **Update nav** kat `index.html` untuk link ke `hands-on.html`
7. Test local (`open index.html`), then `git add . && git commit -m "..." && git push` untuk update GitHub Pages

---

## 7. Nota untuk Claude Code

- Kekalkan single-file approach untuk `index.html` (CSS+JS inline) — senang maintain & deploy
- Pastikan semua animasi guna `prefers-reduced-motion` check
- Semua teks dalam Bahasa Melayu, tone santai-profesional (sesuai PM/PPS)
- Test responsive — projector (besar) dan phone peserta (kecil) kedua-dua penting
