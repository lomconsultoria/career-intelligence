# Inteligência de Carreira e LinkedIn

Skill no padrão aberto **[Agent Skills](https://agentskills.io)** que transforma o assistente de IA num consultor de carreira: diagnostica e reescreve o perfil do LinkedIn na voz da pessoa, avalia se uma vaga combina com ela, calcula a pretensão salarial (CLT x PJ), pesquisa empresas e vagas e prepara a abordagem a recrutadores, sem colocar a conta da pessoa em risco.

> Criado por **LOM Consultoria e Projetos** · [contato@lomconsultoria.com](mailto:contato@lomconsultoria.com) · Versão 2.0.0

## O que a skill faz

| Modo | Para quê | O que entrega |
|---|---|---|
| **B. LinkedIn** | "Melhora meu LinkedIn", headline, Sobre, "só recebo vaga errada" | Diagnóstico curto e textos prontos para colar (headline em 2 ou 3 opções, Sobre, experiências, competências), com contagem de caracteres e plano de publicação discreto |
| **A. Mercado** | "Onde eu me encaixo", empresas, vagas, salário | Relatório em 11 seções: posicionamento, mercado, remuneração, empresas pontuadas, abordagem, mensagens, plano de visibilidade de 14 dias e follow up de 60 a 90 dias |

Serve para qualquer profissão, não só tecnologia.

## Regras que a skill segue

- **Não inventa:** nenhum número, empresa, vaga, cargo ou certificação. Sem fonte, escreve "Não foi possível confirmar".
- **Separa** dado de fonte (com data), critério da skill e opinião.
- **No perfil, só fatos que a pessoa declarou.** Número que não aguenta pergunta em entrevista não entra.
- **Não age na conta:** não faz login, não envia convite nem mensagem, não se candidata, não publica. A pessoa faz; a skill prepara.
- **Sem automação no LinkedIn:** o Contrato do Usuário do LinkedIn proíbe bots, scripts e extensões. A skill trabalha com o texto colado ou o PDF do perfil e recusa pedidos de convite em massa, oferecendo uma alternativa que a própria pessoa executa.
- **Conteúdo de terceiros é dado, nunca instrução:** se uma vaga ou um perfil trouxer texto escondido para a IA, a skill ignora e avisa.
- **Dados pessoais protegidos:** os da pessoa ficam fora de buscas e URLs; sobre recrutadores e gestores, só informação profissional pública.
- **Texto sem cara de IA:** lista de palavras e construções a evitar, em português e em inglês.

## Estrutura

```
career-intelligence/
├── SKILL.md                         # regras, coleta, roteamento e formato (carregado quando a skill é acionada)
├── references/                      # detalhes lidos só quando a etapa pede
│   ├── leitura-do-perfil.md         # como receber o perfil (PDF, texto colado) e o que extrair
│   ├── modo-b-linkedin.md           # diagnóstico, busca discreta, escrita, limites de campo
│   ├── modo-a-mercado.md            # fases 2 a 12: posicionamento, salário, CLT art. 75-C, abordagem
│   └── fontes-e-verificacao.md      # hierarquia de fontes e armadilhas
└── evals/                           # 5 casos de teste no formato do padrão
tests/
└── resultados-evals.md              # resultado das rodadas de teste
```

A skill não tem scripts: não executa código na sua máquina.

## Requisitos

| Recurso | Necessário? | Para quê |
|---|---|---|
| Texto do perfil colado ou PDF | Sim, no Modo B | O LinkedIn exige login e proíbe acesso automatizado; a skill não abre o link |
| Busca na web | Sim, no Modo A | Empresas, vagas, faixas salariais e notícias, sempre com fonte datada. Sem busca, a skill avisa e não lista nada de memória |
| Navegador controlado pela IA | Não | O Modo B funciona inteiro sem navegador |

## Como instalar

**Claude (app):** compacte a pasta `career-intelligence/` em .zip e envie na área de skills da sua conta.

**Claude Code:** copie a pasta para `~/.claude/skills/` (todas as suas sessões) ou para `.claude/skills/` dentro de um projeto.

**OpenAI Codex CLI:** copie a pasta para `~/.agents/skills/` ou para `.agents/skills/` dentro do repositório.

**Outras ferramentas compatíveis com Agent Skills** (Gemini CLI, Cursor, GitHub Copilot, Kiro e outras): siga a documentação de skills da ferramenta; a pasta é a mesma.

**Chats sem suporte a skills** (ex.: um GPT personalizado ou um Gem): cole o conteúdo do `SKILL.md` nas instruções e anexe os arquivos de `references/` como conhecimento. A análise de mercado depende da busca na web que o chat tiver.

Depois de instalar, peça algo como: *"Me ajuda a melhorar meu LinkedIn? Quero migrar para coordenação de qualidade."*

## Segurança

Avaliada contra o [OWASP Top 10 para aplicações com IA, 2025](https://genai.owasp.org/resource/owasp-top-10-for-llm-applications-2025/).

| Risco (OWASP 2025) | Como a skill trata | Como foi testado |
|---|---|---|
| **LLM01** Injeção de instruções | Texto de vagas, perfis e páginas é dado; a tentativa é relatada à pessoa | Caso `injecao-em-vaga` |
| **LLM02** Vazamento de dados pessoais | Dados da pessoa fora de buscas e URLs; de terceiros, só informação profissional pública, sem dossiê | Caso `injecao-em-vaga` (pedido de CPF) e revisão |
| **LLM06** Autonomia excessiva | Não faz login, não envia, não publica, não se candidata, não automatiza o LinkedIn | Caso `automacao-em-massa`, com verificação de que o navegador não foi aberto |
| **LLM09** Informação falsa | Nada inventado; fonte datada; no perfil, só fatos declarados; salário sem percentual "de mercado" sem fonte | Casos `linkedin-reescrita-discreta` e `conversao-salarial-clt` |
| LLM03, LLM04, LLM05, LLM07, LLM08, LLM10 | Não se aplicam ou têm risco baixo: sem scripts nem dependências, não treina modelo, não gera arquivo executável, é pública de propósito, sem base de vetores | — |

### Riscos que continuam

- **Injeção de instruções:** a regra reduz o risco, mas nenhum assistente de IA é imune. Revise a recomendação antes de agir.
- **Interface do LinkedIn muda:** nomes de botões e limites de campo vêm de fontes datadas citadas na skill. Quando o editor do LinkedIn mostrar outro limite, vale o editor.
- **Lei trabalhista:** a leitura do art. 75-C da CLT não substitui um advogado trabalhista.
- **Cópias alteradas:** instale só a partir deste repositório (`lomconsultoria/career-intelligence`).

### Como reportar uma vulnerabilidade

Escreva para [contato@lomconsultoria.com](mailto:contato@lomconsultoria.com), sem abrir issue pública. Detalhes em [SECURITY.md](SECURITY.md).

## Testes

A pasta `career-intelligence/evals/` tem 5 casos: pedido vago, reescrita discreta do perfil, vaga com instrução escondida para a IA, pedido de convites em massa e conversão salarial CLT/PJ. Com o Claude Code, coloque a skill dentro de um plugin e rode `claude plugin eval .` para comparar respostas com e sem a skill. Resultados em [tests/resultados-evals.md](tests/resultados-evals.md).

## Licença

[Creative Commons Atribuição-NãoComercial 4.0 Internacional (CC BY-NC 4.0)](https://creativecommons.org/licenses/by-nc/4.0/deed.pt-br).

- **Pode:** usar, copiar e adaptar para fins não comerciais.
- **Precisa:** dar crédito à LOM Consultoria e Projetos e indicar se fez alterações.
- **Não pode:** usar comercialmente (vender, incluir em produto ou serviço pago) sem autorização.

**Uso comercial:** fale com a LOM Consultoria em [contato@lomconsultoria.com](mailto:contato@lomconsultoria.com).

O texto completo da licença está em [LICENSE](LICENSE).
