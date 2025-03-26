<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Estante de Livros</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            margin: 0;
            padding: 0;
            background: linear-gradient(120deg, #84fab0, #8fd3f4);
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
        }
        .container {
            max-width: 600px;
            width: 90%;
            background: white;
            padding: 20px;
            border-radius: 12px;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.3);
            text-align: center;
        }
        h2 {
            color: #333;
            font-size: 24px;
        }
        input {
            width: 100%;
            padding: 12px;
            margin: 15px 0;
            border: 2px solid #8fd3f4;
            border-radius: 8px;
            font-size: 16px;
            outline: none;
        }
        input:focus {
            border-color: #84fab0;
        }
        .book-list {
            list-style: none;
            padding: 0;
        }
        .book-list li {
            padding: 12px;
            border-bottom: 1px solid #ddd;
            font-size: 16px;
            background: #f9f9f9;
            transition: all 0.3s;
            border-radius: 6px;
            margin: 5px 0;
        }
        .book-list li:hover {
            background: #8fd3f4;
            color: white;
            cursor: pointer;
        }
    </style>
</head>
<body>
    <div class="container">
        <h2>📚 Estante de Livros 📖</h2>
        <input type="text" id="search" placeholder="🔍 Pesquisar livros...">
        <ul id="books" class="book-list"></ul>
    </div>

    <script>
        const books = [
            { title: "Cartas Sertanejas Professarias", author: "Júlio Ribeiro", nationality: "br" },
            { title: "Triste Fim de Policarpo Quaresma", author: "Lima Barreto", nationality: "br" },
            { title: "O Cortiço em Cordel", author: "Aluísio de Azevedo", nationality: "br" },
            { title: "Inovação", author: "Renato Cruz", nationality: "br" },
            { title: "A Muralha", author: "Diná Silveira de Queiroz", nationality: "br" },
            { title: "O Seminarista", author: "Bernardo Guimarães", nationality: "br" },
            { title: "Divã", author: "Martha Medeiros", nationality: "br" },
            { title: "Cantar Histórias", author: "José Alércio Zamoner", nationality: "br" },
            { title: "Madrugada sem Deus", author: "Mário Donato", nationality: "br" },
            { title: "Cabo de Guerra", author: "Ivone Benedetti", nationality: "br" },
            { title: "Um Olhar que Transforma", author: "Januário Cristina Alves", nationality: "br" },
            { title: "Memórias Inventadas", author: "Manoel de Barros", nationality: "br" },
            { title: "Fogo Morto", author: "José Lins do Rego", nationality: "br" },
            { title: "A Droga da Obediência", author: "Pedro Bandeira", nationality: "br" },
            { title: "Monteiro Lobato: O Editor do Brasil", author: "Cassiano Nunes", nationality: "br" },
            { title: "O Cabeleira", author: "Franklin Távora", nationality: "br" },
            { title: "O Outro Apaixonado por Marília de Dirceu", author: "Jair Vitória", nationality: "br" },
            { title: "Armadilha", author: "João Targino", nationality: "br" },
            { title: "O Zahir", author: "Paulo Coelho", nationality: "br" },
            { title: "Espumas Flutuantes", author: "Castro Alves", nationality: "br" },
            { title: "A Perfeição", author: "Eça de Queiroz", nationality: "pt" },
            { title: "Gaivota / Tio Vânia", author: "Anton Tchekhov", nationality: "ru" },
            { title: "Viagens na Minha Terra", author: "Almeida Garrett", nationality: "pt" },
            { title: "O Velho da Horta / Auto da Barca do Inferno / A Farsa de Inês Pereira", author: "Gil Vicente", nationality: "pt" }
        ];

        function displayBooks(filter = "") {
            const bookList = document.getElementById("books");
            bookList.innerHTML = "";
            books.filter(book => 
                book.title.toLowerCase().includes(filter.toLowerCase()) ||
                book.author.toLowerCase().includes(filter.toLowerCase())
            ).forEach(book => {
                const li = document.createElement("li");
                li.textContent = `${book.title} – ${book.author}`;
                bookList.appendChild(li);
            });
        }

        document.getElementById("search").addEventListener("input", function() {
            displayBooks(this.value);
        });

        displayBooks();
    </script>
</body>
</html>
