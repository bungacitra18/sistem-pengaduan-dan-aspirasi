# Design System & UI Guidelines
## Sistem Pengaduan dan Aspirasi (Help Desk Ticket)

Dokumen ini memuat standar visual, aturan komponen interaktif, dan panduan desain Tailwind CSS untuk diimplementasikan oleh AI dan pengembang pada proyek Help Desk Ticket.

---

### 1. Palet Warna (Tailwind CSS Tokens)

Aplikasi mengadopsi palet warna modern bertema *Clean Slate & Trustworthy Indigo* dengan kontras tinggi untuk kenyamanan baca petugas dan publik:

| Kategori Peran | Tailwind Class | Nilai HEX / CSS Var | Kegunaan Spesifik |
|---|---|---|---|
| **Canvas Background** | `bg-slate-50` | `#F8FAFC` | Latar belakang utama seluruh halaman antarmuka. |
| **Card / Surface** | `bg-white` | `#FFFFFF` | Latar belakang kartu form, tabel, dan kartu KPI. |
| **Card Border** | `border-slate-200` | `#E2E8F0` | Garis pembatas kartu, input, dan tabel pembagi baris. |
| **Text Primary** | `text-slate-900` | `#0F172A` | Teks judul utama, nomor tiket, dan header tabel. |
| **Text Secondary** | `text-slate-600` | `#475569` | Label form, deskripsi pembantu, dan teks tabel sekunder. |
| **Text Muted** | `text-slate-400` | `#94A3B8` | Placeholder input dan ikon non-aktif. |
| **Primary Brand** | `bg-indigo-600`, `text-indigo-600` | `#4F46E5` | Tombol simpan/kirim utama, link aktif, dan elemen fokus. |
| **Primary Hover** | `hover:bg-indigo-700` | `#4338CA` | State hover pada tombol primer. |
| **Status Pending (Danger)** | `bg-rose-50`, `text-rose-700`, `border-rose-200` | `#FFF1F2`, `#BE123C` | Badge status `Pending` dan Alert Banner error validasi. |
| **Status Diproses (Warning)** | `bg-amber-50`, `text-amber-700`, `border-amber-200`| `#FFFBEB`, `#B45309` | Badge status `Diproses` (sedang dalam penanganan teknisi). |
| **Status Selesai (Success)** | `bg-emerald-50`, `text-emerald-700`, `border-emerald-200`| `#ECFDF5`, `#047857` | Badge status `Selesai` dan badge "Supabase Connected". |

---

### 2. Tipografi & Format Lokalisasi

* **Keluarga Font (Font Family):** `font-sans` menggunakan font sans-serif modern (`Inter`, `Plus Jakarta Sans`, atau `ui-sans-serif, system-ui`).
* **Hirarki Ukuran Teks:**
  - Page Title: `text-2xl font-bold tracking-tight text-slate-900`
  - Section / Card Header: `text-lg font-semibold text-slate-800`
  - KPI Big Numbers: `text-3xl font-extrabold text-slate-900`
  - Body Text / Form Input: `text-sm font-normal text-slate-700`
  - Subtitle / Helper Text: `text-xs text-slate-500`
* **Lokalisasi Format Indonesia (`id-ID`):**
  - **Penanggalan:** Menggunakan standar `Intl.DateTimeFormat('id-ID', { dateStyle: 'medium', timeStyle: 'short' })` (contoh: *15 Nov 2026, 19.30 WIB*).
  - **Angka Metrik:** Pemisah ribuan dengan titik sesuai standar Indonesia.

---

### 3. Komponen Interaktif & State Standar

#### A. Tombol & Loading State
* Tombol primer wajib memiliki transisi halus (`transition-all duration-150 ease-in-out`).
* Saat proses transmisi data asynchronous ke Supabase berlangsung:
  - Tombol diberi atribut `disabled` dan class `opacity-70 cursor-not-allowed`.
  - Label teks berganti memuat spinner SVG: `<svg class="animate-spin ..."></svg> Menyimpan...`.

#### B. Alert Banner Validasi Gagal (`TC-01`)
* Komponen banner peringatan diletakkan tepat di bagian atas form pengaduan.
* Struktur class Tailwind:
  ```html
  <div id="alertBox" class="hidden mb-4 p-3.5 rounded-lg bg-rose-50 border border-rose-200 flex items-start gap-3 text-rose-800 text-sm">
    <svg class="w-5 h-5 text-rose-600 shrink-0 mt-0.5" fill="currentColor" viewBox="0 0 20 20">...</svg>
    <div id="alertMessage" class="font-medium">Deskripsi wajib diisi</div>
  </div>
  ```

#### C. Empty State Tabel
* Ditampilkan apabila data tiket masih kosong atau hasil pencarian tidak ditemukan:
  ```html
  <div class="py-12 flex flex-col items-center justify-center text-center">
    <div class="w-12 h-12 rounded-full bg-slate-100 flex items-center justify-center text-slate-400 mb-3">
      <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">...</svg>
    </div>
    <h4 class="text-sm font-semibold text-slate-700">Tidak ada tiket ditemukan</h4>
    <p class="text-xs text-slate-500 mt-1">Belum ada aduan yang terdaftar atau kata kunci tidak cocok.</p>
  </div>
  ```

#### D. Badges Status Penanganan
* Komponen status tiket wajib menggunakan struktur pill rounded dengan padding konsisten:
  - `Pending`: `<span class="inline-flex items-center px-2.5 py-0.5 rounded-full text-xs font-semibold bg-rose-50 text-rose-700 border border-rose-200">Pending</span>`
  - `Diproses`: `<span class="inline-flex items-center px-2.5 py-0.5 rounded-full text-xs font-semibold bg-amber-50 text-amber-700 border border-amber-200">Diproses</span>`
  - `Selesai`: `<span class="inline-flex items-center px-2.5 py-0.5 rounded-full text-xs font-semibold bg-emerald-50 text-emerald-700 border border-emerald-200">Selesai</span>`
