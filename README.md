# WMK Developer Studio

**IDE desktop para desenvolvimento de software, baseada no projeto open-source OpenIDEA.**

> Projeto em evolução. A presença de um módulo no código não garante que todas as funcionalidades estejam concluídas ou testadas no Windows.

**Desenvolvimento e personalização WMK:** Walney Moreira Klein — walneyk@hotmail.com  
**Projeto original:** [OpenIDEA, de l0ng-ai e colaboradores](https://github.com/l0ng-ai/openidea)  
**Licença:** [Apache 2.0](LICENSE). Consulte também [NOTICE](NOTICE) e [licenças de terceiros](THIRD_PARTY_LICENSES.md).

## Ações de IA no editor — primeira implementação WMK

A base agora registra quatro ações no menu do editor e na busca de ações:

- **WMK IA: Explicar código** — análise em português, somente leitura.
- **WMK IA: Revisar código** — bugs, segurança, desempenho e recomendações, somente leitura.
- **WMK IA: Propor correção** — prepara uma solicitação de alteração com exigência de diff e testes.
- **WMK IA: Gerar testes** — prepara uma solicitação de testes cobrindo casos normais e extremos.

**Como usar:** abra um projeto confiável, selecione um trecho no editor ou mantenha apenas o arquivo aberto, clique com o botão direito e escolha uma ação **WMK IA**. A IDE abre o rascunho de uma tarefa do agente, adicionando a referência ao arquivo e às linhas selecionadas quando possível. Revise o pedido, selecione o agente configurado e só então inicie a tarefa.

**Segurança e estado:** as ações **não executam automaticamente** o agente, comandos ou alterações. A execução posterior segue as permissões e configurações do sistema ACP, e ainda não foi validada no build Windows WMK. Para correções, prefira um projeto de teste e isolamento por worktree. O roadmap completo registra a futura camada WMK Safe Changes, checkpoints e revisão por múltiplos agentes.

## Manual de agentes de IA

**Novo:** [Manual completo de Codex, OpenCode, Groq, Ollama, ACP, MCP e revisão de código](manuais/manual-agentes-ia.html). Guia pt-BR com 12 módulos, configuração Windows, exemplos e exercícios práticos.

## Planejamento e etapas de testes

Consulte o **[roadmap.html](roadmap.html)** para visualizar o planejamento completo e interativo (GameDev, IA, MCP, plugins, tradução e builds Windows). O checklist do HTML é local ao navegador e não altera automaticamente o GitHub.

**Versão de testes Windows:** o workflow já está configurado, mas somente o log de uma execução concluída com sucesso comprova que o executável foi gerado e que o empacotamento funcionou. O nome da aplicação e da janela foi ajustado para WMK Developer Studio; o nome interno de alguns binários continua OpenIDEA nesta fase, para não quebrar integrações existentes.

A arte aprovada deve substituir os PNG/ICO no diretório `src-tauri/icons/`. Até essa substituição, o build ainda poderá mostrar ícones originais. A atualização automática não estará disponível antes de publicarmos nosso próprio manifesto e assinatura.

## O que realmente existe no código

- Editor com CodeMirror e suporte declarado a mais de 60 linguagens.
- Integração LSP para recursos de inteligência de código; depuração via DAP.
- Terminal, Git, execução de projetos, banco de dados e cliente HTTP.
- **Agentes de IA via ACP (Agent Client Protocol):** suporte à conexão com agentes externos, como Claude Code, Codex e Gemini CLI. Instalação/autenticação e disponibilidade dos executáveis dependem do usuário.
- **MCP:** servidor MCP local fornecido por `ide-mcp`, com transporte HTTP em `127.0.0.1` e ponte stdio; interface para configurar servidores MCP externos usados pelos agentes.
- Sistema de plugins WebAssembly, com API ainda em preview.
- Catálogo de tradução em português em `src/platform/locales/text/pt.json`. A cobertura precisa ser revisada.

**Importante:** Groq e Ollama **não estão anunciados aqui como provedores nativos prontos**. É uma melhoria planejada e exigirá implementação e testes de integração. ACP e MCP não significam automaticamente integração direta com qualquer API de modelos.

## Instalação — Windows

Acesse [GitHub Actions](https://github.com/WalneyNF/WMK-Developer-Studio/actions/workflows/wmk-windows.yml), execute **Compilar WMK Windows** e baixe o ZIP gerado na seção *Artifacts* ao terminar com sucesso.

O ZIP de artefato contém os instaladores produzidos pelo Tauri e uma versão portátil quando o build concluir. **Não há executável publicado até que uma execução termine com sucesso.** Para distribuição pública, publique o artefato em [Releases](https://github.com/WalneyNF/WMK-Developer-Studio/releases).

### Desenvolvedores

Pré-requisitos: Windows com MSVC/Build Tools, Rust conforme `Cargo.toml` (mínimo 1.96), Node.js >=22.18 e pnpm 11.

```powershell
git clone https://github.com/WalneyNF/WMK-Developer-Studio.git
cd WMK-Developer-Studio
pnpm install --frozen-lockfile
pnpm tauri dev
```

Para compilar localmente: `pnpm exec tauri build`. Uma compilação fria do Rust consome muitos gigabytes de disco e pode ser demorada. Para computadores com pouco espaço, prefira o Actions.

## Identidade visual

A identidade aprovada é a marca **WMK Developer Studio** em azul/ciano/roxo. A logo oficial deve ser mantida em `assets/brand/logo-oficial.png`; veja [orientações de identidade](assets/brand/README.md). A imagem original foi fornecida pelo responsável pelo fork. Não utilize imagens de terceiros sem permissão.

## Como funciona a IA

1. Abra um projeto confiável.
2. Entre em **Agents / Coding Agents** e configure o executável do agente ACP escolhido.
3. Autentique esse agente por seus próprios meios, caso solicitado.
4. Em **External MCP Servers**, registre as ferramentas MCP que deseja disponibilizar ao agente.
5. Revise as permissões antes de permitir alterações ou execução de comandos.

Os agentes ACP e o servidor MCP são componentes distintos; não confunda o servidor MCP da IDE com uma chave de API de provedores LLM.

## Roadmap WMK

- [ ] Confirmar build funcional da marca WMK no Windows (acompanhar [GitHub Actions](https://github.com/WalneyNF/WMK-Developer-Studio/actions/workflows/wmk-windows.yml)).
- [ ] Aplicar a arte oficial aos ícones do executável e instalador.
- [ ] Auditar e completar a localização pt-BR.
- [ ] Criar painel configurável de Groq/Ollama com armazenamento seguro de credenciais.
- [ ] Perfis de projetos PHP, Python, JavaScript, Rust e Godot.
- [ ] Gerador visual e assistido de projetos com execução de testes.
- [ ] Empacotar releases verificadas e documentadas.

## Créditos e termos

Personalização WMK: **Walney Moreira Klein — walneyk@hotmail.com**.  
Base original: **OpenIDEA**, desenvolvido por **l0ng-ai e colaboradores**.  
Este fork não possui vínculo com a JetBrains. IntelliJ IDEA é marca registrada da JetBrains.

Não remova o arquivo LICENSE, NOTICE ou THIRD_PARTY_LICENSES.md.