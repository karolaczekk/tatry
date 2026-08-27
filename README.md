# Tatry — planer 7 dni (PWA)

Interaktywny planer trekkingowy przygotowany jako **Progressive Web App**. Repozytorium można hostować bezpośrednio na **GitHub Pages**, a następnie dodać aplikację do ekranu początkowego iPhone'a/iPada.

## Zawartość

- `index.html` — planer
- `manifest.webmanifest` — manifest PWA
- `sw.js` — service worker / cache aplikacji
- `icons/` — ikony aplikacji, w tym Apple Touch Icon
- `.github/workflows/pages.yml` — automatyczny deploy do GitHub Pages
- `.nojekyll` — wyłącza przetwarzanie Jekyll

## Publikacja na GitHub Pages

1. Utwórz nowe repozytorium na GitHubie, np. `tatry-planer`.
2. Wgraj całą zawartość tego folderu do gałęzi `main`.
3. Wejdź w **Settings → Pages**.
4. W **Build and deployment → Source** wybierz **GitHub Actions**.
5. Workflow `Deploy PWA to GitHub Pages` opublikuje stronę automatycznie.
6. Po wdrożeniu GitHub pokaże adres podobny do `https://NAZWA-UZYTKOWNIKA.github.io/tatry-planer/`.

> PWA i service worker wymagają HTTPS. GitHub Pages zapewnia HTTPS, dlatego jest dobrym hostem dla tej paczki.

## Instalacja na iOS

1. Otwórz opublikowany adres w **Safari** na iPhonie lub iPadzie.
2. Naciśnij **Udostępnij**.
3. Wybierz **Dodaj do ekranu początkowego**.
4. Potwierdź nazwę i wybierz **Dodaj**.
5. Uruchamiaj planer z ikony na ekranie początkowym — otworzy się w trybie standalone, bez typowego paska Safari.

## Offline

Sam planer, manifest, ikony i biblioteka Leaflet są cache'owane po pierwszym uruchomieniu. **Kafelki mapy OpenStreetMap pozostają funkcją online** i nie są masowo zapisywane do cache. Dane checklisty oraz własna lokalizacja noclegu są przechowywane lokalnie w przeglądarce (`localStorage`).

## Aktualizacje

Po zmianie plików i wypchnięciu ich do `main` GitHub Actions wdroży nową wersję. Jeśli wprowadzisz duże zmiany w assetach, zwiększ numer cache w `sw.js`, np. z `tatry-pwa-v1` na `tatry-pwa-v2`.

## Test lokalny

Service worker nie działa poprawnie przy otwieraniu pliku bezpośrednio jako `file://`. Uruchom prosty serwer HTTP, np.:

```bash
python3 -m http.server 8080
```

Następnie otwórz `http://localhost:8080/`.

## Safari / ikony po aktualizacji

Paczka zawiera osobne `favicon.ico`, favicony PNG i `apple-touch-icon`, a odnośniki do ikon są wersjonowane (`?v=3`). Jeżeli Safari nadal pokazuje starą ikonę po deployu, usuń istniejącą zakładkę / ikonę z ekranu początkowego, zamknij Safari i dodaj ją ponownie po wejściu na nowo opublikowaną stronę. Safari potrafi długo przechowywać cache ikon dla tej samej domeny GitHub Pages.
