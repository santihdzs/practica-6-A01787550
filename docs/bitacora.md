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
