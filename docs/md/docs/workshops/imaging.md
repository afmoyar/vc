# Image and video processing

## Gama de grises

### Usando Promedio RGB

> :P5 width=350, height=450
>
> let img;
> function preload(){
>   img = loadImage('/vc/docs/sketches/Stormlight.jpg');
>}
> function setup() {
>   createCanvas(350, 450);
>   image(img, 0, 0,width,height);
> }


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


### Gama de grises en video

> :P5 width=350, height=250
>
>let vid;
>function setup() {
>  noCanvas();
>
>  vid = createVideo(
>    ['/vc/docs/sketches/youWinTheInternet.mp4'],
>    vidLoad
>  );
>
>  vid.size(350, 250);
>}
>
>// This function is called when the video loads
>function vidLoad() {
>  vid.loop();
>  vid.volume(0);
>}


> :P5 width=350, height=250
>
>let vid;
>
>function setup() {
>  createCanvas(350, 250);
>  // specify multiple formats for different browsers
>  vid = createVideo(['/vc/docs/sketches/youWinTheInternet.mp4']);
>  vid.hide();
>  vid.loop();
>}
>
>function draw() {
>  background(0);
>  image(vid, 0, 0,350, 250); // draw the video frame to canvas
>  filter(GRAY);
>}
>
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
>let vid;
>
> function preload() {
>    vid = createVideo('/vc/docs/sketches/youWinTheInternet.mp4');
>    vid.size(350,250);
>    vid.volume(0);
>}
>
>function setup() {
>    createCanvas(350, 250);
>    vid.loop();
>    vid.hide();
>    vid.size(350,250);
>    vid.volume(0);
>}
>
>function draw() {
>    loadPixels();
>    for (let x = 1; x < vid.width; x++) {
>        for (let y = 1; y < vid.height; y++) {
>            let index = 4 * (x + vid.width * y);
>            let r = pixels[index];
>            let g = pixels[index + 1];
>            let b = pixels[index + 2];
>            let y = r *0.299 + g *0.587 + b *0.0114;
>            let grayColor = color(y, y, y);
>            pixels[index] = red(grayColor);
>            pixels[index + 1] = green(grayColor);
>            pixels[index + 2] = blue(grayColor);
>       }
>   }
>   updatePixels();
> }

## Máscaras de convolución

Una matriz de convolución o máscara es una matriz pequeña que se utiliza para desenfoque, enfoque, realce, detección de bordes.
Para hacer estos procesamientos se debe realizar una convolución entre un núcleo y una imagen.
El kernel de una imagen es una pequeña matriz cuadrada de tamaño impar que, por medio de la convolución entre el kernel y la imagen, se utiliza para aplicar distintos efectos en la imagen. La convolución es el proceso en el cual se suma cada píxel de la imagen con sus vecinos locales, teniendo en cuenta los pesos indicados por el kernel. De esta forma, si tenemos la matriz de píxeles:

# Máscaras en Imágenes

> :P5 width=350, height=450
>
> let img;
> function preload(){
>   img = loadImage('/vc/docs/sketches/hushky.jpg');
>}
> function setup() {
>   createCanvas(350, 450);
>   image(img, 0, 0,width,height);
> }

identidad
> :P5  width=350, height=500
>
> let img;
>
> let identity = [
>    [0, 0, 0],
>    [0, 1, 0],
>    [0, 0, 0]
> ];
>
> function preload() {
>    img = loadImage('/vc/docs/sketches/hushky.jpg');
>}
>
> function setup() {
>    createCanvas(350, 500);
>    img.loadPixels();
>}
>
> function draw() {
>   identityImg = createImage(img.width, img.height);
>   identityImg.loadPixels();
>   for (let x = 1; x < img.width; x++) {
>     for (let y = 1; y < img.height; y++) {
>        let c = convolution(x, y, identity);
>            let index = 4 * (x + img.width * y);
>            identityImg.pixels[index] = red(c);
>            identityImg.pixels[index + 1] = green(c);
>            identityImg.pixels[index + 2] = blue(c);
>            identityImg.pixels[index + 3] = alpha(c);
>        }
>    }
>    identityImg.updatePixels();
>    image(identityImg, 0, 0,width,height);
>}
>
> function convolution(x, y, matrix) {
>    let rtotal = 0;
>    let gtotal = 0;
>    let btotal = 0;
>    for (kx = -1; kx <= 1; kx++) {
>        for (ky = -1; ky <= 1; ky++) {
>            let xpos = x + kx;
>            let ypos = y + ky;
>            let r = 0;
>            let g = 0;
>            let b = 0;
>            if ((xpos >= 0 && xpos < img.width) && (ypos >= 0 || ypos < img.height)) {
>                let index = 4 * (xpos + img.width * ypos);
>                r = img.pixels[index];
>                g = img.pixels[index + 1];
>                b = img.pixels[index + 2];
>            }
>            rtotal += matrix[kx + 1][ky + 1] * r;
>            gtotal += matrix[kx + 1][ky + 1] * g;
>            btotal += matrix[kx + 1][ky + 1] * b;
>        }
>    }
>    rtotal = constrain(rtotal, 0, 255);
>    gtotal = constrain(gtotal, 0, 255);
>    btotal = constrain(btotal, 0, 255);
>    return color(rtotal, gtotal, btotal);
>}

Detección de bordes
> :P5  width=350, height=500
>
> let img;
>
> let edgeDetection = [
>    [1, 0, -1],
>    [0, 0, 0],
>    [-1, 0, 1]
> ];
>
> function preload() {
>    img = loadImage('/vc/docs/sketches/hushky.jpg');
>}
>
> function setup() {
>    createCanvas(350, 500);
>    img.loadPixels();
>}
>
> function draw() {
>   edgeDetectionImg = createImage(img.width, img.height);
>   edgeDetectionImg.loadPixels();
>   for (let x = 1; x < img.width; x++) {
>     for (let y = 1; y < img.height; y++) {
>        let c = convolution(x, y, edgeDetection);
>            let index = 4 * (x + img.width * y);
>            edgeDetectionImg.pixels[index] = red(c);
>            edgeDetectionImg.pixels[index + 1] = green(c);
>            edgeDetectionImg.pixels[index + 2] = blue(c);
>            edgeDetectionImg.pixels[index + 3] = alpha(c);
>        }
>    }
>    edgeDetectionImg.updatePixels();
>    image(edgeDetectionImg, 0, 0,width,height);
>}
>
> function convolution(x, y, matrix) {
>    let rtotal = 0;
>    let gtotal = 0;
>    let btotal = 0;
>    for (kx = -1; kx <= 1; kx++) {
>        for (ky = -1; ky <= 1; ky++) {
>            let xpos = x + kx;
>            let ypos = y + ky;
>            let r = 0;
>            let g = 0;
>            let b = 0;
>            if ((xpos >= 0 && xpos < img.width) && (ypos >= 0 || ypos < img.height)) {
>                let index = 4 * (xpos + img.width * ypos);
>                r = img.pixels[index];
>                g = img.pixels[index + 1];
>                b = img.pixels[index + 2];
>            }
>            rtotal += matrix[kx + 1][ky + 1] * r;
>            gtotal += matrix[kx + 1][ky + 1] * g;
>            btotal += matrix[kx + 1][ky + 1] * b;
>        }
>    }
>    rtotal = constrain(rtotal, 0, 255);
>    gtotal = constrain(gtotal, 0, 255);
>    btotal = constrain(btotal, 0, 255);
>    return color(rtotal, gtotal, btotal);
>}

> :P5  width=350, height=500
>
> let img;
>
> let edgeDetection2 = [
>    [0, -1, 0],
>    [-1, 4, -1],
>    [0, -1, 0]
> ];
>
> function preload() {
>    img = loadImage('/vc/docs/sketches/hushky.jpg');
>}
>
> function setup() {
>    createCanvas(350, 500);
>    img.loadPixels();
>}
>
> function draw() {
>   edgeDetection2Img = createImage(img.width, img.height);
>   edgeDetection2Img.loadPixels();
>   for (let x = 1; x < img.width; x++) {
>     for (let y = 1; y < img.height; y++) {
>        let c = convolution(x, y, edgeDetection2);
>            let index = 4 * (x + img.width * y);
>            edgeDetection2Img.pixels[index] = red(c);
>            edgeDetection2Img.pixels[index + 1] = green(c);
>            edgeDetection2Img.pixels[index + 2] = blue(c);
>            edgeDetection2Img.pixels[index + 3] = alpha(c);
>        }
>    }
>    edgeDetection2Img.updatePixels();
>    image(edgeDetection2Img, 0, 0,width,height);
>}
>
> function convolution(x, y, matrix) {
>    let rtotal = 0;
>    let gtotal = 0;
>    let btotal = 0;
>    for (kx = -1; kx <= 1; kx++) {
>        for (ky = -1; ky <= 1; ky++) {
>            let xpos = x + kx;
>            let ypos = y + ky;
>            let r = 0;
>            let g = 0;
>            let b = 0;
>            if ((xpos >= 0 && xpos < img.width) && (ypos >= 0 || ypos < img.height)) {
>                let index = 4 * (xpos + img.width * ypos);
>                r = img.pixels[index];
>                g = img.pixels[index + 1];
>                b = img.pixels[index + 2];
>            }
>            rtotal += matrix[kx + 1][ky + 1] * r;
>            gtotal += matrix[kx + 1][ky + 1] * g;
>            btotal += matrix[kx + 1][ky + 1] * b;
>        }
>    }
>    rtotal = constrain(rtotal, 0, 255);
>    gtotal = constrain(gtotal, 0, 255);
>    btotal = constrain(btotal, 0, 255);
>    return color(rtotal, gtotal, btotal);
>}

> :P5  width=350, height=500
>
> let img;
>
> let edgeDetection3 = [
>    [-1, -1, -1],
>    [-1, 8, -1],
>    [-1, -1, -1]
> ];
>
> function preload() {
>    img = loadImage('/vc/docs/sketches/hushky.jpg');
>}
>
> function setup() {
>    createCanvas(350, 500);
>    img.loadPixels();
>}
>
> function draw() {
>   edgeDetection3Img = createImage(img.width, img.height);
>   edgeDetection3Img.loadPixels();
>   for (let x = 1; x < img.width; x++) {
>     for (let y = 1; y < img.height; y++) {
>        let c = convolution(x, y, edgeDetection3);
>            let index = 4 * (x + img.width * y);
>            edgeDetection3Img.pixels[index] = red(c);
>            edgeDetection3Img.pixels[index + 1] = green(c);
>            edgeDetection3Img.pixels[index + 2] = blue(c);
>            edgeDetection3Img.pixels[index + 3] = alpha(c);
>        }
>    }
>    edgeDetection3Img.updatePixels();
>    image(edgeDetection3Img, 0, 0,width,height);
>}
>
> function convolution(x, y, matrix) {
>    let rtotal = 0;
>    let gtotal = 0;
>    let btotal = 0;
>    for (kx = -1; kx <= 1; kx++) {
>        for (ky = -1; ky <= 1; ky++) {
>            let xpos = x + kx;
>            let ypos = y + ky;
>            let r = 0;
>            let g = 0;
>            let b = 0;
>            if ((xpos >= 0 && xpos < img.width) && (ypos >= 0 || ypos < img.height)) {
>                let index = 4 * (xpos + img.width * ypos);
>                r = img.pixels[index];
>                g = img.pixels[index + 1];
>                b = img.pixels[index + 2];
>            }
>            rtotal += matrix[kx + 1][ky + 1] * r;
>            gtotal += matrix[kx + 1][ky + 1] * g;
>            btotal += matrix[kx + 1][ky + 1] * b;
>        }
>    }
>    rtotal = constrain(rtotal, 0, 255);
>    gtotal = constrain(gtotal, 0, 255);
>    btotal = constrain(btotal, 0, 255);
>    return color(rtotal, gtotal, btotal);
>}

Enfocar
> :P5  width=350, height=500
>
> let img;
>
> let sharpen = [
>    [0, -1, 0],
>    [-1, 5, -1],
>    [0, -1, 0]
> ];
>
> function preload() {
>    img = loadImage('/vc/docs/sketches/hushky.jpg');
>}
>
> function setup() {
>    createCanvas(350, 500);
>    img.loadPixels();
>}
>
> function draw() {
>   sharpenImg = createImage(img.width, img.height);
>   sharpenImg.loadPixels();
>   for (let x = 1; x < img.width; x++) {
>     for (let y = 1; y < img.height; y++) {
>        let c = convolution(x, y, sharpen);
>            let index = 4 * (x + img.width * y);
>            sharpenImg.pixels[index] = red(c);
>            sharpenImg.pixels[index + 1] = green(c);
>            sharpenImg.pixels[index + 2] = blue(c);
>            sharpenImg.pixels[index + 3] = alpha(c);
>        }
>    }
>    sharpenImg.updatePixels();
>    image(sharpenImg, 0, 0,width,height);
>}
>
> function convolution(x, y, matrix) {
>    let rtotal = 0;
>    let gtotal = 0;
>    let btotal = 0;
>    for (kx = -1; kx <= 1; kx++) {
>        for (ky = -1; ky <= 1; ky++) {
>            let xpos = x + kx;
>            let ypos = y + ky;
>            let r = 0;
>            let g = 0;
>            let b = 0;
>            if ((xpos >= 0 && xpos < img.width) && (ypos >= 0 || ypos < img.height)) {
>                let index = 4 * (xpos + img.width * ypos);
>                r = img.pixels[index];
>                g = img.pixels[index + 1];
>                b = img.pixels[index + 2];
>            }
>            rtotal += matrix[kx + 1][ky + 1] * r;
>            gtotal += matrix[kx + 1][ky + 1] * g;
>            btotal += matrix[kx + 1][ky + 1] * b;
>        }
>    }
>    rtotal = constrain(rtotal, 0, 255);
>    gtotal = constrain(gtotal, 0, 255);
>    btotal = constrain(btotal, 0, 255);
>    return color(rtotal, gtotal, btotal);
>}

Desenfoque de cuadro
> :P5  width=350, height=500
>
> let img;
>
> let boxBlur= [
>    [1.0 / 9.0, 1.0 / 9.0, 1.0 / 9.0],
>    [1.0 / 9.0, 1.0 / 9.0, 1.0 / 9.0],
>    [1.0 / 9.0, 1.0 / 9.0, 1.0 / 9.0]
> ];
>
> function preload() {
>    img = loadImage('/vc/docs/sketches/hushky.jpg');
>}
>
> function setup() {
>    createCanvas(350, 500);
>    img.loadPixels();
>}
>
> function draw() {
>   boxBlurImg = createImage(img.width, img.height);
>   boxBlurImg.loadPixels();
>   for (let x = 1; x < img.width; x++) {
>     for (let y = 1; y < img.height; y++) {
>        let c = convolution(x, y, boxBlur);
>            let index = 4 * (x + img.width * y);
>            boxBlurImg.pixels[index] = red(c);
>            boxBlurImg.pixels[index + 1] = green(c);
>            boxBlurImg.pixels[index + 2] = blue(c);
>            boxBlurImg.pixels[index + 3] = alpha(c);
>        }
>    }
>    boxBlurImg.updatePixels();
>    image(boxBlurImg, 0, 0,width,height);
>}
>
> function convolution(x, y, matrix) {
>    let rtotal = 0;
>    let gtotal = 0;
>    let btotal = 0;
>    for (kx = -1; kx <= 1; kx++) {
>        for (ky = -1; ky <= 1; ky++) {
>            let xpos = x + kx;
>            let ypos = y + ky;
>            let r = 0;
>            let g = 0;
>            let b = 0;
>            if ((xpos >= 0 && xpos < img.width) && (ypos >= 0 || ypos < img.height)) {
>                let index = 4 * (xpos + img.width * ypos);
>                r = img.pixels[index];
>                g = img.pixels[index + 1];
>                b = img.pixels[index + 2];
>            }
>            rtotal += matrix[kx + 1][ky + 1] * r;
>            gtotal += matrix[kx + 1][ky + 1] * g;
>            btotal += matrix[kx + 1][ky + 1] * b;
>        }
>    }
>    rtotal = constrain(rtotal, 0, 255);
>    gtotal = constrain(gtotal, 0, 255);
>    btotal = constrain(btotal, 0, 255);
>    return color(rtotal, gtotal, btotal);
>}

Desenfoque Gausiano 3x3
> :P5  width=350, height=500
>
> let img;
>
> let gaussianBlur3 = [
>    [1.0 / 16.0, 2.0 / 16.0, 1.0 / 16.0],
>    [2.0 / 16.0, 4.0 / 16.0, 2.0 / 16.0],
>    [1.0 / 16.0, 2.0 / 16.0, 1.0 / 16.0]
> ];
>
> function preload() {
>    img = loadImage('/vc/docs/sketches/hushky.jpg');
>}
>
> function setup() {
>    createCanvas(350, 500);
>    img.loadPixels();
>}
>
> function draw() {
>   gaussianBlur3Img = createImage(img.width, img.height);
>   gaussianBlur3Img.loadPixels();
>   for (let x = 1; x < img.width; x++) {
>     for (let y = 1; y < img.height; y++) {
>        let c = convolution(x, y, gaussianBlur3);
>            let index = 4 * (x + img.width * y);
>            gaussianBlur3Img.pixels[index] = red(c);
>            gaussianBlur3Img.pixels[index + 1] = green(c);
>            gaussianBlur3Img.pixels[index + 2] = blue(c);
>            gaussianBlur3Img.pixels[index + 3] = alpha(c);
>        }
>    }
>    gaussianBlur3Img.updatePixels();
>    image(gaussianBlur3Img, 0, 0,width,height);
>}
>
> function convolution(x, y, matrix) {
>    let rtotal = 0;
>    let gtotal = 0;
>    let btotal = 0;
>    for (kx = -1; kx <= 1; kx++) {
>        for (ky = -1; ky <= 1; ky++) {
>            let xpos = x + kx;
>            let ypos = y + ky;
>            let r = 0;
>            let g = 0;
>            let b = 0;
>            if ((xpos >= 0 && xpos < img.width) && (ypos >= 0 || ypos < img.height)) {
>                let index = 4 * (xpos + img.width * ypos);
>                r = img.pixels[index];
>                g = img.pixels[index + 1];
>                b = img.pixels[index + 2];
>            }
>            rtotal += matrix[kx + 1][ky + 1] * r;
>            gtotal += matrix[kx + 1][ky + 1] * g;
>            btotal += matrix[kx + 1][ky + 1] * b;
>        }
>    }
>    rtotal = constrain(rtotal, 0, 255);
>    gtotal = constrain(gtotal, 0, 255);
>    btotal = constrain(btotal, 0, 255);
>    return color(rtotal, gtotal, btotal);
>}

Desenfoque Gausiano 5x5
> :P5  width=350, height=500
>
> let img;
>
> let gaussianBlur5 = [
>    [1.0 / 256.0, 4.0 / 256.0, 6.0 / 256.0, 4.0 / 256.0, 1.0 / 256.0],
>    [4.0 / 256.0, 16.0 / 256.0, 24.0 / 256.0, 16.0 / 256.0, 4.0 / 256.0],
>    [6.0 / 256.0, 24.0 / 256.0, 36.0 / 256.0, 24.0 / 256.0, 6.0 / 256.0],
>    [4.0 / 256.0, 16.0 / 256.0, 24.0 / 256.0, 16.0 / 256.0, 4.0 / 256.0],
>    [1.0 / 256.0, 4.0 / 256.0, 6.0 / 256.0, 4.0 / 256.0, 1.0 / 256.0]
> ];
> function preload() {
>    img = loadImage('/vc/docs/sketches/hushky.jpg');
>}
>
> function setup() {
>    createCanvas(350, 500);
>    img.loadPixels();
>}
>
> function draw() {
>   gaussianBlur5Img = createImage(img.width, img.height);
>   gaussianBlur5Img.loadPixels();
>   for (let x = 1; x < img.width; x++) {
>     for (let y = 1; y < img.height; y++) {
>        let c = convolution(x, y, gaussianBlur5);
>            let index = 4 * (x + img.width * y);
>            gaussianBlur5Img.pixels[index] = red(c);
>            gaussianBlur5Img.pixels[index + 1] = green(c);
>            gaussianBlur5Img.pixels[index + 2] = blue(c);
>            gaussianBlur5Img.pixels[index + 3] = alpha(c);
>        }
>    }
>    gaussianBlur5Img.updatePixels();
>    image(gaussianBlur5Img, 0, 0,width,height);
>}
>
> function convolution(x, y, matrix) {
>    let rtotal = 0;
>    let gtotal = 0;
>    let btotal = 0;
>    for (kx = -1; kx <= 1; kx++) {
>        for (ky = -1; ky <= 1; ky++) {
>            let xpos = x + kx;
>            let ypos = y + ky;
>            let r = 0;
>            let g = 0;
>            let b = 0;
>            if ((xpos >= 0 && xpos < img.width) && (ypos >= 0 || ypos < img.height)) {
>                let index = 4 * (xpos + img.width * ypos);
>                r = img.pixels[index];
>                g = img.pixels[index + 1];
>                b = img.pixels[index + 2];
>            }
>            rtotal += matrix[kx + 1][ky + 1] * r;
>            gtotal += matrix[kx + 1][ky + 1] * g;
>            btotal += matrix[kx + 1][ky + 1] * b;
>        }
>    }
>    rtotal = constrain(rtotal, 0, 255);
>    gtotal = constrain(gtotal, 0, 255);
>    btotal = constrain(btotal, 0, 255);
>    return color(rtotal, gtotal, btotal);
>}

Mascara de desenfoque 5x5
> :P5  width=350, height=500
>
> let img;
>
> let unsharpMasking5 = [
>    [1.0 / -256.0, 4.0 / -256.0, 6.0 / -256.0, 4.0 / -256.0, 1.0 / -256.0],
>    [4.0 / -256.0, 16.0 / -256.0, 24.0 / -256.0, 16.0 / -256.0, 4.0 / -256.0],
>    [6.0 / -256.0, 24.0 / -256.0, -476.0 / -256.0, 24.0 / -256.0, 6.0 / -256.0],
>    [4.0 / -256.0, 16.0 / -256.0, 24.0 / -256.0, 16.0 / -256.0, 4.0 / -256.0],
>    [1.0 / -256.0, 4.0 / -256.0, 6.0 / -256.0, 4.0 / -256.0, 1.0 / -256.0]
> ];
> function preload() {
>    img = loadImage('/vc/docs/sketches/hushky.jpg');
>}
>
> function setup() {
>    createCanvas(350, 500);
>    img.loadPixels();
>}
>
> function draw() {
>   unsharpMasking5Img = createImage(img.width, img.height);
>   unsharpMasking5Img.loadPixels();
>   for (let x = 1; x < img.width; x++) {
>     for (let y = 1; y < img.height; y++) {
>        let c = convolution(x, y, unsharpMasking5);
>            let index = 4 * (x + img.width * y);
>            unsharpMasking5Img.pixels[index] = red(c);
>            unsharpMasking5Img.pixels[index + 1] = green(c);
>            unsharpMasking5Img.pixels[index + 2] = blue(c);
>            unsharpMasking5Img.pixels[index + 3] = alpha(c);
>        }
>    }
>    unsharpMasking5Img.updatePixels();
>    image(unsharpMasking5Img, 0, 0,width,height);
>}
>
> function convolution(x, y, matrix) {
>    let rtotal = 0;
>    let gtotal = 0;
>    let btotal = 0;
>    for (kx = -1; kx <= 1; kx++) {
>        for (ky = -1; ky <= 1; ky++) {
>            let xpos = x + kx;
>            let ypos = y + ky;
>            let r = 0;
>            let g = 0;
>            let b = 0;
>            if ((xpos >= 0 && xpos < img.width) && (ypos >= 0 || ypos < img.height)) {
>                let index = 4 * (xpos + img.width * ypos);
>                r = img.pixels[index];
>                g = img.pixels[index + 1];
>                b = img.pixels[index + 2];
>            }
>            rtotal += matrix[kx + 1][ky + 1] * r;
>            gtotal += matrix[kx + 1][ky + 1] * g;
>            btotal += matrix[kx + 1][ky + 1] * b;
>        }
>    }
>    rtotal = constrain(rtotal, 0, 255);
>    gtotal = constrain(gtotal, 0, 255);
>    btotal = constrain(btotal, 0, 255);
>    return color(rtotal, gtotal, btotal);
>}

# Máscaras en videos

> :P5 width=350, height=250
>
>let vid;
>function setup() {
>  noCanvas();
>
>  vid = createVideo(
>    ['/vc/docs/sketches/flower.mp4'],
>    vidLoad
>  );
>
>  vid.size(350, 250);
>}
>
>// This function is called when the video loads
>function vidLoad() {
>  vid.loop();
>  vid.volume(0);
>}

identidad 
> :P5 width=350, height=250
>
>let vid;
>
> let identity= [
>    [0, 0, 0],
>    [0, 1, 0],
>    [0, 0, 0]
> ];
> function preload() {
>    vid =  createVideo('/vc/docs/sketches/flower.mp4');
>    vid.size(350,250);
>    vid.volume(0);
>}
>
>function mousePressed() {
>    vid.loop();
>}
>
>function setup() {
>    createCanvas(350, 250);
>    vid =  createVideo('/vc/docs/sketches/flower.mp4'); 
>    vid.hide();
>    vid.size(350,250);
>    vid.volume(0);
>}
>
>function draw() {   
>    vid.loadPixels();
>    loadPixels();
>    for (let x = 1; x < vid.width; x++) {
>        for (let y = 1; y < vid.height; y++) {
>            let c = convolution(x, y, identity);
>            let index = 4 * (x + vid.width * y);
>            pixels[index] = red(c);
>            pixels[index + 1] = green(c);
>            pixels[index + 2] = blue(c);
>            pixels[index + 3] = alpha(c);
>        }
>    }
>    updatePixels();
>}
>
>function convolution(x, y, matrix) {
>    let rtotal = 0;
>    let gtotal = 0;
>    let btotal = 0;
>    for (kx = -1; kx <= 1; kx++) {
>        for (ky = -1; ky <= 1; ky++) {
>            let xpos = x + kx;
>            let ypos = y + ky;
>            let r = 0;
>            let g = 0;
>            let b = 0;
>            if ((xpos >= 0 && xpos < vid.width) && (ypos >= 0 || ypos < vid.height)) {
>                let index = 4 * (xpos + vid.width * ypos);
>                r = vid.pixels[index];
>                g = vid.pixels[index + 1];
>                b = vid.pixels[index + 2];
>            }
>            rtotal += matrix[kx + 1][ky + 1] * r;
>            gtotal += matrix[kx + 1][ky + 1] * g;
>            btotal += matrix[kx + 1][ky + 1] * b;
>        }
>    }
>    rtotal = constrain(rtotal, 0, 255);
>    gtotal = constrain(gtotal, 0, 255);
>    btotal = constrain(btotal, 0, 255);
>    return color(rtotal, gtotal, btotal);
>}

Detección de bordes
> :P5 width=350, height=250
>
>let vid;
>
> let edgeDetection = [
>    [1, 0, -1],
>    [0, 0, 0],
>    [-1, 0, 1]
> ];
>
> function preload() {
>    vid =  createVideo('/vc/docs/sketches/flower.mp4');
>    vid.size(350,250);
>    vid.volume(0);
>}
>
>function setup() {
>    createCanvas(350, 250);
>    vid.loop();
>    vid.hide();
>    vid.size(350,250);
>    vid.volume(0);
>}
>
>function draw() {
>    loadPixels();
>    for (let x = 1; x < vid.width; x++) {
>        for (let y = 1; y < vid.height; y++) {
>            let c = convolution(x, y, edgeDetection);
>            let index = 4 * (x + vid.width * y);
>            pixels[index] = red(c);
>            pixels[index + 1] = green(c);
>            pixels[index + 2] = blue(c);
>            pixels[index + 3] = alpha(c);
>        }
>    }
>    updatePixels();
>}
>
>function convolution(x, y, matrix) {
>    let rtotal = 0;
>    let gtotal = 0;
>    let btotal = 0;
>    for (kx = -1; kx <= 1; kx++) {
>        for (ky = -1; ky <= 1; ky++) {
>            let xpos = x + kx;
>            let ypos = y + ky;
>            let r = 0;
>            let g = 0;
>            let b = 0;
>            if ((xpos >= 0 && xpos < vid.width) && (ypos >= 0 || ypos < vid.height)) {
>                let index = 4 * (xpos + vid.width * ypos);
>                r = vid.pixels[index];
>                g = vid.pixels[index + 1];
>                b = vid.pixels[index + 2];
>            }
>            rtotal += matrix[kx + 1][ky + 1] * r;
>            gtotal += matrix[kx + 1][ky + 1] * g;
>            btotal += matrix[kx + 1][ky + 1] * b;
>        }
>    }
>    rtotal = constrain(rtotal, 0, 255);
>    gtotal = constrain(gtotal, 0, 255);
>    btotal = constrain(btotal, 0, 255);
>    return color(rtotal, gtotal, btotal);
>}

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

## Conversión de la imagen a un foto-mosaico.

Conversión con una imagen pequeña (mosaico de imagenes 3x3):

> :P5 width=350, height=450
>
> let img;
> let img2
> function preload(){
>   img = loadImage('/vc/docs/sketches/tree.jpg');   
>}
> function setup() {
>   createCanvas(350, 450);
>   image(img, 0, 0,width,height);
> }

> :P5 width=350, height=450
>
>let imgColor;
>let Rimgs = new Array(20);
>let Bimgs = new Array(20);
>let Gimgs = new Array(20);
>let Yimgs = new Array(20);
>let Grayimgs = new Array(20);
>let total = 0;
>//CARACTERISTICAS DE LA IMAGEN PRINCIPAL
>let MainImgName = "tree";
>let MainImgX = 350;
>let MainImgY = 450;
>let pixelSize = 3;
>let pixel;
>
>//FUNCION PARA RETORNAR EL INDICE DE LA IMAGEN A UTILIZAR SEGUN SU BRILLO
> function brightlevel(S) {
>  if (S<0.05){
>    return 20;
>  }
>  else if (S<0.14){
>    return 19;
>  }
>  else if (S<0.23){
>    return 18;
>  }
>  else if (S<0.32){
>    return 17;
>  }
>  else if (S<0.41){
>    return 16;
>  }
>  else if (S<0.5){
>    return 15;
>  }
>  else if (S<0.59){
>    return 14;
>  }
>  else if (S<0.68){
>    return 13;
>  }
>  else if (S<0.77){
>    return 12;
>  }
>  else if (S<0.86){
>    return 11;
>  }
>  else if (S<0.95){
>    return 10;
>  }
>  else if (S<1.04){
>    return 9;
>  }
>  else if (S<1.13){
>    return 8;
>  }
>  else if (S<1.22){
>    return 7;
>  }
>  else if (S<1.31){
>    return 6;
>  }
>  else if (S<1.4){
>    return 5;
>  }
>  else if (S<1.49){
>    return 4;
>  }
>  else if (S<1.58){
>    return 3;
>  }
>  else if (S<1.67){
>    return 2;
>  }
>  else if (S<=1.76){
>    return 1;
>  }
>  else{
>    return 100;
>  }
>}
>
>function preload(){
>  //SE CARGAN LAS IMAGENES RGB
>  for (let i=0; i<20; i++){
>    Rimgs[i] = loadImage("/vc/docs/sketches/imagenes/red"+(i+1)+".jpg");
>    Gimgs[i] = loadImage("/vc/docs/sketches/imagenes/green"+(i+1)+".jpg");
>    Bimgs[i] = loadImage("/vc/docs/sketches/imagenes/blue"+(i+1)+".jpg");
>    Yimgs[i] = loadImage("/vc/docs/sketches/imagenes/yellowOrange"+(i+1)+".jpg");
>    Grayimgs[i] = loadImage("/vc/docs/sketches/imagenes/gray"+(i+1)+".jpg");
>  }
>  //SE CARGA LA IMAGEN CON LA QUE SE TRABAJA 2 VECES PARA TENER UNA VERSION ORIGINAL Y OTRA A ESCALA DE GRISES
>  imgColor = loadImage("/vc/docs/sketches/"+MainImgName+".jpg");
>}
> 
>function setup() {
>  createCanvas(350,450);
>  background(255);
>  fill(0);
>  
>  //SE APLICA EL FILTRO GRIS
>  imgColor.loadPixels();
>  
>  let i = 0;
>  
>  //SE HALLA EL PROMEDIO DE LOS VALORES RGB PARA EL BRILLO
>  for (let y = 0; y < imgColor.height; y += 1) {
>    for (let x = 0; x < imgColor.width; x += 1) {
>      pixel = imgColor.pixels[(y * imgColor.width + x)];
>      total = total + brightness(pixel);
>      i++;
>    }
>  }
>  total = total / i;
>
>}
>  
>function draw(){
>  
>  imgColor.resize(MainImgX,MainImgY);
>  
>  for (let i=0; i<20; i++){
>    Rimgs[i].resize(pixelSize,pixelSize);
>    Gimgs[i].resize(pixelSize,pixelSize);
>    Bimgs[i].resize(pixelSize,pixelSize);
>    Yimgs[i].resize(pixelSize,pixelSize);
>    Grayimgs[i].resize(pixelSize,pixelSize);
>  }
>  
> //SE RECORRE LA IMAGEN
>  for (let y = 0; y < imgColor.height; y += pixelSize) {
>    for (let x = 0; x < imgColor.width; x += pixelSize) {
>      //CON LA IMAGEN GRIS VERIFICAMOS EL BRILLO DEL PIXEL
>        pixel = imgColor.get(x,y);
>        let S=brightness(pixel);
>        S = S/total;
>        //CON LA IMAGEN A COLOR VERIFICAMOS EL RGB DEL PIXEL
>        let r = red(pixel);
>        let g = green(pixel);
>        let b = blue(pixel);        
>        //LLAMAMOS A LA FUNCION PARA EL INDICE CORRESPONDIENTE EL BRILLO
>        let bright = brightlevel(S)-1;
>        if(r==255 && b==255 && g==255){
>         image(Grayimgs[0],x,y);
>        }
>        //SI RETORNA 99 ES BLANCO ASI QUE SE USA LA IMAGEN BLANCA DEL ELSE
>        else if(bright!=99){
>          //SE VERIFICA EL COLOR MAYORITARIO Y SE APLICA UNA IMAGEN CON ESE COLOR
>          if (r>=g && g>=125 && r>b){
>            image(Yimgs[bright],x,y);
>          }else if (r>b && r>g){
>            image(Rimgs[bright],x,y);
>          }else if(b>r && b>g){
>            image(Bimgs[bright],x,y);
>          }else if(g>b && g>r){
>            image(Gimgs[bright],x,y);
>          }else{
>            image(Grayimgs[bright],x,y);
>          }
>        }else{
>          image(Grayimgs[0],x,y);
>        }
>    }
>  }
>}

Conversión con una imagen grande (mosaico de imagenes 5x5):

> :P5 width=1500, height=1000
>
> let img;
> let img2
> function preload(){
>   img = loadImage('/vc/docs/sketches/paisaje2.jpg');   
>}
> function setup() {
>   createCanvas(1500, 1000);
>   image(img, 0, 0,width,height);
> }

> :P5 width=1500, height=1000
>
>let imgColor;
>let Rimgs = new Array(20);
>let Bimgs = new Array(20);
>let Gimgs = new Array(20);
>let Yimgs = new Array(20);
>let Grayimgs = new Array(20);
>let total = 0;
>//CARACTERISTICAS DE LA IMAGEN PRINCIPAL
>let MainImgName = "paisaje2";
>let MainImgX = 1500;
>let MainImgY = 1000;
>let pixelSize = 5;
>let pixel;
>
>//FUNCION PARA RETORNAR EL INDICE DE LA IMAGEN A UTILIZAR SEGUN SU BRILLO
> function brightlevel(S) {
>  if (S<0.05){
>    return 20;
>  }
>  else if (S<0.14){
>    return 19;
>  }
>  else if (S<0.23){
>    return 18;
>  }
>  else if (S<0.32){
>    return 17;
>  }
>  else if (S<0.41){
>    return 16;
>  }
>  else if (S<0.5){
>    return 15;
>  }
>  else if (S<0.59){
>    return 14;
>  }
>  else if (S<0.68){
>    return 13;
>  }
>  else if (S<0.77){
>    return 12;
>  }
>  else if (S<0.86){
>    return 11;
>  }
>  else if (S<0.95){
>    return 10;
>  }
>  else if (S<1.04){
>    return 9;
>  }
>  else if (S<1.13){
>    return 8;
>  }
>  else if (S<1.22){
>    return 7;
>  }
>  else if (S<1.31){
>    return 6;
>  }
>  else if (S<1.4){
>    return 5;
>  }
>  else if (S<1.49){
>    return 4;
>  }
>  else if (S<1.58){
>    return 3;
>  }
>  else if (S<1.67){
>    return 2;
>  }
>  else if (S<=1.76){
>    return 1;
>  }
>  else{
>    return 100;
>  }
>}
>
>function preload(){
>  //SE CARGAN LAS IMAGENES RGB
>  for (let i=0; i<20; i++){
>    Rimgs[i] = loadImage("/vc/docs/sketches/imagenes/red"+(i+1)+".jpg");
>    Gimgs[i] = loadImage("/vc/docs/sketches/imagenes/green"+(i+1)+".jpg");
>    Bimgs[i] = loadImage("/vc/docs/sketches/imagenes/blue"+(i+1)+".jpg");
>    Yimgs[i] = loadImage("/vc/docs/sketches/imagenes/yellowOrange"+(i+1)+".jpg");
>    Grayimgs[i] = loadImage("/vc/docs/sketches/imagenes/gray"+(i+1)+".jpg");
>  }
>  //SE CARGA LA IMAGEN CON LA QUE SE TRABAJA 2 VECES PARA TENER UNA VERSION ORIGINAL Y OTRA A ESCALA DE GRISES
>  imgColor = loadImage("/vc/docs/sketches/"+MainImgName+".jpg");
>}
> 
>function setup() {
>  createCanvas(1500,1000);
>  background(255);
>  fill(0);
>  
>  //SE APLICA EL FILTRO GRIS
>  imgColor.loadPixels();
>  
>  let i = 0;
>  
>  //SE HALLA EL PROMEDIO DE LOS VALORES RGB PARA EL BRILLO
>  for (let y = 0; y < imgColor.height; y += 1) {
>    for (let x = 0; x < imgColor.width; x += 1) {
>      pixel = imgColor.pixels[(y * imgColor.width + x)];
>      total = total + brightness(pixel);
>      i++;
>    }
>  }
>  total = total / i;
>
>}
>  
>function draw(){
>  
>  imgColor.resize(MainImgX,MainImgY);
>  
>  for (let i=0; i<20; i++){
>    Rimgs[i].resize(pixelSize,pixelSize);
>    Gimgs[i].resize(pixelSize,pixelSize);
>    Bimgs[i].resize(pixelSize,pixelSize);
>    Yimgs[i].resize(pixelSize,pixelSize);
>    Grayimgs[i].resize(pixelSize,pixelSize);
>  }
>  
> //SE RECORRE LA IMAGEN
>  for (let y = 0; y < imgColor.height; y += pixelSize) {
>    for (let x = 0; x < imgColor.width; x += pixelSize) {
>      //CON LA IMAGEN GRIS VERIFICAMOS EL BRILLO DEL PIXEL
>        pixel = imgColor.get(x,y);
>        let S=brightness(pixel);
>        S = S/total;
>        //CON LA IMAGEN A COLOR VERIFICAMOS EL RGB DEL PIXEL
>        let r = red(pixel);
>        let g = green(pixel);
>        let b = blue(pixel);        
>        //LLAMAMOS A LA FUNCION PARA EL INDICE CORRESPONDIENTE EL BRILLO
>        let bright = brightlevel(S)-1;
>        if(r==255 && b==255 && g==255){
>         image(Grayimgs[0],x,y);
>        }
>        //SI RETORNA 99 ES BLANCO ASI QUE SE USA LA IMAGEN BLANCA DEL ELSE
>        else if(bright!=99){
>          //SE VERIFICA EL COLOR MAYORITARIO Y SE APLICA UNA IMAGEN CON ESE COLOR
>          if (r>=g && g>=125 && r>b){
>            image(Yimgs[bright],x,y);
>          }else if (r>b && r>g){
>            image(Rimgs[bright],x,y);
>          }else if(b>r && b>g){
>            image(Bimgs[bright],x,y);
>          }else if(g>b && g>r){
>            image(Gimgs[bright],x,y);
>          }else{
>            image(Grayimgs[bright],x,y);
>          }
>        }else{
>          image(Grayimgs[0],x,y);
>        }
>    }
>  }
>}








> :ToCPrevNext
