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
1.- Navegar al formulario de Personalización de cualquier categoria. 
2.- Completar los pasos iniciales obligatorias del flujo visual. 
3.- El campo de entrada de texto "Identifica tu mascota" por ejemplo ingresar el limite superior de valores permitidos 
(Ej:¨Identifica a tu mascota¨ 50 caracteres alfánumeriocos) y (Ej:¨Detalle¨ 300 caracteres alfánumeriocos)
4.- Abrir las herramientas de desarrollador (F12) en la pestaña Network (Red)
5.- Agregar al carrito de compras

### **Resultado Esperado**
El producto es agregado al carrito de compras, enviando la información por medio de backend y obteniendo un Sattus Code de 200OK. 

### **Resultado Obtenido**
La interfaz de usuario se congela sin mostrar alertas de error nativas, y la petición hacia el servidor, se registra en color rojo con un código de estado 400 Bad Request.

### **Entorno**
* **Tipo y versión del navegador**  (Chrome 148, Firefox 150)
* **Sistema operativo** (Windows 11)
* **Entorno** ( puesta en escena)

### 📑 **Evidencia del Comportamiento Asimétrico**

#### 1.- Datos Enviador por el Cliente (payload Interceptado)
El cliente envio una cadena de **50 caracteres** llegando al Bounday Values (Valores Límites) en la caja de texto


#### 2.- Pestaña Header del payload Interceptado
Se puede evidenciar el rechazó de la solicitud por parte del backend, enviando un Status Code 400 Bad Request


### 3.- Visión de los datos devueltos por el servidor


### 4.- Visión del codigo HTML del mensaje enviado por el backend
<div class="wp-die-message">
    <h3>⚠️ Error de Integridad de Datos</h3>
    <p>La solicitud ha sido rechazada por el sistema de seguridad debido a que uno de los campos de texto excede el límite máximo permitido de caracteres. Por favor, reduce el texto e intenta nuevamente.</p>
</div>


