# Veryfia Standard v1.0 – Especificación técnica

**Veryfia** es un estándar abierto para la certificación y verificación de archivos digitales, especialmente aquellos generados por Inteligencia Artificial.  
Su objetivo es proporcionar una forma **neutral, transparente e inmutable** de probar la existencia y origen de un archivo en un momento concreto.

---

## 1. Principios del estándar
- **Neutralidad**: cualquier IA, servicio o persona puede generar un manifiesto Veryfia.  
- **Simplicidad**: formato JSON legible, fácil de integrar.  
- **Inmutabilidad**: uso de blockchain para anclaje de pruebas.  
- **Interoperabilidad**: puede convivir con otros estándares como C2PA.  

---

## 2. Estructura general del manifiesto

El manifiesto es un objeto JSON con los siguientes bloques:

```json
{
  "version": "1.0",
  "file": { ... },
  "generator": { ... },
  "issuer": { ... },
  "anchor": { ... },
  "verification": { ... }
}

3. Definición de campos
3.1. version (obligatorio)

Tipo: string

Ejemplo: "1.0"

Descripción: versión del estándar Veryfia usada para generar el manifiesto.

3.2. file (obligatorio)

Campos:

hash: string (SHA-256 en hex) → huella única del archivo.

type: string (MIME type, ej. image/png, application/pdf).

size_bytes: integer → tamaño en bytes.

Ejemplo:

"file": {
  "hash": "2bf1c7a4e1a3...e9fb",
  "type": "image/png",
  "size_bytes": 3214421
}

3.3. generator (opcional pero recomendado)

Campos:

source: "AI_GENERATED" | "HUMAN_CREATED" | "MIXED".

name: string → nombre de la IA o proceso generador.

version: string → versión del modelo/software.

prompt: string (opcional) → prompt o parámetros usados.

Ejemplo:

"generator": {
  "source": "AI_GENERATED",
  "name": "Stable Diffusion XL",
  "version": "2.1",
  "prompt": "cover photo, lifestyle, beach, morning light"
}

3.4. issuer (opcional)

Campos:

organization: string → entidad emisora del registro.

api_key_id: string (opcional) → identificador de la clave usada en la API.

Ejemplo:

"issuer": {
  "organization": "FotoIA S.L.",
  "api_key_id": "vf_org_01JD2S..."
}

3.5. anchor (obligatorio)

Campos:

chain: string → blockchain usada (Polygon, Ethereum, Arbitrum, etc.).

tx_hash: string → hash de la transacción en la blockchain.

merkle_root: string → raíz del batch en el que se incluyó el archivo.

anchored_at: string (ISO 8601 UTC) → fecha y hora de anclaje.

Ejemplo:

"anchor": {
  "chain": "Polygon",
  "tx_hash": "0x9a3b...42dd",
  "merkle_root": "a4c9...7e12",
  "anchored_at": "2025-10-02T09:32:58Z"
}

3.6. verification (opcional)

Campos:

url: string → endpoint público de verificación.

Ejemplo:

"verification": {
  "url": "https://verify.veryfia.com/v/vf_asset_01JD2STXQ8M5G9H8"
}

4. Reglas mínimas

El file.hash debe calcularse con SHA-256.

Todos los timestamps deben expresarse en UTC ISO 8601.

El manifiesto debe anclarse en blockchain a través de un Merkle root para permitir escalabilidad.

El estándar es agnóstico de blockchain, pero Polygon se recomienda por costes y velocidad.

5. Extensiones futuras

signatures: soporte para firmas digitales de organizaciones.

geo: datos de localización (si procede).

c2pa_ref: hash del manifiesto C2PA para interoperabilidad.

6. Licencia

El estándar Veryfia se publica bajo licencia MIT, abierto para uso y adopción libre.
