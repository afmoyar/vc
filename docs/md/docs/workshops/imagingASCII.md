# Image and video processing

## Arte ASCII


> :P5 width=350, height=450
>
> let img;
> function preload(){
>   img = loadImage('/vc/docs/sketches/tree.jpg');
>}
> function setup() {
>   createCanvas(350, 450);
>   image(img, 0, 0,width,height);
> }


> :P5 width=350, height=450
>
>let img;
>let total = 0;
>
>
>function preload() {
> img = loadImage('/vc/docs/sketches/tree.jpg');
>}
>function setup() {
>  createCanvas(350,450);
>  background(255);
>  fill(0);
>  textFont("Courier", 6);
>  img.resize(width,height);
>  img.filter(GRAY);
>  img.loadPixels();
>  
>  let i = 0;
>  
>  for (let y = 0; y < height; y += 8) {
>    for (let x = 0; x < width; x += 8) {
>      let pixel = img.pixels[(y * img.width + x)];
>      let r = red(pixel);
>      let g = green(pixel);
>      let b = blue(pixel);
>      total = total + r + g + b;
>      i++;
>    }
>  }
>  
>  total = total / i;
>  for (let y = 0; y < height; y += 2) {
>    for (let x = 0; x < width; x += 2) {
>        let pixel = img.pixels[4*(y * img.width + x)];
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
>}

> :ToCPrevNext