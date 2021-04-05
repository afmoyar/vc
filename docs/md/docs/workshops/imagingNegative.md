# Image and video processing

Para esta sección se desarrolló un programa para generar el negativo de una imagen. Para ello se reemplazó los valores rgb de cada pixel por su negativo, es decir:
<center>r := 255 - r</center>
<center>g := 255 - g</center>
<center>b := 255 - b</center>

## Negativo

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

>:ToCPrevNext