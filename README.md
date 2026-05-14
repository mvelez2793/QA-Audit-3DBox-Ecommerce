# 🛡️ Security & Quality Audit: 3DBox E-commerce Platform
*(Auditoría de Seguridad y Calidad: Plataforma E-commerce 3DBox)*

## 📋 Executive Summary / Resumen Ejecutivo
**EN:** Technical audit for the digital transition of **3DBox**, a 3D printing leader with 9 years of experience. This process ensures a secure, resilient, and high-quality launch.

**ES:** Auditoría técnica para la transición digital de **3DBox**, empresa líder en impresión 3D con 9 años de experiencia. Este proceso garantiza un lanzamiento seguro, resiliente y de alta calidad.

---

## 🚀 Critical Findings & Mitigations / Hallazgos Críticos y Mitigaciones

### 1. Financial Data Integrity (DOM Manipulation)
*Integridad de Datos Financieros (Manipulación del DOM)*

* **Risk / Riesgo:** Potential price fraud by altering client-side HTML values. *(Fraude potencial alterando valores HTML en el cliente).*
* **Test / Prueba:** Modified cart prices from $51.50 to $1.50 via DevTools. *(Modificación de precios de $51.50 a $1.50 mediante DevTools).*
* **Result / Resultado:** **✅ PASSED.** The system implements robust **Server-Side re-calculation**, ignoring client-side values at checkout. *(El sistema implementa un recálculo robusto en el servidor, ignorando valores del lado del cliente).*

### 2. File Upload Security (Bypass Attempt)
*Seguridad en Carga de Archivos (Intento de Bypass)*

* **Risk / Riesgo:** Malware injection through the 3D model upload form. *(Inyección de malware a través del formulario de modelos 3D).*
* **Test / Prueba:** Extension masking (renaming `.txt` to `.jpg`) and MIME-Type spoofing. *(Enmascaramiento de extensión y suplantación de MIME-Type).*
* **Result / Resultado:** **⚠️ PARTIAL.** UI blocks invalid files, but deep server-side sanitization is being audited to prevent DoS (Denial of Service). *(La interfaz bloquea archivos inválidos, pero se audita la sanitización profunda en el servidor para prevenir ataques DoS).*

---

## 🛠️ Tech Stack & Methodology / Stack Tecnológico y Metodología

* **Platform:** WordPress + WooCommerce.
* **Testing Tools:** Chrome DevTools, Postman (API Testing), JMeter (Performance), Gherkin.
* **Frameworks:** OWASP Top 10 (Security Focus).
* **Methodology:** Risk-Based Testing (RBT) & BDD (Behavior Driven Development).

---

## 📁 Detailed Reports / Reportes Detallados
**EN:** You can track the full lifecycle of discovered bugs and test cases in the [Issues](https://github.com/mvelez2793/QA-Audit-3DBox-Ecommerce/issues) section.

**ES:** Puedes seguir el ciclo de vida completo de los errores encontrados y casos de prueba en la sección de [Issues](https://github.com/mvelez2793/QA-Audit-3DBox-Ecommerce/issues).
