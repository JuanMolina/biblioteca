<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>Escáner de Libros</title>
    <script src="https://serratus.github.io/quaggaJS/dist/quagga.min.js"></script>
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
                    target: document.querySelector('#scanner')
                },
                decoder: {
                    readers: ["ean_reader"]
                }
            }, function (err) {
                if (err) {
                    console.log(err);
                    return;
                }
                Quagga.start();
            });

            Quagga.onDetected(async function(result) {
                const isbn = result.codeResult.code;
                document.getElementById("isbn").value = isbn;
                Quagga.stop();

                // Obtener datos del libro usando la API de Google Books
                try {
                    const response = await fetch(`https://www.googleapis.com/books/v1/volumes?q=isbn:${isbn}`);
                    const data = await response.json();
                    if (data.totalItems > 0) {
                        document.getElementById("title").value = data.items[0].volumeInfo.title;
                    } else {
                        document.getElementById("title").value = "No encontrado";
                    }
                } catch (error) {
                    console.error("Error obteniendo datos del libro:", error);
                }
            });
        }

        function saveToGoogleSheet() {
            const isbn = document.getElementById("isbn").value;
            const title = document.getElementById("title").value;
            const tags = document.getElementById("tags").value;
            const statusJuan = document.getElementById("statusJuan").value;
            const statusTiago = document.getElementById("statusTiago").value;
            const language = document.getElementById("language").value;

            fetch('https://script.google.com/macros/s/TU_API_URL/exec', {
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
