# DIO - Trilha .NET - Nuvem com Microsoft Azure
www.dio.me

## Desafio de projeto
Para este desafio, você precisará usar seus conhecimentos adquiridos no módulo de Nuvem com Microsoft Azure, da trilha .NET da DIO.

## Contexto
Você precisa construir um sistema de RH, onde para essa versão inicial do sistema o usuário poderá cadastrar os funcionários de uma empresa. 

Essa cadastro precisa precisa ter um CRUD, ou seja, deverá permitir obter os registros, criar, salvar e deletar esses registros. A sua aplicação também precisa armazenar logs de toda e qualquer alteração que venha a ocorrer com um funcionário.

## Premissas
A sua aplicação deverá ser do tipo Web API, Azure Functions ou MVC, fique a vontade para implementar a solução que achar mais adequado.

A sua aplicação deverá ser implantada no Microsoft Azure, utilizando o App Service para a API, SQL Database para o banco relacional e Azure Table para armazenar os logs.

A sua aplicação deverá armazenar os logs de todas as alterações que venha a acontecer com o funcionário. Os logs deverão serem armazenados em uma Azure Table.

A sua classe principal, a classe Funcionario e a FuncionarioLog, deve ser a seguinte:

![Diagrama da classe Funcionario](Imagens/diagrama_classe.png)

A classe FuncionarioLog é filha da classe Funcionario, pois o log terá as mesmas informações da Funcionario.

Não se esqueça de gerar a sua migration para atualização no banco de dados.

## Métodos esperados
É esperado que você crie o seus métodos conforme a seguir:


**Swagger**


![Métodos Swagger](Imagens/swagger.png)


**Endpoints**


| Verbo  | Endpoint                | Parâmetro | Body               |
|--------|-------------------------|-----------|--------------------|
| GET    | /Funcionario/{id}       | id        | N/A                |
| PUT    | /Funcionario/{id}       | id        | Schema Funcionario |
| DELETE | /Funcionario/{id}       | id        | N/A                |
| POST   | /Funcionario            | N/A       | Schema Funcionario |

Esse é o schema (model) de Funcionario, utilizado para passar para os métodos que exigirem:

```json
{
  "nome": "Nome funcionario",
  "endereco": "Rua 1234",
  "ramal": "1234",
  "emailProfissional": "email@email.com",
  "departamento": "TI",
  "salario": 1000,
  "dataAdmissao": "2022-06-23T02:58:36.345Z"
}
```

## Ambiente
Este é um diagrama do ambiente que deverá ser montado no Microsoft Azure, utilizando o App Service para a API, SQL Database para o banco relacional e Azure Table para armazenar os logs.

![Diagrama da classe Funcionario](Imagens/diagrama_api.png)


## Solução
O código foi completamente implementado conforme as regras do desafio, incluindo as operações CRUD com Entity Framework Core e o log no Azure Table Storage.

## Configuração e Execução

Para executar o projeto localmente e testar 100% de suas funcionalidades, é necessário configurar as strings de conexão do banco de dados (Azure SQL ou Local) e do Storage Account (Azure Storage Account ou Azurite local).

Por questões de segurança, **credenciais reais não foram versionadas no repositório**. 
O arquivo `appsettings.json` está configurado com strings vazias e o projeto irá falhar nas operações de banco de dados e Table Storage até que elas sejam preenchidas.

### Passo a passo:

1. Renomeie o arquivo `appsettings.Example.json` para `appsettings.json` (ou apenas copie o conteúdo e preencha as chaves vazias no `appsettings.json` existente):

```json
"ConnectionStrings": {
  "ConexaoPadrao": "SUA_CONNECTION_STRING_DO_AZURE_SQL",
  "SAConnectionString": "SUA_CONNECTION_STRING_DO_STORAGE_ACCOUNT",
  "AzureTableName": "FuncionarioLog"
}
```

2. Restaure as dependências do projeto:
```bash
dotnet restore
```

3. Compile o projeto:
```bash
dotnet build
```

4. Aplique as migrations no banco de dados (certifique-se de que a string de conexão do banco `ConexaoPadrao` seja válida):
```bash
dotnet ef database update
```

5. Inicie a aplicação:
```bash
dotnet run
```

6. Acesse a documentação da API (Swagger) pelo navegador em:
```
http://localhost:5000/swagger
```
*(A porta pode variar dependendo da configuração da sua máquina, verifique o terminal após rodar o dotnet run).*

### Observação importante
A aplicação compila e a interface do Swagger pode ser acessada normalmente mesmo sem as strings de conexão preenchidas, porém qualquer requisição aos endpoints resultará em erro caso a comunicação com o Banco de Dados ou o Azure Table Storage não esteja configurada.
