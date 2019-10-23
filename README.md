# AWS NLP Workshop

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

## Cleanup
Depois de concluir o workshop, você pode excluir todos os recursos usando as seguintes etapas:
1. Excluir todas as pilhas do Cloudformation criadas em todos os módulos
