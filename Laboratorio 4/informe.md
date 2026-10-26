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

# Actividad 2 — Identificar los archivos de configuración

## Objetivo

Identificar las rutas de los principales archivos y directorios de
configuración de PostgreSQL.

## Resultados

| Parámetro | Resultado |
|---|---|
| config_file | |
| hba_file | |
| ident_file | |
| data_directory | |
| log_directory | |
| log_connections | |
| log_disconnections | |

## Análisis

### 1. ¿Por qué es importante conocer la ubicación de estos archivos?

Es importante conocer las rutas para localizar la configuración de
PostgreSQL, revisar sus permisos y asegurarse de modificar los archivos
correctos cuando sea necesario.

### 2. ¿Qué archivo controla las reglas de acceso?

El archivo pg_hba.conf contiene las reglas que determinan qué conexiones
pueden autenticarse, para qué bases de datos, con qué usuarios y mediante
qué métodos de autenticación.

### 3. ¿Por qué deben protegerse los archivos de configuración?

Porque una modificación no autorizada podría debilitar la seguridad,
permitir accesos indebidos o afectar el funcionamiento del servidor.

## Conclusión

Completar después de ejecutar las consultas y analizar los resultados.


# Actividad 3 — Revisar listen_addresses

## Objetivo

Identificar las interfaces de red en las que PostgreSQL acepta conexiones y evaluar si su configuración puede representar un riesgo de seguridad.

## Resultado obtenido

- Parámetro: `listen_addresses`
- Valor encontrado: (completar con el resultado de pgAdmin)

## Análisis

### 1. Configuración encontrada

(Escribir el valor que devolvió PostgreSQL).

### 2. Interfaces necesarias

Las interfaces necesarias son aquellas que utilizan las aplicaciones y los usuarios autorizados para conectarse a PostgreSQL.

### 3. Interfaces innecesarias

Se consideran innecesarias las interfaces que permiten conexiones que no forman parte de los requerimientos del sistema.

### 4. ¿Qué arquitectura reduce mejor la exposición?

La arquitectura que mantiene PostgreSQL dentro de una red privada y limita el acceso mediante un firewall reduce mejor la exposición. De esta manera, se evita que el servicio quede directamente accesible desde Internet.

