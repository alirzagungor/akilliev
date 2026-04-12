# Apple Home + Homebridge Webhook Kurulumu (Shortcuts ve Home Assistant olmadan)

Bu doküman, `index.html` panelindeki AÇ/KPT butonlarını Homebridge webhook endpoint'lerine yönlendirir.

## 1) Homebridge tarafı

- Homebridge'i kur.
- Her cihaz için iki endpoint oluştur (on/off).
- Örnek endpoint deseni:
  - `POST /salon-tavan/on`
  - `POST /salon-tavan/off`
  - `POST /mutfak-tavan/on`
  - `POST /mutfak-tavan/off`

> Not: Endpoint adları `index.html` içindeki `shortcutWebhookMap` ile birebir aynı olmalıdır.

## 2) Panel tarafı

Panel şu iki değeri localStorage üzerinden okur:

- `bridge_base_url` (örn: `http://192.168.1.50:8581`)
- `bridge_token` (opsiyonel bearer token)

Safari konsolundan bir kez set etmek için:

```js
localStorage.setItem('bridge_base_url', 'http://192.168.1.50:8581');
localStorage.setItem('bridge_token', '');
location.reload();
```

## 3) Apple Home otomasyon eşleşmesi

Home app içinde her sanal switch için iki otomasyon oluştur:

- `Salon Tavan Virtual ON` aktif olunca -> `Salon Tavan` AÇ
- `Salon Tavan Virtual OFF` aktif olunca -> `Salon Tavan` KAPAT

Aynı deseni diğer cihazlara da uygula (Mutfak, Koridor, Yatak vb.).

## 4) Hızlı test

```bash
curl -X POST http://192.168.1.50:8581/salon-tavan/on
curl -X POST http://192.168.1.50:8581/salon-tavan/off
```

Panelde AÇ/KPT butonuna basınca kısa süreli `OK` görünmesi beklenir.
