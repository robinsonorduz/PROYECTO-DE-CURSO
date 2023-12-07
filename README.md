# PROYECTO-DE-CURSO- PICK AND PLACE
En esta aplicacion desarrollada en RobotStudio, se hizo una rutina donde el robot recoge tres productos de una estanteria que tiene 6 opciones, luego los organiza en tre ubicaciones sobre una banda transportadora, las opciones de recogida en la estanteria son A1, A2, A3, B1,B2,B3.
Para este trbajo se diseño una herramienta especial que se ajusta a los requisitos tanto de montaje en el manipulador como de sujecion de los productos que va a transportar.
## diseño de la herramienta:
La herramienta se diseño y fabrico en base a unas pinzas de cocina de acero inoxidable, se escogio esta opcion debido a que es u  elemento diseñado para manipular objetos de distintos tamaños y texturas.
Para controlar el cierre y apertura de las pinzas se uso una jeringa de 30 ml que funciona como actuador neumatico de simple efecto, el cierre de las pinzas se da cuando se le aplica presión a la entrada de la jeringa y la camara que se forma entre chasis y embolo se expande, en ese momento las pinzas sujetan el objeto que se va a transportar.
Para ejecutar la liberacion del objeto se abren las pinzas y esto se logra haciendo que la camara que anteriormente se expandio, se contraiga haciendo vacio sobre ella con una valvula de venturi.
Ambos movimientos son ejecutados por un sistema electroneumatico y controlados por 2 salidas digitales desde el controlador IRC5 ASI:

https://github.com/robinsonorduz/PROYECTO-DE-CURSO/blob/main/cto%20neumatico.JPG

se usaron los siguientes elementos neumaticos:

- 1 tee.
- manguera 6mm.
- manguera 8mm.
- racores 6 y 8 mm con rosca 1/4 y 3/8 segun las especificaciones de las valvulas.
- 1 reduccion de 6 a 8mm.
- 1 regulador de caudal.
- 1 valvula venturi con silenciador.
- 1 valvula 5/2 monoestable con mando neumatico y retorno por muelle.
- 1 valvula 5/2 biestable con mando manual y electrico.
El resultado final fue el siguiente:
https://github.com/robinsonorduz/PROYECTO-DE-CURSO/blob/main/pinza.jpg
Luego se hizo un modelado de la herramienta copiando las cotas geometricas principales en Inventor y se exporto a Robotstudio, para configurar el orgen y el TCP de manera conveniente, luego se guardo como herramienta para que aparezca en la biblioteca y poder usarla luego desde cualquier estación:
https://github.com/robinsonorduz/PROYECTO-DE-CURSO/blob/main/RSpinza.JPG

