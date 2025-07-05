# Netlify Manuel Yükleme Rehberi

## Doğru Dosya Yükleme Adımları

### 1. Build İşlemi
Önce projeyi build edin:
```bash
npm run build
```

### 2. Yüklenecek Klasör
Build işleminden sonra **`dist/public`** klasörünün içindeki dosyaları yükleyin.

**ÖNEMLİ:** Tüm projeyi değil, sadece `dist/public` klasörünün **içindeki** dosyaları yükleyin.

### 3. Netlify'de Yükleme
1. Netlify Dashboard'a gidin
2. "Add new site" > "Deploy manually" seçin
3. **`dist/public`** klasörünü sürükleyip bırakın (klasörün kendisini değil, içindeki dosyaları)

### 4. Dosya Yapısı Kontrolü
Yükleme sonrası Netlify'de şu dosyalar görünmeli:
```
/
├── index.html          ← Ana sayfa
├── _redirects          ← SPA routing için
├── assets/
│   ├── index-xxx.js    ← JavaScript bundle
│   └── index-xxx.css   ← CSS bundle
└── vite.svg           ← Favicon
```

### 5. Site Ayarları
Netlify'de site ayarlarından:
- **Publish directory**: `/` (root)
- **Build command**: Boş bırakın (manuel yükleme için)

### 6. Sorun Giderme
Eğer hala 404 alıyorsanız:
1. Netlify site overview'da "Functions" sekmesini kontrol edin
2. "Deploys" sekmesinde build log'larını inceleyin
3. Site settings > Build & deploy > Post processing'de "Pretty URLs" kapalı olsun

## Alternatif: Git ile Otomatik Deploy
Manuel yükleme yerine Git repository bağlayabilirsiniz:
1. Projeyi GitHub'a push edin
2. Netlify'de "Import from Git" seçin
3. Build settings:
   - **Build command**: `npm run build`
   - **Publish directory**: `dist/public`