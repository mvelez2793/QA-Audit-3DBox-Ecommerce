# BUG_01 Defecto Funcional: Inyeccion de caracteres masivos en el campo "Identifica tu mascota" en la categoria Mascota
## Titulo: Personalización de nombre en Base de Madera - Categoria Mascotas 3D

### **Historia de Usuario:** 

* **Como:** Cliente de 3D-BOX
* **Quiero:** Ingresar el nombre de mi mascota en el campo "Identifica tu mascota"
* **Para que:** mi figura Coleccionable incluya la placa con su nombre en la base

## **Criterios de Aceptación (Gerkind)**

* **Escenario 1: Validación Exitosa de Nombre (HAPPY PATH)**
* **Given** el usuario se encuentre en el formulario de personalizacion de ´Crear mi mascota´ en 3D
* **When** ingresa su nombre alfanumérico de 30 caracteres
* **Then** el sistema permite continuar con el siguiente requesito para continuar con la compra de la figura personalizada

### **Escenario 2: Rechazo del sistema por exceso de caracteres**

* **Given** el sistema tiene una restriccion de negocio de 50 caracteres
* **When** el usuario intenta enviar un payload  de 10.000 caracteres mediante bypass de frontend
* **Then** el servidor debe retornar un codigo de error de 400 bad resquest y no aceptar los datos.

