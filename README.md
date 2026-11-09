# Suno — awaaz se phone control (mirror kit v3)

Ek hi app, kai platform par. Koi server nahi, koi database nahi, koi account nahi.
Aapka data (notes, contacts, history, settings) sirf aapke phone me rehta hai.

## Folder me kya hai

| File | Kaam |
|---|---|
| `index.html` | poora app (ek hi file me) |
| `manifest.webmanifest` | phone me app ki tarah install hone ke liye |
| `sw.js` | offline cache (net band hone par bhi app khule) |
| `portal.html` | sabhi mirror jaanch kar chalu wala khol deta hai |
| `.gitlab-ci.yml` | GitLab Pages auto-deploy |
| `netlify.toml` / `vercel.json` | Netlify / Vercel ke settings |
| `README.md` | yahi guide |

## 1) Netlify Drop — sabse fast (account bhi nahi chahiye)
1. Browser me `app.netlify.com/drop` kholo.
2. Is poore folder ko drag-drop karo.
3. Turant `https://xxxx.netlify.app` link mil jayega. (Site name badal sakte ho.)
4. Account bana lo to link permanent.

## 2) GitHub Pages
1. github.com par naya public repo banao (e.g. `suno`).
2. "Add file → Upload files" se ye files upload karo (`.gitlab-ci.yml`, `netlify.toml`, `vercel.json` ki zaroorat nahi).
3. Settings → Pages → Source: *Deploy from a branch*, Branch: `main`, Folder: `/ (root)` → Save.
4. 1–2 minute me: `https://<username>.github.io/suno/`

## 3) GitLab Pages
1. gitlab.com par naya public project banao.
2. Saari files upload karo (`.gitlab-ci.yml` bhi — isse build khud chalega).
3. CI/CD → Pipelines chalu hone do; Settings → Pages me link milega:
   `https://<username>.gitlab.io/<project>/`

## 4) Cloudflare Pages / Codeberg / Vercel
Wahi files upload — koi build command nahi, output folder root. Sab par chal jayega.

## 5) Mirror ko app se jodna (failover)
1. App → Settings → **Mirror links** me sabhi link ek-ek line me.
2. **Mirror check karo** → ✅ chalu, ❌ down.
3. Doctor → **Mirror switch** → jo pehla chalu mile, wahi khul jayega.
4. `portal.html` ke `MIRRORS` array me wahi links daal do — ek link dabne par portal dusra chala dega.
5. Ek mirror se dusre par notes/contacts le jaane ke liye: Settings → **Copy karo (export)** → naye mirror par **Paste karke import karo**.

Note: kam se kam ek link hamesha chalu rehna chahiye — agar sab down hain to koi bhi page khul hi nahi sakta. Isliye 3–4 alag platform par rakhein.

## Doctor (system khud ki jaanch karta hai)
Doctor tab har baar check karta hai: mic permission, voice engine, bolne wali awaaz, phone storage,
offline cache, internet, mirror links, error log. Jo theek ho sakta hai, **Auto-repair** theek kar deta hai
(cache saaf + service worker dobara + kharab settings hataana + reload). Error log phone me hi rehta hai.

## AI samajhne wala (optional)
Settings me apni Gemini/OpenAI key daal do — jo command samajh na aaye, wahi AI se samajh kar chala diya jayega.
Key sirf aapke phone me rehti hai, kahin nahi jati. Band rakhna hai to "Band" hi chhod do. Iske liye net chahiye.


## Advanced features (v4)

- **Do kaam ek saath**: "youtube kholo aur 5 minute ka timer lagao" — chaining `aur / and / then / phir` par.
- **Fuzzy samajh**: bolne me thoda bigde to bhi ("yootube", "instgram", "whatsap") sahi command chalti hai.
- **Devanagari bhi**: "यूट्यूब खोलो", "मौसम बताओ", "कॉल करो 98765…" chalte hain.
- **Phone se contact**: Settings → "Phone se contact chuno" → naam+number save → phir "call karo Ramesh".
- **Doosre systems se trigger**: app URL me `?cmd=` ya `?text=` daal kar koi bhi command chal sakti hai.
  Example: `.../suno/?cmd=call%20karo%209876543210` — Tasker/Shortcuts/MacroDroid se seedha call.
- **Home-screen shortcuts**: icon ko long-press karne par Call / Mausam / Notes / Time ke shortcut.
- **Share target**: kisi bhi app se text "Share → Suno" karo, wahi text command ban kar chal jayegi.
- **Doctor**: 8 checks + auto-repair + error log (phone me hi).

## Phone par install
Chrome me link kholo → mic **Allow** → 3-dot menu → **Add to Home screen**. Uske baad icon se full-screen khulega.

## Offline
- App shell offline khulta hai (service worker).
- Notes, timer, alarm, history, contacts, call dial, WhatsApp/SMS draft, maps — bina net.
- **Offline voice**: Settings me on karo. Naye Chrome (Android) me phone me hi sunta hai, net ki zaroorat nahi.
  Purane phone par ye support nahi — tab voice ke liye net chahiye. Weather/search ko net chahiye.

## Jo browser nahi kar sakta (Android ka rule)
- WiFi / Bluetooth / flashlight / volume on-off
- Bina tap kiye call lagana (dialer khulta hai, green button aap dabate ho)
- Dusre apps chalana
- Screen band hone ke baad background me mic sunna

Inke liye native Android app chahiye (foreground service + offline speech model).
