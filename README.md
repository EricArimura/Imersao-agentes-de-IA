# Agente de IA Gemini com LangGraph e RAG

![Python](https://img.shields.io/badge/Python-3.10%2B-blue?style=for-the-badge&logo=python)
![Google Gemini](https://img.shields.io/badge/Google-Gemini-orange?style=for-the-badge&logo=google)
![LangChain](https://img.shields.io/badge/LangChain-white?style=for-the-badge&logo=langchain)
![LangGraph](https://img.shields.io/badge/LangGraph-black?style=for-the-badge&logo=langchain)

---

## 📖 Sobre o Projeto

Este projeto implementa um agente de Inteligência Artificial avançado, projetado para atuar como um assistente de Service Desk. O agente é capaz de compreender, triar e responder a perguntas com base em uma base de conhecimento extraída de documentos.

O diferencial deste projeto é a utilização do **LangGraph** para criar um fluxo de trabalho inteligente (um grafo de estados). Em vez de apenas responder perguntas, o agente primeiro realiza uma **triagem** para decidir a melhor ação:

1.  **`AUTO_RESOLVER`**: Se a pergunta for clara e puder ser respondida com a base de conhecimento, o agente utiliza a técnica **RAG (Retrieval-Augmented Generation)** para encontrar a informação nos documentos e formular uma resposta precisa, com citações da fonte.
2.  **`PEDIR_INFO`**: Se a pergunta for vaga ou ambígua, o agente solicita ao usuário mais detalhes para poder prosseguir.
3.  **`ABRIR_CHAMADO`**: Se o usuário fizer um pedido de exceção, aprovação ou solicitar explicitamente a abertura de um chamado, o agente simula essa ação.

---

## 💡 Adaptando para seu Próprio Caso de Uso

Este projeto foi construído como um framework flexível. O uso de "Políticas Internas de RH" é apenas um exemplo de aplicação. Você pode facilmente adaptar este agente para analisar qualquer conjunto de documentos do seu interesse.

Para isso, siga os passos:

1.  **Substitua a Base de Conhecimento:** Remova os arquivos `.pdf` de exemplo e adicione seus próprios documentos na pasta do projeto. O código está preparado para carregar múltiplos PDFs, mas pode ser ajustado para outros formatos (como `.txt`, `.docx`) com outros [Loaders do LangChain](https://python.langchain.com/v0.2/docs/integrations/document_loaders/).
2.  **Ajuste as Perguntas de Teste:** No notebook, modifique a lista de `testes` para incluir perguntas que sejam relevantes para o conteúdo dos seus novos documentos.
3.  **(Opcional) Refine os Prompts:** Para obter melhores resultados, você pode ajustar os prompts do sistema (como o `TRIAGEM_PROMPT`) para refletir o novo domínio. Por exemplo, em vez de um "triador de Service Desk", o agente pode se tornar um "analista de documentos legais".

---

## ✨ Funcionalidades

-   **Agente Multi-etapa:** Utiliza LangGraph para criar um fluxo de trabalho com lógica condicional.
-   **Triagem Inteligente:** Classifica a intenção do usuário antes de agir.
-   **Base de Conhecimento em PDFs:** Carrega e processa múltiplos documentos PDF como fonte de informação.
-   **Respostas com Citações:** As respostas geradas pelo RAG incluem a fonte (documento e página) de onde a informação foi extraída, garantindo transparência e confiabilidade.
-   **Saída Estruturada:** Utiliza Pydantic para garantir que a etapa de triagem retorne dados em um formato JSON consistente.

---

## 🛠️ Tecnologias Utilizadas

-   **Linguagem:** Python 3.10+
-   **Modelo de IA:** Google Gemini 1.5 Flash
-   **Frameworks e Bibliotecas:**
    -   LangChain & LangGraph
    -   LangChain Google GenerativeAI
    -   Google Generative AI SDK
    -   PyMuPDF (para leitura de PDFs)
    -   FAISS (para busca de similaridade em vetores)
    -   Pydantic (para validação de dados)

---

## 🚀 Começando

Siga as instruções abaixo para configurar e executar o projeto.

### Pré-requisitos

-   Python 3.10 ou superior
-   Uma chave de API do Google AI Studio. Você pode obter a sua em [makersuite.google.com/app/apikey](https://makersuite.google.com/app/apikey).

### Instalação

1.  **Clone o repositório:**
    ```bash
    git clone [https://github.com/EricArimura/Imersao-agentes-de-IA.git](https://github.com/EricArimura/Imersao-agentes-de-IA.git)
    cd Imersao-agentes-de-IA
    ```

2.  **Crie e ative um ambiente virtual (recomendado):**
    ```bash
    # Para Windows
    python -m venv venv
    .\venv\Scripts\activate

    # Para macOS/Linux
    python3 -m venv venv
    source venv/bin/activate
    ```

3.  **Instale as dependências:**
    ```bash
    pip install -r requirements.txt
    ```

4.  **Configure sua chave de API:**
    Para executar o projeto em um ambiente como o Google Colab, configure um *secret* chamado `GEMINI_API_KEY` com o valor da sua chave. Se for executar localmente, crie um arquivo `.env` na raiz do projeto e adicione a seguinte linha:
    ```
    GOOGLE_API_KEY="SUA_CHAVE_DE_API_AQUI"
    ```

### Uso

O projeto está contido em um Jupyter Notebook (`.ipynb`).

1.  **Adicione os PDFs:** Coloque os arquivos PDF com as políticas da empresa na mesma pasta do notebook. O código está preparado para carregar todos os arquivos `.pdf` que encontrar.
2.  **Abra o Notebook:** Utilize um ambiente compatível como [Google Colab](https://colab.research.google.com/), [VS Code](https://code.visualstudio.com/) com a extensão de Jupyter, ou Jupyter Lab.
3.  **Execute as Células:** Execute as células do notebook em ordem sequencial para ver o agente em ação, desde a triagem até a resposta final.

---

## 📂 Estrutura do Projeto

A estrutura de arquivos do projeto é simples e organizada da seguinte forma:

.
├── agente_de_ia.ipynb                                     # Notebook principal com a lógica do agente<br>
├── Política de Reembolsos (Viagens e Despesas).pdf        # 1º Documento da base de conhecimento (exemplo)<br>
├── Política de Uso de E-mail e Segurança da Informação.pdf  # 2º Documento da base de conhecimento (exemplo)<br>
├── Políticas de Home Office.pdf                           # 3º Documento da base de conhecimento (exemplo)<br>
├── requirements.txt                                       # Lista de dependências para instalação<br>
└── README.md                                              # Documentação do projeto (este arquivo)
