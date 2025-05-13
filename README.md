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

**RESPUESTA:**
La red 172.16.0.0 tiene una máscara de subred /24, lo que significa que tenemos 24 bits para la parte de red y 8 bits para la parte de host. Esto nos da un total de $2^8 - 2 = 254$ hosts utilizables.
-----------------------------------------------
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
