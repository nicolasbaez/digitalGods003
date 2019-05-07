# digitalGods003
Jugando con luz!

![digitalGods](https://github.com/nicolasbaez/digitalGods003/blob/master/portada.png)

1. gameDev.htm
```html
<html>
    <script src="p5.js">
        //Descarga: https://cdnjs.cloudflare.com/ajax/libs/p5.js/0.8.0/p5.js
    </script>
    <script src="p5.dom.js">
        //Descarga: https://raw.githubusercontent.com/lmccart/p5.js/master/lib/addons/p5.dom.js
    </script>
    <script src="digitalGods.js">
        //Nuestro juego de video
    </script>
    <body style="margin:0;">
    </body>
</html>
```
2. digitalGods.js
```javascript
//variables
//variables
var nEdificios=128;
var pisosEdificio=64;
var wEdificios=[];
var hEdificios=[];
var pEdificios=[];
var xStars=[];
var yStars=[];
var dStars=[];
var txLight=[];
function setup(){
	createCanvas(window.innerWidth,window.innerHeight);
	background(0);
	for(var i=0;i<nEdificios;i++){
		wEdificios[i]=random(width*0.02,width*0.04);
		hEdificios[i]=random(height*0.25,height*0.75);
		xStars[i]=random(width);
		yStars[i]=random(height);
		dStars[i]=random(4);
		pEdificios[i]=random(pisosEdificio)+1;
		txLight[i]=random(192);
	}
}
function atardecer(){
	for(var i=0;i<=height;i++){
		//rr,gg,bb
		stroke(
			map(i,0,height,map(mouseX,0,width,0,0),map(mouseX,0,width,255,255)),
			map(i,0,height,map(mouseX,0,width,153,0),map(mouseX,0,width,255,102)),
			map(i,0,height,map(mouseX,0,width,255,0),map(mouseX,0,width,255,0)),
		);
		line(0,i,width,i);
	}
}
function draw(){
	atardecer();
	var dx=0;
	for(var i=0;i<nEdificios;i++){
		fill(255,255,255,map(mouseX,0,width,0,255));
		noStroke();
		ellipse(xStars[i],yStars[i],dStars[i],dStars[i]);
	}
	for(var i=0;i<nEdificios;i++){
		noStroke();
		fill(map(mouseX,0,width,32,0));
		rect(dx,height-hEdificios[i],wEdificios[i],hEdificios[i]);
		stroke(
			map(mouseX,0,width,255,255),
			map(mouseX,0,width,255,102),
			map(mouseX,0,width,255,0)
		);
		line(dx,height-hEdificios[i],dx+wEdificios[i],height-hEdificios[i]);
		for(var j=height-hEdificios[i];j<=hEdificios[i];j+=hEdificios[i]/pEdificios[i]){
			stroke(map(mouseX,0,width,64,0));
			fill(0,255,255,map(mouseX,0,width,0,txLight[i]));
			rect(dx,j,wEdificios[i],hEdificios[i]/pEdificios[i]);
		}
		dx+=width*0.02;
	}
}
```
