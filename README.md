# Carsai LMS — App Releases 🚀

**Hub público de distribuição das apps da plataforma [Carsai LMS](https://carsailms.vercel.app).**
**Public distribution hub for the Carsai LMS platform apps.**

> PT: Os binários oficiais (Android / Windows / Linux) vivem nas **Releases** deste
> repositório, cada uma com o **CHANGELOG da própria versão** no corpo — qualquer
> pessoa pode baixar aqui no GitHub ou pela página oficial
> [carsailms.vercel.app/download-app](https://carsailms.vercel.app/download-app).
>
> EN: Official binaries (Android / Windows / Linux) live in this repository's
> **Releases**, each with the **per-version CHANGELOG** in its body — anyone can
> download here on GitHub or from the official download page.

## Downloads / Releases

| Canal | Ficheiro | Origem |
|---|---|---|
| Android (estável) | `CarsaiLMS-vX.Y.Z-release.apk` | release assinada |
| Android (beta) | `CarsaiLMS-vX.Y.Z-beta.apk` | build mais recente |
| Windows (instalador) | `CarsaiLMS-Setup-vX.Y.Z.exe` | Electron NSIS |
| Windows (portátil) | `CarsaiLMS-Portable-vX.Y.Z.exe` | Electron portable |
| Linux (AppImage) | `CarsaiLMS-X.Y.Z-x86_64.AppImage` | Electron AppImage |
| Linux (.deb) | `CarsaiLMS-X.Y.Z-amd64.deb` | Electron deb |

A página da plataforma verifica automaticamente actualizações a cada 30 minutos
e baixa dentro da própria app (`/api/app-version` → `/api/app-download`).

## Como é que os builds chegam aqui / How builds land here

O workflow **`release-hub`** corre **neste repositório público** (minutos ilimitados
no plano free — o repo privado está sujeito à quota mensal):

1. **Gatilho**: a cada 2 h (schedule) ou manualmente (workflow_dispatch, input
   `force` para reconstruir).
2. **Fonte**: faz checkout do código-fonte em [`carsaimz/carsailms`](https://github.com/carsaimz/carsailms)
   (privado) com o segredo `APP_GH_TOKEN`.
3. **Constrói**: Android (Capacitor/Gradle), Windows (Electron NSIS+Portable) e
   Linux (Electron AppImage+deb).
4. **Publica**: release `vX.Y.Z` com os 6 ficheiros + a secção do `CHANGELOG.md`
   dessa versão no corpo; depois registra as metas na plataforma
   (`/api/app-release-upload`) para a página de download e o verificador de
   actualizações.

## Segredos / Secrets

| Segredo | Obrigatório | Efeito |
|---|---|---|
| `APP_GH_TOKEN` | ✅ | PAT com leitura do repo privado + escrita das metas |
| `ANDROID_KEYSTORE` + `ANDROID_KEYSTORE_PASSWORD` (+`ALIAS`) | — | APK **release assinado**; sem eles só o beta (ex-debug) é publicado |
| `GOOGLE_SERVICES_JSON` | — | FCM nativo (push); sem ele o push segue pelo canal web |

> Nota: o GitHub nunca expõe o valor de segredos existentes — para o APK release
> assinado, o dono cola os mesmos valores do repo privado aqui (UI → Settings →
> Secrets and variables → Actions).

## Histórico / History

O conteúdo antigo deste repositório (protótipo nativo Android v1.1.1) foi
preservado na branch [`legacy/v1.1.1`](https://github.com/carsaimz/carsailms-app/tree/legacy/v1.1.1)
e as releases de debug antigas foram removidas.

---

© [Carsai Mozambique](https://carsailms.vercel.app) — Aprende hoje, lidera amanhã.
