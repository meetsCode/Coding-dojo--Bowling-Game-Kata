Intento implementar el algoritmo propuesto en:
http://slocums.homestead.com/gamescore.html

en la kata:
https://www.meetup.com/es-ES/Barcelona-Software-Craftsmanship/events/236984523/
del 30 de Enero de 2017

Lo implementaré en Smalltalk. Usaré Pharo5.0. Sobre cómo usar Pharo lee: https://github.com/meetsCode/Introduccion-PharoSmalltalk 
 
INTENCIÓN
La intención del ejercicio es implementar un contador de puntos de una bolera. El sistema es complejo sobretodo porque la puntuación de cada jugada puede, en ocasiones, depender de la siguiente jugada. Esto hace que el cálculo quede suspendido hasta que suceda la siguiente.
Por partes:
La puntuación del juego de los bolos se muestra en unos tableros cuadrados. Cada cuadrado representa dos tiradas. Podríamos decir que estas dos tiradas son “la tirada” y la segunda “la posibilidad de arreglar lo anterior”. Así cuando empiezas un cuadrado tienes 10 piezas levantadas. Haces la primera tirada y luego una segunda tirada para llevarte por delante las que no hayas podido tirar en la primera. Tras esta segunda tirada se cuentan los tirados, y otros puntos extra que ya contaré, y se vuelven a colocar las 10 piezas de nuevo. Si en la primera tirada se tiran todos ya no tira una segunda. Una partida de bolos completa son 10 cuadrados (o sea 20 tiradas) por jugador. Cuando juegan dos personas se dice que “juegan dos juegos” ¿Por qué eso y no decir un juego con dos jugadores” Ni idea.

“2 games”				 := dos jugadores aunque literalmente dice dos juegos.  
“per game” o “per game per person”	 := 10 cuadrados o “full frames” (:=20 tiradas).

PUNTUACIÓN:
La puntuación se guarda en un cuadrado (frame). En cada cuadrado se guarda registro de las piezas tiradas en cada uno de los dos tiros a que tiene derecho el jugador pero se hace de manera peculiar. En él también se guarda el total de puntos acumulados hasta el momento, es decir el acumulado de esa tirada más la acumulada del anterior. También se indica con símbolos cómo fue la primera tirada y/o la segunda. Los símbolos se ponen en un cuadrado que hay en la esquina superior derecha.
______
|   L|
|    |
—————-
Símbolos: 
X := strike. Esto indica que en la primera tirada tiró todas las piezas a la vez.(by the first roll) 
/ := space. Esto indica que en la primera tirada ha tirado alguna pero no todas. El número se escribe a la izq.
- := miss. Esto indica que no tiró ninguna en la primera tirada.
F := Foul. 
O Sobre los números := indica que tras el primer tiro las piezas quedaron en una formación específica, por ejemplo en forma “split”

Inicialmente cada frame tiene tantos puntos como piezas tire en sus dos tiradas. Hay puntos extra como por ejemplo si hace Strike. En el caso de Strike no hay segunda tirada (ya las tiró todas a la primera) así que se le suman (como un plus) las piezas que tire en el siguiente “frame”, o sea las que tire en los dos siguientes “roll”.
  
