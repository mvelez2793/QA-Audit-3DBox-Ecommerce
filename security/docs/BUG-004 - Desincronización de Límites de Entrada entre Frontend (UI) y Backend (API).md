# 🛑 Reporte de Defecto: BUG-004
## Desincronización de Límites de Entrada entre Frontend (UI) y Backend (API)

### 📊 **Clasificación del Defecto**

* **Severidad:**  Alta (Bloqueo de funcion principal de negocio: Añadir al carrito)
* **Prioridad:**  Alta (Afecta la experiencia del usuario y detiene el flujo de negocio)
* **Componente:** Formulario de Personalización - Categoria Mascota 3D (Sistémico).
* **Estado del Backend:** ´HTTP 400 Bad Request´ (Excepción Controlada mediante plantilla)

---
### 🔍 **Descripción del Problema**
El backend implemento un mecanismo perimetral para mitigar la falla de inyección masiva en todos los campos de texto de los formularios de la pagina.
Sin embargo, la restricción de longitud máxima de caracteres **No fue replicada en la capa de presentación (Frontend)**

Al no existir el atributo de restricción de caracteres de acuerdo a las reglas de negocio en la interfaz de usuario, el sistema permite al cliente escribir y enviar cadenas 
de texto superiores a las establecidas en los requsitos. Al procesar el payload, el backend aborta la transacción, devolviendo Status Code ´400 Bad Request´, en el POST, con un documento
HTML estructura de error. 

Provocando que la interfaz visual ** se congele (UI Freezing)** y el producto nunca se agregue al carrito de compras, para continuar con el flujo de negocio. 

---
### 🧪 **Pasos para Reproducir (Steps to Reproduce)**
* 1.- Navegar al formulario de Personalización de cualquier categoria. 
* 2.- Completar los pasos iniciales obligatorias del flujo visual. 
* 3.- El campo de entrada de texto "Identifica tu mascota" por ejemplo ingresar el limite superior de valores permitidos 
(Ej:¨Identifica a tu mascota¨ 50 caracteres alfánumeriocos) y (Ej:¨Detalle¨ 300 caracteres alfánumeriocos)
* 4.- Abrir las herramientas de desarrollador (F12) en la pestaña Network (Red)
* 5.- Agregar al carrito de compras
---
### **Resultado Esperado**.
El producto es agregado al carrito de compras, enviando la información por medio de backend y obteniendo un Sattus Code de 200OK. 
---
### **Resultado Obtenido**.
La interfaz de usuario se congela sin mostrar alertas de error nativas, y la petición hacia el servidor, se registra en color rojo con un código de estado 400 Bad Request.

---
### ** Solución Propuesta**
* **Fronted (Restricciones y UX):** Aprovechar las propiedades nativas de WooCommerce (Inyectando atributos como maxlength="50" en los inputs) para evitar que payloads inválidos viajes por la red.
  Esto debe de acompañarse de mensajes de error de validación claros en la interfaz para proteger la experiencia del usuario.
* **Backend (Sincronización de Seguridad):** Sincronizar las defensas del servidor contra la inyección de payloads masivos.
* **SecOps(Trazabilidad y Monitoreo):** Implementar la agregación de logs de seguridad en el backend para registrar intentos de inyección o violaciones de límites (Registrando IP, timestamp y payload rechazado).
  Esto garantizará el correcto funcionamiento y la detección temprana de vulnerabilidades sistémicas en la plataforma.

---
### **Entorno**
* **Tipo y versión del navegador**  (Chrome 148, Firefox 150)
* **Sistema operativo** (Windows 11)
* **Entorno** ( puesta en escena)

### 📑 **Evidencia del Comportamiento Asimétrico**

#### 1.- Datos Enviador por el Cliente (payload Interceptado)
El cliente envio una cadena de **50 caracteres** llegando al Bounday Values (Valores Límites) en la caja de texto
<img width="1588" height="733" alt="BUG_03 Payload Interceptado" src="https://github.com/user-attachments/assets/9b842297-b61c-4a37-96e1-3a938696fa62" />

#### 2.- Pestaña Header del payload Interceptado
Se puede evidenciar el rechazó de la solicitud por parte del backend, enviando un Status Code 400 Bad Request

<img width="1593" height="730" alt="BUG_03 Header de la peticion enviada Post 400 Bad Resquest" src="https://github.com/user-attachments/assets/4768e6f6-5da4-4bcc-a818-2bb85ca4dd99" />

### 3.- Visión del mensaje devueltos por el servidor

<img width="1582" height="732" alt="BUG_03  HTML estructurado de error" src="https://github.com/user-attachments/assets/186e5b01-5b02-4d5f-b93e-cd22877d7fff" />

### 4.- Visión del codigo HTML del mensaje enviado por el backend
 ```
<div class="wp-die-message">
    <h3>⚠️ Error de Integridad de Datos</h3>
    <p>La solicitud ha sido rechazada por el sistema de seguridad debido a que uno de los campos de texto excede el límite máximo permitido de caracteres. Por favor, reduce el texto e intenta nuevamente.</p>
</div>
 ```
<img width="1592" height="729" alt="BUG_03 Html de mensaje de error, por parte del backend, para mitigar la inyección masiva de caracteres " src="https://github.com/user-attachments/assets/7361391c-4dab-44b4-957c-33751d8811e8" />


