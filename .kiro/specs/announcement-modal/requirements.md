# Requirements Document

## Introduction

Fitur popup modal pengumuman untuk menginformasikan kepada pengunjung website OMDI 7 tentang penundaan pelaksanaan acara akibat bencana alam dan putusnya akses jalan. Modal akan muncul secara otomatis beberapa detik setelah halaman dimuat dengan tampilan yang menarik dan profesional.

## Glossary

- **Modal**: Jendela dialog yang muncul di atas konten halaman utama untuk menampilkan informasi penting
- **Popup**: Elemen UI yang muncul secara otomatis di atas konten halaman
- **Auto-display**: Fitur yang menampilkan modal secara otomatis setelah delay waktu tertentu
- **Close Button**: Tombol yang memungkinkan pengguna menutup modal
- **Overlay**: Lapisan semi-transparan di belakang modal yang menggelapkan konten halaman

## Requirements

### Requirement 1

**User Story:** Sebagai pengunjung website, saya ingin melihat pengumuman penting tentang penundaan acara segera setelah membuka website, sehingga saya mendapat informasi terkini tentang jadwal pelaksanaan OMDI 7.

#### Acceptance Criteria

1. WHEN a user loads the website THEN the system SHALL display the announcement modal automatically after 3 seconds
2. WHEN the modal is displayed THEN the system SHALL show a semi-transparent overlay behind the modal
3. WHEN the modal appears THEN the system SHALL prevent scrolling of the background content
4. WHEN the page is still loading THEN the system SHALL wait until the page is fully loaded before starting the delay timer
5. WHEN the modal is displayed THEN the system SHALL center it on the viewport

### Requirement 2

**User Story:** Sebagai pengunjung website, saya ingin membaca pengumuman dengan jelas dalam tampilan yang menarik, sehingga saya dapat memahami informasi penundaan dengan baik.

#### Acceptance Criteria

1. WHEN the modal is displayed THEN the system SHALL show the complete announcement text with proper formatting
2. WHEN the modal is rendered THEN the system SHALL display a title "PENGUMUMAN PENTING" at the top
3. WHEN the modal content is shown THEN the system SHALL include the disaster reason, new date (Sabtu, 24 Januari 2026), and closing signature
4. WHEN the modal is displayed THEN the system SHALL use readable typography with appropriate font sizes and line spacing
5. WHEN the modal is rendered THEN the system SHALL apply visual styling with colors, borders, and shadows for professional appearance

### Requirement 3

**User Story:** Sebagai pengunjung website, saya ingin dapat menutup modal pengumuman setelah membacanya, sehingga saya dapat melanjutkan menjelajahi website.

#### Acceptance Criteria

1. WHEN the modal is displayed THEN the system SHALL show a close button labeled "Tutup"
2. WHEN a user clicks the close button THEN the system SHALL hide the modal immediately
3. WHEN the modal is closed THEN the system SHALL restore scrolling capability to the background content
4. WHEN the modal is closed THEN the system SHALL remove the overlay
5. WHEN a user clicks outside the modal on the overlay THEN the system SHALL close the modal

### Requirement 4

**User Story:** Sebagai pengunjung website di berbagai perangkat, saya ingin modal pengumuman tampil dengan baik di layar saya, sehingga saya dapat membaca pengumuman dengan nyaman.

#### Acceptance Criteria

1. WHEN the modal is displayed on desktop devices THEN the system SHALL render the modal with appropriate width and padding
2. WHEN the modal is displayed on mobile devices THEN the system SHALL adjust the modal width to fit the screen
3. WHEN the modal is displayed on small screens THEN the system SHALL maintain readability with responsive font sizes
4. WHEN the viewport is resized THEN the system SHALL keep the modal centered
5. WHEN the modal is displayed on any device THEN the system SHALL ensure all content is visible without horizontal scrolling
