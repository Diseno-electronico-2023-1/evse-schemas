# evse-schemas

Cada grupo crea una rama para su PCB, cuando acaben hacen merge a la rama

Para crear una rama:

git checkout -b branch-name

Donde branch-name es el nombre de la rama Ej: Potencia

Una vez que estan en la nueva rama pueden subir sus cambios con:

git add .

git commit -m "Descripción de sus cambios"

git push -u origin branch-name

## Table of Contents
- [Conector](#conector)


## CONECTOR
### Pruebas
#### Tension
Para esta prueba se realiza un montaje en paralelo entre una linea y neutro del conector con una fuente de tensión en AC, Como se observa en el siguiente montaje.

<p align="center">
  <img width="460" height="300" src="https://github.com/Diseno-electronico-2023-1/evse-schemas/blob/Conector/Conector/Images_LABE/Tension/montajevoltaje.png">
  <img width="460" height="300" src="https://github.com/Diseno-electronico-2023-1/evse-schemas/blob/Conector/Conector/Images_LABE/Tension/montajevoltaje2.png">
</p>

Se realiza la respectiva verificación de la tensión a la que estará expuesto el conector y se realizan distintas pruebas con diferentes valores de voltaje obteniendo los siguientes resultados.

<p align="center">
  <img width="460" height="300" src="https://github.com/Diseno-electronico-2023-1/evse-schemas/blob/Conector/Conector/Images_LABE/Tension/00.png">
  <img width="460" height="300" src="https://github.com/Diseno-electronico-2023-1/evse-schemas/blob/Conector/Conector/Images_LABE/Tension/01.png">
</p>

<p align="center">
  <img width="460" height="300" src="https://github.com/Diseno-electronico-2023-1/evse-schemas/blob/Conector/Conector/Images_LABE/Tension/02.png">
  <img width="460" height="300" src="https://github.com/Diseno-electronico-2023-1/evse-schemas/blob/Conector/Conector/Images_LABE/Tension/03.png">
</p>

#### Corriente
En esta prueba se conecto en serie una fuente de corriente como se muestra en la siguiente figura.

<p align="center">
  <img width="460" height="300" src="https://github.com/Diseno-electronico-2023-1/evse-schemas/blob/Conector/Conector/Images_LABE/Corriente/montajecorriente.png">
</p>

Se inicio la medicion con 5 A y posteriormente se aumento a los 15 A que están propuestos para el cargador y con la ayuda de una pinza amperimétrica y un osciloscopio se observaron las corrientes suministradas en una escala de 10mV por cada amperio.

<p align="center">
  <img width="460" height="300" src="https://github.com/Diseno-electronico-2023-1/evse-schemas/blob/Conector/Conector/Images_LABE/Corriente/07.png">
  <img width="460" height="300" src="https://github.com/Diseno-electronico-2023-1/evse-schemas/blob/Conector/Conector/Images_LABE/Corriente/08.png">
</p>

<p align="center">
  <img width="460" height="300" src="https://github.com/Diseno-electronico-2023-1/evse-schemas/blob/Conector/Conector/Images_LABE/Corriente/09.png">
  <img width="460" height="300" src="https://github.com/Diseno-electronico-2023-1/evse-schemas/blob/Conector/Conector/Images_LABE/Corriente/10.png">
</p>

#### Aislamiento
Para determinar la resistencia de aislamiento del conector se utiliza un medidor de resistencia de aislamiento, con los cables aislados entre si se conectan a una linea y al neutro del conector como se observa el montaje en la siguiente figura. La resistencia obtenida fue de 319 Gohm. 

<p align="center">
  <img width="460" height="300" src="https://github.com/Diseno-electronico-2023-1/evse-schemas/blob/Conector/Conector/Images_LABE/Aislamiento/montajeaislamiento.png">
</p>

Comparando este valor con el dado comercialmente se obtiene una resistencia considerablemente mayor a la descrita en el manual.

<div align="center">

Votaje [RMS]  | Corriente [A] | Aislamiento [Gomh]
------------- | ------------- | -------------
121  | 5  | 319
383  | 15 
447  | 16
</div>

<p align="center">
  <img width="460" height="300" src="https://github.com/Diseno-electronico-2023-1/evse-schemas/blob/Conector/Conector/Images_LABE/Aislamiento/Untitled.png">
</p>

## CONTROL PILOT
El circuito piloto de control es el principal medio de control para garantizar un funcionamiento correcto al conectar un EV/PHEV al EVSE. La señal piloto es el método clave a través del cual un EVSE compatible con J1772 se comunica con un vehículo. La señal piloto se basa en una señal PWM de ±12 V y 1 kHz que se transmite a un vehículo a través del cable de carga. El vehículo puede entonces responder colocando diversas cargas en la línea, afectando a su tensión, que mide el EVSE.
Esta seccion esta basado en la plantilla [Conector](https://github.com/Diseno-electronico-2023-1/evse-schemas/tree/Conector/Conector "Conector")

Comienzan las funciones del piloto de control (CP)

- El equipo de alimentación detecta el vehículo eléctrico enchufable (PEV)
- El equipo de suministro indica al PEV que está preparado para suministrar corriente
- Se determinan las necesidades de ventilación del PEV
- el equipo de alimentación suministra corriente al PEV
- El PEV ordena el flujo de energía
- El PEV y el equipo de alimentación supervisan continuamente la continuidad de la toma de tierra de seguridad
- La carga continúa según lo determinado por el PEV
- La carga puede interrumpirse desconectando el enchufe del vehículo

### Control Pilot - simulación
Este apartado tiene como carpeta principal [Simulación](https://github.com/Diseno-electronico-2023-1/evse-schemas/tree/Conector/Conector/Simulacion)

#### Table SAE J1772 - PILOT SIGNAL
<div align="center">
                    
Designación del estado del vehículo  |Voltaje (VDC nominal) | Descripción del estado del vehículo
------------- | ------------- | -------------
Estado A  | 12 | Vehículo no conectado
Estado B  | 9 | Vehículo conectado / no está listo para aceptar energía
Estado C  | 6 | Vehículo conectado / listo para aceptar energía / no se requiere ventilación en el área de carga interna
Estado D  | 3 | Vehículo conectado / listo para aceptar energía /requiere ventilación en el área de carga interna
Estado E  | 0 | EVSE desconectado, poder de utilidad no disponible, u otro problema de EVSE
Estado F  | -12 | EVSE no disponible, u otro problema de EVSE
</div>

1. El EVSE pone 12V en el cable piloto. Esta transmisión señala al vehículo cuando el enchufe está conectado.
2. Cuando se conecta el enchufe, el vehículo coloca una carga de 2,74 kΩ en la línea piloto, lo que disminuye la tensión a 9 V.
3. La EVSE pasa al estado B, donde activa el PWM, que indica al vehículo cuánta corriente puede consumir. El EVSE también cierra los relés, proporcionando energía al vehículo.
4. El vehículo comienza a consumir energía y cambia a la carga de 822-Ω, que baja la tensión a 6 V, señalando al EVSE que la carga ha comenzado.
5. La mayoría de los vehículos siguen consumiendo pequeñas cantidades de energía en el estado C, incluso cuando están completamente cargados, por lo que el proceso de carga finaliza desenchufando el cable, lo que devuelve la tensión a 12 V. El EVSE mide este proceso y cierra los relés y vuelve al estado A.

<p align="center">
  <img width="460" height="300" src="https://github.com/Diseno-electronico-2023-1/evse-schemas/blob/Conector/Conector/Simulacion/images/schematic.png">
</p>

<p align="center">
  <img width="460" height="300" src="https://github.com/Diseno-electronico-2023-1/evse-schemas/blob/Conector/Conector/Simulacion/images/simulation.png">
</p>

#### J1772 Ciclo de trabajo

El ciclo de trabajo de las señales piloto comunica el límite de corriente que el EVSE es capaz de suministrar al vehículo; el vehículo puede entonces utilizar hasta esa cantidad de corriente para su circuito de carga. Este límite de corriente viene determinada principalmente por los componentes electromecánicos de la EVSE, como conductores, relés contactores y la conexión de servicio. La relación entre el ciclo de trabajo y la corriente se define mediante dos ecuaciones diferentes en función del rango de corriente especificado.

Rango de corriente especificado; para un servicio de 6 a 51 A, es:
Duty Cycle = Amps / 0.6

<div align="center">

AMPS  | DUTY CYCLE
------------- | -------------
5  | 8.3%
15  | 25% 
30  | 50%
40  | 66.6%
65  | 90%
80  | 96%
</div>

### Control Pilot - PCB
Esta subseccion esta basado en la plantilla [PCB](https://github.com/Diseno-electronico-2023-1/evse-schemas/tree/Conector/Conector/ControlPilotPCB-backups)

<p align="center">
  <img align="left" width="460" height="600" src="https://github.com/Diseno-electronico-2023-1/evse-schemas/blob/Conector/Conector/pcb/images/schematic.png">
  <p align="center">
    <img align="right" width="460" height="300" src="https://github.com/Diseno-electronico-2023-1/evse-schemas/blob/Conector/Conector/pcb/images/routing.png">
    <img align="right" width="460" height="300" src="https://github.com/Diseno-electronico-2023-1/evse-schemas/blob/Conector/Conector/pcb/images/pcb2.png">
  </p>
</p>



