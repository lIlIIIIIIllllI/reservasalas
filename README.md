<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Gestión de Salas de Reservación</title>
    <style>

        body {
            background: linear-gradient(#ff0000, #ec4242, #fa6868) ;
            font-family: Arial, sans-serif;
            
        }
        
        .container {
            max-width: 500px;
            margin: 0 auto;
            padding: 20px;
            border: 30px solid rgba(91, 7, 7, 0.8);
            border-radius: 100px;
            
        }
        h1 {
            text-align: center;

        }
        .button {
           background-color: rgb(255, 255, 255);
            margin: 10px 0;
            padding: 40px;
            width: 100%;
            cursor: pointer;
            font-size: 30px;
            border-radius: 100px;
        }

    div{
        
        text-align: center;
        font-size: 20px;
    }
    </style>
</head>
<body>
    <div class="container">
        <h1>Gestión de Salas de Reservación</h1>
        <button class="button" onclick="mostrarSalasDisponibles()">Ver Salas Disponibles</button>
        <button class="button" onclick="reservarSala()">Reservar Sala</button>
        <button class="button" onclick="liberarSala()">Liberar Sala</button>
        <div id="resultado"></div>
    </div>

    <script>
        class SalaDeReservacion {
            constructor(capacidad) {
                this.capacidad = capacidad;
                this.reservado = false;
            }
        
            reservar() {
                if (!this.reservado) {
                    this.reservado = true;
                    return true;
                }
                return false;
            }
        
            liberar() {
                if (this.reservado) {
                    this.reservado = false;
                    return true;
                }
                return false;
            }
        }
        
        class SalaDeReservacionManager {
            constructor(num_salas) {
                this.salas = Array.from({ length: num_salas }, () => new SalaDeReservacion());
            }
        
            mostrarSalasDisponibles() {
                return this.salas.map((sala, index) => !sala.reservado ? index + 1 : null).filter(index => index !== null);
            }
        
            reservarSala(num_sala) {
                return num_sala >= 1 && num_sala <= this.salas.length && this.salas[num_sala - 1].reservar();
            }
        
            liberarSala(num_sala) {
                return num_sala >= 1 && num_sala <= this.salas.length && this.salas[num_sala - 1].liberar();
            }
        }
        
        const manager = new SalaDeReservacionManager(5);
        
        function mostrarSalasDisponibles() {
            const disponibles = manager.mostrarSalasDisponibles();
            document.getElementById('resultado').innerHTML = 'Salas disponibles: ' + disponibles.join(', ');
        }
        
        function reservarSala() {
            const num_sala = parseInt(prompt("Ingrese el número de la sala que desea reservar:"));
            if (manager.reservarSala(num_sala)) {
                document.getElementById('resultado').innerHTML = 'Sala ' + num_sala + ' reservada con éxito.';
            } else {
                document.getElementById('resultado').innerHTML = 'La sala no está disponible.';
            }
        }
        
        function liberarSala() {
            const num_sala = parseInt(prompt("Ingrese el número de la sala que desea liberar:"));
            if (manager.liberarSala(num_sala)) {
                document.getElementById('resultado').innerHTML = 'Sala ' + num_sala + ' liberada con éxito.';
            } else {
                document.getElementById('resultado').innerHTML = 'La sala no está reservada.';
            }
        }
        
    </script>
</body>
</html>
