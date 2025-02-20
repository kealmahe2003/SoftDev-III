# Documento de Arquitectura del Sistema de Gestión de Órdenes y Entregas

## 1. Introducción

Este documento describe la arquitectura inicial del sistema de gestión de órdenes y entregas, incluyendo requisitos funcionales, requisitos de calidad y restricciones clave que deben ser consideradas en el diseño del software.

**Equipo:** *1*

**Integrantes:** *Alejandro Marin Hoyos, Carlos Alberto Camacho Castaño, Jessica Villa Nuñez, Juan David Valencia Montalvo, Kevin Alexander Marín Henao, Manuel Antonio Vidales Duran.*

**Fecha:** *20/02/2025*


## 3. Requisitos de Calidad

Los requisitos de calidad se presentan en forma de **historias de calidad**, siguiendo la estructura de Len Bass.

### **Historias de Calidad**

| **ID** | **Fuente** | **Estímulo** | **Artefactos** | **Entorno** | **Respuesta** | **Medida de Respuesta** |
| --- | --- | --- | --- | --- | --- | --- |
| **RQ-01** | Operario | Se reporta una demora en la carga de la página de pedidos. | Interfaz de usuario | Picos de alta demanda | La página debe cargarse en menos de 2 segundos en condiciones normales. | Tiempo de carga medido con herramientas de monitoreo. |
| **RQ-02** | Gerente | Se necesita un reporte detallado de ventas en tiempo real. | Módulo de reportes | Horario de cierre | El sistema debe generar reportes en menos de 5 segundos. | Tiempo de generación del reporte medido con logs del sistema. |
| **RQ-03** | Auditor de seguridad | Se detecta una vulnerabilidad en el módulo de pagos. | Módulo de pago | Entorno de producción | Se debe aplicar un parche de seguridad en menos de 24 horas. | Tiempo entre la notificación y la resolución del problema. |

---