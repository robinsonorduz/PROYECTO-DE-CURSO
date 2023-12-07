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
https://github.com/robinsonorduz/PROYECTO-DE-CURSO/blob/main/toolbiblioteca.JPG

## diseño de la rutina de movimiento
Se crearon 6 subrutinas para carga de objetos que corresponden a las seis posiciones de la estanteria, cada una con una posicion de acercamiento donde se abre la pinza y llega al lugar indicado de la estanteria lista para agarrar; y tres subrutinas de descarga correspondientes a los tres lugares donde se puede dejar el objeto esta con un pnto de acercamiento comun,  que en este caso coincide con el home general de todo el programa.

MODULE Module1
        PERS tooldata dedos:=[TRUE,[[-115.966,-98.995,0],[1,0,0,0]],[1,[0,0,1],[1,0,0,0],0,0,0]];
    PERS wobjdata baggebo:=[FALSE,TRUE,"",[[700,300,0],[0,0.707106781,0.707106781,0]],[[0,0,0],[1,0,0,0]]];
    CONST robtarget home:=[[172.690062052,495.100374153,736.516220152],[0.324151653,-0.220200787,0.662389688,0.638496061],[0,-1,1,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget ACA1:=[[-194.999998875,-348.68819099,-702.497481396],[0.639233487,-0.662368123,-0.224938022,-0.319455637],[0,0,-1,1],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget A1:=[[-195.000000286,-98.782674168,-508.879710331],[0.639233498,-0.662368126,-0.224938,-0.319455627],[0,0,0,1],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget ACA2:=[[-351.14010191,-352.528118681,-702.344066147],[0.639233511,-0.662368111,-0.224937995,-0.319455634],[0,1,-1,1],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget A2:=[[-362.003858979,-98.782672851,-508.879717927],[0.63923349,-0.662368124,-0.224938012,-0.319455637],[0,0,0,1],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget ACA3:=[[-611.038206662,-395.942029611,-737.164408575],[0.639233531,-0.662368119,-0.224937943,-0.319455615],[-1,-2,1,1],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget A3:=[[-570.352597157,-98.782671341,-508.879715195],[0.639233497,-0.66236811,-0.224938015,-0.319455649],[-1,-1,0,1],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget ACB1:=[[-195.000006258,-348.688198632,-384.07407352],[0.639233503,-0.662368117,-0.22493801,-0.319455628],[0,0,0,1],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget B1:=[[-175.650105838,-98.782679588,-188.730986448],[0.639233524,-0.662368106,-0.224937966,-0.31945564],[0,0,0,1],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget ACB2:=[[-376.005697021,-290.771586392,-415.919881951],[0.639233498,-0.662368124,-0.224938,-0.319455631],[0,0,0,1],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget B2:=[[-366.039370563,-98.782683768,-188.730979145],[0.639233527,-0.662368105,-0.22493796,-0.319455639],[0,0,0,1],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget ACB3:=[[-604.166656597,-385.068640924,-510.070810804],[0.639233484,-0.662368123,-0.22493801,-0.319455653],[-1,-1,0,1],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget B3:=[[-570.35260163,-98.782675135,-188.731018808],[0.639233518,-0.662368101,-0.224937983,-0.319455649],[-1,-1,0,1],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget descarga1:=[[294.156301942,-904.554863837,-255.213170465],[0.230997582,-0.647006976,0.306811492,-0.658702359],[1,-2,2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget descarga2:=[[294.156319825,-730.167349498,-255.213189787],[0.230997665,-0.647006983,0.306811435,-0.65870235],[1,-2,2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget descarga3:=[[294.156300475,-557.178673512,-255.213170731],[0.230997652,-0.647007036,0.306811428,-0.658702306],[1,-3,2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
!***********************************************************
    !
    ! Módulo:  Module1
    !
    ! Descripción:
    !   <Introduzca la descripción aquí>
    !
    ! Autor: robin
    !
    ! Versión: 1.0
    !
    !***********************************************************
    
    
    !***********************************************************
    !
    ! Procedimiento Main
    !
    !   Este es el punto de entrada de su programa
    !
    !***********************************************************
    PROC main()
        !Añada aquí su código
        SetDO abrir,0;
        SetDO cerrar,0;
        
        cargaA1;
        descargue1;
        cargaA2;
        descargue2;
        cargaA3;
        descargue3;
        cargaB1;
        descargue1;
        cargaB2;
        descargue2;
        cargaB3;
        descargue3;
    ENDPROC
    PROC cargaA1()
        MoveJ home,v100,fine,dedos\WObj:=wobj0;
        MoveJ ACA1,v100,fine,dedos\WObj:=baggebo;
        SetDO abrir,1;
        WaitTime 2;
        SetDO abrir,0;
        MoveJ A1,v100,fine,dedos\WObj:=baggebo;
        SetDO cerrar,1;
        WaitTime 2;
        SetDO cerrar,0;
        MoveJ ACA1,v100,fine,dedos\WObj:=baggebo;
        MoveJ home,v100,fine,dedos\WObj:=wobj0;
    ENDPROC
    PROC cargaA2()
        MoveJ home,v100,fine,dedos\WObj:=wobj0;
        MoveJ ACA2,v100,fine,dedos\WObj:=baggebo;
        SetDO abrir,1;
        WaitTime 2;
        SetDO abrir,0;
        MoveJ A2,v100,fine,dedos\WObj:=baggebo;
        SetDO cerrar,1;
        WaitTime 2;
        SetDO cerrar,0;
        MoveJ ACA2,v100,fine,dedos\WObj:=baggebo;
        MoveJ home,v100,fine,dedos\WObj:=wobj0;
    ENDPROC
    PROC cargaA3()
        MoveJ home,v100,fine,dedos\WObj:=wobj0;
        MoveJ ACA3,v100,fine,dedos\WObj:=baggebo;
        SetDO abrir,1;
        WaitTime 2;
        SetDO abrir,0;
        MoveJ A3,v100,fine,dedos\WObj:=baggebo;
        SetDO cerrar,1;
        WaitTime 2;
        SetDO cerrar,0;
        MoveJ ACA3,v100,fine,dedos\WObj:=baggebo;
        MoveJ home,v100,fine,dedos\WObj:=wobj0;
    ENDPROC
    PROC cargaB1()
        MoveJ home,v100,fine,dedos\WObj:=wobj0;
        MoveJ ACB1,v100,fine,dedos\WObj:=baggebo;
        SetDO abrir,1;
        WaitTime 2;
        SetDO abrir,0;
        MoveJ B1,v100,fine,dedos\WObj:=baggebo;
        SetDO cerrar,1;
        WaitTime 2;
        SetDO cerrar,0;
        MoveJ ACB1,v100,fine,dedos\WObj:=baggebo;
        MoveJ home,v100,fine,dedos\WObj:=wobj0;
    ENDPROC
    PROC cargaB2()
        MoveJ home,v100,fine,dedos\WObj:=wobj0;
        MoveJ ACB2,v100,fine,dedos\WObj:=baggebo;
        SetDO abrir,1;
        WaitTime 2;
        SetDO abrir,0;
        MoveJ B2,v100,fine,dedos\WObj:=baggebo;
        SetDO cerrar,1;
        WaitTime 2;
        SetDO cerrar,0;
        MoveJ ACB2,v100,fine,dedos\WObj:=baggebo;
        MoveJ home,v100,fine,dedos\WObj:=wobj0;
    ENDPROC
    PROC cargaB3()
        MoveJ home,v100,fine,dedos\WObj:=wobj0;
        MoveJ ACB3,v100,fine,dedos\WObj:=baggebo;
        SetDO abrir,1;
        WaitTime 2;
        SetDO abrir,0;
        MoveJ B3,v100,fine,dedos\WObj:=baggebo;
        SetDO cerrar,1;
        WaitTime 2;
        SetDO cerrar,0;
        MoveJ ACB3,v100,fine,dedos\WObj:=baggebo;
        MoveJ home,v100,fine,dedos\WObj:=wobj0;
    ENDPROC
    PROC descargue1()
        MoveJ home,v100,fine,dedos\WObj:=wobj0;
        MoveJ descarga1,v100,fine,dedos\WObj:=baggebo;
        SetDO abrir,1;
        WaitTime 2;
        SetDO abrir,0;
        MoveJ home,v100,fine,dedos\WObj:=wobj0;
        SetDO cerrar,1;
        WaitTime 2;
        SetDO cerrar,0;
    ENDPROC
    PROC descargue2()
        MoveJ home,v100,fine,dedos\WObj:=wobj0;
        MoveJ descarga2,v100,fine,dedos\WObj:=baggebo;
        SetDO abrir,1;
        WaitTime 2;
        SetDO abrir,0;
        MoveJ home,v100,fine,dedos\WObj:=wobj0;
        SetDO cerrar,1;
        WaitTime 2;
        SetDO cerrar,0;
    ENDPROC
    PROC descargue3()
        MoveJ home,v100,fine,dedos\WObj:=wobj0;
        MoveJ descarga3,v100,fine,dedos\WObj:=baggebo;
        SetDO abrir,1;
        WaitTime 2;
        SetDO abrir,0;
        MoveJ home,v100,fine,dedos\WObj:=wobj0;
        SetDO cerrar,1;
        WaitTime 2;
        SetDO cerrar,0;
    ENDPROC
ENDMODULE

El resultado de la simulacion es este:
https://youtu.be/em6pgqhC7fs
