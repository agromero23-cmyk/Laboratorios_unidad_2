# Actividad 1 — Identificar la superficie de ataque

## 1. Información del servidor

- Versión de PostgreSQL:
- Puerto:
- Interfaces de escucha:
- SSL:
- Método de almacenamiento de contraseñas:

## 2. Conexiones activas

Describe las conexiones que aparecen en el resultado de `pg_stat_activity`.

## 3. Análisis de seguridad

- **Puerto PostgreSQL:** indicar si es necesario para el funcionamiento del servicio y qué riesgo representa si queda expuesto sin controles.
- **Interfaces de escucha:** explicar en qué interfaces acepta conexiones el servidor.
- **Conexiones remotas:** indicar si aparecen conexiones remotas y si puedes determinar que son legítimas.
- **Usuarios administrativos:** identificar las cuentas administrativas que puedas verificar.
- **SSL/TLS:** registrar el estado que devuelve PostgreSQL.
- **Autenticación:** registrar el método de almacenamiento de contraseñas y señalar que las reglas de autenticación se revisarán en la Actividad 4.

## 4. Pregunta

**¿Por qué conocer la superficie de ataque debe preceder al hardening?**

Primero es necesario identificar los servicios, puertos, conexiones, usuarios y configuraciones que pueden representar riesgos. Con esa información se pueden detectar exposiciones innecesarias y elegir medidas de seguridad apropiadas sin afectar las conexiones legítimas.