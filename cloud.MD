# Kontekst projektu ESP32-4848S040C_I

Jesteś moim asystentem i specem od elektroniki i programowania ESP32.
Budujemy projekt na płytce **Guition ESP32-4848S040C_I**.
Zawsze odpowiadaj po polsku.
Praca wyłącznie lokalna — ESP32 podpięty przez USB do komputera Windows 11.
Środowisko Python: `.venv` w katalogu projektu.

---

## Sprzęt: Guition ESP32-S3-4848S040C_I

### Procesor i pamięć

| Komponent | Specyfikacja |
|-----------|-------------|
| MCU | ESP32-S3R8 (dual-core Xtensa LX7) |
| Taktowanie | do 240 MHz |
| SRAM | 512 KB wbudowany |
| PSRAM | 8 MB (Octal SPI) |
| Flash | 16 MB |
| Wi-Fi | 2.4 GHz 802.11 b/g/n |
| Bluetooth | BLE 5.0 |
| Zasilanie | 5V, ~260 mA |

### Wyświetlacz

| Parametr | Wartość |
|----------|---------|
| Przekątna | 4.0 cala |
| Rozdzielczość | 480 × 480 px |
| Typ | IPS TFT |
| Sterownik LCD | ST7701S |
| Interfejs LCD | RGB565 równoległy (16-bit) |
| Backlight | GPIO 38 (PWM) |
| Inicjalizacja SPI | CS=GPIO39, SCK=GPIO48, MOSI=GPIO47 |

### Touch

| Parametr | Wartość |
|----------|---------|
| Kontroler | GT911 (Goodix) |
| Interfejs | I2C, adres 0x5D |
| SDA | GPIO 19 |
| SCL | GPIO 45 |

### Mapa pinów RGB (ST7701S)

| Kolor | GPIO |
|-------|------|
| PCLK | 21 |
| HSYNC | 16 |
| VSYNC | 17 |
| DE | 18 |
| R0–R4 | 11, 12, 13, 14, 0 |
| G0–G5 | 8, 20, 3, 46, 9, 10 |
| B0–B4 | 4, 5, 6, 7, 15 |

### MicroSD (TF Card)

| Sygnał | GPIO |
|--------|------|
| CS | 42 |
| MOSI | 47 (współdzielony z ST7701 init) |
| MISO | 41 |
| SCK | 48 (współdzielony z ST7701 init) |

### Przekaźniki (wariant C_I — wersja Industrial)

| Przekaźnik | GPIO |
|------------|------|
| Relay 1 | 40 |
| Relay 2 | 2 |
| Relay 3 | 1 |

### Ważne uwagi

- **Sekwencja inicjalizacji ST7701** musi być Type 9 — inne powodują czarny ekran
- **GPIO 0 i GPIO 3** to piny strappingowe — używane jednocześnie jako R0 i G2 w RGB, nie podłączać zewnętrznie
- **GPIO 33–37** zajęte przez Octal PSRAM (ESP32-S3R8) — niedostępne
- SD i LCD init dzielą GPIO 47 i 48 — inicjalizacja LCD odbywa się tylko raz przy starcie

---

## Środowisko deweloperskie

- Framework: **ESP-IDF** (lokalne)
- Biblioteka UI: **LVGL**
- Środowisko Python: `.venv` (Python 3.13)
- MCP zainstalowane w `.venv`:
  - `openocd-mcp` 0.4.5 — debugowanie przez OpenOCD (JTAG)
  - `mcp` 1.30.0

---

## Przydatne zasoby

- [NorthernMan54/ESP32-4848S040 – pinout](https://github.com/NorthernMan54/ESP32-4848S040)
- [MarcLob/GUITION-ESP32-4848S040-PlatformIO – PlatformIO + Arduino_GFX](https://github.com/MarcLob/GUITION-ESP32-4848S040-PlatformIO)
- [ESPHome device page – timingsi RGB](https://devices.esphome.io/devices/guition-esp32-s3-4848s040)
- [atomic14 – gotchas i specs](https://www.atomic14.com/esp32/boards/guition-4848s040/)
- [LCD Wizard – ST7701 Type 9 init](https://lcdwizard.com/boards/guition-4848s040)
