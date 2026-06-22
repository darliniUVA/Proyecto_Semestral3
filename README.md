# ISY1101 — EP2 Proyecto Semestral
**Despacho Dashboard — Innovatech Chile**
**Integrantes:** Mario Loyola — Lucia Salazar

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
