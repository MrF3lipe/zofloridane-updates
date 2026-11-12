# zofloridane-updates

Repositorio público de actualizaciones de la app Zofloridane. La app consulta el `version.json` de `main` y se actualiza sola (parche bsdiff o APK completo).

Repositorio: `MrF3lipe/zofloridane-updates`. El código de la app está en `MrF3lipe/zofloridane_app`. El plugin de la tienda, en `MrF3lipe/zfl-admin`. La tienda es [zofloridane.com](https://zofloridane.com): la gente que vive fuera le compra a la familia en Cuba.

## Estructura

| Ruta | Qué es |
|---|---|
| `version.json` | Manifiesto que lee la app (`format: 1`, variante `universal`) |
| Releases de GitHub | APK (`universal-<code>.apk`) y parches (`universal-<from>-<code>.bsdiff`) |
| `README.md` | Nota corta de uso |

No hay código de la app ni del plugin aquí. El script que arma el manifiesto y los parches es `tools/make_update.py` en `zofloridane_app`.

## Versión actual

`version.json` en `main` apunta a **3.0.9.3**, versionCode **80** (en el pubspec de la app: `3.0.9+80`; el versionName real es 3.0.9.3). Hay parches desde los versionCode 76, 78 y 79.

## Cómo publicar

1. Compila el APK de release en la box, desde `zofloridane_app` (con la clave de release).
2. Genera los parches con `tools/make_update.py` de ese repo.
3. Crea el release Latest con tag `v<versión>-<code>` y sube APK + parches.
4. Actualiza `version.json` en `main` (url, sha256, size, `fromVersionCode` / `fromSha256` de cada parche).
5. Copia el APK a `https://zofloridane.com/app/descargar/` (nombre tipo `zofloridane-v3.0.9.3.apk`).
6. Comprueba sha256, el manifiesto y la descarga.

## Variables de entorno

Este repo no usa variables de entorno propias. Las de firma y Firebase viven en `zofloridane_app` y en los secretos de ese repositorio (`ZFL_KEYSTORE_B64`, `ZFL_KEYSTORE_PASSWORD`, `ZFL_KEY_PASSWORD`, `ZFL_KEY_ALIAS`, `ZFL_GOOGLE_SERVICES_B64`, `ZFL_KEY_PROPERTIES`). No pongas sus valores aquí ni en el chat.

## Integraciones

- La app (`com.zofloridane.zofloridane`) descarga este `version.json` y los assets del release.
- La página `/app/descargar/` de la tienda (plugin zfl-admin) ofrece el mismo APK.
- El endpoint socio/nómina de CG (`GET /wp-json/zfl/v1/socio/nomina`, cabecera `X-ZFL-Socio-Key`) no forma parte de este repo.

## Reglas de negocio (contexto; no se implementan aquí)

- Ganancia de la tienda en USD, 100 % dueños: Michel 90 / Felipe 10.
- Empleados: 10 CUP por USD vendido, Yasniely 60 / Yani 20 / almacenero 20.
- Propinas: 50/50 dueños y empleados, y luego 90/10 y 60/20/20 dentro de cada grupo.
- Cuentas `vladimir`, `Luis Felipe` y `admin` = Felipe.
- Familias por peso: sin marca y por peso → familia (cada peso es una opción); con marca o paquete de unidades iguales → suelto; con hueso ≠ deshuesado; fresco ≠ ahumado; congelado = fresco; jamón de pierna entero en familia; viandas sueltas.
