# pesquisa-cognitiva
Direcionamento para o uso de pesquisa cognitiva usando azure

# Pesquisa Cognitiva com Azure Cognitive Search

Este repositório descreve o passo a passo para configurar uma pesquisa usando as **Soluções de Pesquisa Cognitiva da Azure**, além de insights, possibilidades de ferramentas que podem se beneficiar dessa tecnologia e os aprendizados adquiridos durante o processo.

## Passo a Passo para Configuração

### 1. **Criação de uma Conta na Azure**
   - Acesse o [Portal do Azure](https://portal.azure.com/).
   - Crie uma conta ou faça login, se já tiver uma.
   - Crie um novo **Recurso de Pesquisa Cognitiva** (Azure Cognitive Search).
     - Clique em **Criar um recurso** e pesquise por "Azure Cognitive Search".
     - Selecione o recurso e preencha as informações solicitadas, como nome do recurso, grupo de recursos e região.
     - Clique em **Criar**.

### 2. **Configuração do Serviço de Pesquisa Cognitiva**
   - Após a criação do recurso de pesquisa, vá até a página do serviço recém-criado.
   - Obtenha a **chave de API** para autenticação acessando a seção "Chaves e endpoint".
   - Copie o **endpoint** e a **chave de API** para utilizá-los nas configurações do seu código.

### 3. **Instalação do SDK do Azure Cognitive Search**
   - Para interagir com o serviço de pesquisa da Azure, instale o SDK correspondente. No Python, use o seguinte comando para instalar o pacote `azure-search-documents`:

     ```bash
     pip install azure-search-documents
     ```

### 4. **Configuração do Código**
   - Crie um arquivo Python (exemplo: `azure_search.py`) para configurar e interagir com o serviço de Pesquisa Cognitiva da Azure. Utilize o código abaixo para realizar consultas de pesquisa:

     ```python
     from azure.core.credentials import AzureKeyCredential
     from azure.search.documents import SearchClient

     # Substitua pelos valores do seu serviço de pesquisa
     endpoint = "SEU_ENDPOINT"
     api_key = "SUA_CHAVE_DE_API"
     index_name = "nome-do-seu-index"

     # Configuração do cliente de pesquisa
     client = SearchClient(endpoint=endpoint, index_name=index_name, credential=AzureKeyCredential(api_key))

     # Função de pesquisa
     def search_documents(query):
         results = client.search(query)
         for result in results:
             print(result)

     # Realizando uma consulta de pesquisa
     query = "exemplo de consulta"
     search_documents(query)
     ```

### 5. **Indexação de Dados**
   - Antes de realizar pesquisas, é necessário indexar os dados. A Azure Cognitive Search suporta diversos tipos de dados, como documentos, PDFs e imagens.
   - Para indexar dados, é preciso criar um índice. Aqui está um exemplo de como definir um índice na Azure:

     ```python
     from azure.search.documents.indexes import SearchIndexClient
     from azure.search.documents.indexes.models import *

     index_client = SearchIndexClient(endpoint=endpoint, credential=AzureKeyCredential(api_key))

     # Definindo o esquema do índice
     fields = [
         SearchableField(name="id", type=SearchFieldDataType.String, key=True),
         SearchableField(name="title", type=SearchFieldDataType.String),
         SearchableField(name="content", type=SearchFieldDataType.String),
     ]

     index = SearchIndex(name="example-index", fields=fields)
     index_client.create_index(index)
     ```

### 6. **Execução e Consultas**
   - Após configurar o índice e indexar os dados, execute o script Python para realizar consultas de pesquisa.

---

## Insights

### **Pesquisa Semântica e Cognitiva**
   - Permite buscas baseadas no significado das palavras, não apenas em correspondências exatas.
   - Pode ser integrada com **Cognitive Services** para análise de imagens e PDFs.
   
### **Extração de Insights**
   - Pode ser utilizada para **análise de sentimento**, **extração de entidades** e **classificação de texto**.

---

## Ferramentas que se Beneficiam

### 1. **Plataformas de Suporte ao Cliente**
   - Indexa interações com clientes para respostas rápidas e relevantes.

### 2. **Sistemas de Gestão de Conteúdo (CMS)**
   - Melhora a busca por documentos e artigos em bases de conhecimento.

### 3. **Plataformas de Pesquisa Empresarial**
   - Facilita a recuperação de documentos internos, contratos e relatórios.

---

## Aprendizados Adquiridos

### **Integração com Azure**
   - Aprendizado sobre autenticação via chave de API e uso do SDK.

### **Criação e Gerenciamento de Índices**
   - Importância de definir corretamente os campos e tipos de dados.

### **Pesquisa Semântica**
   - Permite buscas mais inteligentes e contextuais.

---

## Conclusão

As soluções de **Pesquisa Cognitiva da Azure** oferecem uma ferramenta poderosa para aprimorar a pesquisa de dados em sistemas empresariais. Com suporte a análise semântica, indexação de documentos e integração com Cognitive Services, é uma solução robusta para buscas inteligentes e eficientes.

Se precisar de mais informações, sinta-se à vontade para entrar em contato!

