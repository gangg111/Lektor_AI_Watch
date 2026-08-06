# Lektor AI -- pilot na Wear OS

Sterownik do [Lektor AI](https://github.com/gangg111/Lektor_AI) na zegarek z Wear OS. Startuj i zatrzymuj renderowanie filmow z nadgarstka, bez wyciagania telefonu.

Zegarek laczy sie bezposrednio z mostem HTTP w aplikacji na PC -- zero posrednikow, zero chmury. Wykrywa komputer sam (broadcast UDP + zamiatanie podsieci), paruje sie 6-cyfrowym PIN-em i dziala w tej samej sieci Wi-Fi. Poza domem przez tunel cloudflared (wymaga apki mobilnej jako przekaźnika).

## Co pokazuje

- **Luk postepu** przy krawedzi tarczy -- widzisz na pierwszy rzut oka, ile jeszcze zostało
- **Procent i licznik** -- np. "72%" + "3 / 8 filmow"
- **Przycisk start/stop** -- jedna pastylka, przełącza renderowanie na PC
- **Kolejka filmow** -- przesuniecie w lewo: lista z miniaturami, nazwami i parametrami (rozdzielczosc, czas, rozmiar)
- **Log z PC** -- pionowy gest na tarczy otwiera log z komputera (kolorowany po znacznikach)
- **Kafelek Wear OS** -- te same informacje na glownej tarczy zegarka (luk + procent + przycisk)
- **Tryb Always-On** -- uproszczony widok na wygaszonym ekranie, zero wypalania pikseli

## Wymagania

- Zegarek z Wear OS 3.0 lub nowszym (Galaxy Watch4 i nowsze, Pixel Watch, itp.)
- [Lektor AI](https://github.com/gangg111/Lektor_AI) na PC (v2.3.0 lub nowszy, z wlaczonym mostem w panelu "Zdalne sterowanie")
- Obie maszyny w tej samej sieci Wi-Fi

## Instalacja

Pobierz APK z zakladki [Releases](https://github.com/gangg111/LektorAI_Watch/releases) i wgraj przez ADB:

```
adb install LektorAI-Watch-1.0.0.apk
```

Albo przez Wireless Debugging (Ustawienia -> Opcje programisty -> Debugowanie bezprzewodowe -> Sparuj z kodem).

## Pierwsze uruchomienie

1. Na PC: otworz panel "Zdalne sterowanie", wlacz most, skopiuj PIN
2. Na zegarku: otworz Lektor AI, wpisz PIN, kliknij "Paruj"
3. Gotowe -- tarcza pokazuje stan "GOTOWY" i liczbe filmow w kolejce

## Budowanie ze zrodla

```bash
git clone https://github.com/gangg111/LektorAI_Watch.git
cd LektorAI_Watch
./gradlew assembleRelease
```

APK wyladuje w `app/build/outputs/apk/release/`. Do podpisu potrzebujesz wlasnego `keystore.properties` (nie ma go w repo).

## Technicznie

- **Jezyk:** Kotlin
- **UI:** Android Views + Canvas (zero Compose -- oszczednosc APK, narzut ~40 KB zamiast ~2 MB)
- **Komunikacja:** REST/JSON przez OkHttp 4.12, long-polling zamiast SSE (Wear usypia radio i zrywa dlugie strumienie przy gaszeniu ekranu)
- **Wykrywanie PC:** broadcast UDP `LEKTORAI?` na porcie 45455 + zamiatanie podsieci /24 jako rezerwa
- **Cache:** LruCache na miniatury (8 pozycji), bufor logu w pamieci (pierscien 200 linii)
- **Rozmiar APK:** ~180 KB (arm64-v8a)

## Zaleznosci

- [OkHttp](https://square.github.io/okhttp/) -- klient HTTP
- [Gson](https://github.com/google/gson) -- JSON
- [AndroidX Wear](https://developer.android.com/jetpack/androidx/releases/wear) -- tryb ambientowy
- [Wear Tiles / ProtoLayout](https://developer.android.com/training/wearables/tiles) -- kafelek na tarczy
- [Kotlin Coroutines](https://github.com/Kotlin/kotlinx.coroutines) -- asynchronicznosc
