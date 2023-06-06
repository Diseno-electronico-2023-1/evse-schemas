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

![montajevoltaje](https://github.com/Diseno-electronico-2023-1/evse-schemas/assets/126024376/e3151760-9257-4b66-8d34-9814eae60585)

![montajevoltaje2](https://github.com/Diseno-electronico-2023-1/evse-schemas/assets/126024376/ee67c2b6-122b-4c2d-aa93-b73e22e80ddb)

Se realiza la respectiva verificación de la tensión a la que estará expuesto el conector y se realizan distintas pruebas con diferentes valores de voltaje obteniendo los siguientes resultados.

![00](https://github.com/Diseno-electronico-2023-1/evse-schemas/assets/126024376/19d34b16-3f0d-4fbd-95ec-39776bd8a159)

![01](https://github.com/Diseno-electronico-2023-1/evse-schemas/assets/126024376/4b1a411e-3756-4d08-9663-e1f2a84d182b)

![02](https://github.com/Diseno-electronico-2023-1/evse-schemas/assets/126024376/5418677a-0e67-45c0-8245-8e3b8161a9d3)

![03](https://github.com/Diseno-electronico-2023-1/evse-schemas/assets/126024376/7204324c-56df-45b2-b15f-c6053519bb1a)

#### Corriente
En esta prueba se conecto en serie una fuente de corriente como se muestra en la siguiente figura.

![montajecorriente](https://github.com/Diseno-electronico-2023-1/evse-schemas/assets/126024376/5b951a4b-343f-4e9a-9b92-4de6fb1cd54c)

Se inicio la medicion con 5 A y posteriormente se aumento a los 15 A que están propuestos para el cargador y con la ayuda de una pinza amperimétrica y un osciloscopio se observaron las corrientes suministradas en una escala de 10mV por cada amperio.

![07](https://github.com/Diseno-electronico-2023-1/evse-schemas/assets/126024376/79ba6fec-0cb1-4b4f-b1c7-8f7ceb47fc50)

![08](https://github.com/Diseno-electronico-2023-1/evse-schemas/assets/126024376/22e601b4-d1d8-4573-81c5-c534f9afcd81)

#### Aislamiento
Para determinar la resistencia de aislamiento del conector se utiliza un medidor de resistencia de aislamiento, con los cables aislados entre si se conectan a una linea y al neutro del conector como se observa el montaje en la siguiente figura. La resistencia obtenida fue de 319 Gohm. 

![montajeaislamiento](https://github.com/Diseno-electronico-2023-1/evse-schemas/assets/126024376/ed20d8f2-1d77-4b19-a47e-3a304317ba95)

Comparando este valor con el dado comercialmente se obtiene una resistencia considerablemente mayor a la descrita en el manual.

Votaje [RMS]  | Corriente [A] | Aislamiento [Gomh]
------------- | ------------- | -------------
121  | 5  | 319
383  | 15 
447  | 16

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
                    
Designación del estado del vehículo  |Voltaje (VDC nominal) | Descripción del estado del vehículo
------------- | ------------- | -------------
Estado A  | 12 | Vehículo no conectado
Estado B  | 9 | Vehículo conectado / no está listo para aceptar energía
Estado C  | 6 | Vehículo conectado / listo para aceptar energía / no se requiere ventilación en el área de carga interna
Estado D  | 3 | Vehículo conectado / listo para aceptar energía /requiere ventilación en el área de carga interna
Estado E  | 0 | EVSE desconectado, poder de utilidad no disponible, u otro problema de EVSE
Estado F  | -12 | EVSE no disponible, u otro problema de EVSE

1. El EVSE pone 12V en el cable piloto. Esta transmisión señala al vehículo cuando el enchufe está conectado.
2. Cuando se conecta el enchufe, el vehículo coloca una carga de 2,74 kΩ en la línea piloto, lo que disminuye la tensión a 9 V.
3. La EVSE pasa al estado B, donde activa el PWM, que indica al vehículo cuánta corriente puede consumir. El EVSE también cierra los relés, proporcionando energía al vehículo.
4. El vehículo comienza a consumir energía y cambia a la carga de 822-Ω, que baja la tensión a 6 V, señalando al EVSE que la carga ha comenzado.
5. La mayoría de los vehículos siguen consumiendo pequeñas cantidades de energía en el estado C, incluso cuando están completamente cargados, por lo que el proceso de carga finaliza desenchufando el cable, lo que devuelve la tensión a 12 V. El EVSE mide este proceso y cierra los relés y vuelve al estado A.

![schematic](https://github.com/Diseno-electronico-2023-1/evse-schemas/assets/126024376/2b02a925-df56-40a1-965b-ab35b09d1547)

![simulation](https://github.com/Diseno-electronico-2023-1/evse-schemas/assets/126024376/deecbd8a-70e5-406f-ac1c-a4d636f5dd03)

#### J1772 Ciclo de trabajo

El ciclo de trabajo de las señales piloto comunica el límite de corriente que el EVSE es capaz de suministrar al vehículo; el vehículo puede entonces utilizar hasta esa cantidad de corriente para su circuito de carga. Este límite de corriente viene determinada principalmente por los componentes electromecánicos de la EVSE, como conductores, relés contactores y la conexión de servicio. La relación entre el ciclo de trabajo y la corriente se define mediante dos ecuaciones diferentes en función del rango de corriente especificado.

Rango de corriente especificado; para un servicio de 6 a 51 A, es:
Duty Cycle = Amps / 0.6

AMPS  | DUTY CYCLE
------------- | -------------
5  | 8.3%
15  | 25% 
30  | 50%
40  | 66.6%
65  | 90%
80  | 96%

### Control Pilot - PCB
Esta subseccion esta basado en la plantilla [PCB](https://github.com/Diseno-electronico-2023-1/evse-schemas/tree/Conector/Conector/ControlPilotPCB-backups)

![pcb2](https://github.com/Diseno-electronico-2023-1/evse-schemas/assets/126024376/388b68eb-7794-44ec-ab23-544f392cd22e)

![pcb1](https://github.com/Diseno-electronico-2023-1/evse-schemas/assets/126024376/5aead935-cc50-4a8b-9edb-77d0d74f67f4)

![routing](https://github.com/Diseno-electronico-2023-1/evse-schemas/assets/126024376/bb78755c-777a-4983-a05c-2d47f261344c)

![schematic](https://github.com/Diseno-electronico-2023-1/evse-schemas/assets/126024376/1d457d81-68a7-4640-a62b-dd5cba44fd54)



