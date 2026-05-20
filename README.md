# 🏗️ Orquestación de Infraestructura Multi-Servicio Controlada con Docker y WSL2

## 👥 Información del Grupo
* **Institución:** Universidad del Valle
* **Integrantes:** * Integrante 1 (Nombre Completo y Código)
  * Integrante 2 (Nombre Completo y Código)

---

## 📝 Descripción del Proyecto
Este proyecto implementa un entorno local controlado de alta disponibilidad y multi-contenedorizado utilizando **Docker Compose** sobre el Kernel nativo de Linux mediante **WSL2 (Windows Subsystem for Linux)**. 

El clúster automatiza el despliegue de 5 servicios independientes que interactúan entre sí a través de redes aisladas y puentes seguros, simulando una arquitectura moderna de microservicios en producción.

---

## 🗺️ Arquitectura del Entorno y Redes
El diseño se segmenta en dos redes virtuales internas (`bridge`):
1. **`dmz_frontend`**: Zona desmilitarizada expuesta que interconecta el Servidor Web (Nginx) y la API lógica (Node.js).
2. **`secure_backend`**: Red privada aislada de accesos externos directos, encargada de la intercomunicación segura entre la API, el motor relacional (PostgreSQL), la administración (pgAdmin) y el laboratorio de analítica (Jupyter Lab).

---

## 🛠️ Requisitos Previos e Instalación Base (WSL2 Linux)
Pasos sistemáticos ejecutados en la terminal de Ubuntu:
1. Actualización de dependencias principales del sistema: `sudo apt update && sudo apt upgrade -y`
2. Configuración de repositorios de Docker e instalación nativa de `docker-ce` y `docker-compose-plugin`.
3. Gestión de privilegios de usuario sin root: `sudo usermod -aG docker $USER`.
4. Inicialización manual del servicio en WSL2: `sudo service docker start`.

---

## 💻 Comandos Operativos Utilizados
* **Despliegue del entorno:** `docker compose up -d`
* **Validación de orquestación:** `docker ps`
* **Inspección de logs:** `docker logs api_node`
* **Conexión interactiva SQL:** `docker exec -it postgres_container psql -U dev_root -d production_db`

---

## 📸 Evidencias de Funcionamiento (Resultados del Laboratorio)

### 1. Estado del Clúster Local
El despliegue fue exitoso y los 5 contenedores se encuentran levantados y saludables (`Healthy` / `Running`).
*(Inserta aquí tu captura de la terminal ejecutando `docker ps`)*

### 2. Capa Frontend - Servidor Web Nginx
Verificación del puerto `8080`, sirviendo el archivo HTML mapeado mediante volúmenes.
*(Inserta aquí tu imagen: image_e644af.png)*

### 3. Capa Lógica - API Node.js (Health Check)
Verificación del puerto `3000` respondiendo de forma nativa en formato JSON.
*(Inserta aquí tu imagen: image_e644f2.png)*

### 4. Capa de Datos - Conexión Exitosa API 🔄 PostgreSQL
Demostración de la comunicación inter-contenedor. La API resuelve el DNS interno `postgres_container` y extrae la estampa de tiempo del motor relacional.
*(Inserta aquí tu imagen: image_e64534.png)*

### 5. Capa Analítica - Jupyter Lab
Entorno científico persistente inicializado correctamente mediante Token de seguridad.
*(Inserta aquí tu imagen: image_e64838.png)*
