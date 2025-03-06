# Documento de Arquitectura del Sistema de Gestión de Órdenes y Entregas

## 1. Introducción

Este documento describe la arquitectura inicial (requisitos funcionales, requisitos de calidad y restricciones) del sistema de gestión de órdenes y entregas de Frenchie Cases, una tienda en línea especializada en la comercialización de accesorios para teléfonos móviles. El sistema estará basado en microservicios para garantizar escalabilidad, resiliencia y facilidad de mantenimiento.

**Equipo:** *1*

**Integrantes:** *Alejandro Marin Hoyos, Carlos Alberto Camacho Castaño, Juan David Valencia Montalvo, Kevin Alexander Marín Henao, Manuel Antonio Vidales Duran.*

**Fecha:** *20/02/2025*

---

## 2. Requisitos Funcionales  
Los requisitos funcionales se presentan en forma de **historias de usuario**, especificando los **criterios de aceptación**.

### **Historias de Usuario**
| **ID**    | **Historia de Usuario**                                                                                                           | **Criterios de Aceptación**                                                                                                                                                                                                                                                                                            |
| --------- | --------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **US-01** | Como usuario quiero que la aplicación cuente con registro de usuarios, con diferentes roles como administrador y repartidor | - Dado que un usuario desea registrarse, cuando complete el formulario de registro con sus datos y rol correspondiente, entonces la aplicación creará la cuenta y asignará el rol seleccionado. |
| **US-02** | Como cliente, quiero poder agregar productos a un carrito de compras para realizar pedidos fácilmente. | - Dado que un cliente desea comprar productos, cuando agregue o elimine artículos del carrito, entonces la aplicación actualizará el contenido del carrito de compras. <br> - Dado que un cliente ha añadido productos al carrito, cuando acceda a la vista del carrito, entonces podrá ver la lista con el nombre, imagen, cantidad y precio de los productos añadidos. <br> - Dado que un cliente desea cambiar la cantidad de un producto en el carrito, cuando edite la cantidad, entonces el sistema actualizará el total del pedido. |
| **US-03** | Como cliente, quiero conocer el estado de mi pedido en tiempo real. | - Dado que un cliente tiene un pedido en curso, cuando consulte su estado, entonces la aplicación mostrará si está "EN PROCESO", "EN CAMINO" o "ENTREGADO". <br> - Dado que el estado de un pedido cambia, cuando ocurra una actualización, entonces el sistema reflejará el cambio en menos de un segundo. |
| **US-04** | Como cliente, quiero realizar pedidos de productos desde la tienda en línea. | - Dado que un cliente ha finalizado su selección de productos, cuando confirme la compra, entonces el sistema generará una orden de pedido. <br> - Dado que un cliente está por confirmar su compra, cuando acceda a la pantalla de pago, entonces la aplicación mostrará un resumen del pedido antes de la confirmación. |
| **US-05** | Como administrador, quiero gestionar productos en el inventario (agregar, editar, eliminar y ver stock). | - Dado que un administrador desea gestionar el inventario, cuando realice operaciones de agregar, editar o eliminar productos, entonces la aplicación reflejará los cambios en el sistema. <br> - Dado que el stock de un producto es bajo, cuando este alcance un nivel crítico, entonces el sistema enviará una notificación al administrador. |
| **US-06** | Como usuario, quiero buscar productos por nombre o categoría. | - Dado que un usuario necesita encontrar un producto, cuando ingrese un término de búsqueda o seleccione una categoría, entonces el sistema mostrará los productos relevantes. <br> - Dado que un usuario realiza una búsqueda, cuando el término sea ambiguo, entonces el sistema priorizará los resultados más relevantes. |
| **US-07** | Como repartidor, quiero visualizar los pedidos asignados y sus rutas de entrega. | - Dado que hay pedidos pendientes de entrega, cuando un repartidor inicie sesión, entonces verá los pedidos asignados automáticamente. <br> - Dado que un repartidor necesita entregar un pedido, cuando consulte su ruta de entrega, entonces el sistema mostrará el trayecto en un mapa. <br> - Dado que un repartidor completa una entrega, cuando actualice el estado del pedido, entonces la aplicación reflejará el cambio en tiempo real. |
| **US-08** | Como administrador, quiero recibir alertas cuando haya fallos en el sistema. | - Dado que ocurre un error crítico en el sistema, cuando se detecte una falla, entonces el sistema generará logs y métricas para su análisis. <br> - Dado que se ha identificado un error crítico, cuando este ocurra, entonces se enviará una notificación al administrador. |
| **US-09** | Como cliente, quiero recibir una notificación cuando mi pedido cambie de estado. | - Dado que el estado de un pedido cambia, cuando se actualice a una nueva etapa, entonces el usuario recibirá una notificación en la aplicación. <br> - Dado que un usuario tiene pedidos en curso, cuando consulte su historial de notificaciones, entonces podrá ver un registro de los cambios de estado de sus pedidos. |
| **US-10** | Como administrador, quiero integrar un sistema de pagos para procesar transacciones. | - Dado que un cliente desea pagar un pedido, cuando ingrese los datos de su tarjeta de crédito/débito, entonces el sistema procesará la transacción. <br> - Dado que se ha realizado un intento de pago, cuando este sea exitoso o fallido, entonces el sistema notificará el resultado al cliente. |
| **US-11** | Como usuario, quiero que la aplicación sea segura y requiera autenticación para acceder a sus funcionalidades. | - Dado que un usuario intenta acceder a una ruta protegida, cuando no esté autenticado, entonces el sistema le pedirá iniciar sesión. <br> - Dado que un usuario ha iniciado sesión, cuando supere un tiempo de inactividad, entonces el sistema cerrará la sesión automáticamente. |
| **US-12** | Como administrador, quiero que el API Gateway gestione las peticiones a los microservicios para mejorar el rendimiento y la seguridad. | - Dado que el sistema recibe múltiples solicitudes, cuando se implemente el API Gateway, entonces se configurará el balanceo de carga para distribuirlas eficientemente. <br> - Dado que un usuario intenta acceder a un microservicio, cuando este requiera autenticación, entonces el API Gateway validará sus credenciales. <br> - Dado que un usuario realiza muchas solicitudes en poco tiempo, cuando exceda el límite permitido, entonces el sistema bloqueará temporalmente las peticiones. |
| **US-13** | Como administrador, quiero ver un dashboard con métricas del sistema. | - Dado que un administrador necesita monitorear el sistema, cuando acceda al dashboard, entonces verá métricas en tiempo real sobre órdenes, entregas y actividad de usuarios. <br> - Dado que un administrador consulta el rendimiento del sistema, cuando visualice el dashboard, entonces verá gráficos con datos históricos de uso y rendimiento. |
| **US-14** | Como cliente, quiero poder calificar los productos y dejar reseñas para ayudar a otros compradores. | - Dado que un cliente ha comprado un producto, cuando acceda a la opción de calificación, entonces podrá asignarle entre 1 y 5 estrellas. <br> - Dado que un cliente desea dejar una reseña, cuando escriba su opinión y agregue fotos o videos, entonces la aplicación permitirá guardar y publicar su comentario. |
| **US-15** | Como cliente, quiero ver un historial de mis pedidos para consultar compras pasadas. | Dado que el usuario ha realizado compras, cuando acceda a la sección "Historial de pedidos", entonces podrá ver una lista con todas sus órdenes anteriores.|
| **US-16** | Como usuario, quiero poder actualizar mi información personal (nombre, dirección, etc.). | - Dado que el usuario está autenticado, cuando acceda a la sección "Mi perfil", entonces podrá ver su información personal actual. <br>- Dado que el usuario desea actualizar su información, cuando edite campos como nombre, dirección o teléfono, entonces podrá guardar los cambios exitosamente. <br>- Dado que el usuario desea administrar sus direcciones de envío, cuando acceda a la sección de direcciones en su perfil, entonces podrá agregar, editar, eliminar y seleccionar una dirección predeterminada para sus pedidos.                                                                                                                                |                                                                                                                                                                                                                                                                                                                        |
|           |                                                                                                                                   |                                                                                                                                                                                                                                                                                                                        |



## 3. Requisitos de Calidad

Los requisitos de calidad se presentan en forma de **historias de calidad**, siguiendo la estructura de Len Bass.

### **Historias de Calidad**

| **ID** | **Fuente** | **Estímulo** | **Artefactos** | **Entorno** | **Respuesta** | **Medida de Respuesta** |
| --- | --- | --- | --- | --- | --- | --- |
| **RQ-01** | Cliente | Se reporta una demora en la carga de la tienda en línea. | Interfaz de usuario, API de productos | Picos de alta demanda | La tienda debe cargar en menos de 2 segundos en condiciones normales y no superar los 5 segundos en picos de demanda. | Tiempo de carga medido con herramientas de monitoreo. |
| **RQ-02** | Administrador | Se necesita un reporte detallado de inventario en tiempo real. | Módulo de reportes | Cualquier momento | El sistema debe generar reportes en menos de 5 segundos. | Tiempo de generación del reporte medido con logs del sistema. |
| **RQ-03** | Auditor de seguridad | Se detecta una vulnerabilidad en la autenticación de usuarios. | Módulo de autenticación | Entorno de producción | Se debe aplicar un parche de seguridad en menos de 24 horas. | Tiempo entre la notificación y la resolución del problema. |
| **RQ-04** | Cliente | Se experimenta una caída del servicio durante una transacción de pago. | API de pagos, base de datos | Entorno de producción | El sistema debe contar con mecanismos de recuperación automática para reintentar la transacción. | Tiempo de recuperación del sistema medido en logs y herramientas de monitoreo. |
| **RQ-05** | Repartidor | Se necesita acceder a los pedidos asignados sin interrupciones. | Módulo de pedidos | Durante la jornada de trabajo | La aplicación debe estar disponible el 99.9% del tiempo. | Medición del uptime con herramientas de monitoreo. |
| **RQ-06** | Cliente | Se reporta inconsistencia en el seguimiento del pedido. | Módulo de rastreo de pedidos | En tránsito | La actualización del estado del pedido no debe tardar más de 10 segundos. | Tiempo de latencia medido en pruebas de rendimiento. |
| **RQ-07** | Cliente | Se experimenta lentitud en la carga del carrito de compras. | Módulo de carrito | Picos de tráfico en la tienda | El carrito de compras debe cargar en menos de 2 segundos. | Tiempo de respuesta medido con herramientas de monitoreo. |
| **RQ-08** | Administrador | Se necesita detectar y prevenir ataques de denegación de servicio (DDoS). | API Gateway, firewall de seguridad | Cualquier momento | Se deben aplicar restricciones de tasa de peticiones para prevenir sobrecargas y rechazar tráfico malicioso. | Número de peticiones bloqueadas y estabilidad del servicio medida en logs. |
| **RQ-09** | Cliente | Se desea asegurar que los pagos procesados sean seguros y confiables. | Módulo de pagos | Entorno de producción | Todas las transacciones deben estar cifradas con protocolos seguros y verificadas antes de ser procesadas. | Auditorías de seguridad y validaciones de cumplimiento (PCI DSS). |
| **RQ-10** | Cliente | Se requiere que las notificaciones sobre cambios en el estado del pedido sean inmediatas. | Módulo de notificaciones | Entorno de producción | Las notificaciones deben enviarse en menos de 3 segundos tras un cambio de estado. | Tiempo de entrega de la notificación medido en pruebas de rendimiento. |




## 4. Restricciones del Sistema  
Las restricciones establecen **limitaciones** en la arquitectura del sistema, ya sean tecnológicas, de negocio, regulatorias o de infraestructura.

### **Lista de Restricciones**
| **Tipo de Restricción** | **Descripción** |
|------------------------|----------------|
| **Regulatoria** | El sistema debe cumplir con las políticas de uso de datos establecidas por la empresa, garantizando la protección de la información sensible y el cumplimiento de normativas como GDPR o la Ley de Protección de Datos Personales. Esto implica la implementación de controles de acceso, cifrado de datos y mecanismos de auditoría para asegurar el manejo adecuado de la información. |
| **Tecnológica** | El sistema debe desarrollarse utilizando Angular para el frontend y Spring Boot con APIs REST para la capa de servicios, asegurando una arquitectura moderna y escalable. La base de datos deberá ser PostgreSQL, garantizando compatibilidad con la infraestructura existente y optimización en el manejo de datos |
| **Tecnológica** | La aplicación debe seguir una arquitectura basada en **microservicios**, utilizando **Spring Boot** para el backend y **Angular** para el frontend. Además, los microservicios deben comunicarse mediante **API REST** y gestionarse a través de un API Gateway que implemente balanceo de carga y autenticación centralizada. |
| **De Negocio** | La plataforma debe permitir la **trazabilidad completa de los pedidos** desde su creación hasta su entrega, registrando cambios en los estados y generando reportes accesibles para los administradores. Esto es un requisito para garantizar el cumplimiento de auditorías internas y mejorar la calidad del servicio. |
| **De Infraestructura** | La base de datos **PostgreSQL** debe estar configurada con replicación automática y balanceo de carga para garantizar la continuidad del servicio.|
| **De Infraestructura** | La aplicación debe ser desplegada en **AWS** utilizando **contenedores Docker**, asegurando escalabilidad y alta disponibilidad del sistema. Además, se debe implementar un monitoreo continuo de recursos y rendimiento para detectar posibles fallos antes de que afecten a los usuarios. |
|


