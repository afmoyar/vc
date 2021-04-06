# Image and video processing

## Máscaras de convolución

# Máscaras en videos

> :P5 width=350, height=250
>
> let vid;
>
> function setup() {
>  noCanvas();
>
>  vid = createVideo(
>    ['/vc/docs/sketches/walk.mp4'],
>    vidLoad
>  );
>
>  vid.size(350, 250);
>}
>
>// This function is called when the video loads
> function vidLoad() {
>  vid.loop();
>  vid.volume(0);
>}

Identidad

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
>    vid =  createVideo('/vc/docs/sketches/walk.mp4');
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
>    vid =  createVideo('/vc/docs/sketches/walk.mp4'); 
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
>    vid =  createVideo('/vc/docs/sketches/walk.mp4');
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

> :ToCPrevNext
