# Como usar o GitHub no projeto (pelo Colab)

Repositório: <https://github.com/Renata-Nascimento/Projeto-U02-CD>

Todo o trabalho é feito **pelo Google Colab**: é nele que editamos os notebooks e é dele que salvamos no GitHub.

O professor usa o **histórico de commits** como prova de participação. Por isso, **cada pessoa salva o próprio notebook com a própria conta**, e não manda o arquivo para outra pessoa subir.

---

## 1. Preparação (uma vez só)

- **a)** Tenha uma conta em <https://github.com>.
- **b)** **Aceite o convite** da Renata para o repositório: ele chega por e-mail ou aparece em <https://github.com/notifications>. Sem aceitar, você não consegue salvar nada.
- **c)** Na primeira vez que for salvar do Colab no GitHub (seção 4), o Colab pede para **autorizar o acesso à sua conta do GitHub**. Autorize.

---

## 2. Regras de ouro

- **a)** **Cada pessoa mexe só no próprio notebook.** Se duas pessoas salvarem no mesmo arquivo, a última **apaga** o trabalho da outra.
- **b)** **Sempre salve no mesmo caminho.** O GitHub guarda as versões antigas no histórico, então salvar por cima não perde nada.
- **c)** **Escreva mensagens claras** ao salvar: `Adiciona boxplots por mesorregião`, e não `update`.
- **d)** **Só suba versões que rodam sem erro.** O notebook no GitHub deve sempre funcionar do início ao fim.

### Notebooks do projeto

| Notebook | Responsável |
|---|---|
| `notebooks/01_coleta.ipynb` | notebook apresentado no CP1 |
| `notebooks/02_limpeza_eda.ipynb` | Pessoa A |
| `notebooks/03_graficos.ipynb` | Pessoa B |
| `notebooks/04_emendas_convenios.ipynb` | Pessoa C |
| `notebooks/05_serie_longa.ipynb` | Pessoa D |

---

## 3. Primeira vez: criar o seu notebook

- **a)** Abra <https://colab.research.google.com> e crie um notebook novo (**Arquivo → Novo notebook**).
- **b)** Renomeie clicando no nome lá em cima, por exemplo `03_graficos.ipynb`.
- **c)** Ele fica salvo no seu **Google Drive** (pasta "Colab Notebooks") e salva sozinho enquanto você edita.
- **d)** Quando tiver a primeira versão, siga a seção 4 para subir no GitHub.

> Se o seu notebook já existe no GitHub e você não tem uma cópia no Drive: abra pela seção 5 e use
> **Arquivo → Salvar uma cópia no Drive**. A partir daí, trabalhe nessa cópia.

---

## 4. Salvar no GitHub (toda vez que terminar uma sessão de trabalho)

- **a)** No seu notebook, **Arquivo → Salvar uma cópia no GitHub**.
- **b)** Preencha:
   - **Repositório:** `Renata-Nascimento/Projeto-U02-CD`
   - **Branch:** `main`
   - **Caminho do arquivo:** `notebooks/NOME_DO_SEU_NOTEBOOK.ipynb` (sempre o mesmo)
   - **Mensagem de commit:** o que você fez nesta sessão
   - Deixe marcado **"Incluir um link para o Colab"**
- **c)** Clique em **OK**.

Pronto. No GitHub, o arquivo passa a mostrar a versão nova, e a anterior fica no histórico (botão **History** do arquivo), com data, autor e mensagem.

### Rotina do dia a dia

```
Abrir o notebook no Drive → editar → rodar tudo sem erro → Salvar uma cópia no GitHub
```

Pode salvar no GitHub quantas vezes quiser. Uma vez por sessão de trabalho já é ótimo.

---

## 5. Abrir o notebook de um colega (só para ver ou rodar)

- **a)** No Colab: **Arquivo → Abrir notebook → aba GitHub**.
- **b)** Digite `Renata-Nascimento/Projeto-U02-CD`, escolha a branch `main` e clique no notebook.

Atalho: troque o começo do link do arquivo no GitHub.

`https://github.com/Renata-Nascimento/Projeto-U02-CD/blob/main/notebooks/03_graficos.ipynb`

vira

`https://colab.research.google.com/github/Renata-Nascimento/Projeto-U02-CD/blob/main/notebooks/03_graficos.ipynb`

> ⚠️ Pode rodar e testar à vontade, mas **não salve no GitHub** um notebook que não é seu.
> Edições num notebook aberto direto do GitHub não ficam salvas em lugar nenhum: ao fechar a aba, somem.

---

## 6. Usar dados do repositório dentro do notebook

Não precisa fazer upload de arquivo no Colab. O notebook lê direto do GitHub pelo link "raw":

```python
BASE = 'https://raw.githubusercontent.com/Renata-Nascimento/Projeto-U02-CD/main/'

df = pd.read_csv(BASE + 'saida/base_municipios_2020_2023.csv')
```

Para pegar o link de qualquer arquivo: abra o arquivo no GitHub → botão **Raw** → copie o endereço.

### Arquivos de dados (CSV, XLS, PDF)

O "Salvar uma cópia no GitHub" do Colab **só sobe notebooks**. Quando um notebook gerar um arquivo que outra pessoa vai usar (por exemplo, a base limpa da Pessoa A), baixe o arquivo do Colab (painel de arquivos à esquerda → botão direito → **Fazer download**) e mande no grupo para a Fernanda subir na pasta certa.

---

## Glossário rápido

| Termo | O que é |
|---|---|
| **Repositório** | A pasta do projeto no GitHub, com todo o histórico |
| **Commit** | Um "salvamento" com uma mensagem dizendo o que mudou |
| **Branch** | Uma linha de trabalho. Usamos só a `main` |
| **History** | Lista de todas as versões de um arquivo |
| **Raw** | O arquivo "puro", sem a página do GitHub em volta; é o link que o pandas consegue ler |
