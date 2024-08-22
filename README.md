# Net_Practice

### ¿Qué es NetPractice?
NetPractice es un proyecto en el que nos introducimos en el mundo de las redes informáticas a través de ejercicios prácticos. Nos permite aprender sobre la configuración de direcciones IP, subredes, y enrutamiento, resolviendo problemas de conectividad en distintos escenarios. Es una experiencia que nos ayuda a comprender cómo funcionan las redes y nos prepara para desafíos más avanzados en el campo de la administración de redes.

### Índice
1. [Conceptos Básicos](#conceptos-básicos)
2. [Rangos Especiales de IP](#rangos-especiales-de-ip)
3. [Máscaras de Subred Especiales](#máscaras-de-subred-especiales)
4. [Switches de Red](#switches-de-red)
5. [Routers de Red](#routers-de-red)
6. [Tabla de Rutas](#tabla-de-rutas)
7. [Red de Computadoras](#red-de-computadoras)
8. [Quizás pueda interesarte!](#quizás-pueda-interesarte)
9. [Contactos 📥](#contactos-)

### Conceptos Básicos
Para este proyecto, solo utilizamos IPv4, por lo que no abordaremos IPv6.<br>
Una dirección IPv4 es un número de 32 bits dividido en 4 "bloques", cada uno de 8 bits.<br>
Por ejemplo:<br>
**192.168.100.1** se convierte en **11000000.10101000.01100100.00000001**<br>
Así, el valor mínimo de un "bloque" es **0** y el valor máximo es **255**.<br>
La misma lógica se aplica a la máscara de red:<br>
**255.255.255.0** se convierte en **11111111.11111111.11111111.00000000**<br>
Lo especial de la máscara es que, después de que un bit sea **0**, no puede haber más bits **1** a su derecha.<br>
Por lo tanto, los únicos números válidos son:

 - 255 (binario: 11111111)
 - 254 (binario: 11111110)
 - 252 (binario: 11111100)
 - 248 (binario: 11111000)
 - 240 (binario: 11110000)
 - 224 (binario: 11100000)
 - 192 (binario: 11000000)
 - 128 (binario: 10000000)
 - 0 (binario: 00000000)

Así, **255.255.255.0** ES una máscara válida,<br>
mientras que **255.255.128.128 NO** es una máscara válida.<br>
<br>
Para que sea posible enviar paquetes entre dos direcciones IP, estas deben estar en la misma red o deben estar conectadas a través de un router que forme parte de ambas subredes.

### Rangos Especiales de IP

En las redes IPv4, hay ciertos rangos de direcciones IP que tienen significados especiales y usos específicos. Aquí te explico de manera sencilla y concisa:

1. **Direcciones de Red**:
   - **Rango**: `x.x.x.0` (donde `x` es cualquier valor entre `0` y `255`).
   - **Uso**: Representa la red en sí misma. No se puede asignar a un dispositivo. Por ejemplo, `192.168.1.0` es la dirección de red para la subred `192.168.1.0/24`.

2. **Dirección de Broadcast**:
   - **Rango**: `x.x.x.255` (donde `x` es cualquier valor entre `0` y `255`).
   - **Uso**: Se utiliza para enviar mensajes a todos los dispositivos en una red específica. Por ejemplo, `192.168.1.255` envía un mensaje a todos los dispositivos en la subred `192.168.1.0/24`.

3. **Direcciones de Loopback**:
   - **Rango**: `127.0.0.0` a `127.255.255.255`.
   - **Uso**: Estas direcciones se utilizan para probar la red en la misma máquina. La dirección más común es `127.0.0.1`, conocida como `localhost`.

4. **Direcciones Privadas**:
   - **Rangos**:
     - `10.0.0.0` a `10.255.255.255`
     - `172.16.0.0` a `172.31.255.255`
     - `192.168.0.0` a `192.168.255.255`
   - **Uso**: Estas direcciones se usan en redes internas y no son enrutables por Internet. Los dispositivos dentro de una red local (LAN) pueden usar estas direcciones.

5. **Direcciones de Enlace Local**:
   - **Rango**: `169.254.0.0` a `169.254.255.255`.
   - **Uso**: Se utilizan para comunicación automática entre dispositivos en una red local cuando no hay un servidor DHCP disponible. Son direcciones autoconfiguradas (APIPA).

6. **Direcciones de Multicast**:
   - **Rango**: `224.0.0.0` a `239.255.255.255`.
   - **Uso**: Se utilizan para enviar mensajes a un grupo específico de dispositivos en una red. Son útiles para aplicaciones que necesitan enviar datos a múltiples destinatarios al mismo tiempo.


### Máscaras de Subred Especiales

Las máscaras de subred determinan qué parte de una dirección IP se utiliza para la red y qué parte se usa para los dispositivos (hosts). Aquí te explico algunos rangos y usos especiales de las máscaras de subred de manera sencilla:

1. **Máscara de Subred Completa (255.255.255.255)**:
   - **Representación Binaria**: `11111111.11111111.11111111.11111111`
   - **Uso**: Define una subred con solo una dirección IP, generalmente usada en configuraciones muy específicas o para direcciones de loopback.

2. **Máscara de Subred por Defecto**:
   - **Clase A**: `255.0.0.0` (o `/8`)
     - **Rango de Direcciones**: `10.0.0.0` a `10.255.255.255`
     - **Uso**: Para redes muy grandes, con hasta 16 millones de direcciones.
   - **Clase B**: `255.255.0.0` (o `/16`)
     - **Rango de Direcciones**: `172.16.0.0` a `172.31.255.255`
     - **Uso**: Para redes medianas, con hasta 65,000 direcciones.
   - **Clase C**: `255.255.255.0` (o `/24`)
     - **Rango de Direcciones**: `192.168.0.0` a `192.168.255.255`
     - **Uso**: Para redes pequeñas, con hasta 254 direcciones.

3. **Máscaras de Subred Personalizadas**:
   - **Máscara**: `255.255.255.128` (o `/25`)
     - **Rango de Direcciones**: `192.168.1.0` a `192.168.1.127`
     - **Uso**: Divide una red `/24` en dos subredes, cada una con 128 direcciones.
   - **Máscara**: `255.255.255.192` (o `/26`)
     - **Rango de Direcciones**: `192.168.1.0` a `192.168.1.63`
     - **Uso**: Divide una red `/24` en cuatro subredes, cada una con 64 direcciones.

4. **Máscaras de Subred Inválidas**:
   - **Ejemplo**: `255.255.128.128`
     - **Representación Binaria**: `11111111.11111111.10000000.10000000`
     - **Uso**: No es válida porque los bits `1` están seguidos por bits `0` en una posición incorrecta. Las máscaras deben tener todos los `1` seguidos por todos los `0`.

| CIDR | Dot-decimal | Number of IP-addresses<br /> per subnet | Usable IP-addresses <br /> per subnet | Number of subnets |
| :---: | :-----------: | :---: | :---: | :---: |
| /32 | 255.255.255.255 | 1 | 0 | 256 |
| /31 | 255.255.255.254 | 2 | 0 | 128 |
| /30 | 255.255.255.252 | 4 | 2 | 64 |
| /29 | 255.255.255.248 | 8 | 6 | 32 |
| /28 | 255.255.255.240 | 16 | 14 | 16 |
| /27 | 255.255.255.224 | 32 | 30 | 8 |
| /26 | 255.255.255.192 | 64 | 62 | 4 |
| /25 | 255.255.255.128 | 128 | 126 | 2 |
| /24 | 255.255.255.0 | 256 | 254 | 1 |


Las máscaras de subred son esenciales para dividir y organizar redes, permitiendo que una sola red IP se divida en subredes más pequeñas o se ajuste para necesidades específicas.

Claro, aquí tienes una explicación de los switches con un ejemplo numérico:

### Switches de Red

Un **switch** es un dispositivo de red que conecta varios dispositivos dentro de una misma red local (LAN). Aquí te explico cómo funciona con un ejemplo numérico:

- **Función Principal**: Un switch recibe datos de un dispositivo y los envía solo al dispositivo específico al que están destinados, en lugar de enviar los datos a todos los dispositivos en la red.

- **Cómo Funciona**:
  - **Recibe Datos**: Imagina que tienes tres dispositivos en la red con las siguientes direcciones IP:
    - **Dispositivo A**: `192.168.1.10`
    - **Dispositivo B**: `192.168.1.20`
    - **Dispositivo C**: `192.168.1.30`
  
    Cuando el **Dispositivo A** envía un mensaje al switch, el switch recibe el mensaje y registra que el **Dispositivo A** (`192.168.1.10`) es el remitente.

  - **Envía Datos**: Supongamos que el mensaje enviado por **Dispositivo A** está destinado a **Dispositivo B** (`192.168.1.20`). El switch consulta su tabla de direcciones y envía el mensaje solo a **Dispositivo B**, basado en la dirección IP registrada.

**Ejemplo Práctico**:
- **Dispositivo A** (`192.168.1.10`) quiere enviar un archivo a **Dispositivo B** (`192.168.1.20`).
- **Dispositivo A** envía el archivo al switch.
- El switch identifica que el archivo está destinado a **Dispositivo B** (`192.168.1.20`).
- El switch envía el archivo directamente a **Dispositivo B** y no a **Dispositivo C** (`192.168.1.30`), que no necesita recibir el archivo.


### Routers de Red

Un **router** es un dispositivo que conecta diferentes redes y dirige el tráfico de datos entre ellas. Aquí te explico cómo funciona con un ejemplo numérico:

- **Función Principal**: Un router recibe datos de una red y los envía a otra red, determinando el mejor camino para que lleguen a su destino.

- **Cómo Funciona**:
  - **Recibe Datos**: Imagina que tienes dos redes separadas:
    - **Red A**: `192.168.1.0/24`
    - **Red B**: `10.0.0.0/24`
  
    Supongamos que **Dispositivo A** en **Red A** (`192.168.1.10`) quiere enviar un mensaje a **Dispositivo B** en **Red B** (`10.0.0.20`). **Dispositivo A** envía el mensaje al router.

  - **Envía Datos**: El router recibe el mensaje y determina que debe enviarlo a **Red B**. Utiliza una tabla de enrutamiento para decidir el mejor camino para enviar el mensaje a **Dispositivo B** (`10.0.0.20`). El router dirige el mensaje a través de la red hacia su destino.

**Ejemplo Práctico**:
- **Dispositivo A** (`192.168.1.10`) está en una oficina conectada a **Red A** y necesita enviar un archivo a **Dispositivo B** (`10.0.0.20`) que está en otra oficina conectada a **Red B**.
- **Dispositivo A** envía el archivo al router.
- El router examina la dirección de destino (`10.0.0.20`) y determina que está en **Red B**.
- El router envía el archivo a través de la red hacia **Dispositivo B** en **Red B**.

¡Claro! Aquí tienes una explicación de la tabla de rutas (o tabla de enrutamiento) en routers:

### Tabla de Rutas (Tabla de Enrutamiento)

La **tabla de rutas** es una estructura de datos utilizada por los routers para determinar la mejor ruta para enviar paquetes de datos a través de una red. Cada entrada en la tabla de rutas especifica cómo llegar a una red o a una dirección IP específica.

#### Componentes de la Tabla de Rutas

1. **Destino**:
   - **Descripción**: La red o dirección IP a la que el router desea enviar los paquetes.
   - **Ejemplo**: `192.168.1.0/24` (una subred completa) o `10.0.0.20` (una dirección IP específica).

2. **Máscara de Subred**:
   - **Descripción**: Define el rango de direcciones IP que pertenecen a la red de destino.
   - **Ejemplo**: `255.255.255.0` para `192.168.1.0/24`.

3. **Puerta de Enlace (Gateway)**:
   - **Descripción**: La dirección IP del siguiente salto en la red hacia el destino.
   - **Ejemplo**: `192.168.1.1` (la dirección del router de salida para la red `192.168.1.0/24`).

4. **Interfaz**:
   - **Descripción**: La interfaz de red a través de la cual el router debe enviar los paquetes.
   - **Ejemplo**: `eth0` (una interfaz Ethernet).

5. **Métrica**:
   - **Descripción**: Un valor que indica la preferencia o costo de la ruta. Las rutas con métricas más bajas se consideran más preferibles.
   - **Ejemplo**: `10` (una métrica de costo para la ruta).

#### Ejemplo de Tabla de Rutas

| Destino       | Máscara de Subred   | Puerta de Enlace | Interfaz | Métrica |
|---------------|----------------------|------------------|----------|---------|
| `192.168.1.0` | `255.255.255.0`     | `192.168.1.1`    | `eth0`   | `10`    |
| `10.0.0.0`    | `255.255.255.0`     | `10.0.0.1`       | `eth1`   | `20`    |
| `0.0.0.0`     | `0.0.0.0`           | `192.168.1.1`    | `eth0`   | `1`     |

- **Primera Entrada**: Rutas hacia la red `192.168.1.0/24` se envían a través de la puerta de enlace `192.168.1.1` utilizando la interfaz `eth0`.
- **Segunda Entrada**: Rutas hacia la red `10.0.0.0/24` se envían a través de la puerta de enlace `10.0.0.1` utilizando la interfaz `eth1`.
- **Tercera Entrada**: `0.0.0.0/0` es una ruta por defecto, usada para enviar paquetes a redes fuera de las redes locales. En este caso, se envían a través de `192.168.1.1` usando `eth0`.

#### Cómo Funciona

Cuando un router recibe un paquete, examina la dirección IP de destino del paquete y consulta su tabla de rutas para determinar el mejor camino para enviar el paquete. El router utiliza la entrada más específica que coincide con la dirección de destino y envía el paquete a través de la puerta de enlace y la interfaz especificadas.

En resumen, la tabla de rutas ayuda a los routers a dirigir el tráfico de manera eficiente hacia su destino a través de las rutas más adecuadas.

# Quizás pueda interesarte!

### - Perfil de GitHub gmacias-
[AQUÍ](https://github.com/gjmacias)

# Contactos 📥

◦ Email gmacias-: gmacias-@student.42barcelona.com

[1]: https://www.42barcelona.com/ "42 BCN"
