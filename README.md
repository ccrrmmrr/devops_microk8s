# Proyecto Final - Docker & Kubernetes

**Alumno:** Carlos Roberto Martinez Rivadeneira
**Fecha:**  30-10-2025
**Curso:** Docker & Kubernetes - i-Quattro

## 🔗 Enlaces Importantes

- **Repositorio GitHub:** https://github.com/ccrrmmrr/devops_microk8s
- **Backend v2.1:** https://hub.docker.com/repository/docker/carloscrmr/springboot-api/tags
- **Frontend v2.2:** https://hub.docker.com/repository/docker/carloscrmr/angular-frontend/tags

## 🏗️ Arquitectura del Proyecto

```bash
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
```

## 🛠️ Parte 1:Configuración del Ambiente

### Especificaciones Técnicas
- **Proveedor:** Digital Ocean
- **Instancia:** `carlos-martinez-k8s`
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

### 📁 Estructura del Proyecto
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


## 🔧 Parte 2: Backend v2.1

### Nuevo Endpoint Implementado

```bash

@GetMapping("/api/info")
public ResponseEntity<Map<String, Object>> getInfo() {
    Map<String, Object> info = new HashMap<>();
    info.put("alumno", "Carlos Martinez");
    info.put("version", "v2.1");
    info.put("curso", "Docker & Kubernetes - i-Quattro");
    info.put("timestamp", LocalDateTime.now().toString());
    info.put("hostname", System.getenv("HOSTNAME"));
    return ResponseEntity.ok(info);
}
```

### Workflow de Actualización

```bash

# Build y push de la imagen
docker build -t ccrrmmrr/springboot-api:v2.1 .
docker push ccrrmmrr/springboot-api:v2.1

# Actualización en Kubernetes
kubectl apply -f k8s/05-backend/api-deployment.yaml
kubectl rollout status deployment/api -n proyecto-integrador

```

### Screemshots
- [Código del endpoint agregado](https://github.com/ccrrmmrr/devops_microk8s/tree/main/Screemshots/part02/codigo_java.PNG)
- [docker images](https://github.com/ccrrmmrr/devops_microk8s/tree/main/Screemshots/part02/docker_images.PNG)
- [docker_hub](https://github.com/ccrrmmrr/devops_microk8s/tree/main/Screemshots/part02/dockerHub_tags.PNG)
- [kubectl rollout status](https://github.com/ccrrmmrr/devops_microk8s/tree/main/Screemshots/part02/kubectl_rollout_status.PNG)
- [kubectl get pods](https://github.com/ccrrmmrr/devops_microk8s/tree/main/Screemshots/part02/kubectl_get_pods.PNG)
- [API Info](https://github.com/ccrrmmrr/devops_microk8s/tree/main/Screemshots/part02/api_info.PNG)


## 🎨 Parte 3: Frontend v2.2

### Modificaciones en Angular 

#### app.component.html:
```bash

<div class="form-group">
  <button (click)="getSystemInfo()" class="btn-primary">
    Ver Info del Sistema
  </button>
</div>

<div *ngIf="systemInfo" class="card info-section">
  <h3>Información del Sistema</h3>
  <p><strong>Alumno:</strong> {{ systemInfo.alumno }}</p>
  <p><strong>Versión:</strong> {{ systemInfo.version }}</p>
  <!-- ... más campos ... -->
</div>

```

#### app.component.ts:

```bash

systemInfo: any = null;

getSystemInfo(): void {
  this.http.get('/api/info').subscribe({
    next: (data) => {
      this.systemInfo = data;
      this.success = 'Información del sistema cargada';
    },
    error: (err) => {
      this.error = 'Error al obtener información del sistema';
    }
  });
}
```

#### Deployment:

```bash
docker build -t ccrrmmrr/angular-frontend:v2.2 .
docker push ccrrmmrr/angular-frontend:v2.2
kubectl apply -f k8s/06-frontend/frontend-deployment.yaml
```
### Screemshots

- [Código modificado de Angular](https://github.com/ccrrmmrr/devops_microk8s/tree/main/Screemshots/part03/cod_change.PNG)
- [Link a tu imagen en Docker Hub](https://hub.docker.com/repository/docker/carloscrmr/angular-frontend/general)
- [docker images](https://github.com/ccrrmmrr/devops_microk8s/tree/main/Screemshots/part03/docker_hub.PNG)
- [kubectl get pods -w](https://github.com/ccrrmmrr/devops_microk8s/tree/main/Screemshots/part03/roll_out.PNG)
- [botón "Ver Info del Sistema"](https://github.com/ccrrmmrr/devops_microk8s/tree/main/Screemshots/part03/info_sistema.PNG)
- [información del sistema cargada](https://github.com/ccrrmmrr/devops_microk8s/tree/main/Screemshots/part03/boton_sistema.PNG)


### 🔄 Parte 4: Gestión de Versiones

#### Comandos de Rollout:

```bash

# Historial de deployments
kubectl rollout history deployment/api -n proyecto-integrador
kubectl rollout history deployment/frontend -n proyecto-integrador

# Rollback a versión anterior
kubectl rollout undo deployment/api -n proyecto-integrador

# Rollforward específico
kubectl rollout undo deployment/api --to-revision=2 -n proyecto-integrador

# Reinicio forzado
kubectl rollout restart deployment/api -n proyecto-integrador

```

#### ¿Qué hace kubectl rollout undo?
```bash
El comando kubectl rollout undo revierte un deployment a su revisión anterior, 
realizando  un  rolling update  automático que mantiene  la disponibilidad del 
servicio  durante el proceso. Es equivalente a un "ctrl+Z" para deployments de 
Kubernetes.

```

### Screemshots

- [kubectl rollout history del backend](https://github.com/ccrrmmrr/devops_microk8s/tree/main/Screemshots/part04/rollout_history_backend.PNG)
- [kubectl rollout history del frontend](https://github.com/ccrrmmrr/devops_microk8s/tree/main/Screemshots/part04/rollout_history_frontend.PNG)
- [proceso de rollback (undo)](https://github.com/ccrrmmrr/devops_microk8s/tree/main/Screemshots/part04/rollback_undo.PNG)
- [/api/info dejó de funcionar después del rollback](https://github.com/ccrrmmrr/devops_microk8s/tree/main/Screemshots/part04/api_info_NOK.PNG)
- [proceso de rollforward (undo)](https://github.com/ccrrmmrr/devops_microk8s/tree/main/Screemshots/part04/rollforward.PNG)
- [/api/info vuelve a funcionar](https://github.com/ccrrmmrr/devops_microk8s/tree/main/Screemshots/part04/api_info_OK.PNG)


### 🌐 Parte 5: Ingress + MetalLB
#### 🎯 Objetivo Cumplido
Configurar acceso externo a la aplicación mediante Ingress Controller y MetalLB como LoadBalancer en Digital Ocean.

#### 🔧 Configuración Implementada
##### Ingress Controller (Nginx)

```yaml
# k8s/07-ingress/ingress.yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: app-ingress
  namespace: proyecto-integrador
  labels:
    app: proyecto-integrador
    version: v2.0
  annotations:
    nginx.ingress.kubernetes.io/ssl-redirect: "false"
spec:
  ingressClassName: public
  rules:
  - http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: frontend-service
            port:
              number: 80
      - path: /api
        pathType: Prefix
        backend:
          service:
            name: api-service
            port:
              number: 8080
      - path: /actuator
        pathType: Prefix
        backend:
          service:
            name: api-service
            port:
              number: 8080
```

##### Servicio LoadBalancer para Ingress Controller

```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-ingress-microk8s-controller
  namespace: ingress
spec:
  type: LoadBalancer
  selector:
    name: nginx-ingress-microk8s
  ports:
    - name: http
      protocol: TCP
      port: 80
      targetPort: 80
    - name: https
      protocol: TCP
      port: 443
      targetPort: 443
```

#### MetalLB Configuration
```bash
# Habilitar MetalLB con rango de IPs en la VPC
microk8s enable metallb:138.68.10.100-138.68.10.110
```
### 🚀 Resultado Final

#### Estado del LoadBalancer
```bash
kubectl get svc -n ingress
```
```text
NAME                                TYPE           CLUSTER-IP       EXTERNAL-IP     PORT(S)                      AGE
nginx-ingress-microk8s-controller   LoadBalancer   10.152.183.197   138.68.10.100   80:32747/TCP,443:31223/TCP   15m
```

#### Estado del Ingress
```bash
kubectl get ingress -n proyecto-integrador
```
```text
NAME          CLASS    HOSTS   ADDRESS     PORTS   AGE
app-ingress   public   *       127.0.0.1   80      43h
```

### 🔍 Explicación Técnica
#### Flujo de Tráfico
```text
Internet User
    ↓
138.68.10.100:80 (LoadBalancer IP)
    ↓
nginx-ingress-microk8s-controller Service
    ↓
nginx-ingress-microk8s-controller-mb9j7 Pod
    ↓
Ingress Rules (app-ingress)
    ↓
frontend-service (/) | api-service (/api, /actuator)
    ↓
frontend Pods | api Pods
```

#### Routing Configurado
```
- / → frontend-service:80 (Angular Frontend)
- /api/* → api-service:8080 (Spring Boot API)
- /actuator/* → api-service:8080 (Spring Boot Health Checks)

```
### ✅ Verificación de Funcionamiento
#### Desde Terminal
```bash
# Frontend
curl http://138.68.10.100/

# API Endpoints
curl http://138.68.10.100/api/info
curl http://138.68.10.100/api/users
curl http://138.68.10.100/actuator/health

# Respuesta esperada del endpoint /api/info:
{
  "alumno": "CARLOS MARTINEZ",
  "version": "v2.1",
  "curso": "Docker & Kubernetes - i-Quattro",
  "timestamp": "2025-10-31T14:18:43.739080638",
  "hostname": "api-d89c7785f-plbrd"
}
```
#### Desde Navegador
```
- URL Principal: http://138.68.10.100/
- Funcionalidad: Formulario de registro + "Ver Info del Sistema"
```
### 🐛 Troubleshooting Resuelto
```
- Problema: Servicio LoadBalancer sin Endpoints
- Síntoma: Servicio creado pero sin tráfico (ENDPOINTS: <none>)
- Causa: Selector incorrecto en la definición del Service
- Solución: Usar selector name: nginx-ingress-microk8s que coincide con los labels del pod del ingress controller

- Problema: Ingress muestra ADDRESS: 127.0.0.1
- Explicación: Comportamiento normal del ingress controller de microk8s configurado con --publish-status-address=127.0.0.1. No afecta el funcionamiento externo.
```
### 🎯 Aprendizajes Clave
```
- LoadBalancer vs Ingress: MetalLB proporciona la IP externa, Ingress maneja el routing interno
- Selector Matching: Los servicios deben coincidir exactamente con los labels de los pods
- Cloud Networking: En Digital Ocean, usar IPs dentro del rango VPC para MetalLB
- External Access: Verificación desde múltiples dispositivos para confirmar accesibilidad
```
### 📊 Métricas de Éxito
```
- IP Externa Asignada: 138.68.10.100
- Todos los Endpoints Respondiendo
- Acceso desde Internet Confirmado
- Load Balancing Funcional entre múltiples pods
- Health Checks Operativos
```
### Diagrama
```
┌─────────────────┐ ┌──────────────────┐ ┌─────────────────┐
│ Internet │ │ LoadBalancer │ │ Ingress │
│ Users │───▶│ MetalLB │───▶│ Controller │
│ │ │ 138.68.10.100 │ │ Nginx │
└─────────────────┘ └──────────────────┘ └─────────────────┘
│
▼
┌─────────────────────────────────────────────────────────────────┐
│ Kubernetes Cluster │
│ ┌─────────────┐ ┌─────────────┐ ┌─────────────┐ │
│ │ Frontend │ │ Backend │ │ Database │ │
│ │ Service │ │ Service │ │ Service │ │
│ │ :80 │ │ :8080 │ │ :5432 │ │
│ └─────────────┘ └─────────────┘ └─────────────┘ │
└─────────────────────────────────────────────────────────────────┘

```

### Screemshots

- [Verificar Ingres](https://github.com/ccrrmmrr/devops_microk8s/tree/main/Screemshots/part05/verificar_ingres.PNG)
- [Describe Ingres](https://github.com/ccrrmmrr/devops_microk8s/tree/main/Screemshots/part05/describe_ingres.PNG)
- [fromtemd](https://github.com/ccrrmmrr/devops_microk8s/tree/main/Screemshots/part05/frontend.PNG)
- [EndPoints](https://github.com/ccrrmmrr/devops_microk8s/tree/main/Screemshots/part05/parte5-endpoints-test.PNG)
- [IP del Ingress](https://github.com/ccrrmmrr/devops_microk8s/tree/main/Screemshots/part05/ip_ingres.PNG)


### 📊 Resultados y Métricas

#### Estado Final del Cluster
```bash
# Todos los recursos desplegados
kubectl get all -n proyecto-integrador

# Estado de los deployments
kubectl get deployments -n proyecto-integrador

# Recursos utilizados
kubectl top pods -n proyecto-integrador

```

### 🎯 Conclusiones y Aprendizajes

#### Principales Aprendizajes
```bash
1. Workflow CI/CD en Kubernetes:
   Aprendí el proceso completo de build, push y deploy de aplicaciones en un cluster Kubernetes.

2. Gestión de Estado: 
   Comprendí cómo Kubernetes maneja los rolling updates y rollbacks manteniendo la disponibilidad.

3. Networking: 
   Entendí la configuración de Ingress controllers y MetalLB para exposición de servicios.

4. Troubleshooting: 
   Desarrollé habilidades para diagnosticar y resolver problemas comunes en deployments.
```

#### Aplicaciones en Proyectos Reales
```bash
Este proyecto simula un workflow empresarial real donde:

- Los desarrolladores actualizan código y construyen imágenes
- Las imágenes se publican en un registry (Docker Hub)
- Kubernetes automáticamente despliega las nuevas versiones
- Se mantiene alta disponibilidad durante las actualizaciones
- Se puede revertir cambios fácilmente si hay problemas
```

