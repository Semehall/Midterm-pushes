# Midterm-pushes

let angle = 0;
let stars = [];
let speed;

function setup() {
  createCanvas(windowWidth, windowHeight);
  for (let i = 0; i < 300; i++) {
    stars[i] = new Star();
  }
}

function draw() {
  background(0);
  speed = map(mouseX, 0, width, 0, 10);

  //starfield
  push();
  translate(width / 2, height / 2);
  for (let i = 0; i < stars.length; i++) {
    stars[i].update();
    stars[i].show();
  }
  pop();

  // person representation
  push();
  translate(mouseX, mouseY);
  angleMode(DEGREES);
  rotate(angle);

  //person shape
  stroke(255);
  fill(200);

  // Head
  ellipse(0, -50, 30, 30);

  // Body
  line(0, -35, 0, 30);

  // Arms
  line(0, -20, -20, 10);
  line(0, -20, 20, 10);

  // Legs
  line(0, 30, -15, 60);
  line(0, 30, 15, 60);

  pop();

  // Increment the angle over time
  angle += 0.8;
}

class Star {
  constructor() {
    this.x = random(-width, width);
    this.y = random(-height, height);
    this.z = random(width);
    this.pz = this.z;
  }

  update() {
    this.z = this.z - speed;
    if (this.z < 1) {
      this.z = width;
      this.x = random(-width, width);
      this.y = random(-height, height);
      this.pz = this.z;
    }
  }

  show() {
    fill(255);
    noStroke();

    let sx = map(this.x / this.z, 0, 1, 0, width);
    let sy = map(this.y / this.z, 0, 1, 0, height);

    let r = map(this.z, 0, width, 16, 0);
    ellipse(sx, sy, r, r);

    let px = map(this.x / this.pz, 0, 1, 0, width);
    let py = map(this.y / this.pz, 0, 1, 0, height);

    this.pz = this.z;

    stroke(255);
    line(px, py, sx, sy);
  }
}
