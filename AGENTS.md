# Cómo trabajar en zofloridane-updates

Habla con Felipe en español, de tú, corto y directo. Lo que diga Jefe cuenta como palabra de Felipe, también para publicar un APK. No le pidas a Felipe un sí extra por el chat si Jefe ya lo dio.

## Producción

- Nada a producción (un release Latest o un cambio de `version.json`) sin el sí de Felipe (o de Jefe).
- `main` es producción: la app lee el `version.json` de esta rama.
- El APK se compila en la box, en el repo `zofloridane_app`. Aquí solo se publica.
- Cada arreglo de la app sale como release **Latest** normal (tag `v<versión>-<code>`, por ejemplo `v3.0.9.3-80`). No publiques APKs de prueba ni prereleases de entrega.
- El mismo APK se sirve en `https://zofloridane.com/app/descargar/`. `/descargar/` sin `/app/` da 404.
- No copies archivos al escritorio de Hestia. El plugin se despliega desde Hestia, no desde esta box.

## Qué no tocar

- Nada de secretos en el código ni en el chat.
- No toques pedidos, precios ni cuentas de WordPress si no te lo piden.
- No muestres en público la dirección del almacén.
- No inventes datos (ni un sha256, ni un tamaño, ni una URL).
- Solo herramientas gratis.

## Cómo verificar

- El sha256 y el tamaño de cada APK y de cada parche coinciden con `version.json`.
- `app` es `com.zofloridane.zofloridane` y la `version` / `versionCode` coinciden con la build (el versionName visible es 3.0.9.3 cuando pubspec dice 3.0.9+80).
- Tras publicar, `/app/descargar/` sirve el mismo APK y la app puede leer este `version.json`.
