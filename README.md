# ExamenFinalRedes
https://github.com/Jyejii/ExamenFinalRedes.git
# PARTE 1
## MISION 1- Direccionamiento IP y Subredes

**Objetivo de la misión:** Diseña un plan de direccionamiento IP para la Base Eco utilizando subnetting. Parte de una red asignada (por ejemplo, 172.16.0.0/24) y subdivide en subredes adecuadas para cada departamento, cumpliendo estos requisitos (ficticios):

- **Comando Central:** ~50 hosts (dispositivos)
- **Defensa Perimetral:** ~30 hosts
- **Centro Médico:** ~20 hosts
- **Hangar y Taller:** ~14 hosts

Además, reserva una subred adicional para el **enlace troncal** con la antena de comunicaciones que conecta Hoth con el resto de la galaxia. Debes detallar la **dirección de red**, **máscara** y **rango de hosts** de cada subred resultante.

**Pregunta:** ¿Cómo dividirías la red `172.16.0.0/24` en subredes para satisfacer las necesidades anteriores, asignando direcciones IP a cada segmento de la base? Indica las subredes obtenidas (con su notación de máscara `/xx`), la cantidad de hosts útiles en cada una, y especifica qué subred se destinaría al enlace troncal interplanetario.

----------------------------------------------------------
**RESPUESTA:**
<p>La red 172.16.0.0 tiene una máscara de subred /24, lo que significa que tenemos 24 bits para la parte de red y 8 bits para la parte de host. Esto nos da un total de $2^8 - 2 = 254$ hosts utilizables.</p>

**Red Asignada**

| Red Base          | 172.16.0.0/24 |
|-------------------|---------------|
| Total de direcciones | 256           |
| Direcciones utilizables | 254           |

**1. Comando Central**

| Subred             | 172.16.0.0/26      |
|--------------------|--------------------|
| Máscara            | 255.255.255.192    |
| Hosts útiles       | 62                 |
| Rango de hosts     | 172.16.0.1 – 172.16.0.62 |
| Dirección de broadcast | 172.16.0.63      |

**2. Defensa Perimetral**

| Subred             | 172.16.0.64/27      |
|--------------------|--------------------|
| Máscara            | 255.255.255.224    |
| Hosts útiles       | 30                 |
| Rango de hosts     | 172.16.0.65 – 172.16.0.94 |
| Dirección de broadcast | 172.16.0.95      |

**3. Centro Médico**

| Subred             | 172.16.0.96/27      |
|--------------------|--------------------|
| Máscara            | 255.255.255.224    |
| Hosts útiles       | 30                 |
| Rango de hosts     | 172.16.0.97 – 172.16.0.126 |
| Dirección de broadcast | 172.16.0.127     |

**4. Hangar y Taller**

| Subred             | 172.16.0.128/28     |
|--------------------|--------------------|
| Máscara            | 255.255.255.240    |
| Hosts útiles       | 14                 |
| Rango de hosts     | 172.16.0.129 – 172.16.0.142 |
| Dirección de broadcast | 172.16.0.143     |

**5. Enlace Troncal (Antena de Comunicaciones)**

| Subred             | 172.16.0.144/30     |
|--------------------|--------------------|
| Máscara            | 255.255.255.252    |
| Hosts útiles       | 2                  |
| Rango de hosts     | 172.16.0.145 – 172.16.0.146 |
| Dirección de broadcast | 172.16.0.147     |

---------------------------------------------------------
# Misión 2: Sabiduría de Yoda – Algoritmos de Enrutamiento y Rutas

**Situación:** Completando tu entrenamiento en Dagobah, el Maestro Yoda evalúa tu comprensión de cómo circula la información por la galaxia. Las rutas que toman los paquetes a través de los nodos de la HoloRed pueden establecerse de distintas formas: estáticas o dinámicas, simples o inteligentes. Yoda quiere saber si distingues la filosofía detrás de los algoritmos de enrutamiento clave.

**Narrativa:** En la neblina de los pantanos de Dagobah, Yoda cierra los ojos y enuncia en su peculiar forma: *"En tus redes, joven padawan, dos caminos existen para los datos: uno fijo y otro en movimiento constante. El primero, estático es – manual, control total brinda; el segundo, dinámico – se adapta y vive la red. Grandes diferencias hay... ¿Comprenderlas tú las puedes?"*

A su lado, luces parpadeantes de un viejo router imperial recuperado iluminan tu rostro. Debes explicarle a Yoda las diferencias que percibes en la Fuerza… de la red.

**Pregunta:** Compara el enrutamiento estático con el enrutamiento dinámico. ¿Cuáles son las **ventajas e inconvenientes** de cada enfoque en la administración de rutas? En tu respuesta, menciona al menos un protocolo de enrutamiento dinámico (por ejemplo, RIP u OSPF) y comenta por qué los **protocolos de vector de distancia** difieren de los de **estado de enlace** en términos de rendimiento y complejidad.

------------------------------

**RESPUESTA:**

## Comparación: Enrutamiento Estático y Enrutamiento Dinámico

| Característica           | Enrutamiento Estático             | Enrutamiento Dinámico             |
|--------------------------|-----------------------------------|-----------------------------------|
| **Configuración** | Manual, ingresada por el administrador. | Automática, basada en algoritmos de enrutamiento. |
| **Adaptabilidad** | No se adapta a cambios en la red. | Se ajusta automáticamente ante fallos o cambios. |
| **Complejidad** | Baja complejidad, fácil de implementar. | Mayor complejidad, requiere más recursos. |
| **Consumo de CPU y ancho de banda** | Mínimo, no hay intercambio de información. | Mayor, debido a la comunicación entre routers. |
| **Escalabilidad** | Limitada a redes pequeñas o estables. | Escalable para redes grandes y en constante cambio. |
| **Seguridad** | Más segura, ya que no intercambia rutas. | Menos segura si no se aplican políticas de control. |

**Ejemplo de Enrutamiento Dinámico: OSPF.**
- OSPF (Open Shortest Path First) es un protocolo de enrutamiento dinámico de estado de enlace.
- Calcula las rutas más eficientes usando el algoritmo de Dijkstra.
- Cada router tiene conocimiento completo de la topología de la red y actualiza su tabla de enrutamiento en función de los cambios detectados.

## Diferencias entre Protocolos de Vector de Distancia y Estado de Enlace:

**Protocolos de Vector de Distancia (ej. RIP):**

- Cada router informa a sus vecinos sobre las rutas que conoce.
- Las decisiones de enrutamiento se basan en la distancia (número de saltos).
- Son más simples pero menos eficientes y lentos en converger.
- Riesgo de bucles si no se implementan técnicas como "split horizon" o "count to infinity".

**Protocolos de Estado de Enlace (ej. OSPF):**

- Cada router construye un mapa completo de la red.
- Las rutas se calculan localmente con algoritmos más avanzados.
- Son más rápidos y precisos al reaccionar ante cambios.
- Requieren más memoria y CPU, por lo que son más complejos de implementar.

  Podemos concluir que con el enrutamiento dinámico se obtiene un control obsoluto de la red, por lo que va bien en redes pequeñas.Sin embargo en redes mas grandes es necesario usar el enrutamiento dinámico como el OSPF, ya que sino seria imposible de manejar.
  
  ------------------------
  # Misión 3: Los Nombres del Holonet – DNS y Resolución de Nombres

**Situación:** La flota rebelde ha interceptado transmisiones imperiales que mencionan distintos **códigos de planeta** y nombres en clave. Para coordinar un contraataque, la Alianza necesita entender cómo los nombres de dominio galácticos se traducen en localizaciones reales. En otras palabras, requieren restablecer un servicio **DNS** rebelde que asocie nombres de sistemas estelares con direcciones de la red. Sin DNS, comunicarse es tan difícil como encontrar un Ewok en la noche de Endor.

**Narrativa:** A bordo de la nave de mando *Home One*, los técnicos rebelde te muestran un panel donde parpadea la petición “Unknown host”. El Almirante Ackbar frunce el ceño mientras exclama: *"¡Es una trampa... de nombres! Nuestros sistemas no reconocen las direcciones de destino."* Mon Mothma asiente con gravedad: *"Debemos reconstruir nuestro directorio de comunicaciones. Aprendiz, ¿cómo funciona este **Sistema de Nombres de Dominio** nuestro? ¿Por qué es tan importante?"*

Tú recuerdas tus lecciones sobre cómo en la Red (o la HoloRed) se gestionan las direcciones simbólicas. Un nombre como “echo.base” debe traducirse a una dirección IP para establecer conexión. Ha llegado el momento de explicarlo claramente.

**Pregunta:** Explica el funcionamiento básico del sistema DNS y su importancia en la comunicación en redes. ¿Cómo realiza la red rebelde (o cualquier red TCP/IP) la **resolución de nombres de dominio** a direcciones IP? Incluye en tu explicación qué es un **servidor DNS** y un **registro** (por ejemplo, un registro A), ilustrando con un ejemplo simple (por ejemplo: traducir `holonet.rebelion.org` a una dirección IP).

-------------

**RESPUESTA:**

## ¿Qué es y cómo funciona el sistema DNS?

El sistema DNS básicamente es un sistema jerárquico y distribuido que traduce nombres de dominios como `dns.google` a la IP `8.8.8.8`. Sin este sistema, tendríamos que saber cada IP de las páginas a las que queremos acceder.

Su funcionamiento ocurre de la siguiente manera, por ejemplo, cuando alguien quiere conectarse a `www.youtube.com`:

Cuando un dispositivo rebelde (por ejemplo, una terminal en la Base Eco) quiere conectarse a `holonet.rebelion.org`, se sigue el siguiente proceso:

1.  **Consulta local:** El sistema primero revisa su caché DNS local o su archivo `hosts`.
2.  **Petición al Servidor DNS:** Si no encuentra la respuesta localmente, la terminal pregunta a un servidor DNS configurado (por ejemplo, el DNS principal rebelde).
3.  **Resolución recursiva:**
    - El servidor DNS recorre la jerarquía del dominio:
        - Pregunta a los servidores raíz (`.`)
        - Luego al servidor de `.org`
        - Después al servidor de `rebelion.org`
4.  **Respuesta:** Finalmente, obtiene la dirección IP correspondiente, como `192.0.2.42`.
5.  **Conexión:** La terminal puede ahora establecer conexión directa con el servidor de destino.

## Ejemplo: Resolviendo un nombre rebelde

 Nombre de dominio  `holonet.rebelion.org` 
 **Resultado:** 
  
  - Registro A   `holonet.rebelion.org = 192.0.2.42` <br>
-El registro A (Address) vincula un nombre de dominio con una dirección IPv4. 

## ¿Qué ocurre si el DNS falla?

Si el DNS falla, aunque las redes estén comunicadas físicamente, no se podrían conectar, ya que no encontrarían las direcciones correspondientes a los nombres de dominio. La comunicación se volvería extremadamente difícil, tal como encontrar un Ewok en la noche de Endor.
