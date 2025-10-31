# Proyecto Final - Docker & Kubernetes

**Alumno:** [Carlos Roberto Martinez Rivadeneira]
**Fecha:** [30-10-2025]
**Curso:** Docker & Kubernetes - i-Quattro

## Links de Docker Hub
- Backend v2.1: https://hub.docker.com/repository/docker/carloscrmr/springboot-api/tags
- Frontend v2.2: https://hub.docker.com/repository/docker/carloscrmr/angular-frontend/tags


## Parte 1: Setup del Ambiente
**Ambiente utilizado:**
- [DigitalOcean]
- Nombre de VM/Droplet: [carlos-martinez-k8s]
- Sistema operativo: Ubuntu 24.04 LTS
- Recursos: 4GB RAM, 2 CPU cores
- Red configurada: [Tipo de red en cloud]
- Rango MetalLB: [Tu rango de IPs]


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

Código modificado de Angular (screenshots de .html y .ts)
- [Código modificado de Angular](https://github.com/ccrrmmrr/devops_microk8s/tree/main/Screemshots/pasrt03/codigo_java.PNG)
Link a tu imagen en Docker Hub: https://hub.docker.com/r/tu-usuario/angular-frontend/tags
- [docker images](https://github.com/ccrrmmrr/devops_microk8s/tree/main/Screemshots/pasrt03/docker_hub.PNG)
- [kubectl get pods -w](https://github.com/ccrrmmrr/devops_microk8s/tree/main/Screemshots/pasrt03/roll_out.PNG)
- [botón "Ver Info del Sistema"](https://github.com/ccrrmmrr/devops_microk8s/tree/main/Screemshots/pasrt03/info del sistema.PNG)
- [información del sistema cargada](https://github.com/ccrrmmrr/devops_microk8s/tree/main/Screemshots/pasrt03/boton_ver info del sistema.PNG)


### Parte 4: Gestión de Versiones

- [kubectl rollout history del backend](https://github.com/ccrrmmrr/devops_microk8s/tree/main/Screemshots/part04/rollout_history_backend.PNG)
- [kubectl rollout history del frontend](https://github.com/ccrrmmrr/devops_microk8s/tree/main/Screemshots/part04/rollout_history_frontend.PNG)
- [proceso de rollback (undo)](https://github.com/ccrrmmrr/devops_microk8s/tree/main/Screemshots/part04/rollback_undo.PNG)
- [/api/info dejó de funcionar después del rollback](https://github.com/ccrrmmrr/devops_microk8s/tree/main/Screemshots/part04/api_info_NOK.PNG)
- [proceso de rollforward (undo)](https://github.com/ccrrmmrr/devops_microk8s/tree/main/Screemshots/part04/rollforward.PNG)
- [/api/info dejó vuelve a funcionar](https://github.com/ccrrmmrr/devops_microk8s/tree/main/Screemshots/part04/api_info_OK.PNG)
- [Explicación en tus propias palabras: ¿Qué hace kubectl rollout undo?]



### Parte 5: Ingress + MetalLB

Screenshot de kubectl get ingress mostrando la IP asignada
- [Verificar Ingres](https://github.com/ccrrmmrr/devops_microk8s/tree/main/Screemshots/part05/verificar_ingres.PNG)

Screenshot de kubectl describe ingress mostrando las rutas configuradas
- [Describe Ingres](https://github.com/ccrrmmrr/devops_microk8s/tree/main/Screemshots/part05/describe_ingres.PNG)

Screenshot del navegador accediendo a http://<IP-METALLB>/ (frontend)
- [fromtemd](https://github.com/ccrrmmrr/devops_microk8s/tree/main/Screemshots/part05/frontend.PNG)

Screenshot de EndPoints
- [EndPoints](https://github.com/ccrrmmrr/devops_microk8s/tree/main/Screemshots/part05/parte5-endpoints-test.PNG)

Screenshot de curl a /actuator/health mostrando status UP
- [proceso de rollforward (undo)](https://github.com/ccrrmmrr/devops_microk8s/tree/main/Screemshots/part05/rollforward.PNG)
IP del Ingress (anotar)
- [/api/info dejó vuelve a funcionar](https://github.com/ccrrmmrr/devops_microk8s/tree/main/Screemshots/part05/ip_ingres.PNG)
