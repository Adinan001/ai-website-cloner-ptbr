# AI Website Cloner Template — Tradução PT-BR 🇧🇷

<a href="https://github.com/JCodesMore/ai-website-cloner-template/blob/master/LICENSE"><img src="https://img.shields.io/badge/license-MIT-blue" alt="MIT License" /></a> <a href="https://github.com/JCodesMore/ai-website-cloner-template/stargazers"><img src="https://img.shields.io/github/stars/JCodesMore/ai-website-cloner-template?style=flat" alt="Stars" /></a> <a href="https://discord.gg/hrTSX5yTpB"><img src="https://img.shields.io/discord/1400896964597383279?label=discord" alt="Discord" /></a>

> **Créditos:** Este repositório é uma tradução para o português brasileiro do projeto original [ai-website-cloner-template](https://github.com/JCodesMore/ai-website-cloner-template), criado por [JCodesMore](https://github.com/JCodesMore). Todo o código, arquitetura e lógica do skill pertencem ao autor original. Esta versão tem apenas o objetivo de tornar a documentação acessível para a comunidade brasileira.

Um template reutilizável para engenharia reversa de qualquer site, transformando-o em uma base de código Next.js limpa e moderna usando agentes de codificação com IA.

**Recomendado: [Claude Code](https://docs.anthropic.com/en/docs/claude-code) com Opus 4.8 para melhores resultados** — mas funciona com diversos agentes de codificação com IA.

Aponte para uma URL, execute `/clone-website`, e seu agente de IA inspecionará o site, extrairá tokens de design e assets, escreverá especificações de componentes e despachará construtores em paralelo para reconstruir cada seção.

## Demonstração

[![Assista à demonstração](docs/design-references/comparison.png)](https://youtu.be/O669pVZ_qr0)

> Clique na imagem acima para assistir à demonstração completa no YouTube.

## Início Rápido

> **Importante:** Comece criando sua própria cópia com o botão **Use this template** do GitHub. Não clone este repositório de template diretamente para o seu projeto de site, e não abra pull requests aqui com o site que você gerou.

1. **Crie seu próprio repositório a partir deste template**

   Na página do GitHub deste projeto, clique em **Use this template** e depois em **Create a new repository**.

   Dê um nome ao seu novo repositório, escolha se ele será público ou privado e clique em **Create repository**. Se o GitHub mostrar a opção **Include all branches**, pode deixar desmarcada.

   Isso lhe dá um projeto separado para trabalhar, de modo que as alterações do seu site fiquem na sua conta em vez de voltarem para o template principal.

2. **Abra seu novo repositório no computador**

   Depois que o GitHub criar sua cópia, abra o novo repositório. Clique em **Code** e abra ou clone o repositório com a ferramenta de codificação de sua preferência.

   No terminal, o comando será:

   ```bash
   git clone https://github.com/SEU-USUARIO/SEU-NOVO-REPOSITORIO.git
   cd SEU-NOVO-REPOSITORIO
   ```

3. **Instale as dependências**
   ```bash
   npm install
   ```
4. **Inicie seu agente de IA** — Claude Code recomendado:
   ```bash
   claude --chrome
   ```
   > **Nota para Windows:** Se o Chrome MCP não conectar, use o Playwright MCP como alternativa:
   > ```bash
   > claude mcp add playwright -- npx -y @playwright/mcp@latest
   > ```
   > Depois reinicie o Claude Code com `claude` normalmente.

5. **Execute o skill:**
   ```
   /clone-website <url-alvo1> [<url-alvo2> ...]
   ```
6. **Personalize** (opcional) — após a clonagem base ser construída, modifique conforme necessário

> Usando outro agente? Abra `AGENTS.md` para as instruções do projeto — a maioria dos agentes detecta automaticamente.

## Plataformas Suportadas

| Agente | Status |
| --- | --- |
| [Claude Code](https://docs.anthropic.com/en/docs/claude-code) | **Recomendado** — Opus 4.8 |
| [Codex CLI](https://github.com/openai/codex) | Suportado |
| [OpenCode](https://opencode.ai/) | Suportado |
| [GitHub Copilot](https://github.com/features/copilot) | Suportado |
| [Cursor](https://cursor.com/) | Suportado |
| [Windsurf](https://codeium.com/windsurf) | Suportado |
| [Gemini CLI](https://github.com/google-gemini/gemini-cli) | Suportado |
| [Cline](https://github.com/cline/cline) | Suportado |
| [Roo Code](https://github.com/RooCodeInc/Roo-Code) | Suportado |
| [Continue](https://continue.dev/) | Suportado |
| [Amazon Q](https://aws.amazon.com/q/developer/) | Suportado |
| [Augment Code](https://www.augmentcode.com/) | Suportado |
| [Aider](https://aider.chat/) | Suportado |

## Pré-requisitos

- [Node.js](https://nodejs.org/) 24+
- Um agente de codificação com IA (veja [Plataformas Suportadas](#plataformas-suportadas))

## Stack Tecnológica

- **Next.js 16** — App Router, React 19, TypeScript estrito
- **shadcn/ui** — Primitivos Radix + Tailwind CSS v4
- **Tailwind CSS v4** — Tokens de design oklch
- **Lucide React** — Ícones padrão (substituídos por SVGs extraídos durante a clonagem)

## Como Funciona

O skill `/clone-website` executa um pipeline em múltiplas fases:

1. **Reconhecimento** — capturas de tela, extração de tokens de design, varredura de interações (rolagem, clique, hover, responsividade)
2. **Fundação** — atualiza fontes, cores, estilos globais, baixa todos os assets
3. **Especificações de Componentes** — escreve arquivos de especificação detalhados (`docs/research/components/`) com valores CSS computados exatos, estados, comportamentos e conteúdo
4. **Construção em Paralelo** — despacha agentes construtores em git worktrees, um por seção/componente
5. **Montagem e QA** — mescla worktrees, conecta a página, executa comparação visual contra o original

Cada agente construtor recebe a especificação completa do componente inline — valores exatos de `getComputedStyle()`, modelos de interação, conteúdo com múltiplos estados, breakpoints responsivos e caminhos de assets. Sem adivinhação.

## Casos de Uso

- **Migração de plataforma** — reconstrua um site que você possui, saindo de WordPress/Webflow/Squarespace para uma base de código Next.js moderna
- **Código-fonte perdido** — seu site está no ar, mas o repositório sumiu, o desenvolvedor saiu ou a stack é legada. Recupere o código em formato moderno
- **Aprendizado** — desconstrua como sites em produção alcançam layouts, animações e comportamento responsivo específicos, trabalhando com código real

## Não Destinado Para

- **Phishing ou falsificação de identidade** — este projeto não deve ser usado para fins enganosos, falsificação de identidade ou qualquer atividade que viole a lei.
- **Apresentar o design de outra pessoa como seu** — logos, assets de marca e textos originais pertencem a seus proprietários.
- **Violar termos de serviço** — alguns sites proíbem explicitamente scraping ou reprodução. Verifique antes.

## Estrutura do Projeto

```
src/
  app/              # Rotas do Next.js
  components/       # Componentes React
    ui/             # Primitivos shadcn/ui
    icons.tsx       # Ícones SVG extraídos
  lib/utils.ts      # Utilitário cn()
  types/            # Interfaces TypeScript
  hooks/            # Hooks React customizados
public/
  images/           # Imagens baixadas do alvo
  videos/           # Vídeos baixados do alvo
  seo/              # Favicons, imagens OG
docs/
  research/         # Saída de extração e specs de componentes
  design-references/ # Capturas de tela
scripts/
  sync-agent-rules.sh  # Regenera arquivos de instrução para agentes
  sync-skills.mjs      # Regenera /clone-website para todas as plataformas
AGENTS.md           # Instruções do agente (fonte única da verdade)
CLAUDE.md           # Configuração do Claude Code (importa AGENTS.md)
GEMINI.md           # Configuração do Gemini CLI (importa AGENTS.md)
```

## Comandos

```bash
npm run dev        # Inicia servidor de desenvolvimento
npm run build      # Build de produção
npm run lint       # Verificação ESLint
npm run typecheck  # Verificação TypeScript
npm run check      # Executa lint + typecheck + build
```

### Com Docker

```bash
docker compose up app --build  # Compila e executa o app
docker compose up dev --build  # Executa o app em modo dev na porta 3001
```

## Atualização para Outras Plataformas

Dois arquivos-fonte da verdade sustentam todo o suporte a plataformas. Edite o fonte e depois execute o script de sincronização:

| O quê | Fonte da verdade | Comando de sincronização |
| --- | --- | --- |
| Instruções do projeto | `AGENTS.md` | `bash scripts/sync-agent-rules.sh` |
| Skill `/clone-website` | `.claude/skills/clone-website/SKILL.md` | `node scripts/sync-skills.mjs` |

Cada script regenera automaticamente as cópias específicas de cada plataforma. Agentes que leem os arquivos-fonte nativamente não precisam de regeneração.

## Dica para Usuários Windows

Se o `claude --chrome` não conectar o Chrome MCP corretamente, use o Playwright como alternativa de automação de browser:

```bash
# Fora do Claude Code, no terminal:
claude mcp add playwright -- npx -y @playwright/mcp@latest

# Depois abra o Claude Code normalmente:
claude
```

## Histórico de Estrelas (Projeto Original)

[![Star History Chart](https://api.star-history.com/svg?repos=JCodesMore/ai-website-cloner-template&type=Date)](https://star-history.com/#JCodesMore/ai-website-cloner-template&Date)

## Créditos

- **Autor original:** [JCodesMore](https://github.com/JCodesMore) — [Repositório original](https://github.com/JCodesMore/ai-website-cloner-template)
- **Tradução PT-BR:** [Adinan001](https://github.com/Adinan001) — [MMG Soluções](https://github.com/Adinan001)

## Licença

MIT — veja o [repositório original](https://github.com/JCodesMore/ai-website-cloner-template/blob/master/LICENSE) para detalhes.
