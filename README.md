# LeptoScope — Prototype Pilmapres

WebGIS prototype untuk prioritisasi surveilans leptospirosis tingkat kecamatan di Kota Semarang. Repository ini adalah **paket deployment yang sudah dipisahkan dari arsip riset**: tidak memuat notebook, backup, project ArcGIS, maupun data mentah klinis.

## Struktur
```text
backend/      FastAPI + histori + simulasi + pemantauan eksperimental
dist/         frontend aktif yang dilayani FastAPI
model/        satu model aktif + metadata konsisten
data/         dataset agregat minimum untuk histori/baseline
data_static/  referensi penduduk
data_live/    template input operator/cache runtime
docs/         flowchart, metode, dan deployment
```

## Menjalankan lokal
Gunakan Python 3.12.

### Windows PowerShell
```powershell
cd "D:\Website Leptoscope"
py -3.12 -m venv .venv
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
pip install -r requirements.txt
python -m uvicorn backend.app:app --host 127.0.0.1 --port 8000
```

### macOS/Linux
```bash
python3.12 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
uvicorn backend.app:app --host 0.0.0.0 --port 8000
```

Buka `http://localhost:8000`. Health check: `http://localhost:8000/api/health`.

## Mode demo
Tampilan awal menggunakan **evaluasi historis 2023** agar demo tetap stabil dan sesuai periode yang dievaluasi. Menu **Eksperimental** tetap tersedia untuk pemantauan bulan berjalan. Sistem selalu memakai **bulan kalender terakhir yang sudah lengkap** sebagai input dan menargetkan bulan sesudahnya. Contoh: pada 2 Oktober 2026, input model = September 2026 dan target = Oktober 2026. Mode ini tetap tidak boleh diklaim sebagai prediksi operasional tervalidasi.

## Input kasus operator
Salin `data_live/kasus_terbaru_TEMPLATE.csv` menjadi `data_live/kasus_terbaru.csv`. Sistem hanya memakai data operator jika matriks **16 kecamatan × 4 bulan lengkap sampai bulan input** tersedia. Pada Oktober 2026, periode yang dibutuhkan adalah Juni–September 2026. Sel kosong berarti data belum diterima; angka 0 berarti nihil kasus yang telah diverifikasi.

## Deploy
Konfigurasi Render tersedia pada `render.yaml`; Docker tersedia pada `Dockerfile`. Lihat `docs/DEPLOY.md`.

## Batas interpretasi
Target model adalah kejadian kasus tercatat pada bulan berikutnya. Skor menunjukkan prioritas relatif, bukan diagnosis individu atau probabilitas klinis. Metrik 2023 merupakan evaluasi retrospektif pada dataset tersebut.
