# Criação de um recurso do Azure AI Search

No [portal do Azure](https://portal.azure.com/#home) .

Criei um recurso Azure AI Search com as seguintes configurações:

Assinatura : Minha assinatura do Azure .
Grupo de recursos : Selecionei um grupo existente (lab-dio2).
Nome do serviço : lab4minera.
Localização : East US .
Nível de preços : Básico
Selecionei Review + create e depois de ver a resposta Validation Success , selecionei Create .

Retornei à página inicial do portal do Azure. 
Cliquei em + recurso e pesquisei os serviços de IA do Azure . 

Selecionei criar um plano de serviços de IA do Azure, com as seguintes configurações:

Assinatura : sua assinatura do Azure .
Grupo de recursos : O mesmo grupo de recursos do recurso do Azure AI Search .
Região : o mesmo local do recurso do Azure AI Search .
Nome : lab4minera.
Nível de preços : Padrão S0
Ao marcar esta caixa, confirmo que li e compreendi todos os termos abaixo : Marcado!

Selecionei Revisar + criar . Depois de ver a resposta Validation Passed , selecionei Create .

Aguarde a conclusão da implantação e visualizei os detalhes da implantação.

## Criei uma conta de armazenamento

Na página inicial do portal do Azure Criei um recurso Resource group.

com as seguintes configurações:
Assinatura : sua assinatura do Azure .
Grupo de recursos : O mesmo grupo de recursos que os recursos do Azure AI Search e dos serviços Azure AI .
Nome da conta de armazenamento : minlab4.
Localização : eastus .
Padrão de desempenho
Redundância : armazenamento localmente redundante (LRS)
Revisar e em Criar . Aguarde a conclusão da implantação.

Na conta de Armazenamento do Azure criada, no painel de menu esquerdo, selecionei Configuração (em Configurações ).
Alterei a configuração de Permitir acesso anônimo de Blob para Habilitado e Salvei.
No painel do menu esquerdo, selecionei Containers.

![storage-blob-1](https://github.com/manoelasilva/lab4dio/assets/50303832/e128c7f9-a90d-42cf-bcfb-246257934e7b)

criei Contêiner . Um painel do seu lado direito, fazendo as seguintes configurações. 

Nome : Coffee-Reviews
Nível de acesso público : Container (acesso de leitura anônimo para containers e blobs)
Avançado : sem alterações .

Baixei e extrai do link https://aka.ms/mslearn-coffee-reviewse os arquivos para uma pasta.

No contêiner, selecionei Uploud .

![1](https://github.com/manoelasilva/lab4dio/assets/50303832/243291eb-35c6-4fe7-98ef-2e7660b64fe3)


Depois que o upload for concluído, No portal do Azure, acessei o recurso Azure AI Search. Na página Visão geral , selecionei Importar dados .

![azure-search-wizard-1](https://github.com/manoelasilva/lab4dio/assets/50303832/049bc62b-86d9-4abe-a953-91d62dc6fdf0)

Na opção Conectar-se aos seus dados , na lista Fonte de Dados , selecionei Azure Blob Storage . preenchi as seguintes informações:

Fonte de dados : Armazenamento de Blobs do Azure
Nome da fonte de dados : coffee-customer-data
Dados a extrair : Conteúdo e metadados
Modo de análise : Padrão
Cadeia de conexão : coffee-customer-data.
Autenticação de identidade gerenciada : Nenhuma
Nome do contêiner : esta configuração é preenchida automaticamente depois que você escolhe uma conexão existente .
Pasta Blob : deixei em branco .
Descrição : Avaliações sobre Fourth Coffee Shops.
Selecione Próximo: Adicionar habilidades cognitivas (opcional) .

Na secção Anexar Serviços Cognitivos , selecione o seu recurso de serviços Azure AI.

Na seção Adicionar enriquecimentos :
Alterei o nome da qualificação para coffee-skillset .
Marquei a caixa de seleção Habilitar OCR e mesclar todo o texto no campo merged_content .
selecionei Habilitar OCR para ver todas as opções de campo enriquecido.

campo Dados de origem: merged_content .
Alterei o nível de granularidade de enriquecimento para Páginas (blocos de 5.000 caracteres) .

Selecionei os seguintes campos enriquecidos:
Habilidade Cognitiva	Parâmetro	Nome do campo
Extraia nomes de locais	 	Localizações
Extraia frases-chave	 	frases chave
Detectar sentimento	 	sentimento
Gerar tags de imagens	 	imagemTags
Gere legendas de imagens	 	legenda da imagem
Em Salvar enriquecimentos em um armazenamento de conhecimento , selecione:
Projeções de imagem
Documentos
Páginas
Frases chave
Entidades
Detalhes da imagem
Referências de imagem

Selecionei Escolha uma conexão existente . 
![6a-azure-cognitive-search-enrichments-warning](https://github.com/manoelasilva/lab4dio/assets/50303832/ee629160-920a-4561-a696-9f6c2a4476b6)

Cliquei em + Container para criar um novo contêiner chamado armazenamento de conhecimento com o nível de privacidade definido como Private e selecione Create .
Selecione o contêiner de armazenamento de conhecimento e clique em Selecionar na parte inferior da tela.
Selecionei projeções de blob do Azure: Documento . Uma configuração para o nome do contêiner com as exibições preenchidas automaticamente do contêiner de armazenamento de conhecimento . Não alterei o nome do contêiner.

Selecionei Próximo: Personalizar índice de destino . Alterei o nome do índice para coffee-index .

configurada como metadata_storage_path . Deixei o nome do sugerido em branco e o modo de pesquisa preenchido automaticamente.
Selecionei filtrável para todos os campos que já estão selecionados por padrão.
![6a-azure-cognitive-search-customize-index](https://github.com/manoelasilva/lab4dio/assets/50303832/71d1d4ac-fcb4-4d2a-9a07-3e640d80433a)

alterei o nome do indexador para coffee-indexer .

programação definida: Once .

Nesta etapa Expanda as opções avançadas . 
Certifique-se de que a opção Base-64 Encode Keys esteja marcada.
Selecione Enviar para criar a fonte de dados, o conjunto de habilidades, o índice e o indexador. 

Volte à página de recursos do Azure AI Search. No painel esquerdo, em Gerenciamento de pesquisa , selecione Indexadores . Selecione o indexador de café recém-criado . Espere um minuto e selecione ↻ Atualize até que o Status indique sucesso.

clique no nome do indexador para ver mais detalhes.
![6a-search-indexer-success](https://github.com/manoelasilva/lab4dio/assets/50303832/5508aa73-61ed-4998-960a-9ec7953e84c5)

No Search Explorer para escrever e testar consultas. 
![5-exercise-screenshot-7](https://github.com/manoelasilva/lab4dio/assets/50303832/9714a295-fb16-412b-ad65-2a7a0c6f816b)

 Abaixo do índice selecionado, alterei a visualização para JSON view .

No campo do editor de consultas JSON , copiei e colei os codigos abaixo:

consulta de pesquisa retorna todos os documentos no índice de pesquisa, incluindo uma contagem de todos os documentos no campo @odata.count . O índice de pesquisa deve retornar um documento JSON contendo os resultados da pesquisa.
{
    "search": "*",
    "count": true
}
![c1](https://github.com/manoelasilva/lab4dio/assets/50303832/6a6e7098-294a-4a2a-9d83-53b480f30be5)

consulta pesquisa todos os documentos no índice e filtra revisões com localização em Chicago.
{
 "search": "locations:'Chicago'",
 "count": true
}
![c2](https://github.com/manoelasilva/lab4dio/assets/50303832/5508f8b2-1ce1-4ce8-b51b-22ea61bb8982)

Consulta pesquisa todos os documentos no índice e filtra revisões com sentimento negativo.
{
 "search": "sentiment:'negative'",
 "count": true
}
![c3](https://github.com/manoelasilva/lab4dio/assets/50303832/4c77efdf-3b03-4b17-9ca6-83dabf322bb0)

## Resumo
Laboratório dio bem completo, mas com as orintações da documentação e da [Valéria Baptista](https://github.com/valeriafarias),consegui concluir com sucesso as etapas.
