# Diagrama de Classes de Domínio

```mermaid
classDiagram
    class Assinante {
        -id: String
        -nomeCompleto: String
        -celular: String
        -preferencias: Set~PreferenciaAlimentar~
    }

    class CodigoConfirmacaoSMS {
        -codigo: String
        -celular: String
        -tentativas: int
        -expiraEm: DateTime
    }

    class PlanoAssinatura {
        -id: String
        -periodicidade: Periodicidade
        -quantidadeRefeicoes: int
        -valor: BigDecimal
    }

    class Periodicidade {
        <<enumeration>>
        SEMANAL
        MENSAL
        PACOTE_5_DIAS
        PACOTE_15_DIAS
        PACOTE_20_DIAS
    }

    class PreferenciaAlimentar {
        <<enumeration>>
        TRADICIONAL
        VEGETARIANA
        SEM_LACTOSE
    }

    class CardapioSemanal {
        -semanaReferencia: String
        -itensDisponiveis: List~ItemCardapio~
    }

    class ItemCardapio {
        <<abstract>>
        -codigo: String
        -nome: String
        -calorias: int
        -disponivel: boolean
    }

    class PratoPrincipal {
        -tipoProteina: String
    }

    class Acompanhamento {
        -tipo: String
    }

    class Sobremesa {
        -contemAcucar: boolean
    }

    class PedidoRefeicoes {
        -itens: List~ItemPedido~
    }

    class ItemPedido {
        -quantidade: int
    }

    class EnderecoEntrega {
        -cep: String
        -logradouro: String
        -numero: String
        -bairro: String
        -cidade: String
        -uf: String
    }

    class Assinatura {
        -id: String
        -status: StatusAssinatura
        -dataInicio: DateTime
    }

    class StatusAssinatura {
        <<enumeration>>
        AGUARDANDO_PAGAMENTO
        ATIVA
        CANCELADA
    }

    class Pagamento {
        -id: String
        -valor: BigDecimal
        -status: StatusPagamento
        -dataHora: DateTime
    }

    class StatusPagamento {
        <<enumeration>>
        AUTORIZADO
        RECUSADO
    }

    class CartaoCredito {
        -numeroMascarado: String
        -validade: String
        -titular: String
    }

    class GatewayPagamento {
        <<interface>>
        +autorizar(cartao, valor) StatusPagamento
    }

    class OperadoraCartaoCreditoGateway {
        +autorizar(cartao, valor) StatusPagamento
    }

    class Protocolo {
        -numero: String
        -geradoEm: DateTime
    }

    Assinante "1" --> "0..*" Assinatura
    Assinante "1" --> "0..*" PreferenciaAlimentar : registra
    Assinante ..> CodigoConfirmacaoSMS : autentica com

    Assinatura "1" --> "1" PlanoAssinatura
    Assinatura "1" --> "1" PedidoRefeicoes
    Assinatura "1" --> "1" EnderecoEntrega
    Assinatura "1" --> "0..1" Pagamento
    Assinatura "1" --> "0..1" Protocolo
    Assinatura "1" --> "1" StatusAssinatura

    PlanoAssinatura "1" --> "1" Periodicidade

    PedidoRefeicoes "1" --> "1..*" ItemPedido
    ItemPedido "1" --> "1" ItemCardapio

    ItemCardapio <|-- PratoPrincipal
    ItemCardapio <|-- Acompanhamento
    ItemCardapio <|-- Sobremesa

    CardapioSemanal "1" --> "0..*" ItemCardapio

    Pagamento "1" --> "1" CartaoCredito
    Pagamento "1" --> "1" StatusPagamento
    Pagamento ..> GatewayPagamento : usa
    GatewayPagamento <|.. OperadoraCartaoCreditoGateway
```

## Relacionamentos principais

- Um **Assinante** pode ter várias **Assinaturas** ao longo do tempo, e registra suas **PreferenciaAlimentar**.
- Cada **Assinatura** agrega um **PlanoAssinatura**, um **PedidoRefeicoes**, um **EnderecoEntrega**, e opcionalmente um **Pagamento** e um **Protocolo**.
- **ItemCardapio** é uma superclasse abstrata especializada em **PratoPrincipal**, **Acompanhamento** e **Sobremesa**; o **CardapioSemanal** reúne os itens disponíveis na semana.
- **PedidoRefeicoes** é composto por **ItemPedido**, cada um referenciando um **ItemCardapio** com sua quantidade.
- **Pagamento** depende da interface **GatewayPagamento** (implementada por **OperadoraCartaoCreditoGateway**) em vez de depender diretamente da operadora — isso garante baixo acoplamento entre o domínio e o sistema externo.
