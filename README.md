# Liskov Substitution Principle - LSP

Imagine que você está desenvolvendo um sistema de pagamento online e possui uma hierarquia de classes para diferentes tipos de pagamentos. Temos a classe base Pagamento, que é herdada pelas classes PagamentoOnline e PagamentoBoleto. Essas classes têm métodos para processar o pagamento, como ProcessarPagamento().

Vamos analisar um cenário onde o Princípio da Substituição de Liskov não é seguido. Suponha que a classe PagamentoBoleto decida, erroneamente, que ela não precisa implementar o método ProcessarPagamento(), pois pagamentos por boleto não são processados online. Veja o exemplo abaixo:

```csharp
class Pagamento
{
    public virtual void ProcessarPagamento()
    {
        // Implementação genérica para processar um pagamento
    }
}

class PagamentoOnline : Pagamento
{
    public override void ProcessarPagamento()
    {
        // Implementação específica para processar um pagamento online
    }
}

class PagamentoBoleto : Pagamento
{
    // Esta classe não implementa o método ProcessarPagamento()
    // Pois pagamentos por boleto não são processados online
}

No exemplo acima, a classe PagamentoBoleto viola o Princípio da Substituição de Liskov. Isso ocorre porque a classe base Pagamento espera que todas as suas classes derivadas implementem o método ProcessarPagamento(), mas a classe PagamentoBoleto não o faz.

A consequência disso é que, ao utilizar essa hierarquia de classes em seu código, você pode encontrar problemas. Por exemplo, se você tiver um loop que processa pagamentos de forma genérica, como o seguinte:

List<Pagamento> pagamentos = ObterPagamentos();
foreach (var pagamento in pagamentos)
{
    pagamento.ProcessarPagamento();
}

Quando o loop chegar a um objeto PagamentoBoleto, ocorrerá uma exceção, pois a classe PagamentoBoleto não implementa o método ProcessarPagamento() esperado.

Portanto, o Princípio da Substituição de Liskov nos diz que as classes derivadas devem ser substituíveis por suas classes base, sem alterar a correção do programa. Isso significa que todas as classes derivadas devem implementar os métodos esperados pela classe base e não devem introduzir comportamentos inesperados ou exceções.
