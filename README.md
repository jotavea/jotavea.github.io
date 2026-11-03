# jotavea.github.io

Meu portfólio: desenvolvedor Python focado em dados e backend.

Site estático (HTML e CSS), publicado com GitHub Pages em https://jotavea.github.io/.

## Estrutura

- `index.html`: página única com Sobre, Projetos, Skills e Contato
- `style.css`: estilos, com modo escuro automático
- `assets/`: prints reais dos projetos (WebP), usados nos cards e na ampliação
- `demos/estudai/`: demo online do Estudaí (cópia do `outputs/estudai.html` do repositório do projeto)
- `favicon.svg`: ícone da aba
- `og.png`: imagem de pré-visualização para LinkedIn e WhatsApp

## Como adicionar um projeto novo

1. Tire um print do projeto rodando e salve em `assets/` (ideal: WebP, 1400 px de largura).
2. Copie um bloco `<article class="projeto">` do `index.html` e troque imagem, texto, tecnologias e links.
3. Se o projeto tiver demo, adicione um botão `class="botao pequeno demo"` na área `links`.
