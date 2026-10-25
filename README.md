# World of Daxia v2

Game web (single-file HTML) yang dibungkus jadi aplikasi native Android memakai [Capacitor](https://capacitorjs.com) dan di-build otomatis lewat GitHub Actions.

## Struktur

```
www/index.html                  ← game (edit di sini)
assets/icon.png, splash.png     ← sumber ikon & splash screen
android-overrides/MainActivity  ← immersive fullscreen
capacitor.config.json
.github/workflows/build-android.yml
```

## Cara build

1. Push ke branch `main` → tab **Actions** → job **Build Android APK**.
2. Setelah selesai, unduh artifact **WorldOfDaxia-apk** (berisi `WorldOfDaxia-debug.apk`).
3. Di HP Android: izinkan "Install dari sumber tidak dikenal", lalu install APK.

Build manual: tab Actions → Build Android APK → **Run workflow**.

## Rilis otomatis

```bash
git tag v2.0.0 && git push origin v2.0.0
```
APK akan terlampir di halaman **Releases**.

## APK release bertanda tangan (opsional)

```bash
keytool -genkey -v -keystore release.jks -keyalg RSA -keysize 2048 -validity 10000 -alias daxia
base64 -w0 release.jks     # salin hasilnya
```
Tambahkan di Settings → Secrets and variables → Actions:
`KEYSTORE_BASE64`, `KEYSTORE_PASSWORD`, `KEY_ALIAS`, `KEY_PASSWORD`.
Simpan file `release.jks` dengan aman, jangan di-commit.

## Catatan

- Progress game memakai `localStorage` WebView, tersimpan selama app tidak di-uninstall / data tidak dihapus.
- Ganti `appId` di `capacitor.config.json` **dan** di `android-overrides/MainActivity.java` + path pada workflow bila ingin package name lain.
