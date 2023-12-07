# PROYECTO-DE-CURSO- PICK AND PLACE
En esta aplicacion desarrollada en RobotStudio, se hizo una rutina donde el robot recoge tres productos de una estanteria que tiene 6 opciones, luego los organiza en tre ubicaciones sobre una banda transportadora, las opciones de recogida en la estanteria son A1, A2, A3, B1,B2,B3.
Para este trbajo se diseño una herramienta especial que se ajusta a los requisitos tanto de montaje en el manipulador como de sujecion de los productos que va a transportar.
## diseño de la herramienta:
La herramienta se diseño y fabrico en base a unas pinzas de cocina de acero inoxidable, se escogio esta opcion debido a que es u  elemento diseñado para manipular objetos de distintos tamaños y texturas.
Para controlar el cierre y apertura de las pinzas se uso una jeringa de 30 ml que funciona como actuador neumatico de simple efecto, el cierre de las pinzas se da cuando se le aplica presión a la entrada de la jeringa y la camara que se forma entre chasis y embolo se expande, en ese momento las pinzas sujetan el objeto que se va a transportar.
Para ejecutar la liberacion del objeto se abren las pinzas y esto se logra haciendo que la camara que anteriormente se expandio, se contraiga haciendo vacio sobre ella con una valvula de venturi.
Ambos movimientos son ejecutados por un sistema electroneumatico y controlados por 2 salidas digitales desde el controlador IRC5 ASI:

