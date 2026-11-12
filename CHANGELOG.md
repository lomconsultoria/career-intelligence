# Histórico de versões

## 2.0.0 — novembro de 2026 (portabilidade, segurança e correções)

**Portabilidade**
- Frontmatter no padrão Agent Skills: `license`, `compatibility` e `metadata` (autor, contato, versão).
- Sem dependência de ferramentas de um assistente específico: o Modo B funciona só com o texto do perfil colado ou o PDF.
- Conteúdo dividido em `references/`, lidas só quando a etapa pede.
- Descrição reescrita para acionar a skill também ao avaliar uma vaga, calcular salário, mandar convites ou mensagens a recrutadores e antes de qualquer ação no LinkedIn em nome da pessoa. No teste, a versão anterior da descrição não acionava a skill em 3 de 5 casos.

**Segurança**
- **Sem automação no LinkedIn:** a 1.x mandava ler o LinkedIn por automação de navegador, o que o Contrato do Usuário do LinkedIn proíbe e pode restringir a conta. Agora a skill usa texto colado ou PDF, não extrai dados em lote, não prepara ferramentas de navegador para pedidos de automação e recusa convites em massa com uma alternativa.
- **Não age na conta:** não faz login, não envia convite ou mensagem, não se candidata, não publica.
- **Conteúdo de terceiros é dado:** textos escondidos em vagas, perfis e páginas são ignorados e relatados.
- **Dados pessoais:** os da pessoa fora de buscas e URLs; de terceiros, só informação profissional pública, sem dossiê.

**Corrigido**
- **Lei 14.442/2022:** a 1.x dizia que a pessoa podia "exigir" o teletrabalho no contrato. O art. 75-C diz que ele deve constar do contrato, e o § 2º permite ao empregador determinar a volta ao presencial com 15 dias de transição.
- **Competências principais:** a 1.x dizia que não eram editáveis. Desde 2023 o LinkedIn permite escolher até 5 na seção Sobre.
- **PJ x CLT:** a 1.x usava "some 20 a 30%" sem fonte. Agora a comparação é item a item, com lacunas declaradas.
- **Faixa salarial:** a 1.x mandava estimar quando a pessoa não sabia. Agora só com fonte citada e datada.
- **Mensagem de abordagem:** nova versão curta de até 200 caracteres para a nota do convite de conexão.
- **Coleta:** o Modo B não pede mais pretensão salarial.

**Testes**
- 5 casos em `evals/` com critérios de comportamento, verificação de que a skill foi acionada e de que o navegador não foi aberto. Resultados em `tests/resultados-evals.md`.

## 1.x — setembro de 2026
Versão inicial, de uso pessoal.
