    //<one line to give the program's name and a brief idea of what it does.>
    //Copyright (C) <2025>  <SJoerd van Kampen / zzeevonkk>

    //This program is free software: you can redistribute it and/or modify
    //it under the terms of the GNU General Public License as published by
    //the Free Software Foundation, either version 3 of the License, or
    //(at your option) any later version.

    //This program is distributed in the hope that it will be useful,
    //but WITHOUT ANY WARRANTY; without even the implied warranty of
    //MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
    //GNU General Public License for more details.

    //You should have received a copy of the GNU General Public License
    //along with this program.  If not, see <https://www.gnu.org/licenses/>.

import controlP5.*;
ControlP5 cp5;
PFont font;

//landscape values
float sandValue = 0;
float groundValue = 0;
float groundValue2 = 0;
float groundValue3 = 0;
float groundValue4 = 0;

// sun values
float sunX = -0.1;
float sunY = -0.1;

// cloud values
float cloudSpeed = 0.005;
float cloudAmount = 0.65;

// terrain vague #075263,#5CB2BE,#FEEEC0,#FF8D32,#F26916

int tileSize = 5;
float nScl = 0.03;
PGraphics pg;
float forw, wforw;

void setup() {
  size(900, 900);
  font = createFont("IBMPlexMono-Bold.otf", 18);
  float x1 = random(width/tileSize*0.25, width/tileSize*0.50);
  float y1 = random(height/tileSize*0.25, height/tileSize*0.50);
  float x2 = random(width/tileSize*0.50, width/tileSize*0.75);
  float y2 = random(height/tileSize*0.25, height/tileSize*0.50);
  float x3 = random(width/tileSize*0.50, width/tileSize*0.75);
  float y3 = random(height/tileSize*0.5, height/tileSize*0.75);
  float x4 = random(width/tileSize*0.25, width/tileSize*0.50);
  float y4 = random(height/tileSize*0.5, height/tileSize*0.75);
  pg = createGraphics(width/tileSize, height/tileSize);
  noStroke();
  pg.beginDraw();
  pg.background(0);
  pg.noStroke();
  pg.fill(200);
  pg.textFont(font);
  pg.textAlign(CENTER);
  pg.text("island generator",pg.width/2,pg.width/2);
  pg.text("press space",pg.width/2,pg.height*0.75);
  pg.filter(BLUR, 0.1);
  pg.endDraw();

  // sliders island
  cp5 = new ControlP5(this);
  cp5.addSlider("sandValue")
    .setPosition(50, 50)
    .setRange(0.2, 0.4)
    .setSize(200, 20)
    .setLabel("sand")
    ;
  cp5.addSlider("groundValue")
    .setPosition(50, 75)
    .setRange(0.3, 0.5)
    .setSize(200, 20)
    .setLabel("ground 1")
    ;
  cp5.addSlider("groundValue2")
    .setPosition(50, 100)
    .setRange(0.4, 0.6)
    .setSize(200, 20)
    .setLabel("ground 2")
    ;
  cp5.addSlider("groundValue3")
    .setPosition(50, 125)
    .setRange(0.5, 0.7)
    .setSize(200, 20)
    ;
  cp5.addSlider("groundValue4")
    .setPosition(50, 150)
    .setRange(0.7, 0.9)
    .setSize(200, 20)
    ;

  //sliders sun
  cp5.addSlider("sunX")
    .setPosition(50, 850)
    .setRange(-0.2, 0.2)
    .setSize(200, 20)
    .setLabel("sun X")
    ;
  cp5.addSlider("sunY")
    .setPosition(50, 600)
    .setRange(-0.2, 0.2)
    .setSize(20, 200)
    .setLabel("sun Y")
    ;

  //sliders clouds
  cp5.addSlider("cloudSpeed")
    .setPosition(600, 50)
    .setRange(0.001, 0.01)
    .setSize(200, 20)
    .setLabel("cloud speed")
    ;
  cp5.addSlider("cloudAmount")
    .setPosition(600, 75)
    .setRange(0.5, 0.8)
    .setSize(200, 20)
    .setLabel("cloud amount")
    ;

  // hide controls
  cp5.hide();
}

void draw() {
  background(#075263);
  forw += cloudSpeed;
  wforw += 0.01;
  // water waves
  for (int i = 0; i < width/tileSize; i++) {
    for (int j = 0; j < height/tileSize; j++) {
      color c = pg.get(i, j);
      float b = -0.32+brightness(c)*0.01;
      float n = (noise(i*nScl+wforw, j*nScl+forw) + noise(i*nScl-wforw, j*nScl-forw))*2;
      float wave = map(sin(radians(frameCount*2-i*20-j*20)), 0, 1, 0.001, 0.002);
      float combo = (b*2+n*0.15+wave*30)*30;
      fill(#5CB2BE, 50*combo);
      rect(i*tileSize, j*tileSize, tileSize, tileSize);
    }
  }

  //island
  for (int i = 0; i < width/tileSize; i++) {
    for (int j = 0; j < height/tileSize; j++) {
      fill(getColor(i, j));
      rect(i*tileSize, j*tileSize, tileSize, tileSize);
    }
  }

  ////island shadows
  //for (int i = 0; i < width/tileSize; i++) {
  //  for (int j = 0; j < height/tileSize; j++) {
  //    fill(getShadows(i, j));
  //    rect(i*tileSize, j*tileSize, tileSize, tileSize);
  //  }
  //}

  //cloud shadows
  for (int i = 0; i < width/tileSize; i++) {
    for (int j = 0; j < height/tileSize; j++) {
      //float b = -2.2+(noise(i*nScl+forw, j*nScl) + noise(i*nScl-forw, j*nScl))*2;

      fill(getCloudShadows(i, j));
      rect(i*tileSize, j*tileSize, tileSize, tileSize);
    }
  }

  //clouds
  for (int i = 0; i < width/tileSize; i++) {
    for (int j = 0; j < height/tileSize; j++) {
      //float b = -2.2+(noise(i*nScl+forw, j*nScl) + noise(i*nScl-forw, j*nScl))*2;

      fill(getClouds(i, j));
      rect(i*tileSize, j*tileSize, tileSize, tileSize);
    }
  }
  //image(pg, 0, 0);
}

void keyPressed() {
  if (key == ' ') {
    float x1 = random(width/tileSize*0.25, width/tileSize*0.50);
    float y1 = random(height/tileSize*0.25, height/tileSize*0.50);
    float x2 = random(width/tileSize*0.50, width/tileSize*0.75);
    float y2 = random(height/tileSize*0.25, height/tileSize*0.50);
    float x3 = random(width/tileSize*0.50, width/tileSize*0.75);
    float y3 = random(height/tileSize*0.5, height/tileSize*0.75);
    float x4 = random(width/tileSize*0.25, width/tileSize*0.50);
    float y4 = random(height/tileSize*0.5, height/tileSize*0.75);
    noiseSeed(millis());
    pg.beginDraw();
    pg.background(0);
    pg.noStroke();
    pg.fill(255);
    pg.quad(x1, y1, x2, y2, x3, y3, x4, y4);
    pg.filter(BLUR, 30);
    pg.endDraw();
  }
  cp5.show();
}

color getColor(int x, int y) {
  color c = pg.get(x, y);
  float b = brightness(c);
  float v = (b*0.02)*noise(x*nScl, y*nScl);
  if (v < sandValue) {
    // water
    //return color(#5CB2BE);
    return color(255, 0);
  } else if (v < groundValue) {
    // sand
    return color(#FEEEC0);
  } else if (v < groundValue2) {
    // grass
    return color(#FF8D32);
  } else if (v < groundValue3) {
    // forest
    return color(#F26916);
  } else if (v < groundValue4) {
    // forest
    return color(#2A5C0B);
  } else {
    // forest
    return color(120);
  }
}

color getShadows(int x, int y) {
  color c = pg.get(x, y);
  float b = brightness(c);
  float v = (b*0.04)*noise(sunX-x*nScl, sunY+y*nScl)-(b*0.04)*noise(x*nScl, y*nScl);
  if (v < sandValue) {
    // water
    //return color(#5CB2BE);
    return color(1, 0);
  } else if (v < groundValue) {
    // sand
    return color(1, 50);
  } else if (v < groundValue2) {
    // grass
    return color(1, 50);
  } else if (v < groundValue3) {
    // forest
    return color(1, 50);
  } else if (v < groundValue4) {
    // forest
    return color(1, 50);  
  } else {
    // forest
    return color(1, 0);
  }
}

color getCloudShadows(int x, int y) {
  float v = (noise(sunX-x*nScl+forw, sunY+y*nScl) + noise(sunX-x*nScl-forw, sunY+y*nScl))/2;
  if (v < cloudAmount) {
    // water
    return color(1, 0);
  } else {
    // forest
    return color(1, 50);
  }
}

color getClouds(int x, int y) {
  float v = (noise(x*nScl+forw, y*nScl) + noise(x*nScl-forw, y*nScl))/2;
  if (v < cloudAmount) {
    // water
    return color(1, 0);
  } else if (v < 0.075 + cloudAmount) {
    // sand
    return color(150);
  } else {
    // forest
    return color(200);
  }
}
