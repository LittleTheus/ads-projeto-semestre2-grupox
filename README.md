# Padaria Santo Antônio – Controle Financeiro e Conferência de Caixa

Projeto integrador da disciplina **Tópicos de Big Data em Python** (ADS, 4º período, Estácio Juiz de Fora, 2026/2), desenvolvido como atividade extensionista junto à **Padaria Santo Antônio**, de Goianá/MG, que funciona desde 1920 e tem o maior forno a lenha do Brasil.

## Problema

A padaria não tem controle organizado do que entra e do que sai: vendas e gastos são anotados em papel, e ninguém confere o caixa no fim de cada turno. Assim, não dá para saber o lucro real nem para onde vai o dinheiro, e diferenças no caixa passam despercebidas.

## Solução

Uma aplicação em Python que:

- registra **vendas** (por cupom, com forma de pagamento, turno e operador), **despesas** por categoria e **fechamentos de caixa** em um banco **SQLite**, substituindo as anotações em papel;
- monta o **fluxo de caixa mensal** com **Pandas**: entradas, saídas, saldo, margem e saldo acumulado;
- mostra as **despesas por categoria**, a **receita por forma de pagamento** (dinheiro, Pix e cartões) e os produtos que mais faturam;
- faz a **conferência de caixa**: compara o dinheiro esperado (troco inicial + vendas em dinheiro) com o valor contado em cada turno, aponta as faltas acima da tolerância e emite um **alerta** quando um operador tem faltas frequentes;
- reúne tudo em um **painel Streamlit**, com formulários para lançar despesas e fechamentos de caixa.

> Enquanto os dados reais da padaria não são coletados, o projeto usa uma **base simulada** de 12 meses: cerca de 136 mil vendas, 600 despesas e 730 fechamentos de caixa (`src/padaria/gerar_dados.py`). Os operadores de caixa da simulação são fictícios (Funcionário A, B, C e D).

## Integrantes

| Nome completo | Matrícula | Função | Usuário GitHub |
|---|---|---|---|
| Matheus Amorim Gonçalves | 202503839883 | Gerente de Projeto | [@LittleTheus](https://github.com/LittleTheus) |
| Thiago Barros de Souza Fabri | 202502517386 | Analista de Negócio | [@TllFabri](https://github.com/TllFabri) |
| Cauan Iglésias Letra de Freitas | 202502435746 | Desenvolvedor | [@iglesiasz](https://github.com/iglesiasz) |

## Stack tecnológica

| Camada | Tecnologia |
|---|---|
| Linguagem | Python 3.11+ |
| Análise de dados | Pandas, NumPy |
| Banco de dados | SQLite |
| Visualização | Matplotlib (relatórios) e Streamlit (painel e formulários) |
| Testes | unittest |
| Gestão | Trello, GitHub (Git Flow simplificado) e Slack |

## Como executar localmente

```bash
# 1. Clonar o repositório
git clone https://github.com/LittleTheus/ads-projeto-semestre2-grupox.git
cd ads-projeto-semestre2-grupox

# 2. Criar e ativar um ambiente virtual
python -m venv .venv
.venv\Scripts\activate          # Windows
# source .venv/bin/activate     # Linux/Mac

# 3. Instalar as dependências
pip install -r requirements.txt

# 4. Gerar a base, carregar no SQLite e imprimir o relatório financeiro (gráficos em relatorios/)
python main.py --gerar

# 5. Abrir o painel no navegador
streamlit run app.py

# 6. Rodar os testes
python -m unittest discover -s tests -v
```

## Estrutura

```
├── app.py                 # painel Streamlit
├── main.py                # pipeline: dados -> SQLite -> relatório financeiro e gráficos
├── src/padaria/
│   ├── config.py          # caminhos
│   ├── gerar_dados.py     # base simulada: vendas, despesas e fechamentos
│   ├── banco.py           # leitura e lançamentos no SQLite
│   ├── analise.py         # fluxo de caixa, despesas e receitas
│   └── conferencia_caixa.py  # conferência dos fechamentos e alertas
├── tests/                 # testes automatizados
└── docs/                  # Trello, Slack e passo a passo de configuração
```

## Fluxo de trabalho

- `main`: código estável de entrega. **Commits diretos são proibidos.**
- `develop`: branch de integração. **Commits diretos são proibidos.**
- `feature/nome-da-tarefa`: cada card do Trello vira uma branch criada a partir da `develop`.
- Os commits seguem o padrão semântico (`feat:`, `fix:`, `docs:`, `test:`, `refactor:`).
- Todo Pull Request para a `develop` precisa da aprovação de pelo menos 1 colega.
