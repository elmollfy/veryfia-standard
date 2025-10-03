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
