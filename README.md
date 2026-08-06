# Lektor AI - pilot na Wear OS

Sterownik do [Lektor AI](https://github.com/gangg111/Lektor_AI) na zegarek z Wear OS. Startuj i zatrzymuj renderowanie filmów z nadgarstka, bez wyciągania telefonu.

Zegarek łączy się bezpośrednio z mostem HTTP w aplikacji na PC - zero pośredników, zero chmury. Wykrywa komputer sam (broadcast UDP + zamiatanie podsieci), paruje się 6-cyfrowym PIN-em i działa w tej samej sieci Wi-Fi. Poza domem przez tunel cloudflared (wymaga apki mobilnej jako przekaźnika).

## Co pokazuje

- **Łuk postępu** przy krawędzi tarczy - widzisz na pierwszy rzut oka, ile jeszcze zostało
- **Procent i licznik** - np. "72%" + "3 / 8 filmów"
- **Przycisk start/stop** - jedna pastylka, przełącza renderowanie na PC
- **Kolejka filmów** - przesunięcie w lewo: lista z miniaturami, nazwami i parametrami (rozdzielczość, czas, rozmiar)
- **Log z PC** - pionowy gest na tarczy otwiera log z komputera (kolorowany po znacznikach)
- **Kafelek Wear OS** - te same informacje na głównej tarczy zegarka (łuk + procent + przycisk)
- **Tryb Always-On** - uproszczony widok na wygaszonym ekranie, zero wypalania pikseli

## Wymagania

- Zegarek z Wear OS 3.0 lub nowszym (Galaxy Watch4 i nowsze, Pixel Watch, itp.)
- [Lektor AI](https://github.com/gangg111/Lektor_AI) na PC (v2.3.0 lub nowszy, z włączonym mostem w panelu "Zdalne sterowanie")
- Obie maszyny w tej samej sieci Wi-Fi

## Instalacja

Pobierz APK z zakładki [Releases](https://github.com/gangg111/LektorAI_Watch/releases) i wgraj przez ADB:
