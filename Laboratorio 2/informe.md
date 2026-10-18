# 7. Actividad 1 — Protección de credenciales

## 7.1 El problema

### ¿Qué ocurriría si una persona obtiene acceso de lectura a esta tabla?

Si una persona obtiene acceso de lectura a la tabla `usuarios_insegura`, podría ver los nombres de usuario y sus contraseñas en texto plano.

Esto representa un riesgo de seguridad, porque podría utilizar las contraseñas para entrar a las cuentas de los usuarios sin autorización. Si una persona utiliza la misma contraseña en otros sistemas, esas cuentas también podrían verse afectadas.

Para evitar este problema, las contraseñas no deben almacenarse directamente en la base de datos. Se deben proteger mediante algoritmos de hash seguros, como Argon2id o bcrypt.

# 7.3 Generar una representación no reversible

## Preguntas y respuestas

### 1. ¿Son iguales?

No, los resultados son diferentes, aunque se utilice la misma contraseña (`Password123`).

### 2. Si no son iguales, ¿por qué?

Porque la función `gen_salt()` genera una sal aleatoria cada vez que se ejecuta. Esta sal se utiliza para calcular el hash, por lo que una misma contraseña puede producir resultados diferentes.

### 3. ¿Qué función cumple `gen_salt()`?

La función `gen_salt()` genera una sal aleatoria que se utiliza en el proceso de hash. Esto ayuda a evitar que contraseñas iguales produzcan siempre el mismo resultado.

### 4. ¿Qué función cumple `crypt()`?

La función `crypt()` genera un hash de la contraseña utilizando el algoritmo y la sal proporcionados. En este ejemplo, `gen_salt('bf')` utiliza Blowfish para generar la sal y calcular el hash.

### 5. ¿Esto es cifrado reversible?

No. Es un proceso de hash que no permite recuperar directamente la contraseña original a partir del resultado. Para verificar una contraseña, se utiliza el hash almacenado y se comprueba si coincide con la contraseña ingresada.

# 7.5 Verificar una contraseña

## Preguntas y respuestas

### 1. ¿Qué resultado obtuviste con la contraseña correcta?

El resultado fue `true`, porque la contraseña ingresada (`Password123`) coincide con el hash almacenado en la base de datos.

### 2. ¿Qué resultado obtuviste con la contraseña incorrecta?

El resultado fue `false`, porque la contraseña ingresada (`OtraPassword`) no coincide con el hash almacenado.

### 3. ¿Por qué no es necesario recuperar la contraseña original?

Porque el sistema puede comprobar si la contraseña ingresada es correcta comparando su hash con el que está guardado en la base de datos. De esta manera, no necesita conocer ni recuperar la contraseña original.

### 4. ¿Por qué un hash no debe confundirse con cifrado?

Porque el hash es una representación diseñada para no recuperar directamente la información original, mientras que el cifrado permite recuperar los datos originales mediante una clave. Por eso, las contraseñas deben almacenarse como hashes seguros y no como texto plano.

# 8. Actividad 2 — Cifrado de información sensible

## 8.1 Crear una tabla de demostración

## 8.2 Recuperar el dato

### Preguntas y respuestas

### 1. ¿Qué diferencia existe entre `crypt()` y `pgp_sym_encrypt()`?

La función `crypt()` se utiliza para generar un hash de una contraseña, mientras que `pgp_sym_encrypt()` cifra información utilizando una clave secreta. El hash no permite recuperar directamente el dato original, pero el cifrado sí permite recuperarlo con la clave correcta.

### 2. ¿Cuál de los dos mecanismos permite recuperar el dato original?

`pgp_sym_encrypt()` permite recuperar el dato original mediante la función `pgp_sym_decrypt()` y utilizando la misma clave secreta con la que se cifró.

### 3. ¿Qué ocurre si se utiliza una clave incorrecta?

Si se utiliza una clave incorrecta, la función `pgp_sym_decrypt()` no podrá recuperar correctamente el dato original y PostgreSQL normalmente generará un error de descifrado.

### 4. ¿Qué problema de seguridad representa colocar la clave directamente en una consulta?

Colocar la clave directamente en una consulta representa un riesgo porque puede quedar expuesta en el historial de consultas, registros del sistema o capturas de pantalla. Si una persona obtiene la clave, podría descifrar la información protegida. Por eso, es importante almacenar y administrar las claves de forma segura, evitando escribirlas directamente en el código.

# 9. Actividad 3 — El problema de la gestión de claves

## 9.1 Identificar una mala práctica

### Pregunta

**¿Qué ocurriría si esta clave fuera una clave utilizada realmente por una organización y el archivo se publicara en un repositorio Git?**

Si el archivo se publicara en un repositorio Git, una persona que tuviera acceso al código podría obtener la clave y utilizarla para descifrar información sensible, como los RFC de los clientes. Esto representaría un riesgo para la privacidad y la seguridad de la organización.

Aunque el archivo se elimine después, la clave podría permanecer en el historial de Git y seguir expuesta.

## 9.2 Regla del laboratorio

No se deben almacenar claves, contraseñas, tokens ni secretos reales en un repositorio. Para esta práctica se utilizan valores ficticios con fines demostrativos.

El archivo `sql/ejemplo-mala-practica.sql` debe eliminarse antes de realizar la entrega final.
