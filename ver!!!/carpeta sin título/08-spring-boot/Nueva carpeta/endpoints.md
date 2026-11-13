#  📌 Endpoints en Spring Boot

### ▫️ ¿Qué es un Endpoint?

Un **endpoint** es una URL que permite acceder a tu aplicación.  
Es como una «puerta de entrada» para interactuar con ella desde el exterior.

<br>

**EJEMPLO:**

```
http://localhost:8080/actuator/health
```

Este endpoint indica si tu aplicación está funcionando.

<br>

**--- FALTA ACTUALIZAR Y ORGANIZAR !!!!!!!** 🚧🚧🚧🚧🚧🚧🚧🚧🚧🚧🚧🚧🚧🚧🚧🚧 

## 🔍 Spring Boot Actuator

**Actuator** añade automáticamente endpoints que permiten monitorear y gestionar tu aplicación.

### ¿Para qué sirven?

* Ver si la aplicación funciona correctamente.
* Consultar información del sistema.
* Revisar métricas (CPU, memoria, etc.).
* Ver beans cargados.
* Consultar variables de entorno.

--- 🚧🚧🚧🚧🚧🚧

<br>

---

## 🏷️ Endpoints Principales

#### ✔ `/actuator/health` — Estado de salud

Muestra si la aplicación está funcionando.

```json
// Ejemplo

{
  "status": "UP"
}
```

<br>

#### ✔ `/actuator/info` — Información de la aplicación

Devuelve datos configurados sobre tu aplicación.

```json
// Ejemplo

{
  "app": {
    "name": "Mi Aplicación",
    "version": "1.0.0"
  }
}
```

<br>

#### ✔ `/actuator/metrics` — Métricas

Muestra estadísticas de CPU, memoria, etc.

<br>

#### ✔ `/actuator/beans` — Beans de Spring

Lista todos los componentes gestionados por Spring.

<br>

#### ✔ `/actuator/env` — Variables de entorno

Muestra configuraciones y propiedades.








## ⚙️ Configuración Básica

### 1. Agregar dependencia en `pom.xml`:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```

### 2. Configurar `application.properties`:

```properties
management.endpoints.web.exposure.include=*
management.endpoint.health.show-details=always
```

Para exponer solo ciertos endpoints:

```properties
management.endpoints.web.exposure.include=health,info,metrics
```

---

## 🛠️ Cómo probar los endpoints

### Navegador

```
http://localhost:8080/actuator/health
```

### Postman

* Método GET
* URL: `http://localhost:8080/actuator/health`

### curl

```bash
curl http://localhost:8080/actuator/health
```

---

## 🔒 Seguridad en Producción

⚠️ **No expongas todos los endpoints en producción.**

Recomendación:

```properties
management.endpoints.web.exposure.include=health,info
```

Usa **Spring Security** para proteger otros endpoints.

---

## 💡 Crear tu propio Health Indicator

```java
import org.springframework.boot.actuate.health.Health;
import org.springframework.boot.actuate.health.HealthIndicator;
import org.springframework.stereotype.Component;

@Component
public class MiVerificacionSalud implements HealthIndicator {

    @Override
    public Health health() {
        boolean sistemaFunciona = verificarAlgo();

        if (sistemaFunciona) {
            return Health.up().withDetail("mensaje", "Todo está bien").build();
        } else {
            return Health.down().withDetail("error", "Algo no funciona").build();
        }
    }

    private boolean verificarAlgo() {
        return true;
    }
}
```

---

## 📋 Tabla Resumen

| Endpoint            | Descripción                 | Expuesto por defecto |
| ------------------- | --------------------------- | -------------------- |
| `/actuator`         | Lista endpoints disponibles | Sí                   |
| `/actuator/health`  | Estado de salud             | Sí                   |
| `/actuator/info`    | Información de la app       | Sí                   |
| `/actuator/metrics` | Métricas del sistema        | No                   |
| `/actuator/beans`   | Beans de Spring             | No                   |
| `/actuator/env`     | Variables de entorno        | No                   |
| `/actuator/loggers` | Configuración de logs       | No                   |

---

## 🚦 Estados del Health Endpoint

| Estado           | Significado       |
| ---------------- | ----------------- |
| `UP`             | Todo funciona     |
| `DOWN`           | Algo falla        |
| `OUT_OF_SERVICE` | Fuera de servicio |
| `UNKNOWN`        | Desconocido       |

---

## 📚 Recursos

* Documentación Spring Boot Actuator
* Spring Boot Reference Guide

---

## ✔️ Checklist de Aprendizaje

* [ ] Comprendo qué es un endpoint
* [ ] Sé agregar Actuator al proyecto
* [ ] Sé configurar endpoints
* [ ] Probé `/actuator/health`
* [ ] Entiendo la importancia de la seguridad
* [ ] Puedo crear un HealthIndicator básico

---

Guía diseñada para estudiantes principiantes.
