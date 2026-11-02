# Plano de projetos para estágio e vaga júnior (backend e dados)

Objetivo: sair de "projetos de curso" para "projetos que parecem trabalho real". Os prazos são só referência; dependem do seu ritmo.

Ordem sugerida: **Etapa 0** (rápida, já muda o portfólio) → **Projeto A** (SQL) → **Projeto B** (API).

---

## Etapa 0 · Acabamento do que você já tem (1 a 2 semanas)

Ganho enorme com pouco esforço. Hoje seus melhores projetos não têm demonstração ao vivo.

**Painel de gastos pessoais**
- [ ] Publicar no Streamlit Community Cloud (o passo a passo já está no seu README) e colocar o link da demo no site (há um comentário em `index.html` marcando o lugar).
- [ ] Corrigir uma inconsistência: a última linha do `app.py` diz que "os dados ficam no seu computador", mas na nuvem o processamento acontece no servidor do Streamlit (seu próprio README explica isso na seção Privacidade). Troque a frase por algo como "Os dados são processados apenas durante a sessão e não são armazenados."
- [ ] Adicionar 2 ou 3 prints (ou um GIF curto) ao README.
- [ ] Adicionar testes com `pytest` para `load_transactions` e `infer_category` (por exemplo: CSV com `;`, valores como `1.234,56`, categoria vazia, coluna `tipo`). Testar a limpeza de dados é exatamente o tipo de coisa que recrutadores gostam de ver.
- [ ] Separar a lógica (leitura e limpeza) da interface em um módulo próprio, como `transacoes.py`, para o teste importar sem rodar o Streamlit.

**Estudaí**
- [ ] Hoje o app está em `outputs/estudai.html`, sem demonstração. Para ter link clicável: copie o arquivo para `index.html` na raiz, ative GitHub Pages no repositório (Settings → Pages → branch `main`, pasta `/root`) e use `https://jotavea.github.io/estudai/`.
- [ ] Atualizar o README com prints e a explicação de como o resumo é gerado.

**Sistema de estoque (opcional)**
- [ ] `int(input(...))` quebra o programa se alguém digitar texto. Um `try/except ValueError` resolve e vira uma boa história de "aprendi a validar entrada". Corrija também o erro de digitação "Produtdo".

**GitHub e LinkedIn**
- [ ] Criar o repositório `jotavea/jotavea` com um README de perfil curto (quem você é, o que busca, 3 projetos fixados).
- [ ] Fixar no perfil os repositórios: painel de gastos, Estudaí e os novos projetos abaixo.
- [ ] Deixar o título do LinkedIn igual ao do portfólio.

---

## Projeto A · Pipeline de dados com SQL (3 a 4 semanas)

**Por que este primeiro:** é o seu ponto mais fraco hoje (SQL só aparece como curso) e a vaga de dados pede exatamente isso.

**O que é:** um pipeline que coleta dados públicos todos os dias, guarda em um banco e responde perguntas com SQL.

**Sugestão de dados:** séries públicas do Banco Central (API SGS), como Selic e IPCA. Confira na documentação da API quais códigos de série usar antes de começar. Qualquer fonte pública que você ache interessante serve (IBGE, dados.gov.br, bolsa).

**Stack:** Python, `requests`, Pandas, PostgreSQL (ou SQLite no começo e migrar depois), GitHub Actions para agendar, Streamlit para o painel.

**Passo a passo**
1. Extração: script que busca a série da API e trata erros (falha de rede, resposta vazia).
2. Transformação: limpar tipos e datas com Pandas.
3. Carga: gravar no banco sem duplicar registros ao rodar duas vezes (idempotência). Esse é o detalhe que mostra maturidade.
4. Modelagem: pelo menos duas tabelas com chaves, criadas por um script `schema.sql` versionado.
5. Consultas analíticas em arquivos `.sql`: use `JOIN`, `GROUP BY`, CTEs e funções de janela (média móvel, variação mês a mês, ranking).
6. Painel Streamlit lendo o banco, com 3 ou 4 gráficos.
7. Agendamento diário com GitHub Actions (`cron`).
8. Testes de pytest para a transformação.

**Pronto quando:**
- [ ] Roda do zero com um comando (documentado no README).
- [ ] Rodar duas vezes não duplica dados.
- [ ] README com diagrama simples do fluxo, prints e perguntas que o SQL responde.
- [ ] Demo publicada.

---

## Projeto B · API REST de gastos (4 a 6 semanas)

**Por que:** é o projeto que prova backend. Reaproveita o domínio do painel de gastos, então conta uma história única: "construí a API e o painel que a consome".

**Stack:** Python, FastAPI, PostgreSQL, SQLAlchemy, pytest, Docker.

**Funcionalidades**
1. CRUD de transações (criar, listar com filtros e paginação, editar, apagar).
2. Endpoint de resumo: total por categoria e por mês.
3. Importação de extrato CSV (reaproveitando sua lógica do painel).
4. Cadastro e login de usuário com JWT, cada usuário vendo só os próprios dados.
5. Validação de entrada com Pydantic e erros com códigos HTTP corretos.
6. Documentação automática (o FastAPI gera em `/docs`).

**Qualidade que diferencia**
- [ ] Testes de pytest cobrindo os endpoints principais.
- [ ] `Dockerfile` e `docker-compose.yml` (API + banco) para subir tudo com um comando.
- [ ] GitHub Actions rodando os testes a cada push.
- [ ] Deploy em um serviço gratuito de hospedagem, com o link `/docs` no portfólio.
- [ ] Senhas com hash, segredos em variáveis de ambiente, nada sensível no repositório.

**Pronto quando:** alguém consegue clonar, rodar `docker compose up` e testar a API pelo `/docs`.

---

## Como cada projeto entra no portfólio

Para cada projeto concluído, adicione um card no `index.html` seguindo o mesmo modelo do Painel de gastos:
- **O que resolve** (1 frase)
- **Como funciona** (as decisões técnicas, não só a lista de funções)
- **Tecnologias**
- **Links:** código e demo

Depois, mova o item correspondente de "Estudando" para "Uso nos meus projetos" na seção Skills (SQL, FastAPI, PostgreSQL, Docker, pytest).

## Checklist de README (vale para todos)

- Uma frase dizendo o que é e para quem serve
- Print ou GIF
- Link da demo
- Como rodar localmente (comandos que funcionam)
- Tecnologias
- Decisões e o que você faria diferente
