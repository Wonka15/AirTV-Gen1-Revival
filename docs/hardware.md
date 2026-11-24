# AirTV Player — hardware and feature notes

This document separates manufacturer-published capabilities, the supplied retail-style specification listing, and secondary hardware identification. The project targets the original first-generation AirTV Player, not AirTV Mini or AirTV 2.

## Manufacturer-published hardware

The official AirTV product page lists:

| Feature | Published information |
|---|---|
| Memory | 2 GB DDR RAM |
| Internal storage | 8 GB flash |
| Maximum decode / video resolution | 4Kp60 |
| Wi-Fi | Internal 802.11ac 2x2 dual-band (2.4 GHz and 5 GHz) |
| USB | 2 × USB 2.0 |
| HDMI | HDMI 2.0 / HDCP 2.2 |
| Ethernet | Yes |
| Optical audio | Listed by AirTV under connections as optical input |
| Video decode | MPEG-2, MPEG-4, HEVC, VP9 |
| Audio | Dolby Digital / Dolby Digital Plus |
| Bluetooth | Yes; Bluetooth-capable remote |
| Infrared | Front-facing IR lens and IR remote support |
| Dimensions | 132 × 132 × 26 mm |
| Chassis | White and blue |

Source: [AirTV Player official product page](https://www.airtv.net/products/airtv_player/).

## Product features and intended use

AirTV marketed the Player as a combined streaming and over-the-air television interface:

- Android TV with access to apps and games through Google Play.
- Integration with Sling and Netflix, plus other streaming apps.
- Chromecast built-in.
- Bluetooth support for accessories such as headphones, speakers, and game controllers.
- Remote with voice search, one-touch access to Netflix and Google, and a remote finder.
- USB-host local playback and external storage are listed in the supplied retail-style specifications; these functions should be tested on the actual unit before being treated as confirmed in every firmware build.

### OTA television and DVR

The AirTV Player alone does not contain the OTA tuner described in the marketing material. To receive local broadcast channels, the official product page says users need the AirTV Player, an AirTV Adapter, and an antenna. Local-channel DVR additionally requires an external hard drive. The official product sheet describes single- and dual-tuner adapter options. Availability of ABC, CBS, NBC, FOX, PBS, and other channels depends on antenna reception and location.

## Processor and graphics

The AirTV Player uses a **quad-core 1.2 GHz ARM Cortex-A53 processor** paired with a **Vivante GC7000XS GPU**. Device references identify the platform as the **Marvell Armada 1500 Ultra BG4CT**.

A supplied retailer-style listing says “Single Core.” That entry conflicts with the quad-core identification in device references and a launch-era TechSpot hardware review, so this project treats “Single Core” as a catalog/listing error rather than the device specification.

References:
- [Android TV Guide — DISH AirTV Player](https://www.androidtv-guide.com/pay-tv-provider/dish-airtv-player/)
- [TechSpot — AirTV Player and Adapter Review](https://www.techspot.com/review/1451-air-tv/)
- [DeviWiki — Marvell BG4CT platform references](https://deviwiki.com/wiki/Marvell)

**Verification still required:** read the top marking on the SoC package on this exact motherboard and confirm the device model from its exterior label. The current motherboard photograph does not show a legible SoC marking.

## Release date discrepancy

The supplied listing says 2017. Android TV Guide records the model as 2016, while the TechSpot review is from 2017. Treat 2017 as the listing's stated release date, not a definitive launch date.

## Board observations from the supplied photograph

- Silkscreen labels visible: `PCB 209321` and `SCH 209317`.
- A group of pads is labeled `UART`.
- Two coaxial antenna leads/connectors are visible near the top edge.
- The barcode/assembly sticker appears to include `R509344-09`; confirm with a sharp close-up.

A UART label does not establish pin order, voltage, logic level, baud rate, or whether a boot console is enabled. Do not connect an adapter until ground and voltage levels are independently verified. Never assume a header is 5 V tolerant.

## Research status

No alternative operating system, custom firmware, root method, UART console, or game-streaming client is currently claimed to work. These remain research targets.

## Sources

1. [AirTV Player official product page](https://www.airtv.net/products/airtv_player/)
2. [AirTV Player official product sheet (PDF)](https://order.dish.com/products/airtv_player/downloads/AirTV_ProductSheet.pdf)
3. [Android TV Guide — AirTV Player](https://www.androidtv-guide.com/pay-tv-provider/dish-airtv-player/)
4. [TechSpot — AirTV Player and Adapter Review](https://www.techspot.com/review/1451-air-tv/)
