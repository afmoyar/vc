<style TYPE="text/css">
code.has-jax {font: inherit; font-size: 100%; background: inherit; border: inherit;}
</style>
<script type="text/x-mathjax-config">
MathJax.Hub.Config({
    tex2jax: {
        inlineMath: [['$','$'], ['\\(','\\)']],
        skipTags: ['script', 'noscript', 'style', 'textarea', 'pre'] // removed 'code' entry
    }
});
MathJax.Hub.Queue(function() {
    var all = MathJax.Hub.getAllJax(), i;
    for(i = 0; i < all.length; i += 1) {
        all[i].SourceElement().parentNode.className += ' has-jax';
    }
});
</script>
<script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.4/MathJax.js?config=TeX-AMS_HTML-full"></script>

# Gama de grises usando Luma

Mediante el canvas 3d que proporciona WEBGL se genera una figura rectangular a partir de cuatro vértices. Esta figura va a servir como "marco" para contener la imagen que se quiere mostrar. La imagen se define como una textura que se va aplicar al rectángulo.

Al igual que el anterior metodo de RGB aqui usamos la variable varying vTexCoord  para poder acceder a las coordenadas, y posteriormente el color de cada texel de la imagen y luego poder operar sobre él haciendo un promedio ponderado en el primer de los casos con la fórmula \\[ r * 0.299 + g * 0.587 + b * 0.0114 \\] de los valores de cada canal rgb y asignándoselo al fragmento (pixel) correspondiente y luego en el LUMA normalizado usando \\[ r' * 0.299 + g' * 0.587 + b' * 0.0114 \\] dónde \\[ r' = 255 * ( \frac{r}{255}) ^ {1/2.2} \\] \\[ g' = 255 * ( \frac{g}{255}) ^ {1/2.2} \\] \\[ b' = 255 * ( \frac{b}{255}) ^ {1/2.2} \\].

> :Tabs
> > :Tab title=Luma Ponderado
> > >
> > > :P5 sketch=/docs/sketches/LumaShader/Luma_Ponderado/TextureShader.js, width=400, height=400
> 
> > :Tab title=Luma Normalizado
> > >
> > > :P5 sketch=/docs/sketches/LumaShader/Luma_Normalizado/TextureShader.js, width=400, height=400
> >

> :ToCPrevNext
