# UC-02 — Agendar horário

| Campo | Conteúdo |
| --- | --- |
| **Requisitos** | RF-01, RF-02, RF-08, RNF-04, RD-01 |
| **Ator principal** | Cliente |
| **Atores secundários** | — (o atendente executa o mesmo fluxo no "Fazer encaixe") |
| **Prioridade** | Must Have (US-01 e US-02) |

## Pré-condições
1. O cliente tem acesso ao sistema pelo celular.
2. A barbearia tem ao menos um barbeiro e um serviço cadastrados.

## Pós-condições
- **Sucesso:** agendamento registrado com status AGENDADO; o horário deixa de estar disponível para aquele barbeiro.
- **Falha:** nenhum agendamento é criado e a agenda permanece inalterada.

## Fluxo principal
1. O cliente informa o telefone.
2. O sistema envia um código de uso único (válido por 5 minutos).
3. O cliente informa o código e o sistema o autentica (sem CPF).
4. O sistema exibe os serviços; o cliente escolhe um (ex.: "Corte + barba").
5. O sistema exibe os barbeiros; o cliente escolhe um (ex.: Cauã).
6. O sistema exibe os horários livres do barbeiro; o cliente escolhe um (ex.: 25/09/2026 às 15h00).
7. O cliente revisa o resumo e confirma.
8. O sistema verifica novamente que o horário continua livre.
9. O sistema registra o agendamento (AGENDADO), bloqueia o horário e exibe a confirmação.

## Fluxos alternativos
- **A1 — Cliente já autenticado (passo 1):** o sistema pula os passos 1 a 3.
- **A2 — Cliente volta uma tela (passos 4 a 6):** o sistema mantém as escolhas já feitas.
- **A3 — Cliente desiste (passo 7):** nenhum agendamento é criado.

## Fluxos de exceção
- **E1 — Código inválido ou expirado (passo 3):** o sistema informa o erro e oferece reenviar o código.
- **E2 — Horário ocupado (passo 8):** outro cliente reservou antes. O sistema informa que o horário não está disponível e volta ao passo 6 com a lista atualizada. (RF-02)
- **E3 — Nenhum horário livre (passo 6):** o sistema informa e sugere outro barbeiro ou outro dia.
- **E4 — Falha de comunicação (passo 9):** o sistema não cria o agendamento e pede para tentar novamente.

## Regras de negócio
- RN-01: um barbeiro não pode ter dois agendamentos no mesmo horário.
- RN-02: só são coletados nome e telefone do cliente (RD-01).
- RN-03: o fluxo deve ser concluído em no máximo 3 telas e 60 segundos (RNF-04).
