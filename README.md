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


![schematic](https://github.com/Diseno-electronico-2023-1/evse-schemas/assets/126024376/2b02a925-df56-40a1-965b-ab35b09d1547)

![simulation](https://github.com/Diseno-electronico-2023-1/evse-schemas/assets/126024376/deecbd8a-70e5-406f-ac1c-a4d636f5dd03)

#### Table PWM - PILOT SIGNAL

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



