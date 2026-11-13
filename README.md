# penasihat-skills

Marketplace plugin berisi skill **brief-proyek** dan teks **Instructions** untuk Settings claude.ai. Dibuat untuk bekerja dengan agent AI di terminal: Claude jadi penasihat yang menyelidiki, menilai laporan agent, dan menulis prompt, dan setiap Project claude.ai dibuat dari fakta repo, bukan asumsi.

## Isi

| Berkas | Fungsi |
|---|---|
| `plugins/penasihat/skills/brief-proyek/SKILL.md` | skill yang membaca git bundle atau zip repo lalu membuat Instructions Project dan bundel Files |
| `INSTRUCTIONS.md` | teks kebiasaan kerja umum untuk ditempel ke Settings > Instructions |
| `.claude-plugin/marketplace.json` | katalog marketplace |
| `plugins/penasihat/.claude-plugin/plugin.json` | manifest plugin |

## Pasang

Claude Code:

```bash
claude plugin marketplace add pawangai/penasihat-skills
claude plugin install penasihat@penasihat-skills
```

claude.ai dan Cowork: buka panel Plugins, tambahkan marketplace dari GitHub dengan alamat `pawangai/penasihat-skills`, lalu pasang plugin `penasihat`. Letak menu bisa berbeda menurut paket dan versi aplikasi Anda.

Instructions di Settings tidak bisa dipasang lewat plugin. Salin teks dari [INSTRUCTIONS.md](INSTRUCTIONS.md) secara manual.

## Pakai brief-proyek

1. Di akar repo yang ingin dibuatkan Project, buat bundle:

```bash
git bundle create proyek.bundle main
```

   Perintah itu membuat satu berkas berisi branch `main` beserta riwayatnya. Ganti `main` dengan `--all` untuk semua branch.
2. Unggah `proyek.bundle` ke chat dan minta: "pakai brief-proyek untuk repo ini".
3. Terima zip berisi `instructions.txt`, folder `files/`, `manifest.md`, dan folder `opsional/` bila ada.
4. Buat Project baru. Tempel `instructions.txt` ke Instructions dan unggah isi `files/` ke Files.
5. Saat repo berubah, buat ulang paketnya. Hash commit di akhir Instructions menunjukkan kapan paket basi.

## Jaminan dan batas

- Hanya membaca. Skill tidak menjalankan skrip, install, atau build dari repo.
- Semua kalimat di Instructions menyebut sumbernya. Yang tidak ditemukan ditulis `TIDAK DITEMUKAN`, tidak ditebak.
- Berkas rahasia dan konfigurasi MCP tidak masuk bundel. Pemindaian rahasia dilaporkan sebagai path dan nomor baris saja.
- Git bundle hanya membawa berkas ter-track. Berkas `.env` dan berkas yang di-gitignore tidak ikut. Jangan mengunggah bundle repo privat ke tempat publik.
- Status dinamis (PR dan issue terbuka, rilis terakhir) tidak ada di bundle. Tempelkan dari `gh pr list` dan `git status` tiap sesi.

## Lisensi

MIT. Lihat [LICENSE](LICENSE).
