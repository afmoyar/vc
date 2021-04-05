# Image and video processing

### Usando Luma

> :P5 width=350, height=450
>
> let img3;
> function preload(){
>   img3 = loadImage('/vc/docs/sketches/eye-color.jpg');
>}
> function setup() {
>   createCanvas(350, 450);
>   image(img3, 0, 0,width,height);
> }

> :P5 width=350, height=450
>
> let img4
> function preload(){
>   img4 = loadImage('/vc/docs/sketches/eye-color.jpg');
>}
>
> function setup() {
>   createCanvas(350, 450);
>}
>function draw(){
>   image(img4, 0, 0,width,height);
>   let d = pixelDensity();
>   loadPixels();
>   let numPixels = 8 * (width * d) * (height / 2 * d);
>   
>   for (let i = 0; i < numPixels; i += 4) {
>      let r = red(pixels[i]);
>      let g = green(pixels[i]);
>      let b = blue(pixels[i]);
>      let y = r *0.299 + g *0.587 + b *0.0114;
>      let grayColor = color(y, y, y);
>      pixels[i] = red(grayColor);
>      pixels[i + 1] = green(grayColor);
>      pixels[i + 2] = blue(grayColor);
>    }
>
>   updatePixels();
> }

#### Luma Normalizado

> :P5 width=350, height=450
>
> let img4
> function preload(){
>   img4 = loadImage('/vc/docs/sketches/eye-color.jpg');
>}
>
> function setup() {
>   createCanvas(350, 450);
>}
>
>function draw(){
>   image(img4, 0, 0,width,height);
>   let d = pixelDensity();
>   loadPixels();
>   let numPixels = 8 * (width * d) * (height / 2 * d);
>   
>   for (let i = 0; i < numPixels; i += 4) {
>      let r = red(pixels[i]);
>      let g = green(pixels[i]);
>      let b = blue(pixels[i]);
>      let r_norm = r/255;
>      let g_norm = g/255;
>      let b_norm = b/255;
>      let r_prim = 255 * Math.pow((r_norm/255),(1/2.2));
>      let g_prim = 255 * Math.pow((g_norm/255),(1/2.2));
>      let b_prim = 255 * Math.pow((b_norm/255),(1/2.2));
>      let y = 0.2999 * r_prim + 0.587 * g_prim + 0.114 * b_prim;
>      let grayColor = color(y, y, y);
>      pixels[i] = red(grayColor);
>      pixels[i + 1] = green(grayColor);
>      pixels[i + 2] = blue(grayColor);
>    }
>
>   updatePixels();
> }
> 

## VideoLuma

> :P5 width=350, height=250
>
> let vid;
>
> function setup() {
>    createCanvas(350, 250);
>    vid = createVideo(['/vc/docs/sketches/youWinTheInternet.mp4']);
>    vid.loop();
>    vid.hide();
>}
>
> function draw() {
>  background(0);
>  image(vid, 0, 0, 350, 250);
>  loadPixels();
>  const step = 1;
>  for (let y = 0; y < height; y+= step) {
>    for (let x = 0; x < width; x+= step) {
>       let index = 4 * (x + width * y);
>       let r = pixels[index];
>       let g = pixels[index + 1];
>       let b = pixels[index + 2];
>       let gamma = r * 0.299 + g * 0.587 + b * 0.0114;
>       let grayColor = color(gamma, gamma, gamma);
>       pixels[index] = red(grayColor);
>       pixels[index + 1] = green(grayColor);
>       pixels[index + 2] = blue(grayColor);
>      }
>  }
>  updatePixels();
>}

>:ToCPrevNext
