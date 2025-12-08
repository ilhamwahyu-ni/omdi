# Design Document

## Overview

Fitur popup modal pengumuman adalah komponen UI yang menampilkan informasi penting tentang penundaan pelaksanaan OMDI 7 kepada pengunjung website. Modal akan muncul secara otomatis 3 detik setelah halaman selesai dimuat, dengan tampilan yang menarik, profesional, dan responsif di semua perangkat.

## Architecture

Solusi ini menggunakan pendekatan client-side dengan HTML, CSS, dan vanilla JavaScript:

1. **HTML Structure**: Modal markup ditambahkan ke dalam index.html dengan struktur semantic
2. **CSS Styling**: Styling modal menggunakan CSS modern dengan flexbox untuk centering dan responsive design
3. **JavaScript Logic**: Script untuk mengontrol timing, display, dan interaksi modal

Komponen ini bersifat standalone dan tidak memerlukan library eksternal, sehingga ringan dan mudah dimaintain.

## Components and Interfaces

### HTML Components

1. **Modal Container** (`#announcementModal`)

   - Wrapper utama dengan fixed positioning
   - Overlay semi-transparan
   - Z-index tinggi untuk tampil di atas semua konten

2. **Modal Content** (`.announcement-modal-content`)

   - Container untuk konten modal
   - Background putih dengan border radius
   - Box shadow untuk depth effect

3. **Modal Header**

   - Title "PENGUMUMAN PENTING"
   - Icon atau emoji untuk visual appeal

4. **Modal Body**

   - Paragraf pengumuman dengan formatting
   - Informasi tanggal baru yang di-highlight
   - Signature panitia

5. **Close Button** (`.announcement-close-btn`)
   - Tombol dengan label "Tutup"
   - Positioned di bagian bawah modal
   - Hover effects untuk interactivity

### JavaScript Interface

```javascript
// Modal control functions
function showAnnouncementModal()
function hideAnnouncementModal()
function initAnnouncementModal()
```

### CSS Classes

- `.announcement-modal`: Container styling
- `.announcement-modal-content`: Content box styling
- `.announcement-modal.show`: Visible state
- `.announcement-close-btn`: Button styling

## Data Models

Tidak ada data model kompleks yang diperlukan. Konten pengumuman adalah static HTML text yang embedded langsung dalam markup.

```javascript
// Configuration constants
const MODAL_DELAY = 3000; // 3 seconds in milliseconds
```

## Correctness Properties

_A property is a characteristic or behavior that should hold true across all valid executions of a system-essentially, a formal statement about what the system should do. Properties serve as the bridge between human-readable specifications and machine-verifiable correctness guarantees._

### Property 1: Modal display shows overlay

_For any_ state where the modal is displayed, the overlay element should be visible with semi-transparent background styling
**Validates: Requirements 1.2**

### Property 2: Modal display prevents background scrolling

_For any_ state where the modal is displayed, the body element should have overflow set to hidden
**Validates: Requirements 1.3**

### Property 3: Modal is centered in viewport

_For any_ viewport size, when the modal is displayed, it should be centered both horizontally and vertically
**Validates: Requirements 1.5**

### Property 4: Close button hides modal

_For any_ state where the modal is visible, clicking the close button should result in the modal being hidden
**Validates: Requirements 3.2**

### Property 5: Modal close restores scrolling

_For any_ modal close action, the body overflow should be restored to its original value (allowing scrolling)
**Validates: Requirements 3.3**

### Property 6: Modal close removes overlay

_For any_ modal close action, the overlay should be hidden or removed from view
**Validates: Requirements 3.4**

### Property 7: Responsive width adjustment

_For any_ viewport width, the modal should adjust its width to fit within the screen boundaries with appropriate margins
**Validates: Requirements 4.2**

### Property 8: Viewport resize maintains centering

_For any_ viewport resize event while modal is displayed, the modal should remain centered in the viewport
**Validates: Requirements 4.4**

### Property 9: No horizontal overflow

_For any_ viewport size, when the modal is displayed, the modal content should not cause horizontal scrolling
**Validates: Requirements 4.5**

## Error Handling

1. **Missing DOM Elements**: Script should check for existence of modal elements before attempting to manipulate them
2. **Multiple Modal Instances**: Ensure only one modal instance can be displayed at a time
3. **Timer Conflicts**: Clear any existing timers before setting new ones to prevent multiple modal displays
4. **Event Listener Cleanup**: Remove event listeners when modal is destroyed to prevent memory leaks

## Testing Strategy

### Unit Testing

Unit tests akan fokus pada:

- Verifikasi elemen modal ada dalam DOM
- Verifikasi konten pengumuman lengkap (judul, isi, tanggal, signature)
- Verifikasi tombol close ada dan memiliki label yang benar
- Verifikasi CSS classes diterapkan dengan benar
- Verifikasi timing delay (3 detik)
- Verifikasi click outside to close functionality

### Property-Based Testing

Property-based testing akan menggunakan **fast-check** library untuk JavaScript. Setiap property test akan dikonfigurasi untuk menjalankan minimum 100 iterasi.

Property tests akan mencakup:

1. **Property 1**: Modal display shows overlay - Generate random modal states, verify overlay visibility
2. **Property 2**: Modal display prevents scrolling - Generate random modal display events, verify body overflow
3. **Property 3**: Modal centering - Generate random viewport sizes, verify modal centering
4. **Property 4**: Close button functionality - Generate random modal states, verify close action
5. **Property 5**: Scroll restoration - Generate random close events, verify overflow restoration
6. **Property 6**: Overlay removal - Generate random close events, verify overlay hidden
7. **Property 7**: Responsive width - Generate random viewport widths, verify modal fits
8. **Property 8**: Resize centering - Generate random resize events, verify centering maintained
9. **Property 9**: No horizontal overflow - Generate random viewport sizes, verify no overflow-x

Setiap property-based test akan di-tag dengan format:
`**Feature: announcement-modal, Property {number}: {property_text}**`

### Integration Testing

Integration tests akan memverifikasi:

- Modal terintegrasi dengan baik dalam halaman existing
- Tidak ada konflik dengan modal lain yang sudah ada (modal dan modal2)
- Z-index layering bekerja dengan benar
- Tidak mengganggu fungsi lain di halaman

### Manual Testing Checklist

- [ ] Modal muncul setelah 3 detik di berbagai browser (Chrome, Firefox, Safari, Edge)
- [ ] Tampilan visual sesuai dengan design yang diinginkan
- [ ] Responsiveness di berbagai ukuran layar (mobile, tablet, desktop)
- [ ] Accessibility: keyboard navigation (ESC key untuk close)
- [ ] Performance: tidak ada lag saat modal muncul/hilang

## Implementation Notes

1. **Styling Consistency**: Gunakan CSS variables yang sudah ada (--purple-primary, --text-primary, dll) untuk konsistensi dengan design system
2. **Animation**: Tambahkan smooth fade-in/fade-out animation untuk better UX
3. **Accessibility**:
   - Tambahkan ARIA attributes (role="dialog", aria-modal="true")
   - Support ESC key untuk close modal
   - Focus trap dalam modal saat terbuka
4. **Performance**: Gunakan CSS transforms untuk animation (lebih performant daripada position changes)
5. **Z-index Management**: Pastikan z-index lebih tinggi dari modal existing (modal: 9999, modal2: 9998)
