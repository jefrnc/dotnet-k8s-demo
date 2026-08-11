# ASP.NET Core Demo Application

[![.NET Core 3.1](https://img.shields.io/badge/.NET%20Core-3.1-purple.svg)](https://dotnet.microsoft.com/download/dotnet/3.1)
[![Docker](https://img.shields.io/badge/Docker-Ready-blue.svg)](https://www.docker.com/)
[![Kubernetes](https://img.shields.io/badge/Kubernetes-Ready-326ce5.svg)](https://kubernetes.io/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

> Una aplicación de demostración ASP.NET Core diseñada para pruebas en contenedores Docker y despliegues en Kubernetes.

## 📋 Descripción

Esta es una aplicación web de ejemplo construida con ASP.NET Core 3.1 que incluye:
- 🐳 Soporte completo para Docker
- ☸️ Health checks para Kubernetes
- 📊 Páginas de diagnóstico y pruebas
- 🔧 Endpoints útiles para testing de infraestructura

## 🚀 Inicio Rápido

### Prerrequisitos

- [.NET Core 3.1 SDK](https://dotnet.microsoft.com/download/dotnet/3.1)
- [Docker](https://www.docker.com/get-started) (opcional)
- [Git](https://git-scm.com/)

### Instalación Local

1. Clonar el repositorio:
```bash
git clone https://github.com/jefrnc/App-Demo-Net-Core.git
cd App-Demo-Net-Core
```

2. Restaurar dependencias:
```bash
dotnet restore
```

3. Ejecutar la aplicación:
```bash
dotnet run --project MyAppWeb/MyAppWeb.csproj
```

La aplicación estará disponible en `http://localhost:5000` o `https://localhost:5001`

## 🐳 Docker

### Construir la imagen

```bash
docker build -t myapp-demo .
```

### Ejecutar el contenedor

```bash
docker run -d -p 8080:80 --name myapp-demo myapp-demo
```

Acceder a la aplicación en `http://localhost:8080`

## ☸️ Kubernetes

### Despliegue básico

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp-demo
spec:
  replicas: 3
  selector:
    matchLabels:
      app: myapp-demo
  template:
    metadata:
      labels:
        app: myapp-demo
    spec:
      containers:
      - name: myapp-demo
        image: myapp-demo:latest
        ports:
        - containerPort: 80
        livenessProbe:
          httpGet:
            path: /actuator/health/liveness
            port: 80
          initialDelaySeconds: 30
          periodSeconds: 10
```

## 📁 Estructura del Proyecto

```
App-Demo-Net-Core/
├── MyAppWeb/
│   ├── Controllers/        # Controladores MVC
│   ├── Pages/             # Razor Pages
│   │   ├── Index.cshtml   # Página principal
│   │   ├── Error.cshtml   # Página de errores
│   │   ├── Vars.cshtml    # Variables de entorno
│   │   └── ...           # Otras páginas de prueba
│   ├── Mock/              # Implementaciones mock
│   ├── wwwroot/           # Archivos estáticos
│   ├── Program.cs         # Punto de entrada
│   ├── Startup.cs         # Configuración de la app
│   └── appsettings.json   # Configuración
├── Dockerfile             # Configuración Docker
├── MyAppWeb.sln          # Solución de Visual Studio
└── README.md             # Este archivo
```

## 🔧 Endpoints Disponibles

| Endpoint | Descripción |
|----------|-------------|
| `/` | Página principal con información del contenedor |
| `/actuator/health/liveness` | Health check para Kubernetes |
| `/vars` | Muestra variables de entorno |
| `/Pingout` | Endpoint de ping |
| `/wget` | Página de prueba wget |
| `/Error/500` | Página de manejo de errores |

## 🛠️ Tecnologías Utilizadas

- **Framework**: ASP.NET Core 3.1
- **UI**: Razor Pages
- **Estilos**: Bootstrap 4, jQuery
- **Serialización**: Newtonsoft.Json
- **Contenedores**: Docker (Linux)

## 📦 Dependencias Principales

- Microsoft.NET Core 3.1
- Newtonsoft.Json 13.0.2
- Microsoft.VisualStudio.Azure.Containers.Tools.Targets

## 🤝 Contribuir

Las contribuciones son bienvenidas. Por favor:

1. Fork el proyecto
2. Crea tu feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit tus cambios (`git commit -m 'Add some AmazingFeature'`)
4. Push a la branch (`git push origin feature/AmazingFeature`)
5. Abre un Pull Request

## 📝 Licencia

Este proyecto está bajo la Licencia MIT - ver el archivo [LICENSE](LICENSE) para más detalles.

## ⚠️ Nota Importante

Este proyecto utiliza .NET Core 3.1 que ya no tiene soporte oficial (EOL: Diciembre 2022). Para proyectos en producción, se recomienda actualizar a .NET 6 o .NET 8 (LTS).

## 👤 Autor

**jefrnc**

---
⭐ Si este proyecto te fue útil, considera darle una estrella!

---

## Support this project

Free, and maintained on my own time. If it saved you a weekend of work, you can
[sponsor me on GitHub](https://github.com/sponsors/jefrnc).

[![Sponsor](https://img.shields.io/badge/Sponsor-jefrnc-EA4AAA?logo=githubsponsors&logoColor=white)](https://github.com/sponsors/jefrnc)
