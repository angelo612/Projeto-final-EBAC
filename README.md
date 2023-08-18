## Pipeline de dados do Telegram
## Objetivo


Esse projeto foi desenvolvido para conclusão do curso Profissão Analista de dados da EBAC - Escola Britânica de Artes Criativas e Tecnologia com objetivo de construir um Pipeline de dados utilizando computação em nuvem.


O pipeline de dados foi desenvolvido para ingerir, processar e armazenar mensagens de texto disparadas em um grupo no aplicativo de mensagens Telegram.

Junto ao grupo foi adicionado um bot, criado dentro da própria plataforma, responsável por captar as mensagens e encaminha-lás via API para a plataforma cloud Amazon Web Services (AWS), onde as mensagens foram processadas, armazenadas, limpas e analisadas.

A arquitetura abaixo demostra como projeto funciona e foi desenvolvida pelo professor [André Perez](https://www.linkedin.com/in/andremarcosperez/) para utilização dos alunos.

![image](https://github.com/angelo612/Projeto-final-EBAC/assets/73260926/66e04797-6afb-454c-86d1-579973567e0f)

# Contexto

O projeto consiste em capturar mensagens enviadas a um grupo do telegram, através de um chatbot armazenar em um Buckets da Amazon - S3 e disponibilizar para usuário final por meio de consultas SQL - Athena.

# Telegram

O Telegram é um serviço de mensagens instantâneas baseado na nuvem. O Telegram está disponível para smartphones ou tablets, computadores e também como Aplicação web. Os usuários podem fazer chamadas com vídeo, enviar mensagens e trocar fotos, vídeos, autocolantes e arquivos de qualquer tipo. Wikipédia

# Chatbot

Chatbot é um programa de computador que tenta simular um ser humano na conversação com as pessoas. O objetivo é responder as perguntas de tal forma que as pessoas tenham a impressão de estar conversando com outra pessoa e não com um programa de computador.[Wikipédia]('https://pt.wikipedia.org/wiki/Telegram')

# S3

Um bucket é um contêiner para objetos armazenados no Amazon S3. Você pode armazenar qualquer número de objetos em um bucket e pode ter até 100 buckets na sua conta. [AWS S3]('https://docs.aws.amazon.com/pt_br/AmazonS3/latest/userguide/UsingBucket.html')

# Sistema Transacional

O ambiente transacional representa a origem dos dados, no caso desse projeto a representação desse sistema é o Telegram, contemplando o chatbot e suas configurações.

Através da adição do bot em um grupo, conseguimos configurar a API de bots do Telegram para realizar a captura das mensagens.

## 1\. Ingestão
A etapa de **ingestão** é responsável, como seu o próprio nome diz, pela ingestão dos dados transacionais em ambientes analíticos. De maneira geral, o dado ingerido é persistido no formato mais próximo do original, ou seja, nenhuma transformação é realizada em seu conteúdo ou estrutura (*schema*). Como exemplo, dados de uma API *web* que segue o formato REST (*representational state transfer*) são entregues, logo, persistidos, no formato JSON.

## 2\. ETL

A etapa de **extração, transformação e carregamento** (do inglês *extraction, transformation and load* ou **ETL**) é uma etapa abrangente responsável pela manipulação dos dados ingeridos de sistemas transacionais, ou seja, já persistidos em camadas cruas ou *raw* de sistemas analíticos. Os processos conduzidos nesta etapa variam bastante de acordo com a área da empresa, do volume/variedade/velocidade do dado consumido, etc. Contudo, em geral, o dado cru ingerido passa por um processo recorrente de *data wrangling* onde o dado é limpo, deduplicado, etc. e persistido com técnicas de particionamento, orientação a coluna e compressão. Por fim, o dado processado está pronto para ser analisado por profissionais de dados.

No projeto, as mensagens de um único dia, persistidas na camada cru, serão compactas em um único arquivo, orientado a coluna e comprimido, que será persistido em uma camada enriquecida. Além disso, durante este processo, o dado também passará por etapas de *data wrangling*.

## 3\. Apresentação

A etapa de apresentação é reponsável por entregar o dado para os usuários (analistas, cientistas, etc.) e sistemas (dashboards, motores de consultas, etc.), idealmente através de uma interface de fácil uso, como o SQL, logo, essa é a única etapa que a maioria dos usuários terá acesso. Além disso, é importante que as ferramentas da etapa entregem dados armazenados em camadas refinadas, pois assim as consultas são mais baratas e o dados mais consistentes.
