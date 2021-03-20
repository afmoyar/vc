# Image and video processing

Imagen original

> :P5 width=350, height=450
>
> let img;
> let img2
> function preload(){
>   img = loadImage('/vc/docs/sketches/Stormlight.jpg');
>}
> function setup() {
>   createCanvas(350, 450);
>   image(img, 0, 0,width,height);
> }


Gama de grises

> :P5 width=350, height=450
>
> let img;
> let img2
> function preload(){
>   img = loadImage('/vc/docs/sketches/Stormlight.jpg');
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



Arte ascci

> :P5 width=350, height=450
>
> let img;
> let total = 0;
> function preload(){
>   img = loadImage('/vc/docs/sketches/Stormlight.jpg');
>}
> function setup() {
>   createCanvas(350, 450);
>   img.filter(GRAY);
>   image(img, 0, 0,width,height);
>   loadPixels();
>
>
>   let i = 0;
>   let d = pixelDensity();
>   let numPixels = 8 * (width * d) * (height / 2 * d);
>  for (let y = 0; y < height; y += 10) {
>    for (let x = 0; x < width; x += 10) {
>      let pixel = pixels[y * width + x];
>      let r = red(pixel);
>      let g = green(pixel);
>      let b = blue(pixel);
>      total = total + r + g + b;
>      i++;
>    }
>  }
>  total = total / i;
>  for (let y = 0; y < height; y += 8) {
>    for (let x = 0; x < width; x += 8) {
>        let pixel = pixels[y * width + x];
>        let r = red(pixel);
>        let g = green(pixel);
>        let b = blue(pixel);
>        let S=r+g+b;
>        S = S/total;
>        if (S<0.15){
>          text("@", x, y);
>        }
>        else if (S<0.30){
>          text("#", x, y);
>        }
>        else if (S<0.45){
>          text("M", x, y);
>        }
>        else if (S<0.60){
>          text("H", x, y);
>        }
>        else if (S<0.75){
>          text("L", x, y);
>        }
>        else if (S<1){
>          text("i", x, y);
>        }
>        else if (S<1.15){
>          text(":", x, y);
>        }
>        else if (S<=1.3){
>          text(".", x, y);
>        }
>    }
>  }
> }



> :P5 width=350, height=450
>
> function setup() {
>   createCanvas(350, 450);
>  for (let y = 0; y < height; y += 8) {
>    for (let x = 0; x < width; x += 8) {
>       text(".", x, y);
>    }
>  }
> }



> :ToCPrevNext