# Bitácora — Práctica 6 "Avisos"

Alumno: A01787550

## Ejercicio 0 · ¿Qué se guarda, y dónde?

| # | Dato | ¿Se guarda? | ¿Con qué protección? |
|---|------|-------------|----------------------|
| 1 | La contraseña | No, nunca | Ninguna: se manda una vez y se olvida. Guardarla convierte cualquier fuga en fuga de la cuenta completa. |
| 2 | El token de acceso | Sí | Cifrado con una llave del Android Keystore. Sin él habría que refrescar en cada arranque. |
| 3 | El token de refresco | Sí | Cifrado con una llave del Android Keystore. Es el más valioso: dura 7 días. |
| 4 | `usuario` y `rol` | Sí | En claro. No son secretos: el rol lo decide el servidor leyendo el token, no el archivo. Solo sirven para pintar la pantalla. |
| 5 | El código de profesor | No, nunca | Ninguna: se usó una vez al registrarse y ya cumplió. |
| 6 | La fecha `exp` | Sí | En claro. No protege nada; solo le dice a la app cuándo va a fallar la siguiente petición. |

## Ejercicio B3 · ¿Por dónde se sale un token?

Cuatro lugares, fuera del archivo de DataStore:

1. **El Logcat.** `HttpLoggingInterceptor` en `HEADERS` o `BODY` imprime `Authorization: Bearer …`. → Lo evita `redactHeader("Authorization")`, y nunca dejar `BODY` en release.
2. **Los reportes de error** (Crashlytics y parecidos), que adjuntan el log o la petición que falló. → Mismo arreglo, y revisar qué se manda.
3. **Las capturas de pantalla y el selector de apps**, si el token se pinta en pantalla. → No pintarlo, y `FLAG_SECURE` en pantallas sensibles.
4. **La URL**: `GET /avisos?token=…` queda en logs de servidores, proxies e historiales. → Los tokens van en el encabezado, nunca en la URL.

(Un quinto: el portapapeles, si hubiera un botón de "copiar". No lo hay.)

Ninguno se arregla cifrando el archivo: el cifrado protege el archivo, estos se evitan no dejando salir el dato.
