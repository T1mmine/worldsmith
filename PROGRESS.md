# PROGRESS

Oturumlar arası durum kaydı. Her oturum başında okunur; önemli bir iş bitince veya oturum kapanmadan önce güncellenir.
Proje özeti ve öncelik sırası için bkz. `CLAUDE.md`.

## Son güncelleme
2026-10-09

## Durum
- `src.html`: çalışan tek sayfalık demo (three.js sahne, CodeMirror editör, 4 görev, TR/EN, Web Worker'da kullanıcı kodu).
- Koç hâlâ kural tabanlı; LLM koçu yok (en büyük eksik, CLAUDE.md "Next steps" #1).
- Klasör henüz git reposu değil.

## Devam eden: GitHub kurulumu (bekliyor)
Plan: public `worldsmith` reposu → 2 collaborator (push) → main koruması (1 onaylı PR, doğrudan push yok, enforce_admins kapalı) → `.gitignore` (node_modules, .env, dist) + `.env.example` bir PR ile main'e.

Engeller:
- [ ] `gh` CLI kurulu değil (`winget install --id GitHub.cli`, sonra `gh auth login`).
- [ ] Mevcut dosyalar mı repoya alınacak, yoksa boş klasörde sadece README ile mi başlanacak? Karar bekleniyor.
- [ ] Collaborator'ların gerçek GitHub kullanıcı adları gerekli (ARKADAS1/ARKADAS2 yer tutucu).

## Sıradaki işler
1. GitHub kurulumunu tamamla (yukarıdaki engeller çözülünce).
2. LLM koçu + Python backend (CLAUDE.md #1).
