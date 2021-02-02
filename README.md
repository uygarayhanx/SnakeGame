# SnakeGame
Hi guys today we create a game called "snake game" with javascript
Codes:
            class SnakeGame {
                constructor() {
                    this.canvas = document.getElementById("oyun");
                    this.context = this.canvas.getContext("2d");
                    document.addEventListener("keydown", this.onKeyPress.bind(this));
                }
                init() {
                    this.positionX = this.positionY = 10;
                    this.appleX = this.appleY = 5;
                    this.tailsize = 5;
                    this.trail = [];
                    this.gridSize = this.tileCount = 20;
                    this.velocityX = this.velocityY = 0;
                    this.timer = setInterval(this.loop.bind(this), 1000 / 15);
                }
                reset() {
                    clearInterval(this.timer);
                    this.init();
                }
                loop() {
                    this.update();
                    this.draw();
                }
                update() {
                    this.positionX += this.velocityX;
                    this.positionY += this.velocityY;
                    if (this.positionX < 0) {
                        this.positionX = this.tileCount -1;
                    }
                    else if (this.positionY < 0) {
                        this.positionY = this.tileCount -1;
                    }
                    else if (this.positionX > this.tileCount -1) {
                        this.positionX = 0;
                    }
                    else if (this.positionY > this.tileCount -1) {
                        this.positionY = 0;
                    }
                
               this.trail.forEach(t => {
                   if (this.positionX === t.positionX && this.positionY === t.positionY) {
                       this.reset();
                   }
               });
               this.trail.push({positionX: this.positionX, positionY: this.positionY});
               while (this.trail.length > this.tailsize) {
                   this.trail.shift();
               }
               if (this.appleX === this.positionX && this.appleY === this.positionY) {
                   this.tailsize++;
                   this.appleX = Math.floor(Math.random() * this.tileCount);
                   this.appleY = Math.floor(Math.random() * this.tileCount);
               }
            }
            draw() {
                this.context.fillStyle = "grey";
                this.context.fillRect(0, 0, this.canvas.width, this.canvas.height);
                this.context.fillStyle = "black";
                this.context.font = "20px Arial";
                this.context.fillText(this.tailsize - 5, 20, 40);
                this.context.fillStyle = "Aqua";
                this.trail.forEach(t => {
                    this.context.fillRect(t.positionX * this.gridSize, t.positionY * this.gridSize, this.gridSize -5, this.gridSize -5);
                });
                this.context.fillStyle = "red";
                this.context.fillRect(this.appleX * this.gridSize, this.appleY * this.gridSize, this.gridSize -5, this.gridSize -5);
            }
            onKeyPress(e) {
                if (e.keyCode === 37 && this.velocityX !== 1) {
                    this.velocityX = -1;
                    this.velocityY = 0;
                }
                else if (e.keyCode === 38 && this.velocityY !== 1) {
                    this.velocityX = 0;
                    this.velocityY = -1;
                }
                else if (e.keyCode === 39 && this.velocityX !== -1) {
                    this.velocityX = 1;
                    this.velocityY = 0;
                }
                else if (e.keyCode === 40 && this.velocityY !== -1) {
                    this.velocityX = 0,
                    this.velocityY = 1;
                }
            }
            }
            const game = new YılanOyun();
            window.onload = () => game.init();

