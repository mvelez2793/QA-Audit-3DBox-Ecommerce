# 🧪 Ejecución de Pruebas Funcionales - Mascotas 3D


## 📊 Matriz de Cobertura y Trazabilidad de Endpoints
Esta suite valida la lógica de negocio del formulario de personalización a nivel de protocolo de red (API).

| ID Caso | Componente Evaluado | Entrada / Payload | Resultado Esperado (API) | Estado | Vínculo de Evidencia / Defecto |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **CASO-09** | Input Nombre Mascota | Alfanumérico estándar | `200 OK` | 🟢 PASSED | N/A (Comportamiento Correcto) |
| **CASO-10** | Límite de Caracteres | > 50 caracteres | `400 Bad Request` | 🔴 FAILED | **[Ver Issue #2 en GitHub (Fallo Sistémico)](https://github.com/mvelez2793/QA-Audit-3DBox-Ecommerce/issues/3)** |

> ⚠️ *Nota de Mitigación:* Debido al hallazgo del defecto de seguridad sistémico BUG-02 (Mass Input Injection), las pruebas funcionales de límites de caracteres en las categorías 02 a 06 quedan congeladas hasta el despliegue del parche centralizado en el Backend.