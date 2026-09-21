<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <title>Futbol Copero Haxball</title>
    <script src="https://cdn.jsdelivr.net/npm/phaser@3.60.0/dist/phaser.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/phaser3-plugin-virtual-joystick@1.0.3/dist/phaser3-plugin-virtual-joystick.min.js"></script>
    <style>
        body {
            margin: 0;
            padding: 0;
            background-color: #0d0d0d;
            color: #fff;
            font-family: Arial, sans-serif;
            overflow: hidden;
            touch-action: none;
        }
        #game-container {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }
    </style>
</head>
<body>

<div id="game-container"></div>

<script>
const config = {
    type: Phaser.AUTO,
    width: 1000,
    height: 600,
    parent: 'game-container',
    scale: {
        mode: Phaser.Scale.FIT,
        autoCenter: Phaser.Scale.CENTER_BOTH
    },
    physics: {
        default: 'arcade',
        arcade: {
            gravity: { y: 0 },
            debug: false
        }
    },
    scene: {
        preload: preload,
        create: create,
        update: update
    }
};

const game = new Phaser.Game(config);

let player, ball, rival;
let cursors, keys;
let joystick, kickButton;
let scoreRed = 0, scoreBlue = 0;
let textScore;
let isKickPressed = false;

function preload() {
    // Cargar plugin de joystick para celulares
    this.load.plugin('rexvirtualjoystickplugin', 'https://raw.githubusercontent.com/rexrainbow/phaser3-rex-notes/master/dist/rexvirtualjoystickplugin.min.js', true);
}

function create() {
    const scene = this;

    // --- DIBUJO DE LA CANCHA Y AMBIENTE COPERO ---
    const fieldGraphics = this.add.graphics();
    
    // Gradas / Tribunas
    fieldGraphics.fillStyle(0x1a1a1a, 1);
    fieldGraphics.fillRect(0, 0, 1000, 600);

    // Campo de Juego
    fieldGraphics.fillStyle(0x2e8b57, 1);
    fieldGraphics.fillRect(50, 50, 900, 500);

    // LÍNEAS DE LA CANCHA (Blanco Copero)
    fieldGraphics.lineStyle(4, 0xffffff, 0.9);
    fieldGraphics.strokeRect(50, 50, 900, 500); // Borde
    fieldGraphics.lineBetween(500, 50, 500, 550); // Medio campo
    fieldGraphics.strokeCircle(500, 300, 70); // Círculo central

    // Áreas
    fieldGraphics.strokeRect(50, 180, 120, 240);
    fieldGraphics.strokeRect(830, 180, 120, 240);

    // Porterías (Arcos)
    fieldGraphics.lineStyle(6, 0xffd700, 1); // Arcos Dorados Coperos
    fieldGraphics.strokeRect(30, 220, 20, 160); // Arco Izquierdo
    fieldGraphics.strokeRect(950, 220, 20, 160); // Arco Derecho

    // --- FÍSICAS DE LÍMITES Y PÓRTICOS ---
    const walls = this.physics.add.staticGroup();
    
    // Paredes superiores e inferiores
    createWall(walls, 500, 45, 900, 10);
    createWall(walls, 500, 555, 900, 10);
    // Paredes laterales (excepto el hueco del arco)
    createWall(walls, 45, 115, 10, 130);
    createWall(walls, 45, 485, 10, 130);
    createWall(walls, 955, 115, 10, 130);
    createWall(walls, 955, 485, 10, 130);
    // Fondo de los arcos
    createWall(walls, 20, 300, 10, 160);
    createWall(walls, 980, 300, 10, 160);

    // --- CREACIÓN DE JUGADORES Y PELOTA ---
    
    // Pelota (Haxball Style)
    const ballGraphics = this.add.graphics();
    ballGraphics.fillStyle(0xffffff, 1);
    ballGraphics.fillCircle(12, 12, 12);
    ballGraphics.lineStyle(2, 0x000000, 1);
    ballGraphics.strokeCircle(12, 12, 12);
    ballGraphics.generateTexture('ballTex', 24, 24);
    ballGraphics.destroy();

    ball = this.physics.add.sprite(500, 300, 'ballTex');
    ball.setCollideWorldBounds(true);
    ball.setBounce(0.85);
    ball.setDamping(true);
    ball.setDrag(0.985);
    ball.body.setCircle(12);

    // Jugador (Rojo - Local)
    player = createPlayer(this, 250, 300, 0xd90429, 'Jugador (Tú)');
    
    // Rival / Bot (Azul - Visitante)
    rival = createPlayer(this, 750, 300, 0x0077b6, 'Rival');

    // --- MARCADOR Y TEXTOS ---
    textScore = this.add.text(500, 25, '0 - 0', {
        font: 'bold 28px Arial',
        fill: '#ffffff',
        backgroundColor: '#000000',
        padding: { x: 15, y: 5 }
    }).setOrigin(0.5);

    this.add.text(500, 580, 'COPA LIBERTADORES HAXBALL', {
        font: '14px Arial',
        fill: '#ffd700'
    }).setOrigin(0.5);

    // --- COLISIONES ---
    this.physics.add.collider(player, walls);
    this.physics.add.collider(rival, walls);
    this.physics.add.collider(ball, walls);
    this.physics.add.collider(player, rival);
    
    this.physics.add.collider(player, ball, hitBall, null, this);
    this.physics.add.collider(rival, ball, hitBall, null, this);

    // --- CONTROLES TECLADO (PC) ---
    cursors = this.input.keyboard.createCursorKeys();
    keys = this.input.keyboard.addKeys({
        up: Phaser.Input.Keyboard.KeyCodes.W,
        down: Phaser.Input.Keyboard.KeyCodes.S,
        left: Phaser.Input.Keyboard.KeyCodes.A,
        right: Phaser.Input.Keyboard.KeyCodes.D,
        kick: Phaser.Input.Keyboard.KeyCodes.SPACE
    });

    // --- CONTROLES TÁCTILES (MÓVIL) ---
    if (this.sys.game.device.input.touch) {
        // Joystick analógico
        joystick = this.plugins.get('rexvirtualjoystickplugin').add(this, {
            x: 120,
            y: 480,
            radius: 50,
            base: this.add.circle(0, 0, 50, 0x888888, 0.5),
            thumb: this.add.circle(0, 0, 25, 0xcccccc, 0.8)
        });

        // Botón de Tiro / Patada
        kickButton = this.add.circle(880, 480, 40, 0xd90429, 0.7)
            .setInteractive()
            .setScrollFactor(0);
            
        this.add.text(880, 480, 'PATADA', { font: 'bold 12px Arial', fill: '#fff' }).setOrigin(0.5);

        kickButton.on('pointerdown', () => { isKickPressed = true; });
        kickButton.on('pointerup', () => { isKickPressed = false; });
    }
}

function update() {
    // --- MOVIMIENTO DEL JUGADOR ---
    let speed = 220;
    player.body.setVelocity(0);

    // Entrada por Teclado
    if (keys.left.isDown || cursors.left.isDown) player.body.setVelocityX(-speed);
    else if (keys.right.isDown || cursors.right.isDown) player.body.setVelocityX(speed);

    if (keys.up.isDown || cursors.up.isDown) player.body.setVelocityY(-speed);
    else if (keys.down.isDown || cursors.down.isDown) player.body.setVelocityY(speed);

    // Entrada por Joystick (Celular)
    if (joystick && joystick.force > 0) {
        this.physics.velocityFromAngle(joystick.angle, Math.min(joystick.force, speed), player.body.velocity);
    }

    // --- INTELIGENCIA ARTIFICIAL SIMPLE PARA EL RIVAL ---
    let rivalSpeed = 160;
    if (ball.x > 400) {
        this.physics.moveToObject(rival, ball, rivalSpeed);
    } else {
        this.physics.moveTo(rival, 750, 300, rivalSpeed);
    }

    // --- VERIFICAR GOLES ---
    if (ball.x < 35 && ball.y > 220 && ball.y < 380) {
        goalScored('Blue');
    } else if (ball.x > 965 && ball.y > 220 && ball.y < 380) {
        goalScored('Red');
    }
}

// --- FUNCIONES AUXILIARES ---

function createPlayer(scene, x, y, color, name) {
    const pGraphics = scene.add.graphics();
    pGraphics.fillStyle(color, 1);
    pGraphics.fillCircle(20, 20, 20);
    pGraphics.lineStyle(3, 0xffffff, 1);
    pGraphics.strokeCircle(20, 20, 20);
    pGraphics.generateTexture('player_' + color, 40, 40);
    pGraphics.destroy();

    const p = scene.physics.add.sprite(x, y, 'player_' + color);
    p.setCollideWorldBounds(true);
    p.setBounce(0.2);
    p.setDamping(true);
    p.setDrag(0.90);
    p.body.setCircle(20);
    
    return p;
}

function createWall(group, x, y, w, h) {
    const wall = group.create(x, y, null);
    wall.setSize(w, h);
    wall.setVisible(false);
}

function hitBall(playerObj, ballObj) {
    // Si se presiona ESPACIO o el Botón Táctil, se simula el chuto/patada estilo Haxball
    if (keys.kick.isDown || isKickPressed) {
        let angle = Phaser.Math.Angle.Between(playerObj.x, playerObj.y, ballObj.x, ballObj.y);
        ballObj.body.setVelocity(
            Math.cos(angle) * 550,
            Math.sin(angle) * 550
        );
    }
}

function goalScored(team) {
    if (team === 'Red') scoreRed++;
    else scoreBlue++;

    textScore.setText(`${scoreRed} - ${scoreBlue}`);
    
    // Efecto Copero: Pausa y reinicio
    ball.setPosition(500, 300);
    ball.body.setVelocity(0, 0);
    player.setPosition(250, 300);
    player.body.setVelocity(0, 0);
    rival.setPosition(750, 300);
    rival.body.setVelocity(0, 0);
}
</script>
</body>
</html>
