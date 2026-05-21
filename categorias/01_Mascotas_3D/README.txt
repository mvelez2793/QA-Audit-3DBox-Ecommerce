# 🐾 Auditoría de Calidad: Categoría Mascotas 3D

## 📌 Alcance del Módulo
Este módulo comprende el flujo de personalización y compra de figuras 3D para mascotas. Es una sección crítica debido a la alta interacción del usuario con campos de entrada (inputs) y selectores dinámicos.

<<<<<<< HEAD
#### 🗺️ Arquitectura de Pruebas (Model-Based Testing)
Para este módulo, se diseñó un mapa conceptual del flujo transaccional de WooCommerce. Este modelo permite aislar los frentes de ataque y segmentar las categorías de prueba de forma atómica en la categoria Mascota 3D

🔹 **[Ver Diagrama de Flujo de la Arquitectura de Pruebas (Draw.io)](https://github.com/mvelez2793/QA-Audit-3DBox-Ecommerce/blob/main/categorias/01_Mascotas_3D/docs/Diagrama%203dbox_Ec%20WooComerce.drawio.png)**

> *Nota de Auditoría: El modelado previo al testing manual/automatizado permitió identificar los componentes críticos expuestos a inyecciones de payloads (BUG_01) antes de la ejecución de casos.*


=======
## 🗺️ Mapa de Flujo de Pruebas (Diagrama de Procesos)
Se diseñó un mapa conceptual del flujo transaccional de WooCommerce para aislar los frentes de ataque y segmentar las categorías de prueba de forma atómica en la categoria Mascota 3D
> ![Diagrama de Arquitectura de Pruebas - MASCOTA 3D] https://github.com/mvelez2793/QA-Audit-3DBox-Ecommerce/blob/main/categorias/01_Mascotas_3D/docs/Diagrama%203dbox_Ec%20WooComerce.drawio.png
>>>>>>> 8d41590b07b2c7ca8258b37c822d8c25ac4596b6

### 🔍 Puntos Críticos Identificados (Hotspots):
1. **Input "Identifica tu mascota" "Detalle Adicional":** Riesgo de inyección de payloads y falta de sanitización.
2. **Selector de Base:** Validación de lógica condicional.
3. **Carga de Archivos (Fotos):** Validación de tipos de archivo y límites de tamaño.

## 🧪 Estrategia de Prueba (Atomic Strategy)
Siguiendo el enfoque de **Model-Based Testing**, se han derivado los siguientes tipos de pruebas:

| Tipo de Prueba | Técnica Aplicada | Objetivo |
| :--- | :--- | :--- |
| **Funcional** | Happy Path | Validar compra exitosa con datos estándar. |
| **Seguridad** | Payload Injection | Evaluar la resiliencia del backend ante datos masivos (Vulnerabilidad detectada BUG-01). |
| **Límites (BVA)** | Boundary Value Analysis | Probar los límites de caracteres en campos de texto "Indetifica a tu Mascota" (Min: 1 / Max: 50) ¨Detalle Adicional"(Min: 1 / Max: 500). |

Tras identificar que la Vulnerabilidad de BUG_01 es de naturaleza sist'ematica (capa de persistencia de backend), se determino suspender la ejecuci'on redundante en las 5 categorias restantes para optimizar
el esfuerzo de QA. La suite de pruebaa e las dem'as categorias se limitará a un **Smoke Testing de Validación** una vez que el equipo de desarrollo implmente la sanitizacion global en el servidor.


## 📁 Estructura de Evidencias

El informe detallado y las evidencias de ejecución del caso de prueba se encuentran documentados en el siguiente enlace al issue de GitHub

https://github.com/mvelez2793/QA-Audit-3DBox-Ecommerce/issues/3