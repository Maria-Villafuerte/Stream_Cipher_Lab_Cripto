# Stream Cipher - Laboratorio de Criptografía

## Descripción

Implementación de un cifrador de flujo (Stream Cipher) basado en XOR con un keystream pseudoaleatorio generado a partir de una semilla. El proyecto incluye funciones de cifrado/descifrado y un análisis de seguridad del esquema.

## Estructura del proyecto

- `cripto.ipynb` — Notebook principal con la implementación y pruebas unitarias
- `Parte_2.md` — Análisis de seguridad (variación de clave, reutilización de keystream, longitud, consideraciones prácticas)

## Uso

Abrir `cripto.ipynb` en Jupyter Notebook y ejecutar las celdas en orden.

```python
from cripto import encrypt, decrypt

mensaje = "Hola a todos, esta es una prueba"
clave = 15

cifrado = encrypt(mensaje, clave)
descifrado = decrypt(cifrado, clave)

print(descifrado)  # "Hola a todos, esta es una prueba"
```

## Funciones principales

| Función | Descripción |
|---|---|
| `generacion_de_keystream(seed, length)` | Genera un keystream pseudoaleatorio de la longitud indicada |
| `encrypt(plaintext, key)` | Cifra un mensaje aplicando XOR con el keystream |
| `decrypt(ciphertext, key)` | Descifra un mensaje aplicando XOR con el mismo keystream |

## Respuestas a las preguntas de análisis
### Variación de la Clave 
¿Qué sucede cuando cambia la clave utilizada para generar el keystream? Demuestre con un ejemplo concreto.
### Reutilización del Keystream (5 puntos)
- ¿Qué riesgos de seguridad existen si reutiliza el mismo keystream para cifrar dos mensajes diferentes? Implemente un ejemplo que demuestre esta vulnerabilidad.
- Sugerencia: Cifre dos mensajes con la misma clave y analice qué información puede extraer un atacante que intercepte ambos textos cifrados.
### Longitud del Keystream (5 puntos)
- ¿Cómo afecta la longitud del keystream a la seguridad del cifrado? Considere tanto keystreams más cortos como más largos que el mensaje.
### Consideraciones Prácticas (5 puntos)
- ¿Qué consideraciones debe tener al generar un keystream en un entorno de producción real? Mencione al menos 3 aspectos críticos.


