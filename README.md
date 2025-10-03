# veryfia-standard
Estándar abierto de Veryfia para certificación y verificación de archivos generados por IA.
# Veryfia Standard v1.0

**Veryfia** es un **estándar abierto** para verificar archivos generados por Inteligencia Artificial u otros procesos digitales.  
Su objetivo es proporcionar una forma **neutral, transparente e inmutable** de certificar que un archivo existió en un momento concreto, sin depender de una sola empresa o formato propietario.

---

## 🔹 ¿Por qué Veryfia?
- Los metadatos tradicionales (como **C2PA**) pueden ser eliminados o modificados al editar un archivo.  
- Veryfia se basa en **blockchain** para anclar la prueba de existencia de un archivo de forma inmutable.  
- Cualquier IA, aplicación o servicio puede generar un **Veryfia Manifest** y publicarlo.

---

## 🔹 Cómo funciona
1. Se genera un **hash SHA-256** del archivo.  
2. Se crea un **Veryfia Manifest (JSON)** con metadatos básicos y la información de anclaje.  
3. El manifiesto se **ancla en blockchain** (ej. Polygon) mediante un sistema de batches y Merkle roots.  
4. Cualquiera puede verificar un archivo comparando su hash con el manifiesto anclado.  

---

## 🔹 Ejemplo de manifiesto (v1.0)

```json
{
  "version": "1.0",
  "file": {
    "hash": "2bf1c7a4e1a3...e9fb",
    "type": "image/png",
    "size_bytes": 3214421
  },
  "generator": {
    "source": "AI_GENERATED",
    "name": "Stable Diffusion XL",
    "version": "2.1",
    "prompt": "cover photo, lifestyle, beach, morning light"
  },
  "issuer": {
    "organization": "FotoIA S.L.",
    "api_key_id": "vf_org_01JD2S..."
  },
  "anchor": {
    "chain": "Polygon",
    "tx_hash": "0x9a3b...42dd",
    "merkle_root": "a4c9...7e12",
    "anchored_at": "2025-10-02T09:32:58Z"
  },
  "verification": {
    "url": "https://verify.veryfia.com/v/vf_asset_01JD2STXQ8M5G9H8"
  }
}
