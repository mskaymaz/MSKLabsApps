# MSKLabsApps — Dağıtım & Release Kuralları (`AGENTS.md`)

> **SSOT Referansları:** `D:\Code\istisare\istisareler\015-merkezi-release-tag-ve-surum-yayin-protokolu.md` (`IST-015`) ve `016-melez-hizli-dagitim-r2-ve-worker-cache-mimarisi.md` (`IST-016`).

## 1. Zorunlu Release, Tag ve Dosya Adlandırma Kuralları (`IST-015`)
- **Genel Tag Yasağı:** Bu repoda asla `v1.0.0` gibi genel tag açılmaz; her tag `<app-slug>-vX.Y.Z` (küçük harf kebab-case, ör. `rekatsay-v1.3.1`, `haydi-namaza-v1.0.5`) formatında olmalıdır.
- **Genel / Debug Dosya Adı Yasağı:** `app-release.apk`, `app-debug.apk` veya `app.exe` gibi genel/debug isimlerle **asla** release yüklenmez. Her yüklenen ikili dosya **`<UygulamaAdı>-vX.Y.Z.<uzantı>`** (ör. `RekatSay-v1.3.1.apk`) biçiminde adlandırılmalıdır.
- **Hedef Ayrımı:** Bu repo yalnızca **son kullanıcıya açık (Public)** uygulamalar içindir; bireysel/iç araçlar (`PushPull`, `AGToken` vb.) kendi repolarının Releases sekmesinde tutulur.

## 2. Melez Hızlı Dağıtım & Katalog Senkronizasyon Sırası (`IST-016`)
1. Derlenen standart isimli ikili dosya (`<UygulamaAdı>-vX.Y.Z.<ext>`) **GitHub `MSKLabsApps` Releases** sekmesine (`<app-slug>-vX.Y.Z` tag'iyle) arşivlenir.
2. En güncel **`r2_keep_versions`** (varsayılan `2`) sürüm **Cloudflare R2 (`msklabs-releases` / `releases.msklabs.org`)** üzerine yüklenir; limiti aşan eski sürümler R2'dan silinir ancak GitHub Releases'ta kalır.
3. `app_catalog.json`, `update_manifest.json` ve `manifests/<app>.json` içindeki indirme URL'leri **`https://msklabsdesk-backend.msklabs-org.workers.dev/dl/<app-slug>/<version>`** rotasına işaret edecek şekilde güncellenir.
