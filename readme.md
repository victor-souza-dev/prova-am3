# Prova AM3 Fullstack
Olá!
Essa prova foi criada para testar suas habilidades com .NET, C# e ReactJS em geral. 
Por favor, siga atentamente as instruções antes de começar, ok?

Não conseguiu fazer alguma etapa? Blza, entrega o que você conseguir ;)

## Para começar
O primeiro passo é criar uma **cópia** deste repositório. Por favor, perceba que fazer uma cópia é diferente de realizar um clone ou fork. Siga os passos abaixo para fazer a cópia:

- Crie um novo repositório em sua conta do GitHub. Dê o nome de ***prova-am3***
- Abra seu client do git e siga os comandos:
```
git clone --bare https://github.com/victor-souza-dev/prova-am3.git
```
Esse comando gera uma cópia do repositório da prova em seu computador. Agora, continue com os comandos
```
cd prova-am3.git
git push --mirror https://github.com/SEUSUARIO/prova-am3.git
```
Note que você precisa alterar o SEUUSUARIO pelo seu username do GitHub, utilizado para criar o repositório no primeiro passo.
Você pode apagar o diretório ```prova-am3.git``` que foi criado em seu computador.

Tudo certo: você possui um repositório em seu nome com tudo que precisa para começar responder sua prova. Agora sim, faça o clone (git clone) em sua máquina e você está pronto para trabalhar.
```
git clone https://github.com/SEUSUARIO/prova-am3.git
```

> Lembre-se: NÃO gere um Fork do repositório. Siga os passos acima para copiar o repositório para sua conta.

## Conhecendo o projeto
> Nós recomendamos que você utilize o Visual Studio 2022 (pode ser a versão community). Você também precisa do .NET 6 instalado, ok?
Ah, não esquece de instalar o pacote de desenvolvimento para o ASP NET durante a instalação do Visual Studio.

Ao abrir o projeto no Visual Studio, você pode notar que se trata de um projeto Web API do ASP NET.  Você pode se orientar pela pasta ```Controllers``. 
Dentro dela, cada Controller representa uma etapa da prova.  Logo abaixo vamos falar mais sobre essas etapas e como resolvê-las.

Antes de rodar o projeto, você precisa rodar as migrations. Para isso, primeiro instale o [EF Tools](https://learn.microsoft.com/en-us/ef/core/get-started/overview/install#get-the-entity-framework-core-tools):
```
dotnet tool install --global dotnet-ef
```
Agora, pode rodar as migrations de fato:
```
dotnet ef database update 
``` 

Pronto, o projeto já criou as tabelas e alguns registros no seu localDB. 


Rode o projeto e, se tudo deu certo, você deverá ver uma página do Swagger com as APIs que utilizaremos no teste.

Dê uma passeada pelo projeto e note que ele tem alguns probleminhas de arquitetura. Vamos resolver isso já já

## Restrições
Você deve usar:
 - ReactJS + Vite
 - ASP.NET | C#
 - Zustand
 - React Query
 - Mui5 + Emotion
 - SOLID
 - Clean Code

## Seu trabalho
Certo, tudo configurado e rodando. Agora vamos explicar o que você precisa fazer.

### Parte1Controller
Esse controller foi criado para gerar uma API que sempre retorna um número aleatório. 
Você pode vê-lo funcionando ao rodar o projeto e na página do Swagger, clique em Parte 1 > Try it Out > Execute.

Esse código, no entanto, tem algum problema: ele sempre retorna o mesmo valor.
Seu trabalho, portanto, é corrigir esse comportamente: cada vez que a chamada é realizada um número diferente deverá ser retornado.
Implemente uma interface que realiza a chamada a esse endpoint.

### Parte2Controller
Essa API deveria retornar os produtos cadastrados de forma paginada. O usuário informa a página (page) desejada e o sistema retorna os 10 itens da mesma.
O problema é que não importa qual número de página é utilizado: os resultados estão vindo sempre os mesmos. E não apenas os 10.

Você precisa portanto:
1. Corrigir o bug de paginação. Ao passar page=1, deveria ser retornado os 10 (0 a 9) primeiros itens do banco. Ao passar page=2 deveria ser retornado os itens subsequentes (10 a 19), etc
2. Note que na Action do Controller, chamamos o ```ProductService```. Fazemos isso, instanciando o mesmo (```var productService = new ProductService(_ctx);```). Essa é uma prática ruim. Altere o código para que utilize Injeção de Dependência.
3. Agora, explore os arquivos ```/Models/CustomerList``` e ```/Models/ProductList```. Eles são bem parecidos. De fato, deve haver uma forma melhor de criar esses objetos, com menos repetição de código. Faça essa alteração.
4. Da mesma forma, como você melhoraria o ```CustomerService```e o ```ProductService``` para evitar repetição de código?
5. Além da paginação, implemente também um filtro de pesquisa e um limite de elementos por página, o famoso pageSize.
5. Implementar uma interface com uma tabela que consuma esses dados e realize a paginação e filtros de forma dinâmica utilizando React Query e Zustand.