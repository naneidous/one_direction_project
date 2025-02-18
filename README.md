from flask import Flask, render_template

app = Flask(__name__)

# Dados simulados com todas as músicas e suas durações (em minutos e segundos)
albuns = [
    {
        "nome": "Up All Night", 
        "ano": 2011, 
        "musicas": [
            {"nome": "What Makes You Beautiful", "duracao": "3:20"},
            {"nome": "Gotta Be You", "duracao": "3:05"},
            {"nome": "One Thing", "duracao": "3:06"},
            {"nome": "More Than This", "duracao": "3:48"},
            {"nome": "Up All Night", "duracao": "3:11"},
            {"nome": "I Wish", "duracao": "3:02"},
            {"nome": "Tell Me a Lie", "duracao": "3:17"},
            {"nome": "Taken", "duracao": "3:19"},
            {"nome": "I Want", "duracao": "3:10"},
            {"nome": "Everything About You", "duracao": "3:02"},
            {"nome": "Same Mistakes", "duracao": "3:11"},
            {"nome": "Save You Tonight", "duracao": "3:14"},
            {"nome": "Stole My Heart", "duracao": "2:35"}
        ]
    },
    {
        "nome": "Take Me Home", 
        "ano": 2012, 
        "musicas": [
            {"nome": "Live While We're Young", "duracao": "3:18"},
            {"nome": "Little Things", "duracao": "3:37"},
            {"nome": "Kiss You", "duracao": "3:02"},
            {"nome": "Why Don't We Go There", "duracao": "3:34"},
            {"nome": "Summer Love", "duracao": "3:37"},
            {"nome": "She's Not Afraid", "duracao": "3:19"},
            {"nome": "Loved You First", "duracao": "3:12"},
            {"nome": "Nobody Compares", "duracao": "3:27"},
            {"nome": "Still the One", "duracao": "3:18"},
            {"nome": "Afternoon", "duracao": "3:06"},
            {"nome": "Back for You", "duracao": "3:11"},
            {"nome": "Little Things (Acoustic Version)", "duracao": "3:38"}
        ]
    },
    {
        "nome": "Midnight Memories", 
        "ano": 2013, 
        "musicas": [
            {"nome": "Best Song Ever", "duracao": "3:20"},
            {"nome": "Story of My Life", "duracao": "3:37"},
            {"nome": "Diana", "duracao": "3:12"},
            {"nome": "Midnight Memories", "duracao": "3:19"},
            {"nome": "You & I", "duracao": "3:57"},
            {"nome": "Don't Forget Where You Belong", "duracao": "3:45"},
            {"nome": "Little Black Dress", "duracao": "3:15"},
            {"nome": "Through the Dark", "duracao": "3:45"},
            {"nome": "Something Great", "duracao": "3:47"},
            {"nome": "Little Things", "duracao": "3:38"},
            {"nome": "Change Your Ticket", "duracao": "3:29"},
            {"nome": "No Control", "duracao": "3:51"}
        ]
    },
    {
        "nome": "Four", 
        "ano": 2014, 
        "musicas": [
            {"nome": "Steal My Girl", "duracao": "3:47"},
            {"nome": "Night Changes", "duracao": "3:46"},
            {"nome": "No Control", "duracao": "3:51"},
            {"nome": "Fireproof", "duracao": "3:24"},
            {"nome": "Spaces", "duracao": "3:26"},
            {"nome": "Stockholm Syndrome", "duracao": "3:21"},
            {"nome": "Clouds", "duracao": "3:34"},
            {"nome": "Change Your Ticket", "duracao": "3:32"},
            {"nome": "Once in a Lifetime", "duracao": "3:18"},
            {"nome": "Over Again", "duracao": "3:45"},
            {"nome": "No Control", "duracao": "3:51"},
            {"nome": "Where Do Broken Hearts Go", "duracao": "3:40"}
        ]
    },
    {
        "nome": "Made in the A.M.", 
        "ano": 2015, 
        "musicas": [
            {"nome": "Drag Me Down", "duracao": "3:10"},
            {"nome": "Perfect", "duracao": "3:47"},
            {"nome": "History", "duracao": "3:05"},
            {"nome": "End of the Day", "duracao": "3:13"},
            {"nome": "If I Could Fly", "duracao": "3:48"},
            {"nome": "Long Way Down", "duracao": "3:13"},
            {"nome": "Never Enough", "duracao": "3:28"},
            {"nome": "Olivia", "duracao": "3:17"},
            {"nome": "What a Feeling", "duracao": "3:22"},
            {"nome": "Love You Goodbye", "duracao": "3:20"},
            {"nome": "I Want to Write You a Song", "duracao": "3:13"},
            {"nome": "A.M.", "duracao": "3:18"}
        ]
    }
]

integrantes = [
    {"nome": "Harry Styles", "bio": "Harry Edward Styles é o vocalista principal da banda."},
    {"nome": "Liam Payne", "bio": "Liam James Payne é o vocalista e o baterista."},
    {"nome": "Louis Tomlinson", "bio": "Louis William Tomlinson é o vocalista e também o baixista."},
    {"nome": "Niall Horan", "bio": "Niall James Horan é o guitarrista e vocalista."},
    {"nome": "Zayn Malik", "bio": "Zayn Jawaad Malik foi o cantor da banda até 2015."}
]

# Rota principal (home)
@app.route('/')
def index():
    return render_template('index.html', albuns=albuns, integrantes=integrantes)

# Rota para exibir músicas de um álbum específico
@app.route('/album/<album_name>')
def album(album_name):
    album = next((alb for alb in albuns if alb["nome"].lower().replace(" ", "-") == album_name.lower()), None)
    if album:
        return render_template('album.html', album=album)
    return f"Álbum {album_name} não encontrado!", 404

# Rota para exibir informações sobre um integrante
@app.route('/integrante/<nome>')
def integrante(nome):
    integrante_info = next((intg for intg in integrantes if intg["nome"].lower().replace(" ", "-") == nome.lower()), None)
    if integrante_info:
        return render_template('integrante.html', integrante=integrante_info)
    return f"Integrante {nome} não encontrado!", 404

if __name__ == '__main__':
    app.run(debug=True)






















# One Direction Music Project

Este projeto tem como objetivo fornecer informações sobre os álbuns e integrantes da banda **One Direction**, permitindo o acesso a detalhes das músicas de cada álbum e informações sobre os integrantes. O backend será feito utilizando o **Flask**, enquanto o frontend será desenvolvido com **HTML**, **CSS** e **Bootstrap** para garantir a responsividade.

## Estrutura do Projeto

- **static/**: Arquivos estáticos (como CSS e imagens).
- **templates/**: Arquivos HTML.
- **app.py**: Arquivo principal com a lógica do backend usando Flask.
- **requirements.txt**: Arquivo com as dependências do projeto.
- **README.md**: Documentação do projeto.

## Funcionalidades

- **Listar álbuns** da banda One Direction.
- **Mostrar músicas** de cada álbum.
- **Detalhes sobre os integrantes** da banda.
- **Design responsivo** para boa visualização em dispositivos móveis.
- **Interação visual clara e objetiva** para uma boa experiência de usuário.

## Como Executar o Projeto

### 1. Clone o repositório:

```bash
git clone https://naneidous.github.io/one_direction_project/
