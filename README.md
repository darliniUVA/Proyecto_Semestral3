# ISY1101 — EP2 Proyecto Semestral
**Despacho Dashboard — Innovatech Chile**
**Integrantes:** Mario Loyola — Darleen Ortiz - Juliana Vega

---

## ¿Qué hace este proyecto?

Despacho Dashboard es una aplicación web de gestión de despachos y ventas para Innovatech Chile. Permite consultar órdenes de compra, revisar órdenes de despacho y gestionar productos y usuarios.

La solución está compuesta por 4 servicios dockerizados distribuidos en 3 instancias EC2 en AWS. Solo el Frontend es accesible desde Internet; el Backend y la Base de Datos operan en subredes privadas de la VPC.

El despliegue es completamente automatizado mediante un pipeline CI/CD en GitHub Actions que se activa con cada push a la rama `deploy`, construye las imágenes Docker, las publica en Docker Hub y las despliega en AWS EC2 usando AWS Systems Manager (SSM).

---

## Cómo levantar el proyecto localmente

**Requisitos:** Docker Desktop y Git instalados.

```bash
git clone -b deploy https://github.com/kodevlyu/ISY1101_EP2_Proyecto-Semestral.git
cd ISY1101_EP2_Proyecto-Semestral
docker compose up --build
```

Acceder en `http://localhost`

Para detener: `docker compose down`

---

## Acceso en Producción

- **Aplicación web:** http://52.55.201.206
- **Pipeline CI/CD:** https://github.com/kodevlyu/ISY1101_EP2_Proyecto-Semestral/actions
- **Imágenes Docker Hub:** https://hub.docker.com/repositories/marioloyol4

> Las credenciales de AWS Academy expiran con cada sesión. Actualizar los secrets `AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY` y `AWS_SESSION_TOKEN` en GitHub cada vez que se inicie el lab.

## EVALUACION 3

## Despliegue de Aplicación en AWS EKS con Kubernetes
Este proyecto implementa una arquitectura basada en contenedores utilizando Amazon Elastic Kubernetes Service (EKS), permitiendo ejecutar aplicaciones dentro de un clúster Kubernetes administrado en AWS.

La solución contempla la creación y configuración de un clúster, grupos de nodos administrados, configuración de red mediante subredes y preparación del entorno necesario para desplegar servicios escalables y disponibles.

Arquitectura Cloud Implementada

La infraestructura está basada en:

★ Amazon EKS como servicio de orquestación Kubernetes.

★ Grupo de nodos administrados para ejecutar cargas de trabajo.

★ VPC y subredes para comunicación de recursos.

★ IAM Roles para permisos del clúster y nodos.

★ Kubernetes para administración de contenedores.

## Arquitectura general:

Usuario
   |
   ↓
AWS Load Balancer
   |
   ↓
Servicio Kubernetes
   |
   ↓
Pods / Contenedores
   |
   ↓
Grupo de nodos EKS

## Creación del Clúster EKS

Se creó un clúster Kubernetes llamado:

.- cluster-tienda

Configuración principal:

.- Proveedor: Amazon EKS

.- Versión Kubernetes: 1.35

.- Plataforma: AWS

.- Estado: Activo

El clúster permite administrar los recursos Kubernetes necesarios para el despliegue de la aplicación.

## Configuración de Red

Se configuraron recursos de networking para permitir la comunicación entre los componentes.

Incluye:

• VPC.

• Subredes públicas y privadas.

• Security Groups.

• Etiquetas de Kubernetes.

Ejemplo de etiquetas configuradas:

→ kubernetes.io/role/elb = 1

.- Name = devops-subnet-public1-us-east-1a

.- kubernetes.io/cluster/cluster-tienda = shared

Estas etiquetas permiten que Kubernetes identifique las subredes disponibles para balanceadores y recursos del clúster.

## Grupo de Nodos EKS

Se creó un grupo de nodos administrados:

nodos-tienda

Este grupo permite ejecutar los pods dentro del clúster.

Configuración:

Tipo de capacidad:

Spot

Tipo de instancia:

t3.large

Sistema operativo:

Amazon Linux 2023

Tamaño de disco:

20 GB

## Configuración de Escalabilidad

El grupo de nodos fue configurado con parámetros de escalamiento:

• Tamaño mínimo: 1 nodo

• Tamaño deseado: 1 nodo

• Tamaño máximo: 3 nodos

Esto permite aumentar la capacidad del clúster cuando la demanda aumenta.

Beneficios:

.- Mayor disponibilidad

.- Mejor uso de recursos

.- Capacidad de crecimiento automático

## Roles IAM

Se configuraron permisos mediante IAM para permitir la comunicación segura entre AWS y Kubernetes.

Roles utilizados:

• Rol del clúster EKS.

• Rol IAM del nodo.

• Permisos necesarios para ejecutar recursos.

Esto evita almacenar credenciales directamente dentro de la aplicación.

## Despliegue con Kubernetes

Los servicios de la aplicación son desplegados mediante recursos Kubernetes:

.- Deployments.

.- Services.

.- Pods.

Flujo:

Imagen Docker
       |
       ↓
Amazon ECR
       |
       ↓
Deployment Kubernetes
       |
       ↓
Pods ejecutándose en EKS

## CI/CD

El proyecto utiliza integración y despliegue continuo mediante GitHub Actions.

Proceso automatizado:

Commit GitHub

↓

Build Docker

↓

Push imagen a ECR

↓

Actualizar Deployment Kubernetes

↓

Nueva versión desplegada en EKS

## Monitoreo

Se realiza seguimiento del estado del clúster mediante:

• Estado de nodos.

• Logs Kubernetes.

• Eventos del clúster.

• Métricas de AWS.

Permite detectar errores y validar la disponibilidad del sistema.

Estructura del Proyecto

Proyecto
│
├── frontend
│   ├── Dockerfile
│   └── código fuente
│
├── backend
│   ├── Dockerfile
│   └── API
│
├── kubernetes
│   ├── deployment.yaml
│   ├── service.yaml
│   └── ingress.yaml
│
└── .github
    └── workflows
        └── deploy.yml

## Ejecución

Clonar repositorio:

.- git clone <repositorio>

Aplicar recursos Kubernetes:

.- kubectl apply -f kubernetes/

Verificar pods:

.-kubectl get pods

Ver servicios:

.- kubectl get services

## Estado del Proyecto

.- Clúster EKS creado

.- Grupo de nodos configurado

.- Networking AWS configurado

.- IAM configurado

.- Escalabilidad preparada

.- Infraestructura lista para despliegue Kubernetes

.- Automatización CI/CD implementada

## Conclusión

La implementación permite contar con una infraestructura moderna basada en Kubernetes sobre AWS EKS, preparada para ejecutar aplicaciones contenerizadas de forma escalable, segura y automatizada mediante prácticas DevOps.





