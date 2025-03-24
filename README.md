<!DOCTYPE html>
<html lang="pt">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Upload de Notas de Compra</title>
    <style>
        /* Reset */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: Arial, sans-serif;
        }

        /* Layout principal */
        body {
            display: flex;
            flex-direction: column;
            align-items: center;
            min-height: 100vh;
            background: #f4f4f4;
        }

        header {
            background: #333;
            color: white;
            width: 100%;
            padding: 20px;
            text-align: center;
            font-size: 22px;
        }

        main {
            width: 90%;
            max-width: 600px;
            background: white;
            padding: 20px;
            margin-top: 20px;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            text-align: center;
        }

        input[type="file"] {
            display: none;
        }

        .upload-label {
            display: block;
            background: #4CAF50;
            color: white;
            padding: 10px;
            margin: 10px 0;
            cursor: pointer;
            border-radius: 5px;
        }

        #preview {
            margin-top: 10px;
            max-width: 100%;
            display: none;
            border: 1px solid #ccc;
            border-radius: 5px;
        }

        .nota-lista {
            margin-top: 20px;
            text-align: left;
        }

        .nota-item {
            background: #e3e3e3;
            padding: 10px;
            margin: 5px 0;
            border-radius: 5px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .delete-btn {
            background: red;
            color: white;
            border: none;
            padding: 5px;
            cursor: pointer;
            border-radius: 3px;
        }

        footer {
            margin-top: 20px;
            background: #222;
            color: white;
            padding: 10px;
            width: 100%;
            text-align: center;
        }

        /* Responsividade */
        @media (max-width: 600px) {
            main {
                width: 100%;
            }
        }
    </style>
</head>
<body>

    <header>📄 Envio de Notas de Compra</header>

    <main>
        <h2>📎 Anexar Nota Fiscal</h2>

        <!-- Input para upload -->
        <input type="file" id="notaInput" accept="image/*, .pdf">
        <label for="notaInput" class="upload-label">📤 Selecionar Nota</label>

        <!-- Pré-visualização -->
        <img id="preview" alt="Pré-visualização da Nota">

        <!-- Lista de notas enviadas -->
        <div class="nota-lista" id="notaLista">
            <h3>📂 Notas Enviadas</h3>
        </div>
    </main>

    <footer>© 2025 - Loja Exemplo</footer>

    <script>
        const notaInput = document.getElementById("notaInput");
        const preview = document.getElementById("preview");
        const notaLista = document.getElementById("notaLista");

        // Evento de mudança no input de arquivo
        notaInput.addEventListener("change", function () {
            const file = notaInput.files[0];

            if (file) {
                const reader = new FileReader();
                reader.onload = function (e) {
                    if (file.type.startsWith("image/")) {
                        preview.src = e.target.result;
                        preview.style.display = "block";
                    } else {
                        preview.style.display = "none";
                    }
                    adicionarNota(file.name);
                };
                reader.readAsDataURL(file);
            }
        });

        // Adiciona uma nota à lista
        function adicionarNota(nomeNota) {
            const div = document.createElement("div");
            div.classList.add("nota-item");
            div.innerHTML = `
                <span>${nomeNota}</span>
                <button class="delete-btn" onclick="removerNota(this)">🗑</button>
            `;
            notaLista.appendChild(div);
        }

        // Remove uma nota da lista
        function removerNota(element) {
            element.parentElement.remove();
        }
    </script>

</body>
</html>
