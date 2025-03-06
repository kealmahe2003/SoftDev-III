# Documento de Arquitectura del Sistema de Gestión de Órdenes y Entregas

## 1. Introducción

Este documento describe la arquitectura inicial del sistema de gestión de órdenes y entregas, incluyendo requisitos funcionales, requisitos de calidad y restricciones clave que deben ser consideradas en el diseño del software.

**Equipo:** *1*

**Integrantes:** *Alejandro Marin Hoyos, Carlos Alberto Camacho Castaño, Juan David Valencia Montalvo, Kevin Alexander Marín Henao, Manuel Antonio Vidales Duran.*

**Fecha:** *20/02/2025*

---

## 2. Requisitos Funcionales  
Los requisitos funcionales se presentan en forma de **historias de usuario**, especificando los **criterios de aceptación**.

### **Historias de Usuario**
| **ID**    | **Historia de Usuario**                                                                                                           | **Criterios de Aceptación**                                                                                                                                                                                                                                                                                            |
| --------- | --------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **US-01** |  Como usuario quiero que la aplicación cuente con registro de usuarios, con diferentes roles como administrador, operarios  |La aplicación admite los distintos usuarios, con sus respectivos roles |
| **US-02** | Como cliente, quiero conocer el estado de mi pedido en tiempo real. | - La aplicación muestra el estado del pedido [EN PROCESO, EN CAMINO, ENTREGADO].  <br>- El estado del pedido se actualiza en menos de un segundo. |
| **US-03** | Como cliente, quiero realizar pedidos de productos desde la tienda en línea.| - Los clientes pueden agregar productos al carrito.  <br>- Se puede confirmar la compra y generar una orden.  <br>- Se muestra un resumen del pedido antes de confirmar.|
| **US-04** | Como administrador, quiero gestionar productos en el inventario (agregar, editar, eliminar y ver stock).|- Se pueden realizar operaciones CRUD sobre los productos.  <br>- El sistema notifica cuando el stock de un producto es bajo. 
| **US-05** | Como usuario, quiero buscar productos por nombre o categoría. | - Los productos pueden filtrarse por nombre y categoría.  <br>- La búsqueda devuelve resultados relevantes. |
| **US-06** | Como repartidor, quiero visualizar los pedidos asignados y sus rutas de entrega en tiempo real. | - El sistema asigna automáticamente pedidos a los repartidores disponibles.  <br>- Se muestran rutas de entrega en un mapa interactivo.  <br>- Se pueden actualizar estados de entrega. |
| **US-07** | Como administrador, quiero recibir alertas cuando haya fallos en el sistema. | - Se generan logs y métricas sobre el estado del sistema.  <br>- Se envían notificaciones en caso de errores críticos. |
| **US-08** | Como cliente, quiero recibir una notificación cuando mi pedido cambie de estado. | - Se envía una notificación al usuario cuando su pedido cambia de estado.  <br>- El usuario puede ver un historial de notificaciones. |
| **US-09** | Como administrador, quiero integrar un sistema de pagos para procesar transacciones. | - Se permite simular pagos con tarjetas de crédito/débito.  <br>- El sistema confirma automáticamente el pago exitoso o fallido. | 
| **US-10** | Como usuario, quiero que la aplicación sea segura y requiera autenticación para acceder a sus funcionalidades. | - Se utiliza OAuth2 y JWT para autenticación.  <br>- Las rutas protegidas requieren autenticación válida.  <br>- El sistema cierra sesión automáticamente tras un tiempo de inactividad. | 
| **US-11** | Como administrador, quiero que el API Gateway gestione las peticiones a los microservicios para mejorar el rendimiento y la seguridad. | - Se configura balanceo de carga para distribuir las solicitudes. <br>- Se implementa autenticación centralizada para los microservicios. <br>- Se establece un límite de peticiones por usuario para evitar sobrecarga. |
| **US-12** | Como administrador, quiero ver un dashboard con métricas del sistema. | - Se muestran datos en tiempo real sobre órdenes, entregas y actividad del usuario.  <br>- Se generan gráficos de rendimiento y uso del sistema. |                                                                                                                                    |                                                                                                                                                                                                                                                                                                                        |
|           |                                                                                                                                   |                                                                                                                                                                                                                                                                                                                        |



## 3. Requisitos de Calidad

Los requisitos de calidad se presentan en forma de **historias de calidad**, siguiendo la estructura de Len Bass.

### **Historias de Calidad**

| **ID** | **Fuente** | **Estímulo** | **Artefactos** | **Entorno** | **Respuesta** | **Medida de Respuesta** |
| --- | --- | --- | --- | --- | --- | --- |
| **RQ-01** | Operario | Se reporta una demora en la carga de la página de pedidos. | Interfaz de usuario | Picos de alta demanda | La página debe cargarse en menos de 2 segundos en condiciones normales. | Tiempo de carga medido con herramientas de monitoreo. |
| **RQ-02** | Gerente | Se necesita un reporte detallado de ventas en tiempo real. | Módulo de reportes | Horario de cierre | El sistema debe generar reportes en menos de 5 segundos. | Tiempo de generación del reporte medido con logs del sistema. |
| **RQ-03** | Auditor de seguridad | Se detecta una vulnerabilidad en el módulo de pagos. | Módulo de pago | Entorno de producción | Se debe aplicar un parche de seguridad en menos de 24 horas. | Tiempo entre la notificación y la resolución del problema. |

---


## 4. Restricciones del Sistema  
Las restricciones establecen **limitaciones** en la arquitectura del sistema, ya sean tecnológicas, de negocio, regulatorias o de infraestructura.

### **Lista de Restricciones**
| **Tipo de Restricción** | **Descripción** |
|------------------------|----------------|
| **Regulatoria** | El sistema debe cumplir con las políticas de uso de datos establecidas por la empresa, garantizando la protección de la información sensible y el cumplimiento de normativas como GDPR o la Ley de Protección de Datos Personales. Esto implica la implementación de controles de acceso, cifrado de datos y mecanismos de auditoría para asegurar el manejo adecuado de la información. |
| **Tecnológica** | El sistema debe desarrollarse utilizando Angular para el frontend y Spring Boot con APIs REST para la capa de servicios, asegurando una arquitectura moderna y escalable. La base de datos deberá ser PostgreSQL, garantizando compatibilidad con la infraestructura existente y optimización en el manejo de datos |
| **Tecnológica** | La aplicación debe seguir una arquitectura basada en **microservicios**, utilizando **Spring Boot** para el backend y **Angular** para el frontend. Además, los microservicios deben comunicarse mediante **API REST** y gestionarse a través de un API Gateway que implemente balanceo de carga y autenticación centralizada. |
| **De Negocio** | El sistema debe integrarse con un proveedor de pagos certificado en **PCI DSS**, garantizando la seguridad en el manejo de datos bancarios. No se debe almacenar información de tarjetas de crédito en la infraestructura de la empresa, sino delegar esta responsabilidad a un proveedor externo que cumpla con las normativas de seguridad financiera. |
| **De Negocio** | La plataforma debe permitir la **trazabilidad completa de los pedidos** desde su creación hasta su entrega, registrando cambios en los estados y generando reportes accesibles para los administradores. Esto es un requisito para garantizar el cumplimiento de auditorías internas y mejorar la calidad del servicio. |
| **Regulatoria** | Se debe almacenar un **registro detallado de logs** durante al menos **12 meses**, incluyendo accesos, cambios en la configuración, transacciones y errores críticos. Estos registros deben protegerse contra modificaciones no autorizadas y almacenarse en un sistema seguro y replicado. |
| **De Infraestructura** | La base de datos **PostgreSQL** debe estar configurada en un **clúster de alta disponibilidad**, con replicación automática y balanceo de carga para garantizar la continuidad del servicio. Además, se deben realizar copias de seguridad diarias y contar con un plan de recuperación ante desastres que permita restaurar los datos en menos de 30 minutos. |
| **De Infraestructura** | La aplicación debe ser desplegada en **AWS** utilizando **contenedores Docker** y orquestación con **Kubernetes**, asegurando escalabilidad y alta disponibilidad del sistema. Además, se debe implementar un monitoreo continuo de recursos y rendimiento para detectar posibles fallos antes de que afecten a los usuarios. |
| **De Infraestructura** |  El almacenamiento de logs y métricas debe gestionarse mediante volúmenes persistentes en Kubernetes, evitando dependencias en discos locales. Finalmente, la comunicación entre microservicios debe realizarse dentro de la red privada de Kubernetes, minimizando la exposición externa y mejorando la seguridad del sistema.|
| **De Negocio** | El sistema debe ser capaz de escalar automáticamente en Kubernetes para manejar picos de demanda sin afectar el rendimiento, y todas las operaciones clave, como órdenes, pagos y entregas, deben registrarse en logs auditables para garantizar trazabilidad y seguridad. |

>  **Tipos de restricciones:**  
> - **Tecnológicas:** Lenguajes, frameworks o herramientas que deben utilizarse.
> - **De negocio:** Normativas o estándares de la empresa.  
> - **Regulatorias:** Cumplimiento de normativas legales o de seguridad.  
> - **De infraestructura:** Limitaciones en hardware, red o almacenamiento.  
