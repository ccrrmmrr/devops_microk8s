# Proyecto Final - Docker & Kubernetes

**Alumno:** Carlos Roberto Martinez Rivadeneira
**Fecha:**  30-10-2025
**Curso:** Docker & Kubernetes - i-Quattro

## 🔗 Enlaces Importantes

- **Repositorio GitHub:** https://github.com/ccrrmmrr/devops_microk8s
- **Backend v2.1:** https://hub.docker.com/repository/docker/carloscrmr/springboot-api/tags
- **Frontend v2.2:** https://hub.docker.com/repository/docker/carloscrmr/angular-frontend/tags

## 🏗️ Arquitectura del Proyecto

┌─────────────────┐    ┌──────────────────┐    ┌─────────────────┐
│ Frontend        │    │ Backend          │    │ Base de         │
│ Angular         │◄──►│ Spring Boot      │◄──►│ Datos           │
│ v2.2            │    │ v2.1             │    │ PostgreSQL      │
└─────────────────┘    └──────────────────┘    └─────────────────┘
      │                         │                     │
      │                         │                     │
      └─────────────────────────┼─────────────────────┘
                                │
                         ┌──────▼──────┐
                         │   Redis     │
                         │   Cache     │
                         └─────────────┘
## 🛠️ Parte 1:Configuración del Ambiente

### Especificaciones Técnicas
- **Proveedor:** Digital Ocean
- **Instancia:** `cesar-ramirez-k8s`
- **Sistema Operativo:** Ubuntu 24.04 LTS
- **Recursos:** 2 vCPUs, 4GB RAM
- **Cluster:** microk8s v1.30
- **Network:** VPC con MetalLB

### Addons de microk8s Habilitados
```bash
# Comandos ejecutados
microk8s enable dns
microk8s enable storage
microk8s enable ingress
microk8s enable metrics-server
microk8s enable metallb:10.120.0.100-10.120.0.110
```

## 📁 Estructura del Proyecto
```bash
devops_microk8s/
├── k8s/                    # Manifiestos de Kubernetes
│   ├── 01-namespace/
│   ├── 02-secrets/
│   ├── 03-configmaps/
│   ├── 04-database/
│   ├── 05-backend/
│   └── 06-frontend/
├── src/                    # Código fuente backend
├── frontend/               # Código fuente frontend
├── screenshots/            # Evidencias del proyecto
└── README.md
```

### Screemshots
- [microk8s status](https://github.com/ccrrmmrr/devops_microk8s/tree/main/Screemshots/part01/parte01_microk8s.PNG)
- [Pods running](https://github.com/ccrrmmrr/devops_microk8s/tree/main/Screemshots/part01/parte01_kubectl_get_all.PNG)
- [Frontend vi MetalLB](https://github.com/ccrrmmrr/devops_microk8s/tree/main/Screemshots/part01/parte01_front_end_inicial.PNG)
- [Instancia Cloud](https://github.com/ccrrmmrr/devops_microk8s/tree/main/Screemshots/part01/parte01_InstanciaCloud.PNG)


### Parte 2: Backend v2.1

- [Código del endpoint agregado](https://github.com/ccrrmmrr/devops_microk8s/tree/main/Screemshots/part02/codigo_java.PNG)
- [docker images](https://github.com/ccrrmmrr/devops_microk8s/tree/main/Screemshots/part02/docker_images.PNG)
- [docker_hub](https://github.com/ccrrmmrr/devops_microk8s/tree/main/Screemshots/part02/dockerHub_tags.PNG)
- [kubectl rollout status](https://github.com/ccrrmmrr/devops_microk8s/tree/main/Screemshots/part02/kubectl_rollout_status.PNG)
- [kubectl get pods](https://github.com/ccrrmmrr/devops_microk8s/tree/main/Screemshots/part02/kubectl_get_pods.PNG)
- [API Info](https://github.com/ccrrmmrr/devops_microk8s/tree/main/Screemshots/part02/api_info.PNG)


### Parte 3: Frontend v2.2

- [Código modificado de Angular](https://github.com/ccrrmmrr/devops_microk8s/tree/main/Screemshots/part03/cod_change.PNG)
- [Link a tu imagen en Docker Hub](https://hub.docker.com/repository/docker/carloscrmr/angular-frontend/general)
- [docker images](https://github.com/ccrrmmrr/devops_microk8s/tree/main/Screemshots/part03/docker_hub.PNG)
- [kubectl get pods -w](https://github.com/ccrrmmrr/devops_microk8s/tree/main/Screemshots/part03/roll_out.PNG)
- [botón "Ver Info del Sistema"](https://github.com/ccrrmmrr/devops_microk8s/tree/main/Screemshots/part03/info_sistema.PNG)
- [información del sistema cargada](https://github.com/ccrrmmrr/devops_microk8s/tree/main/Screemshots/part03/boton_sistema.PNG)


### Parte 4: Gestión de Versiones

- [kubectl rollout history del backend](https://github.com/ccrrmmrr/devops_microk8s/tree/main/Screemshots/part04/rollout_history_backend.PNG)
- [kubectl rollout history del frontend](https://github.com/ccrrmmrr/devops_microk8s/tree/main/Screemshots/part04/rollout_history_frontend.PNG)
- [proceso de rollback (undo)](https://github.com/ccrrmmrr/devops_microk8s/tree/main/Screemshots/part04/rollback_undo.PNG)
- [/api/info dejó de funcionar después del rollback](https://github.com/ccrrmmrr/devops_microk8s/tree/main/Screemshots/part04/api_info_NOK.PNG)
- [proceso de rollforward (undo)](https://github.com/ccrrmmrr/devops_microk8s/tree/main/Screemshots/part04/rollforward.PNG)
- [/api/info vuelve a funcionar](https://github.com/ccrrmmrr/devops_microk8s/tree/main/Screemshots/part04/api_info_OK.PNG)
- [Explicación en tus propias palabras: ¿Qué hace kubectl rollout undo?]



### Parte 5: Ingress + MetalLB

- [Verificar Ingres](https://github.com/ccrrmmrr/devops_microk8s/tree/main/Screemshots/part05/verificar_ingres.PNG)
- [Describe Ingres](https://github.com/ccrrmmrr/devops_microk8s/tree/main/Screemshots/part05/describe_ingres.PNG)
- [fromtemd](https://github.com/ccrrmmrr/devops_microk8s/tree/main/Screemshots/part05/frontend.PNG)
- [EndPoints](https://github.com/ccrrmmrr/devops_microk8s/tree/main/Screemshots/part05/parte5-endpoints-test.PNG)
- [IP del Ingress](https://github.com/ccrrmmrr/devops_microk8s/tree/main/Screemshots/part05/ip_ingres.PNG)
