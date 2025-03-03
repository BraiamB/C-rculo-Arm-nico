<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Círculo Armónico Basico</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            background-color: #000;
            color: #fff;
            padding: 20px;
        }
        .container {
            display: flex;
            justify-content: center;
            flex-wrap: wrap;
            gap: 20px;
        }
        .box {
            background: #fff;
            color: #000;
            padding: 15px;
            border-radius: 10px;
            box-shadow: 0px 0px 10px rgba(255, 255, 255, 0.2);
            width: 300px;
            text-align: center;
        }
        select, button {
            padding: 10px;
            font-size: 16px;
            margin: 5px;
            background: #fff;
            color: #000;
            border: 2px solid #000;
            border-radius: 5px;
            cursor: pointer;
        }
        button:hover {
            background: #000;
            color: #fff;
        }
        .acordes-container {
            display: flex;
            justify-content: center;
            flex-wrap: wrap;
            margin-top: 20px;
        }
        .acorde {
            padding: 10px;
            margin: 5px;
            font-size: 18px;
            font-weight: bold;
            border-radius: 5px;
            background: #fff;
            color: #000;
            border: 2px solid #000;
            min-width: 80px;
            text-align: center;
            cursor: pointer;
        }
        .acorde:hover {
            background: #000;
            color: #fff;
        }
        #detalleAcorde {
            margin-top: 20px;
            font-size: 20px;
            font-weight: bold;
            color: #fff;
        }
    </style>
</head>
<body>

    <h2>Círculo Armónico Completo</h2>

    <div class="container">
        <div class="box">
            <h3>Notas Mayores</h3>
            <select id="notaMayor">
                <option value="C">C</option> <option value="C#">C#</option> <option value="D">D</option>
                <option value="D#">D#</option> <option value="E">E</option> <option value="F">F</option>
                <option value="F#">F#</option> <option value="G">G</option> <option value="G#">G#</option>
                <option value="A">A</option> <option value="A#">A#</option> <option value="B">B</option>
            </select>
            <button onclick="mostrarCirculo('notaMayor')">Mostrar</button>
            <div id="resultadoMayor" class="acordes-container"></div>
        </div>

        <div class="box">
            <h3>Notas Menores</h3>
            <select id="notaMenor">
                <option value="Am">Am</option> <option value="A#m">A#m</option> <option value="Bm">Bm</option>
                <option value="Cm">Cm</option> <option value="C#m">C#m</option> <option value="Dm">Dm</option>
                <option value="D#m">D#m</option> <option value="Em">Em</option> <option value="Fm">Fm</option>
                <option value="F#m">F#m</option> <option value="Gm">Gm</option> <option value="G#m">G#m</option>
            </select>
            <button onclick="mostrarCirculo('notaMenor')">Mostrar</button>
            <div id="resultadoMenor" class="acordes-container"></div>
        </div>
    </div>

    <div id="detalleAcorde"></div>

    <script>
        const circuloArmonico = {
            "C": ["C", "Dm", "Em", "F", "G", "Am", "Bdim"],
            "C#": ["C#", "D#m", "Fm", "F#", "G#", "A#m", "Cdim"],
            "D": ["D", "Em", "F#m", "G", "A", "Bm", "C#dim"],
            "D#": ["D#", "Fm", "Gm", "G#", "A#", "Cm", "Ddim"],
            "E": ["E", "F#m", "G#m", "A", "B", "C#m", "D#dim"],
            "F": ["F", "Gm", "Am", "A#", "C", "Dm", "Edim"],
            "F#": ["F#", "G#m", "A#m", "B", "C#", "D#m", "Fdim"],
            "G": ["G", "Am", "Bm", "C", "D", "Em", "F#dim"],
            "G#": ["G#", "A#m", "Cm", "C#", "D#", "Fm", "Gdim"],
            "A": ["A", "Bm", "C#m", "D", "E", "F#m", "G#dim"],
            "A#": ["A#", "Cm", "Dm", "D#", "F", "Gm", "Adim"],
            "B": ["B", "C#m", "D#m", "E", "F#", "G#m", "A#dim"],
            "Am": ["Am", "Bdim", "C", "Dm", "Em", "F", "G"],
            "A#m": ["A#m", "Cdim", "C#", "D#m", "Fm", "F#", "G#"],
            "Bm": ["Bm", "C#dim", "D", "Em", "F#m", "G", "A"],
            "Cm": ["Cm", "Ddim", "D#", "Fm", "Gm", "G#", "A#"],
            "C#m": ["C#m", "D#dim", "E", "F#m", "G#m", "A", "B"],
            "Dm": ["Dm", "Edim", "F", "Gm", "Am", "A#", "C"],
            "D#m": ["D#m", "Fdim", "F#", "G#m", "A#m", "B", "C#"],
            "Em": ["Em", "F#dim", "G", "Am", "Bm", "C", "D"],
            "Fm": ["Fm", "Gdim", "G#", "A#m", "Cm", "C#", "D#"],
            "F#m": ["F#m", "G#dim", "A", "Bm", "C#m", "D", "E"],
            "Gm": ["Gm", "Adim", "A#", "Cm", "Dm", "D#", "F"],
            "G#m": ["G#m", "A#dim", "B", "C#m", "D#m", "E", "F#"]
        };

        function mostrarCirculo(tipo) {
            let nota = document.getElementById(tipo).value;
            let resultado = tipo === "notaMayor" ? document.getElementById("resultadoMayor") : document.getElementById("resultadoMenor");

            resultado.innerHTML = "";
            circuloArmonico[nota]?.forEach(acorde => {
                let div = document.createElement("div");
                div.classList.add("acorde");
                div.textContent = acorde;
                resultado.appendChild(div);
            });
        }
    </script>

</body>
</html>
