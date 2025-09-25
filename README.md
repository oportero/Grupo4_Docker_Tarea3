# 📌 Grupo 4
## 📌 TAREA 03: Manejo de imágenes y análisis de vulnerabilidades con github actions. 


---

## 🚀 Integrantes
| Nro. | Nombre | Link |
|------|---------|---------|
| 1 | Giovanni Xavier Baño Jaya | https://github.com/Giovanni26101982/Grupo4_Docker_Tarea3 |
| 2 | Portero Salas Onofre Lolislao | https://github.com/oportero/Grupo4_Docker_Tarea3 |
| 3 | Jara Pauta Cesar Paúl | https://github.com/PaulJara84/Grupo4_Docker_Tarea3  |
| 4 | Maldonado Flores Oscar Alexander | https://github.com/Oscar112248/Grupo4_Docker_Tarea3 |
| 5 | Balarezo Leon Ricardo Martin | https://github.com/TinchoXD/Grupo4_Docker_Tarea3 |

---

## 📖 Introducción

En la presente tarea se documenta el desarrollo y entrega del laboratorio grupal fastapi-app, cuyo objetivo es construir, publicar y evaluar la seguridad de una imagen Dockerfile multistage, y automatizar el análisis de vulnerabilidades mediante GitHub Actions con Docker Scout.

El trabajo contempla: 

- Con base en el laboratorio de fastapi-app, deberan subir la imagen que le corresponde a su grupo y las aplicaciones a su repositorio de github 
- Construir la imagen, subir a docker hub y realizar el análisis de vulnerabilidades con docker scout mediante un flujo de github actions
- Realizar el reporte de lo ejecutado en el archivo Readme.md del repositorio. Dentro del reporte debe constar la captura de pantalla que muestre la subida de la imagen en su repositorio de Docker hub y los resultados del análisis de vulnerabilidades con docker scout.
- Este trabajo se lo realizó de manera grupal y se encuentra publicado eb el repositorio git.

---

## 🚀 Características
- GitHub Actions  


---  

## 📂 Estructura
```bash
├── app/
|   └── main.py 
├── .gitignore
├── Dockerfile
├── dockerhub-scout.yml
├── README.md
└── requerimientos.txt

```
--- 

## 🛠 Desarrollo - Procedimiento

--- 
1. **# actualizar**

```bash
sudo apt update && sudo apt dist-upgrade –y
```
--- 

2. **#clonar repositorio**

```bash
git clone https://github.com/oportero/Grupo4_Docker_Tarea3.git
```
<img width="798" height="171" alt="01" src="https://github.com/user-attachments/assets/b3f5cfa3-6a3d-4cb6-815f-8597f1010170" />

--- 

3. **#navegar al repositorio**

```bash
cd Grupo4_Docker_Tarea3/
```
<img width="749" height="174" alt="02" src="https://github.com/user-attachments/assets/a308a775-c3ab-4218-84f7-9048b8c24109" />

--- 

4. **# Construir la imagen Local**

```bash
docker build -t fastapi-multistage:dev .
```
<img width="955" height="466" alt="03" src="https://github.com/user-attachments/assets/d3722394-7b5f-4bc7-8307-87c086cf0989" />


<img width="955" height="716" alt="04" src="https://github.com/user-attachments/assets/c3f0dfb4-4297-45a0-a0f8-8e53a4a3b75d" />


<img width="945" height="117" alt="05" src="https://github.com/user-attachments/assets/1e79bbf3-e907-4eed-8b43-42b710c42a83" />

--- 

5. **# Verificar que exista la Imagen**

```bash
docker images | grep fastapi-multistage
```

<img width="951" height="62" alt="06" src="https://github.com/user-attachments/assets/6ba26d6e-3676-41f6-a236-0f9e8b53c763" />

--- 

6. **# Crear el contenedor**

```bash
docker run -d -p 8000:8004 --name fastapi fastapi-multistage:dev
```

<img width="1370" height="60" alt="07" src="https://github.com/user-attachments/assets/8d583ca5-e3ba-4512-a89e-c73c7beaf5af" />

--- 

7. **# Verificar el Log**

```bash
docker logs -f fastapi (ctrl + c para salir)
```
<img width="921" height="115" alt="08" src="https://github.com/user-attachments/assets/fc14feb0-d1ef-4398-b47b-7bf47300fcbd" />

--- 

**Subir a Docker Hub**
--- 
8. **# iniciar sesión en docker**

```bash
docker login -u <username> (docker login -u oportero)
```
--- 

9. **# ingresar contraseña o token**

```bash
El token se obtiene en la cuenta de DockerHub
Docker Hub → Account Settings → Security → New Access Token.
Token generado: en la imagen se muestra el token generado

```
<img width="1180" height="745" alt="image" src="https://github.com/user-attachments/assets/19cefd4c-fdea-4a5b-b177-c6cabe0c3601" />


<img width="1202" height="118" alt="image" src="https://github.com/user-attachments/assets/5b484987-4003-4f8f-a8ab-75717f02b63c" />


--- 

10. **# Etiquetar la imagen**

```bash
docker tag fastapi-multistage:dev oportero/fastapi-multistage:latest

```

<img width="693" height="30" alt="image" src="https://github.com/user-attachments/assets/05e643ca-0e7c-4e16-8660-e50987fb3aa6" />


--- 

11. **# Subir la Imagen**

<img width="1419" height="205" alt="image" src="https://github.com/user-attachments/assets/09b0bbd9-69e2-47e4-abd8-93c800f2dbc4" />

--- 

**Docker Scout**
---
12. **Probar Docker Scout**
   - **# Verificar que exista docker scout**
      ```bash
         docker scout version         
      ```
   - **Verificar donde se encuentran los plugins de docker**
      ```bash
         docker info | grep "Docker Root Dir"
      ```
      <img width="1103" height="48" alt="13" src="https://github.com/user-attachments/assets/703fe37d-d310-4ba9-b429-1ad6164b459f" />

   - **Si no existe crear la carpeta**
      ```bash
         mkdir -p ~/.docker/cli-plugins
      ```
      <img width="1057" height="33" alt="14" src="https://github.com/user-attachments/assets/a487d6c0-6827-4e0c-ab2e-fc3a1c44c525" />

   - **Descarga el binario de Docker Scout**
      ```bash
         curl -sSL https://github.com/docker/scout-cli/releases/latest/download/docker-scout_linux_amd64 -o ~/.docker/cli-plugins/docker-scout
      ```

   - **Otorgar permisos de Ejecución**
      ```bash
         chmod +x ~/.docker/cli-plugins/docker-scout
      ```

   - **Verificar la version de scout**

     <img width="759" height="422" alt="15" src="https://github.com/user-attachments/assets/4c6dfba9-d2d5-4a14-bdac-3c9c298da009" />
 
--- 

13. **# Ejecutar análisis**


      # Ejecutar análisis
      docker scout cves oportero/fastapi-multistage:latest
      
<img width="1460" height="323" alt="image" src="https://github.com/user-attachments/assets/de4b6fd7-d5cf-4b57-8271-c16f6f107fb3" />


      
      ## Packages and Vulnerabilities
      
<img width="1460" height="323" alt="image" src="https://github.com/user-attachments/assets/c6aae08b-3a03-47f4-b372-204589650bcc" />
<img width="1460" height="323" alt="image" src="https://github.com/user-attachments/assets/d10d17f0-f325-490e-a7a1-df421705ce98" />
<img width="846" height="756" alt="image" src="https://github.com/user-attachments/assets/457fa58f-9313-4362-830b-8139b5a7eeb6" />
<img width="936" height="742" alt="image" src="https://github.com/user-attachments/assets/678cf0af-74a2-42ee-a39d-3f2293c581dc" />
<img width="845" height="699" alt="image" src="https://github.com/user-attachments/assets/0a5706c5-5e01-476c-b838-65688ddbb8f7" />
<img width="1119" height="581" alt="image" src="https://github.com/user-attachments/assets/99950263-229a-43df-b7d8-aa36a120d88f" />

      ## docker scout recommendations oportero/fastapi-multistage:latest

<img width="1546" height="548" alt="image" src="https://github.com/user-attachments/assets/4cd9d2b7-3ce6-41ad-9cbe-bdc07506ca9b" />
<img width="1338" height="807" alt="image" src="https://github.com/user-attachments/assets/d18f8527-4071-4486-97bd-0aa5043e3a48" />


14. **Verificar el funcionanmineto del Contenedor**

```bash
curl http://localhost:8000
RESP: {"status":"ok","app":"Aplicación: fastapi-multistage"}

```
<img width="1235" height="40" alt="16" src="https://github.com/user-attachments/assets/af0d6e0b-3c6d-4b67-8b1f-cc63d55a21e5" />


--- 


## ✅ Conclusiones - Recomendaciones

1. El despliegue de la aplicación `FastAPI con Docker` se realizó exitosamente mediante la construcción de una imagen multistage, permitiendo una implementación más ligera y optimizada.
   
3. El análisis con Docker Scout evidenció que, aunque la aplicación funciona correctamente, existen vulnerabilidades conocidas en librerías del sistema base y dependencias de Python.

4. Para mitigar riesgos de seguridad se recomienda:
   - Actualizar la librería starlette a la versión 0.47.2 o superior, corrigiendo fallas de recursos sin límite.
   - Mantener actualizado el sistema base y explorar imágenes oficiales más recientes o variantes “slim” para reducir la superficie de ataque.
   - Establecer un flujo de integración continua (CI/CD) que incluya escaneo automático de vulnerabilidades en cada build de imagen.
  
1. **Cumplimiento de los entregables y trazabilidad**  
   Se construyó la imagen asociada al grupo, se publicó en Docker Hub y se registraron evidencias del proceso y del análisis de vulnerabilidades en el README.md.

1. **Impacto de la estrategia de construcción (single vs multistage)**  
   El uso de `multistage` (cuando aplicó) permitió `reducir tamaño de imagen` y `disminuir la superficie de ataque`, mejorando tiempos de pull y despliegue. En escenarios simples, single puede ser suficiente, pero para producción la strategia multietapa mostró claras ventajas de seguridad y eficiencia.

1. **Integración de seguridad en el ciclo de vida (Docker Scout + CI)**  
   La automatización con `GitHub Actions` y `Docker Scout` aportó `visibilidad continua`. Esta práctica refuerza la cultura `DevSecOps` al detectar riesgos antes del despliegue.

1. **Trabajo individual con enfoque profesional**  
   La organización para la ejecución del trabajo grupal, junto con la publicación en Docker Hub y auditoría automatizada, favoreció la `responsabilidad técnica` y la `calidad del entregable`, alineando el resultado con expectativas de acuerdo a lo solicitado.

1. La actividad no solo cumplió los requerimientos, sino que consolidó un `pipeline reproducible y seguro` para empaquetar aplicaciones con Docker, `publicarlas` y `evaluar su postura de seguridad` de forma integral, dejando como valor final un repositorio verificable y un informe con evidencias claras del proceso.

3. Finalmente, la práctica demuestra la importancia de no solo asegurar la funcionalidad del contenedor, sino también su seguridad y mantenimiento continuo en entornos de producción.

---
