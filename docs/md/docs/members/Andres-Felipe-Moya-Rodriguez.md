# Andres Felipe Moya Rodríguez

## Bio
Nacido en Bogotá, Colombia.
Estudiante de ingeniería de sistemas y computación en la Universidad Nacional de Colombia.

## Interests

Desarrollo de software, estructuras de datos, deep learning.

## Contributions

*Problema de Simon*: Caso especial del problema del subgrupo oculto. Puede ser resuelto con la ayuda de algoritmos cuánticos.
https://es.wikipedia.org/wiki/Problema_de_Simon

## Hobbies

Películas, series de televisión, música y videojuegos.


## Ilusión

En 1904, Mary Everest Boole (matemática inglesa) inventó las ***Curve stitching*** (curva de costura), una forma de arte donde se "crean" líneas curvas a través de líneas rectas. Este fenómeno de crear una aparente curvatura ocurre gracias al hecho que una curva se puede aproximar mediante el trazo de una cantidad finita de tangentes a la misma.


> :P5 width=800, height=800
>
>function setup() {
>  createCanvas(800, 800);
>}
>
>function draw() {
>  background(220);
>  let startx = 400;
>  let starty = 0;
>  let endx = 0;
>  let endy=10;
>  let step = 10;
>  while(startx!=0){
>    line(startx, starty, endx, endy);
>    startx-=step;
>    endy+=step;
>  }
>  
>  startx = 400;
>  starty = 0;
>  endx = 390;
>  endy=400;
>  step = 10;
>  while(endx!=0){
>    line(startx, starty, endx, endy);
>    starty+=step;
>    endx-=step;
>  }
>  
>  
>  startx = 400;
>  starty = 0;
>  endx = 800;
>  endy = 10;
>  while(startx!=800){
>    line(startx, starty, endx, endy);
>    startx+=step;
>    endy+=step;
>  }
>  
>  
>  startx = 400;
>  starty = 0;
>  endx = 410;
>  endy = 400;
>  while(endx!=800){
>    line(startx, starty, endx, endy);
>    endx+=step;
>    starty+=step;
>  }
>  
>  startx = 0;
>  starty = 400;
>  endx = 400;
>  endy = 410;
>  while(startx!=400){
>    line(startx, starty, endx, endy);
>    startx+=step;
>    endy+=step;
>  }
>  
>  startx = 0;
>  starty = 400;
>  endx = 10;
>  endy = 800;
>  while(endx!=400){
>    line(startx, starty, endx, endy);
>    starty+=step;
>    endx+=step;
>  } 
>
>  startx = 400;
>  starty = 800;
>  endx = 410;
>  endy = 400;
>  while(starty!=400){
>    line(startx, starty, endx, endy);
>    starty-=step;
>    endx+=step;
>  } 
> 
>  startx = 800;
>  starty = 400;
>  endx = 790;
>  endy = 800;
>  while(endx!=400){
>    line(startx, starty, endx, endy);
>    starty+=step;
>    endx-=step;
>  }
>  line(0,400,800,400);
>  line(400,0,400,800);
>  line(400,390,0,400);
>  line(400,390,800,400);
>  
>}


> :ToCPrevNext