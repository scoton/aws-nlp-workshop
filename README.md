# Desafio

Bem-vindo ao desafio!

Qual o desafio?

Análise de sentimentos em textos com o Amazon Comprehend. Cada participante deverá indicar um cenário onde a solução poderia ser aplicada observada a realidade do Banco do Brasil. Exemplos poderiam ser: transcrições de chamadas telefônicas com clientes, atendimentos via chat ou e-mail (sensibilidade no atendimento, escolha do próximo melhor método de atendimento), análise de sentimentos em redes sociais (percepção do cliente), resumos feitos por analistas financeiros para ativos ou empresas (humor do Mercado).

Onde consigo materiais para me ajudar?

Você pode encontrar o descritivo e a documentação do serviço Amazon Comprehend nestes dois links:
Descritivo do serviço: https://aws.amazon.com/pt/comprehend/
Documentação do serviço: https://docs.aws.amazon.com/comprehend/index.html

Além disso, recomendamos que siga este guia inicial, pois passa por cada um dos primeiros passos para se usar o Comprehend através da console: 
Getting started: https://docs.aws.amazon.com/pt_br/comprehend/latest/dg/getting-started.html

Caso necessário, você pode encontrar descrições mais detalhadas do uso da API de análise de sentimentos em diferentes linguages, e ter acesso a um dataset de reviews da Amazon.com para extrair ideias para testes. Mas lembre-se, recomendamos que pensem na realidade da sua empresa, como recebem feedback, como abordam clientes, que outros tipos de análises de sentimentos em textos são relevantes para o negócios.
Guia para uso da API de detecção de sentimentos em diferentes linguagens: https://github.com/awsdocs/amazon-comprehend-developer-guide/blob/master/doc_source/get-started-api-sentiment.md
Dataset de reviews da Amazon.com: https://s3.amazonaws.com/fast-ai-nlp/amazon_review_full_csv.tgz

Por fim, deixamos este workshop como exemplo mais complexo àqueles que queiram ir além e desenvolver uma aplicação usando a API de análise de sentimentos do Comprehend. Você pode seguir o passo a passo e entender também um pouco sobre outros serviços da AWS, mas lembrando, este workshop não é essencial para o desafio, apenas um exemplo mais elaborado.
 
## AWS NLP Workshop

Neste workshop, você explorará os serviços da AWS necessários para aprimorar seu aplicativo de voz do cliente com técnicas de processamento de linguagem natural. A arquitetura da aplicação usa [Amazon Comprehend](https://aws.amazon.com/comprehend/), [AWS Lambda](https://aws.amazon.com/lambda/), [Amazon API Gateway](https://aws.amazon.com/api-gateway/), [Amazon S3](https://aws.amazon.com/s3/) e [Amazon DynamoDB](https://aws.amazon.com/dynamodb/). 
  
O Amazon Comprehend é um serviço de processamento de linguagem natural necessário para prever o sentimento dos comentários inseridos pelos usuários. O S3 hospeda recursos da Web estáticos, incluindo HTML, CSS, JavaScript e arquivos de imagem que são carregados no navegador do usuário. Códigos em JavaScript que são executados no navegador enviam e recebem dados de uma API de backend pública criada usando Lambda e API Gateway. O DynamoDB fornece uma camada de persistência na qual os dados podem ser armazenados pela função Lambda da API.

Este workshop não representa o desafio em si, mas um roteiro que serve como base para se entender como desenvolver uma aplicação que use o Amazon Comprehend para analisar o sentimento em textos. Para o objetivo do desafio, não é necessário executar o workshop, use o material para se inspirar. Mas se você quiser executar todo o workshop, espero que se divirta!

## Pré-requisitos

### Usuário da AWS

Para execução deste workshop você precisará de um usuário na AWS com acesso aos serviços IAM, S3, DynamoDB, Lambda, API Gateway, SageMaker, ECR e Comprehend. Para o Desafio, estes usuários serão fornecidos já com as devidas permissões de acesso. Para evitar problemas, é importante que memorize seu usuário e que se lembre de usar o nome designado na criação de recursos, facilitando a identificação do seu recurso contra os dos demais participantes. Ao longo do texto do workshop será indicado exatamente onde agregar o nome de usuário designado.

Todos os recursos que você lançará como parte deste workshop são elegíveis para o nível gratuito da AWS se sua conta tiver menos de 12 meses de idade. Veja o [AWS Free Tier page](https://aws.amazon.com/free/) para maiores detalhes.

### Browser

Recomendamos que utilize a versão mais recente do Chrome para concluir este workshop.

## Módulos

Este workshop divide-se em duas partes. Você deve completar a primeira parte antes de prosseguir para a seguinte.

1. [Creating a VOC application framework](1_VocFramework) - 15 mins
2. [Using Amazon Comprehend to add sentiment analysis](2_SentimentAnalysis) - 30 mins
