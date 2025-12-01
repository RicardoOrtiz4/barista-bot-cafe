# Reporte de CD Firebase App Distribution

Este pipeline automatiza la entrega de Android (AAB release) a Firebase App Distribution.

## Workflow principal
- Archivo: `.github/workflows/cd-firebase.yml`.
- Disparadores: `push` a `main` y `workflow_dispatch`.
- Pasos clave: Flutter stable, Java 17, decodificar keystore (`ANDROID_KEYSTORE_BASE64`), crear `android/key.properties` (passwords y alias), instalar Ruby/fastlane, exportar `FIREBASE_SERVICE_ACCOUNT_JSON` a `GOOGLE_APPLICATION_CREDENTIALS`, ejecutar `bundle exec fastlane beta`.

## Fastlane
- Archivo: `fastlane/Fastfile`.
- Lane `beta`: `flutter build appbundle --release` y `firebase_app_distribution` con `build/app/outputs/bundle/release/app-release.aab`.
- Secrets requeridos: `FIREBASE_APP_ID_ANDROID`, `FIREBASE_SERVICE_ACCOUNT_JSON`, `ANDROID_KEYSTORE_BASE64`, `ANDROID_KEYSTORE_PASSWORD`, `ANDROID_KEY_PASSWORD`, `ANDROID_KEY_ALIAS`.

## Evidencias pendientes de adjuntar
- Capturas de una corrida exitosa del workflow CD (jobs y logs de build + distribucion).
- Captura de Firebase App Distribution mostrando el build publicado.
- Enlaces/artefactos generados (AAB release) y notas de release usadas.
