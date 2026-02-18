# Ejercicio Stream Cipher

### Parte 2: Análisis de Seguridad

### 2.1 Variación de la Clave

Cambiar la clave genera un keystream completamente diferente, produciendo un texto cifrado distinto e incompatible. Con clave `15`:

```
Cifrado: [34, 106, 126, 49, ...]
```

Con clave `99`:
```
Cifrado: [201, 45, 88, 12, ...]  # valores totalmente distintos
```

Si se intenta descifrar con la clave incorrecta, el resultado es basura ilegible, ya que el keystream no coincide.

---

### 2.2 Reutilización del Keystream

Si dos mensajes `M1` y `M2` se cifran con la misma clave (mismo keystream `K`):

```
C1 = M1 XOR K
C2 = M2 XOR K
```

Un atacante puede calcular `C1 XOR C2 = M1 XOR M2`, eliminando completamente el keystream. Con técnicas de análisis de frecuencia o conociendo parte de un mensaje, puede recuperar el otro. Esta vulnerabilidad ("two-time pad") compromete ambos mensajes sin necesidad de conocer la clave. **Nunca se debe reutilizar el mismo keystream.**

---

### 2.3 Longitud del Keystream

- **Keystream más corto que el mensaje:** los bytes finales quedan sin cifrar o el cifrado falla, dejando información expuesta directamente.
- **Keystream igual al mensaje:** funcionamiento correcto y eficiente.
- **Keystream más largo que el mensaje:** no representa riesgo en sí mismo, pero los bytes sobrantes son desperdicio. El riesgo surge si esos bytes sobrantes se reutilizan para cifrar otro mensaje (reutilización de keystream).

La longitud mínima segura es exactamente la longitud del mensaje, sin reusar ningún segmento.

---

### 2.4 Consideraciones Prácticas

1. **Usar un CSPRNG (generador criptográficamente seguro):** `random.Random` de Python NO es apto para producción. Se debe usar `secrets` o `os.urandom()`, ya que un PRNG predecible permite a un atacante reconstruir el keystream.

2. **Nunca reutilizar clave + nonce:** cada mensaje debe cifrarse con una clave o nonce único. En ciphers modernos como ChaCha20 o AES-CTR, se combina clave + nonce para garantizar keystreams distintos por mensaje.

3. **Integridad del mensaje (autenticación):** el cifrado por sí solo no protege contra modificaciones. Se debe añadir un código de autenticación (MAC/HMAC) para detectar alteraciones, usando esquemas como AES-GCM o ChaCha20-Poly1305.