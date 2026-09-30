# 🍱 Minha Refeição – Serviço de Assinatura de Marmitas

Projeto do caso de uso **"Assinar Plano de Refeições"**, da disciplina **Projeto de Software** — Curso de Ciência da Computação, Universidade Presbiteriana Mackenzie — Profa. Ana Claudia Rossi.

**Aluna:** Isabele Dal Pogetto Costa (RA 10721328)

---

## 📖 Sobre o caso de uso

A plataforma **Minha Refeição** permite ao assinante contratar um plano de assinatura de marmitas, definir a periodicidade e a quantidade de refeições, selecionar pratos, acompanhamentos e sobremesas, registrar preferências alimentares, informar o endereço de entrega e efetuar o pagamento da assinatura.

- **Ator principal:** Assinante
- **Ator secundário:** Operadora de Cartão de Crédito

---

## Entregas N1

- **Storyboard / Protótipo de telas** — protótipo navegável cobrindo o fluxo principal completo (identificação, código de confirmação por SMS, seleção de plano, preferências alimentares, cardápio por categoria, resumo do pedido, endereço, mudança de status da assinatura, pagamento, autorização e confirmação).
- **Classes Candidatas** — lista de classes de domínio identificadas a partir do enunciado, organizadas por categoria (entidades de negócio centrais, cardápio/pedido, entrega, pagamento e suporte ao fluxo).
- **Diagrama de Classes de Domínio** — diagrama UML com as classes candidatas, seus atributos, a herança de `ItemCardapio` (especializada em `PratoPrincipal`, `Acompanhamento` e `Sobremesa`) e a dependência de `Pagamento` na interface `GatewayPagamento`.

---

## 🗂️ Wiki

Consulte a [Wiki do projeto](../../wiki) para:
- Storyboard / Protótipo de telas
- Classes Candidatas
- Diagrama de Classes de Domínio
