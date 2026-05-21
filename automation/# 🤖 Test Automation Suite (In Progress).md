# 🤖 Test Automation Suite (In Progress)

## 📌 Objetivo
Este directorio contendrá los scripts de automatización para pruebas de regresión y flujos críticos (E2E) utilizando **Selenium con Java/TestNG** (o el stack que elijas).

## 🛠️ Suite Automática de Humo (Smoke Test Plan)
Para evitar la verificación manual redundante en las 6 categorías del Ecommerce, se diseñará un script automatizado paramétrico.

### 📋 Flujo del Script:
1. Iterar a través del array de endpoints de las categorías.
2. Inyectar un payload masivo de 10k caracteres simulando el bypass del frontend (Mass Input Injection).
3. Realizar la aserción sobre el código de estado HTTP esperado (`Expected: 400 Bad Request`).
4. Generar un reporte automatizado de cumplimiento de parches de seguridad.

## 🚀 Próximos Pasos:
- [ ] Configuración del Framework Base (Page Object Model).
- [ ] Automatización del flujo de "Personalización de Mascota".
- [ ] Reportería dinámica con Allure Reports.

> **Nota:** Actualmente en fase de diseño de casos de prueba para automatización.