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

Escala de grises

> :P5 width=350, height=450
>
> let img;
> function preload(){
>   img = loadImage('/vc/docs/sketches/movie.jpg');   
>}
> function setup() {
>   createCanvas(350, 450);
>   image(img, 0, 0,width,height);
>   let d = pixelDensity();
>   loadPixels();
>   let numPixels = 8 * (width * d) * (height / 2 * d);
>   for (let i = 0; i < numPixels; i += 4) {
>      let r = red(pixels[i]);
>      let g = green(pixels[i]);
>      let b = blue(pixels[i]);
>      let gray = (r+b+g)/3;
>      let grayColor = color(gray, gray, gray);
>      pixels[i] = red(grayColor);
>      pixels[i + 1] = green(grayColor);
>      pixels[i + 2] = blue(grayColor);
>    }
>   updatePixels();
> }

Negativa

> :P5 width=350, height=450
>
> let img;
> function preload(){
>   img = loadImage('/vc/docs/sketches/movie.jpg');   
>}
> function setup() {
>   createCanvas(350, 450);
>   image(img, 0, 0,width,height);
>   let d = pixelDensity();
>   loadPixels();
>   let numPixels = 8 * (width * d) * (height / 2 * d);
>   for (let i = 0; i < numPixels; i += 4) {
>      //pixels[i] = red(pink);
>      let r = red(pixels[i]);
>      let g = green(pixels[i]);
>      let b = blue(pixels[i]);
>      let negative = color(255 - r, 255 - g, 255 - b);
>      pixels[i] = red(negative);
>      pixels[i + 1] = green(negative);
>      pixels[i + 2] = blue(negative);
>    }
>   updatePixels();
> }




Imagen original

> :P5 width=350, height=450
>
> let img;
> function preload(){
>   img = loadImage('/vc/docs/sketches/movie.jpg');   
>}
> function setup() {
>   createCanvas(350, 450);
>   image(img, 0, 0,width,height);
> }

## Ilusión

> :P5 width=400, height=400
>
>function setup() {
>  createCanvas(400, 400);
>}
>
>function draw() {
>  background(220);
>	
>  
>  line(0, 0, 50, 400);
>  line(0, 50, 100, 400);
>  line(0, 100, 150, 400);
>  line(0, 150, 200, 400);
>  line(0, 200, 250, 400);
>  line(0, 250, 300, 400);
>  line(0, 300, 350, 400);
>  line(0, 350, 400, 400);
>line(0, 0, 400, 50);
>line(50, 0, 400, 100);
>line(100, 0, 400, 150);
>line(150, 0, 400, 200);
>line(200, 0, 400, 250);
>line(250, 0, 400, 300);
>line(300, 0, 400, 350);
>line(350, 0, 400, 400);
>}


> :ToCPrevNext