<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
<link rel="stylesheet" href="style.css">
<script src="script.js"></script>
<title>TRES EN RAYA GPT</title>
</head>
<body>
<div class="contenedor-juego">
  <div class="juego-titulo">
    <h2>TRES EN RAYA: GPT</h2>
  </div>
  <p id="juego-info" class="juego-info"></p>
  <div class="juego-cuadricula">
    <div class="cuadro"></div>
    <div class="cuadro"></div>
    <div class="cuadro"></div>
    <div class="cuadro"></div>
    <div class="cuadro"></div>
    <div class="cuadro"></div>
    <div class="cuadro"></div>
    <div class="cuadro"></div>
    <div class="cuadro"></div>
  </div>
  <div id="juego-boton" class="juego-boton">VOLVER A JUGAR</div>
</div>
</body>
</html>


*{ 
margin: 0;
}

.contenedor-juego {
  width: 400px;
  height: 430px;
  margin: 0 auto;
  text-align: center;
  color: white;
  font-size:65px;
  font-family:helvetica;
  padding: 20px;
  margin-bottom: 5px;
  border-radius: 15px;
  background: darkcyan;
  margin-top: 1px;
  border: 3px solid silver;
  box-shadow: 6px 5px darkgray;
}

.juego-titulo h2 {
  font-size: 30px;
  color: white;
  font-family: helvetica;
  text-shadow: 1.5px 1.5px black;
}

.juego-info {
  font-size: 18px;
  margin-button: 1px;
  padding: 0px;
  color: black;
}

.juego-cuadricula {
  margin-left: 15px; 
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  padding: 30px;
  grid-gap: 30px;
}

.cuadro {
  width: 70px;
  height: 72px;
  margin-button: 1px;
  background-color: orange;
  border: 1.5px solid black;
  box-shadow: 3px 5px black;
}

.juego-boton {
  margin-top: 1px;
  padding: 8px 15px;
  background-color: black;
  font-size: 12px;
  color: white;
  text-shadow: 1.5px 1.5px black;
  cursor: pointer;
  border: 1.5px solid silver;
  box-shadow: 2px 2px black;
}
 
.juego-titulo h2:hover {
  color: yellow;
  cursor: pointer;
}

.cuadro:hover {
  color:yellow;
  background-color: darkred;
  cursor: pointer;
  border: 1.5px solid yellow;
}

.juego-boton:hover {
  color: yellow;
  background-color: darkred;
  cursor: pointer;
  border: 1.5px solid yellow;
}


(function() {
  'use strict';

})();

// Obtener las referencias a los elementos del DOM
var juegoCuadricula = document.querySelector('.juego-cuadricula');
var cuadros = juegoCuadricula.querySelectorAll('.cuadro');
var juegoInfo = document.getElementById('juego-info');
var juegoBoton = document.getElementById('juego-boton');

// Variables de estado del juego
var jugadorActual = 'X';
var juegoTerminado = false;

// Función para reiniciar el juego
function reiniciarJuego() {
  jugadorActual = 'X';
  juegoTerminado = false;
  juegoInfo.textContent = '';
  cuadros.forEach(function(cuadro) {
    cuadro.textContent = '';
    cuadro.classList.remove('ocupado');
    cuadro.addEventListener('click', marcarCuadro);
  });
}

// Función para marcar un cuadro
function marcarCuadro(event) {
  var cuadro = event.target;
  if (!juegoTerminado && !cuadro.classList.contains('ocupado')) {
    cuadro.textContent = jugadorActual;
    cuadro.classList.add('ocupado');
    if (hayGanador()) {
      juegoTerminado = true;
      juegoInfo.textContent = '¡EL JUGADOR  ' + jugadorActual + ' GANÓ!';
    } else if (hayEmpate()) {
      juegoTerminado = true;
      juegoInfo.textContent = '¡EMPATE!';
    } else {
      jugadorActual = jugadorActual === 'X' ? 'O' : 'X';
    }
  }
}

// Función para verificar si hay un ganador
function hayGanador() {
  var lineasGanadoras = [
    [0, 1, 2], [3, 4, 5], [6, 7, 8], // Filas
    [0, 3, 6], [1, 4, 7], [2, 5, 8], // Columnas
    [0, 4, 8], [2, 4, 6] // Diagonales
  ];

  for (var i = 0; i < lineasGanadoras.length; i++) {
    var linea = lineasGanadoras[i];
    var a = linea[0], b = linea[1], c = linea[2];
    if (
      cuadros[a].textContent &&
      cuadros[a].textContent === cuadros[b].textContent &&
      cuadros[a].textContent === cuadros[c].textContent
    ) {
      return true;
    }
  }

  return false;
}

// Función para verificar si hay un empate
function hayEmpate() {
  for (var i = 0; i < cuadros.length; i++) {
    if (!cuadros[i].classList.contains('ocupado')) {
      return false;
    }
  }
  return true;
}

// Event listener para el botón "Volver a jugar"
juegoBoton.addEventListener('click', reiniciarJuego);

// Iniciar el juego
reiniciarJuego();
