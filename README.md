# STAFF OS AI

Offline-first işçi idarəetmə PWA: davamiyyət, 3 fasilə, müvəqqəti icazə, icazəli gəlməmə limiti, istirahət günləri, təqvim, hesabat, bildirişlər, offline AI köməkçi, backup və bulud sinxronizasiyası.

## Fayllar
- `index.html` — bütün proqram (interfeys, məntiq, IndexedDB)
- `manifest.json` — PWA quraşdırma məlumatı
- `sw.js` — offline keşləmə (service worker)
- `worker.js` — bulud sinxronizasiyası üçün Cloudflare Worker (GitHub-a yüklənmir)

## Quraşdırma (GitHub Pages)
1. GitHub-da repo yaradın, `index.html`, `manifest.json`, `sw.js` və `README.md` fayllarını yükləyin.
2. Repo → Settings → Pages → Branch: `main` → Save.
3. Ünvan: `https://<istifadəçi>.github.io/<repo>/`
4. Telefonda Chrome menyusundan "Add to Home screen" edin.

## Administrator hesabı
İlk açılışda ad və parol (min 6 simvol) yazılır, bu hesab baş administrator olur. Parol hash olunub cihazda saxlanılır, koda yazılmır. Parolsuz açılış yalnız həmin cihaz üçün Sistem → Giriş bölməsindən açılır.

## Offline rejim
Bütün məlumat cihazın IndexedDB bazasında saxlanılır. İnternet olmasa da proqram açılır və işləyir. Hər gün ilk açılışda avtomatik backup yaradılır (son 7 gün saxlanılır, Sistem bölməsində).

## Bulud sinxronizasiyası (Cloudflare)
1. Cloudflare → Workers & Pages → Create → Worker. Kodu `worker.js` ilə əvəz edib Deploy edin.
2. Storage & Databases → D1 → baza yaradın.
3. Worker → Settings → Bindings → D1 database, Variable name: `DB`.
4. Worker → Settings → Variables and Secrets → Secret `SYNC_TOKEN` (24+ simvol təsadüfi mətn).
5. Proqramda Sistem → Bulud sinxronizasiyası: worker ünvanı və açarı yazın.

Dəyişikliklər 4 saniyə sonra və internet bərpa olunanda avtomatik göndərilir. İki cihaz eyni qeydi dəyişsə, bu cihazın versiyası saxlanılır və audit tarixçəsinə "Sinxron konflikt" yazılır.

Məhdudiyyət: bütün cihazlar bir ortaq açarla qoşulur. Açarı bilən hər kəs bütün məlumatı oxuya və yaza bilər. Açarı yalnız etibarlı şəxslərə verin.

## Backup və bərpa
- Sistem → JSON ixrac: tam məlumat faylı (sinxron açarı daxil deyil).
- Sistem → JSON bərpa: fayl seçilir, təsdiqdən sonra məlumat əvəz olunur.
- Silinmiş qeydlər Sistem → Zibil qutusundan bərpa olunur.

## Vaxt
Bütün tarix və saatlar Asia/Baku ilə işləyir.
