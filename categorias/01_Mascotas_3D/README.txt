# 🐾 Auditoría de Calidad: Categoría Mascotas 3D

## 📌 Alcance del Módulo
Este módulo comprende el flujo de personalización y compra de figuras 3D para mascotas. Es una sección crítica debido a la alta interacción del usuario con campos de entrada (inputs) y selectores dinámicos.

## 🗺️ Mapa de Flujo de Pruebas (Diagrama de Procesos)
Se diseñó un mapa conceptual del flujo transaccional de WooCommerce para aislar los frentes de ataque y segmentar las categorías de prueba de forma atómica en la categoria Mascota 3D
> ![Diagrama de Arquitectura de Pruebas - MASCOTA 3D] https://github.com/mvelez2793/QA-Audit-3DBox-Ecommerce/blob/main/categorias/01_Mascotas_3D/docs/Diagrama%203dbox_Ec%20WooComerce.drawio.png

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

## 📁 Estructura de Evidencias
