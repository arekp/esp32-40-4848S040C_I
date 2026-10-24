# ESP32-4848S040C_I — HA Panel

Panel dotykowy Home Assistant na płytce **Guition ESP32-S3-4848S040C_I**
(4" IPS 480×480, ST7701S, dotyk GT911, 3 przekaźniki), zbudowany w **ESPHome + LVGL**.

## Funkcje

- Sterowanie gniazdkami (switch) z poziomu ekranu dotykowego
- Podgląd mocy, zużycia energii, temperatury i wilgotności z HA
- Sterowanie odtwarzaczami multimedialnymi i pogoda
- Zegar, regulacja jasności, wygaszanie ekranu

## Wymagania

- [ESPHome](https://esphome.io/) >= 2024.6.0
- Home Assistant z włączonym natywnym API ESPHome
- Płytka Guition ESP32-S3-4848S040C_I (szczegóły sprzętu: [cloud.MD](cloud.MD))

## Uruchomienie

1. Skopiuj `secrets.yaml.example` do `secrets.yaml` i uzupełnij dane (plik jest w `.gitignore`).
2. W `ha-panel.yaml` zmień w sekcji `substitutions` oraz w sensorach/przełącznikach
   identyfikatory encji na własne z Home Assistanta.
3. Wgraj firmware (pierwszy raz przez USB):

   ```
   esphome run ha-panel.yaml
   ```

4. Kolejne aktualizacje: OTA (`esphome run ha-panel.yaml` wybierając urządzenie sieciowe).

## Struktura

| Plik | Opis |
|------|------|
| `ha-panel.yaml` | Główna konfiguracja ESPHome (wyświetlacz, dotyk, LVGL, encje HA) |
| `secrets.yaml.example` | Szablon sekretów |
| `cloud.MD` | Specyfikacja sprzętu i mapa pinów |

## Uwagi sprzętowe

- Inicjalizacja ST7701S musi być typu 9, inaczej ekran pozostaje czarny.
- GPIO 33–37 zajęte przez Octal PSRAM.
- SD i LCD współdzielą GPIO 47/48.

## Zasoby

- [ESPHome device page](https://devices.esphome.io/devices/guition-esp32-s3-4848s040)
- [NorthernMan54/ESP32-4848S040](https://github.com/NorthernMan54/ESP32-4848S040)
- [atomic14 – gotchas](https://www.atomic14.com/esp32/boards/guition-4848s040/)

## Licencja

MIT — zobacz [LICENSE](LICENSE).
