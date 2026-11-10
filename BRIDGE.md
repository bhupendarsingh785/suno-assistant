# Suno + MacroDroid Bridge — phone ka asli control

Suno (browser page) awaaz sunta hai. MacroDroid (phone app) haath ka kaam karta hai.
Dono ko ek **webhook URL** jodta hai.

## 1. MacroDroid me webhook URL banao (ek hi baar)

1. MacroDroid kholo → **Add Macro**
2. Trigger dabao → **Connectivity → Webhook (URL)**
3. **Identifier** likho: `wifi_off` (chhote akshar, bina space)
4. Trigger save karo — MacroDroid apne aap ek URL banata hai:
   `https://trigger.macrodroid.com/<device-id>/wifi_off`
5. Us URL ka pehla hissa copy karo — `https://trigger.macrodroid.com/<device-id>/` — Suno ke Settings → **Phone Bridge** me daal do, Save dabao.

Uske baad Suno me bolo: **"wifi band karo"** → Suno webhook hit karega → MacroDroid macro chalayega.

## 2. Har command ke liye ek macro

| Bolo | Identifier | Macro me action |
|---|---|---|
| wifi band karo | `wifi_off` | Connectivity → WiFi off (Shizuku/root chahiye ho sakta hai) |
| wifi chalu karo | `wifi_on` | WiFi on |
| torch chalu karo | `torch_on` | Torch on |
| torch band karo | `torch_off` | Torch off |
| volume badhao | `volume_up` | Volume up |
| volume ghatao | `volume_down` | Volume down |
| brightness up/down | `brightness_up` / `brightness_down` | Screen brightness |
| bluetooth on/off | `bt_on` / `bt_off` | Bluetooth |
| dnd on/off | `dnd_on` / `dnd_off` | Do Not Disturb |
| airplane on/off | `airplane_on` / `airplane_off` | Airplane mode |
| hotspot on/off | `hotspot_on` / `hotspot_off` | Hotspot |
| screenshot lo | `screenshot` | Take screenshot |
| phone lock karo | `lock_screen` | Lock screen |
| bridge test | `bridge_test` | Vibrate + notification (test ke liye) |

MacroDroid free version me **5 macro** hi ban sakte hain. Shuru me in 5 se test karo:
`bridge_test`, `torch_on`, `torch_off`, `volume_up`, `volume_down`.

## 3. Sach — kya nahi hoga

- Webhook ko **internet + Google Play services** chahiye. Net band ho to signal nahi pahunchega.
- Bahut zyada webhook calls karne par MacroDroid ka server thodi der block kar sakta hai.
- **WiFi, mobile data, airplane mode** jaise toggle Android 10+ par app ko seedha nahi deta — MacroDroid ko **Shizuku** ya root chahiye hota hai. Bina uske macro "fail" dikhayega.
- Screen locked ho to UI tap wale macro nahi chalenge.
- Suno khud kuch nahi badal sakta — jo macro tum banaoge, wahi chalega.

## 4. Test kaise karo

1. `bridge_test` macro banao: Webhook trigger + action **Vibrate** (1000 ms).
2. Suno → Settings → Phone Bridge me URL daalo → **Bridge test karo** dabao.
3. Phone guna ho gaya = bridge jud gaya. Nahi hua to URL ka device-id galat hai.
