# Aplicando Testes

Neste repositório eu organizei a documentação do exercício sobre testes em .NET 5, usando como base o tutorial do Renato Groffe e os três repositórios de exemplo.

A ideia foi separar bem cada tipo de teste para ficar fácil de entender o que eu rodei, por que aquele teste existe e qual cenário ele cobre.

## Forks usados

- [DotNet5-xUnit](https://github.com/kauarodriguessss/DotNet5-xUnit)
- [DotNet5-Moq-xUnit-FluentAssertions](https://github.com/kauarodriguessss/DotNet5-Moq-xUnit-FluentAssertions)
- [ASPNETCore5-REST_API-xUnit-SpecFlow-Swagger-Docker_JurosCompostos](https://github.com/kauarodriguessss/ASPNETCore5-REST_API-xUnit-SpecFlow-Swagger-Docker_JurosCompostos)

## Barema

- A revisar na entrega final.

## Teste de Unidade com xUnit

Aqui eu olhei para o projeto de temperatura. O teste de unidade fica bem direto: ele chama o método `FahrenheitParaCelsius` e compara o resultado calculado com o valor esperado. Achei um bom exemplo porque não depende de banco, API ou serviço externo; é só a regra matemática sendo validada.

Fork: [kauarodriguessss/DotNet5-xUnit](https://github.com/kauarodriguessss/DotNet5-xUnit)

Cenários que peguei do próprio repositório:

- Quando a entrada é `32°F`, o resultado esperado é `0°C`.
- Quando a entrada é `212°F`, o resultado esperado é `100°C`.

Print da execução:

![Execução do teste de unidade com xUnit](assets/teste-unidade-xunit.png)

## Teste com Mock Objects usando Moq

Nesse segundo exemplo eu vi como o teste usa Mock Objects para simular o serviço de consulta de crédito. Em vez de chamar um serviço real, o Moq devolve respostas combinadas para cada CPF, e o Fluent Assertions deixa a validação mais legível.

Fork: [kauarodriguessss/DotNet5-Moq-xUnit-FluentAssertions](https://github.com/kauarodriguessss/DotNet5-Moq-xUnit-FluentAssertions)

Cenários que peguei do próprio repositório:

- Quando o CPF é `123A`, o mock retorna `null` e o sistema entende como `ParametroEnvioInvalido`.
- Quando o CPF é `82226651209`, o mock retorna uma pendência e o sistema classifica como `Inadimplente`.

Print da execução:

![Execução do teste com Mock Objects usando Moq](assets/teste-mock-moq.png)

## Teste BDD com SpecFlow

No terceiro exemplo eu olhei para o SpecFlow, que escreve os cenários em um formato mais próximo de conversa: `Dado`, `Quando` e `Então`. Achei legal porque dá para entender a regra de juros compostos mesmo sem começar lendo C#.

Fork: [kauarodriguessss/ASPNETCore5-REST_API-xUnit-SpecFlow-Swagger-Docker_JurosCompostos](https://github.com/kauarodriguessss/ASPNETCore5-REST_API-xUnit-SpecFlow-Swagger-Docker_JurosCompostos)

Cenários que peguei do próprio repositório:

- `SimulacaoJurosCompostos01`: empréstimo de `R$ 10.000,00`, por `12` meses, com juros de `2,00%` ao mês, esperando `12.682,42`.
- `SimulacaoJurosCompostos04`: empréstimo de `R$ 10.000,00`, por `2` meses, com juros de `2,00%` ao mês, esperando `10.404,00`.

Na execução, o SpecFlow rodou os 7 cenários. Dois passaram e cinco falharam por diferença de arredondamento, porque o código original calcula com `double` e compara o valor exato no `Assert.Equal`. Eu mantive o resultado assim porque a proposta aqui era executar e documentar o fork do tutorial, não reescrever a solução.

Print da execução:

![Execução do teste BDD com SpecFlow](assets/teste-bdd-specflow.png)
