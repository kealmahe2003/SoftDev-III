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
| **US-02** |  Los pedidos deben tener un atributo que informen el estado del pedido [EN CAMINO, RECIBIDO]| La aplicación actualiza y gestiona el estado de los pedidos, en un tiempo no mayor a un segundo                                                                                                                                                                                                                                                                                   |
| **US-03** | _[Agregar historia de usuario]_                                                                                                   | _[Agregar criterios de aceptación]_                                                                                                                                                                                                                                                                                    |
|           |                                                                                                                                   |                                                                                                                                                                                                                                                                                                                        |
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
| Regulatoria | El sistema debe cumplir con las políticas de uso de datos establecidas por la empresa, garantizando la protección de la información sensible y el cumplimiento de normativas como GDPR o la Ley de Protección de Datos Personales. Esto implica la implementación de controles de acceso, cifrado de datos y mecanismos de auditoría para asegurar el manejo adecuado de la información. |
| _[Agregar otro tipo]_ | _[Describir la restricción]_ |

>  **Tipos de restricciones:**  
> - **Tecnológicas:** Lenguajes, frameworks o herramientas que deben utilizarse.  
> - **De negocio:** Normativas o estándares de la empresa.  
> - **Regulatorias:** Cumplimiento de normativas legales o de seguridad.  
> - **De infraestructura:** Limitaciones en hardware, red o almacenamiento.  
