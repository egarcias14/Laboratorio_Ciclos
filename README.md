# Laboratorio_Ciclos
function setup() {
  createCanvas(400, 400);
  fill(255);
  noStroke()
 
}
let num=0;
let b=0;

let snowflakes = [];
function draw() {
  //Este contador sera util para el parpadeo de la luz amarilla
  b=b+1;
  background(135, 206, 235);
  (num<=500);{ num=num+1; console.log(num); }
  fill(0);
  rect(width/2-75, height/2-155, 150,350);
  //Luz roja
  if(num<=150){
  fill(255, 0, 0);
    ellipse(width/2, height/2-100,100,100);
  }
  //Luz amarilla
  if(num<=300 && num>=150){
    for(let i=0;i< 15;i++){
    fill(255, 255, 0);
    //parpadeo 
     if(b%20==0){
    ellipse(width/2, height/2,100,100);
  }
}
  }
  //luz verde
  if(num>305){
  fill(0, 128, 0);
    ellipse(width/2, height/2+100,100,100);
  }
  //lineas a los lados del semáforo
  fill(51);
  y = 40;
  for (let a = 0; a < num; a++) {
    rect(width/2+75, y, 30, 10);
    rect(width/2-100, y, 30, 10);
    y += 20;
  }
  //Ejemplod e nieve
  //Tiempo en que cae la nieve
  let t = frameCount / 60; 

  //Copos de nieve
  for (let i = 0; i < random(5); i++) {
    snowflakes.push(new snowflake()); 
  }

  for (let flake of snowflakes) {
    flake.update(t);
    flake.display();
  }
}

function snowflake() {
  //Coordenadas
  this.posX = 0;
  this.posY = random(-50, 0);
  this.initialangle = random(0, 2 * PI);
  this.size = random(2, 5);
//La nieve cae uniforme
  this.radius = sqrt(random(pow(width / 2, 2)));

  this.update = function(time) {
    let w = 0.6; 
    let angle = w * time + this.initialangle;
    this.posX = width / 2 + this.radius * sin(angle);
   
    this.posY += pow(this.size, 0.5);

    if (this.posY > height) {
      let index = snowflakes.indexOf(this);
      snowflakes.splice(index, 1);
    }
  };

  this.display = function() {
    ellipse(this.posX, this.posY, this.size);
  };

}
