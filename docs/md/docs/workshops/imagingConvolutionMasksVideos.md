# Image and video processing

## Máscaras de convolución

# Máscaras en videos

> :P5 width=640, height=360
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
>  vid.size(640, 360);
>}
>
>// This function is called when the video loads
> function vidLoad() {
>  vid.loop();
>  vid.volume(0);
>}

Identidad

> :P5 width=640, height=360
>
> let walkvid;
>
> let kernel = [
>    [0, 0, 0],
>    [0, 1, 0],
>    [0, 0, 0]
> ];
>
> function preload() {
>    walkvid = createVideo("/vc/docs/sketches/walk.mp4");
>}
>
>function mousePressed() {
>    walkvid.loop();
>}
>
> function setup() {
>    createCanvas(640, 360);
>    walkvid.hide();
>    walkvid.volume(0);
>}
>
> function draw() {
>    walkvid.loadPixels();
>    loadPixels();
>    for (let x = 1; x < walkvid.width; x++) {
>        for (let y = 1; y < walkvid.height; y++) {
>            let c = convolution(x, y, kernel);
>            let index = 4 * (x + walkvid.width * y);
>            pixels[index] = red(c);
>            pixels[index + 1] = green(c);
>            pixels[index + 2] = blue(c);
>            pixels[index + 3] = alpha(c);
>        }
>    }
>    updatePixels();
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
>            if ((xpos >= 0 && xpos < walkvid.width) && (ypos >= 0 || ypos < walkvid.height)) {
>                let index = 4 * (xpos + walkvid.width * ypos);
>                r = walkvid.pixels[index];
>                g = walkvid.pixels[index + 1];
>                b = walkvid.pixels[index + 2];
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

> :P5 width=640, height=360
>
> let walkvid;
>
> let kernel = [
>    [1, 0, -1],
>    [0, 0, 0],
>    [-1, 0, 1]
> ];
>
> function preload() {
>    walkvid = createVideo("/vc/docs/sketches/walk.mp4");
>}
>
>function mousePressed() {
>    walkvid.loop();
>}
>
> function setup() {
>    createCanvas(640, 360);
>    walkvid.hide();
>    walkvid.volume(0);
>}
>
> function draw() {
>    walkvid.loadPixels();
>    loadPixels();
>    for (let x = 1; x < walkvid.width; x++) {
>        for (let y = 1; y < walkvid.height; y++) {
>            let c = convolution(x, y, kernel);
>            let index = 4 * (x + walkvid.width * y);
>            pixels[index] = red(c);
>            pixels[index + 1] = green(c);
>            pixels[index + 2] = blue(c);
>            pixels[index + 3] = alpha(c);
>        }
>    }
>    updatePixels();
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
>            if ((xpos >= 0 && xpos < walkvid.width) && (ypos >= 0 || ypos < walkvid.height)) {
>                let index = 4 * (xpos + walkvid.width * ypos);
>                r = walkvid.pixels[index];
>                g = walkvid.pixels[index + 1];
>                b = walkvid.pixels[index + 2];
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

> :P5 width=640, height=360
>
> let walkvid;
>
> let kernel = [
>    [-1, -1, -1],
>    [-1, 8, -1],
>    [-1, -1, -1]
> ];
>
> function preload() {
>    walkvid = createVideo("/vc/docs/sketches/walk.mp4");
>}
>
>function mousePressed() {
>    walkvid.loop();
>}
>
> function setup() {
>    createCanvas(640, 360);
>    walkvid.hide();
>    walkvid.volume(0);
>}
>
> function draw() {
>    walkvid.loadPixels();
>    loadPixels();
>    for (let x = 1; x < walkvid.width; x++) {
>        for (let y = 1; y < walkvid.height; y++) {
>            let c = convolution(x, y, kernel);
>            let index = 4 * (x + walkvid.width * y);
>            pixels[index] = red(c);
>            pixels[index + 1] = green(c);
>            pixels[index + 2] = blue(c);
>            pixels[index + 3] = alpha(c);
>        }
>    }
>    updatePixels();
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
>            if ((xpos >= 0 && xpos < walkvid.width) && (ypos >= 0 || ypos < walkvid.height)) {
>                let index = 4 * (xpos + walkvid.width * ypos);
>                r = walkvid.pixels[index];
>                g = walkvid.pixels[index + 1];
>                b = walkvid.pixels[index + 2];
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
