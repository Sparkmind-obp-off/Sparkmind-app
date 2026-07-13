# ADR-0002: SDOS — Knowledge Hidup di Repository, Bukan di System Prompt

> **Versi**: 1.2 · **Status dokumen**: Partially Superseded by [ADR-0006](ADR-0006-sdos-v2-context-driven-operations.md)
> **Terakhir diperbarui**: 2026-07-13 (Sprint 003)
> **Terkait**: [DECISION_LOG.md](../DECISION_LOG.md) · [README SDOS](../README.md) · [ADR-0006](ADR-0006-sdos-v2-context-driven-operations.md)

- **Tanggal**: 2026-07-13
- **Status**: ✅ Accepted
- **Diputuskan oleh**: CTO

---

## Konteks

Sparkmind menggunakan AI Engineer (GenSpark AI Developer, dan berpotensi AI
lain) sebagai anggota engineering team. Muncul kebutuhan: di mana aturan,
knowledge, dan state proyek disimpan agar konsisten antar sesi dan antar AI?

Opsi yang sempat dipertimbangkan: system prompt yang sangat panjang
(ribuan kata) berisi semua aturan dan knowledge.

## Keputusan

Kami membangun **SDOS (Sparkmind Development Operating System)** di dalam
repository, pada folder `.sparkmind/`, dengan pembagian tegas:

| Tempat | Isi |
|--------|-----|
| System Prompt | Identitas, perilaku, prinsip kerja (pendek & stabil) |
| `.sparkmind/` | Semua knowledge, standar, sprint, keputusan, state |
| Task/Mission | Pekerjaan spesifik satu sesi |

Struktur awal SDOS mencakup constitution, state, context, workflows, standards, sprints, decisions, templates, proposals, dan reports. **Layout operasional ini kemudian disederhanakan oleh ADR-0006; keputusan menyimpan knowledge di repository tetap berlaku.**

## Alasan

1. System prompt bukan tempat menyimpan knowledge — ia akan menjadi "tempat
   sampah" yang terus membengkak dan sulit dipelihara.
2. Repository sebagai Single Source of Truth membuat knowledge ter-version,
   ter-review, dan bisa dipakai AI mana pun (tidak terkunci ke satu vendor AI).
3. State yang ter-version menjembatani hilangnya memori antar sesi AI (kini `CURRENT_STATE.md` sesuai ADR-0006).

## Alternatif yang Dipertimbangkan

| Alternatif | Kenapa tidak dipilih |
|------------|----------------------|
| System prompt panjang (5000 kata) | Tidak stabil, akan diubah berulang kali, tidak ter-version dengan baik |
| Knowledge di chat/notion terpisah | Melanggar prinsip Single Source of Truth |

## Konsekuensi

- **Positif**: onboarding AI/manusia baru = baca `.sparkmind/`; system prompt
  stabil; knowledge ter-version di git.
- **Negatif (historis)**: struktur awal menuntut terlalu banyak context loading dan sinkronisasi dokumen.
- **Ditinjau ulang**: ADR-0006 menyederhanakan layout, workflow, dan update triggers setelah friksi Sprint 002.
