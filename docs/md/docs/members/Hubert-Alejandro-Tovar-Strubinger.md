# Hubert Alejandro Tovar Strubinger

## Bio

Systems engineering student currently at 8th semester, looking forward to learn
the basics of computer vision so it will be easy to determine a career specialization.

## Interests

Software Architecture mostly backend, Artificial Intelligence
and game development.

## Contributions

Other works: I worked on small software developing proyects that usually include
web services, micro-services and movile aplications.

Page: I helped with the concepts of image procesing for the first activities and
upploaded a gif in this current section.

## Hobbies

Video Games, TV series, Movies...

## Optical illusion

> :P5 width=777, height=437
> 
>  let numFrames = 36;  // The number of frames in the animation
> let currentFrame = 0;
> let images = [];
>    
> function setup() {
>   createCanvas(777, 437);
>   frameRate(24);
>  
>   // If you don't want to load each image separately
>   // and you know how many frames you have, you
>   // can create the filenames as the program runs.
>   // The nf() command does number formatting, which will
>   // ensure that the number is (in this case) 4 digits.
>   for (let i = 0; i < numFrames; i++) {
>     let imageName = "/vc/docs/sketches/frame (" + i + ").jpg";
>     images[i] = loadImage(imageName);
>   }
> } 
> 
> function draw() { 
>   background(0);
>   currentFrame = (currentFrame+1) % numFrames;  // Use % to cycle through frames
>   let offset = 0;
>   for (let x = -100; x < width; x += images[0].width) { 
>     image(images[(currentFrame+offset) % numFrames], 0, 0);
>     offset+=2;
>   }
> }

