# Modelado de Arquitecturas de Software (C4 + UML)
## Contexto del caso
La universidad quiere rediseñar su sistema de gestión de inscripciones y pagos en línea. Actualmente es un sistema monolítico que presenta problemas de escalabilidad, disponibilidad y mantenibilidad. Se requiere evolucionarlo a una arquitectura SaaS escalable, con microservicios y microfrontends.


## Objetivo del proyecto

- Modernizar la plataforma de gestión académica. 
- Garantizar seguridad, disponibilidad, escalabilidad y mantenibilidad.
- Implementar pagos en línea, inscripciones y gestión de usuarios bajo una arquitectura flexible.



## Requerimientos

### 1. Requerimientos Funcionales

- Pasarela de pagos segura.
- Microfrontends personalizados según rol (estudiante, docente, administrador).
- Inscripción en línea con validación de prerrequisitos y generación de comprobantes.
- Gestión de usuarios con autenticación, recuperación de contraseñas y administración de roles.

### 2. Requerimientos No Funcionales

- **Seguridad**: Cifrado de datos sensibles.
- **Escalabilidad**: Capacidad para miles de usuarios y transacciones.
- **Baja latencia** en transmisión en tiempo real.

### 3. Atributos de Calidad

- Escalabilidad.
- Seguridad.
- Disponibilidad 24/7.
- Mantenibilidad (modularidad, documentación, pruebas continuas).


## Decisiones Arquitectónicas
### 1. **Arquitectura: Microservicios vs Monolito**

- **Monolito**:
    
    - Ventaja inicial: simplicidad en la construcción.
    - Problema: se convierte en un cuello de botella al crecer, generando complejidad para mantenerlo y escalarlo.
    
- **Microservicios**:
    
    - Cada módulo es independiente (ej: pagos, inscripción, notificaciones).
    - Escalan de manera autónoma según la demanda.
    - Favorecen la mantenibilidad al permitir actualizaciones o correcciones sin afectar al resto.

- **Decisión**: Se eligen **microservicios**, porque garantizan escalabilidad, disponibilidad y facilidad de evolución a largo plazo.


### 2. **Seguridad y Autenticación: OAuth 2 vs JWT**

- **OAuth 2**:
    - Es un marco de autorización que permite a los usuarios acceder a recursos sin exponer sus credenciales.
    - Define flujos de obtención de tokens con permisos limitados.
        
- **JWT (JSON Web Token)**:
    - Es el formato del token que transporta de forma segura la información de autenticación (claims).
    - Se integra perfectamente con OAuth 2 como contenedor seguro de datos.
        
- **Decisión**: Usar **OAuth 2 como protocolo de autorización** y JWT como formato de token.
    - OAuth gestiona el acceso y los permisos.
    - JWT asegura la portabilidad y validez de los tokens entre servicios.
    - Esta combinación refuerza la seguridad y simplifica la autenticación en microservicios.

### 3. **Base de Datos: Distribuida vs Centralizada**

- **Centralizada**:
    - Todo reside en un único servidor.
    - Limita la escalabilidad y genera cuellos de botella en consultas o transacciones intensivas.
    - Adecuada para sistemas pequeños o monolíticos, pero no para SaaS con miles de usuarios.
        
- **Distribuida**:
    - Los datos se almacenan en múltiples nodos, lo que:
        - Mejora la **disponibilidad** (el sistema sigue funcionando incluso si un nodo falla).
        - Reduce la **latencia** al acercar la información al usuario.
        - Permite procesar grandes volúmenes de manera **paralela**.
            
- **Decisión**: Se implementa una base de datos distribuida, asegurando rapidez en pagos, generación de comprobantes y disponibilidad continua en periodos de alta demanda.
