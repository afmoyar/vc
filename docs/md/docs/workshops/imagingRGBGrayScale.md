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

> :ToCPrevNext