<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>Escáner de Libros</title>
    
    <script src="https://cdn.jsdelivr.net/npm/@ericblade/quagga2@1.2.6/dist/quagga.min.js"></script>


</head>
<body>
    <h1>Escanear Libro</h1>
    <button onclick="startScanner()">Escanear ISBN</button>
    <div id="scanner"></div>
    <form id="bookForm">
        <label>ISBN:</label>
        <input type="text" id="isbn" readonly><br><br>

        <label>Nombre del Libro:</label>
        <input type="text" id="title" readonly><br><br>

        <label>Etiquetas:</label>
        <input type="text" id="tags" placeholder="Etiquetas separadas por comas"><br><br>

        <label>¿Leído por Juan?</label>
        <select id="statusJuan">
            <option value="No leído">No leído</option>
            <option value="Leído">Leído</option>
        </select><br><br>

        <label>¿Leído por Tiago?</label>
        <select id="statusTiago">
            <option value="No leído">No leído</option>
            <option value="Leído">Leído</option>
        </select><br><br>

        <label>Lengua del Libro:</label>
        <select id="language">
            <option value="Español">Español</option>
            <option value="Portugués">Portugués</option>
            <option value="Francés">Francés</option>
            <option value="Inglés">Inglés</option>
            <option value="Valenciano">Inglés</option>
            <option value="Otros">Otros</option>
        </select><br><br>

        <button type="button" onclick="saveToGoogleSheet()">Guardar en Google Sheets</button>
    </form>

    <script>
          
        function startScanner() {
            Quagga.init({
                inputStream: {
                    name: "Live",
                    type: "LiveStream",
                    target: document.querySelector('#scanner'), 
                    constraints: {
                        facingMode: "environment" // Usa la cámara trasera si está disponible
                    }
                },
                decoder: {
                    readers: ["ean_reader"] // Cambia según el tipo de código de barras
                },
                locate: true // Habilita la detección automática del código
            }, function (err) {
                if (err) {
                    console.error("Error al inicializar Quagga2:", err);
                    return;
                }
                Quagga.start();
            });

            Quagga.onDetected(function(result) {
                const isbn = result.codeResult.code;
                document.getElementById("isbn").value = isbn;
                Quagga.stop(); // Detiene el escáner después de detectar un código
            });
        }



        function saveToGoogleSheet() {
            const isbn = document.getElementById("isbn").value;
            const title = document.getElementById("title").value;
            const tags = document.getElementById("tags").value;
            const statusJuan = document.getElementById("statusJuan").value;
            const statusTiago = document.getElementById("statusTiago").value;
            const language = document.getElementById("language").value;

            fetch('https://script.google.com/macros/s/AKfycbzc4pNWVTiFRjMNRoYjwxnE6ZuC8ls7vghV7wXmbT2l7mLRtY_J0iT1ax9xLFd-Qup-vA/exec', {
                method: 'POST',
                body: JSON.stringify({ isbn, title, tags, statusJuan, statusTiago, language })
            }).then(response => {
                if (response.ok) {
                    alert("Datos guardados en Google Sheets");
                } else {
                    alert("Error al guardar los datos");
                }
            });
        }
    </script>
</body>
</html>
