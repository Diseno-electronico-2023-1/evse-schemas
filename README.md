# evse-schemas

Cada grupo crea una rama para su PCB, cuando acaben hacen merge a la rama

Para crear una rama:

git checkout -b branch-name

Donde branch-name es el nombre de la rama Ej: Potencia

Una vez que estan en la nueva rama pueden subir sus cambios con:

git add .

git commit -m "Descripción de sus cambios"

git push -u origin branch-name


**Table of Contents**

[TOCM]

[TOC]

## CONECTOR
Esta seccion esta basado en la plantilla [Conector](https://github.com/Diseno-electronico-2023-1/evse-schemas/tree/Conector/Conector "Conector")

###Control Pilot PCB y simulación

###Tables SAE J1772 PILOT SIGNAL
                    
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

                    
AMPS  | DUTY CYCLE
------------- | -------------
5  | 8.3%
15  | 25% 
30  | 50%
40  | 66.6%
65  | 90%
80  | 96%
