# Andres Felipe Moya Rodríguez

## Bio
Born in Bogota, Colombia.
Computer Engineering student at Universidad Nacional de Colombia.

## Interests

Software development, data structures, deep learning.

## Contributions

*Simon's problem*: Special case of the Hidden Subgroup problem. It can be solved with the help of quantum algorithms. 
https://es.wikipedia.org/wiki/Problema_de_Simon

## Hobbies

Movies, TV shows, videogames and music.

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
>   let pink = color(255, 102, 204);
>   let numPixels = 8 * (width * d) * (height / 2 * d);
>   for (let i = 0; i < numPixels; i += 4) {
>      //pixels[i] = red(pink);
>      let r = red(pixels[i]);
>      let g = green(pixels[i]);
>      let b = blue(pixels[i]);
>      let gray = (r+b+g)/3;
>      pixels[i] = color(gray, gray, gray);
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
>   let pink = color(255, 102, 204);
>   let numPixels = 8 * (width * d) * (height / 2 * d);
>   for (let i = 0; i < numPixels; i += 4) {
>      //pixels[i] = red(pink);
>      let r = red(pixels[i]);
>      let g = green(pixels[i]);
>      let b = blue(pixels[i]);
>      pixels[i] = color(255 - r, 255 - g, 255 - b);
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

> :ToCPrevNext