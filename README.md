# Noctools v4

Central de ferramentas criada por 𝑺𝒄𝒐𝒕𝒕.𝑴 em 25 de setembro de 2026.

## Scott.M: IA oficial + APIs próprias

O Scott.M agora pode trabalhar com várias fontes:

- **IA oficial do Noctools:** chaves privadas na Vercel.
- **Automático:** tenta as APIs oficiais configuradas e pode fazer fallback quando uma delas falha por indisponibilidade, quota ou erro temporário.
- **API personalizada:** o visitante informa endpoint, modelo e chave próprios.

O modo personalizado é genérico: aceita serviços com API compatível com OpenAI Chat Completions. Assim, a Scott.M não fica presa a um único fornecedor.

O Gemini oferece compatibilidade com o formato OpenAI; Mistral, DeepSeek, OpenRouter e xAI também documentam compatibilidade com APIs/SDKs no estilo OpenAI. Isso permite ampliar a lista sem prender o Scott.M a um único fornecedor.

## Configuração da aplicação

Configure somente as chaves que você quer oferecer. Todas ficam no servidor:

## Recursos novos além das ferramentas

- Sidebar do site com categorias e tema claro/escuro.
- Sidebar do Scott.M com pesquisa de conversas.
- Renomear conversas.
- Criar, apagar e apagar todas as conversas.
- Exportar e importar histórico em JSON.
- Perfis de instrução: padrão, estudos, programação e criativo.
- Histórico ajustável.
- Upload de imagens e arquivos de texto.
- Tema claro/escuro.
- Atalho `Ctrl/Cmd + K`.
- APIs oficiais com fallback.
- API personalizada para quando a cota oficial acabar.

## Segurança

Não coloque as chaves oficiais em `NEXT_PUBLIC_*` nem no JavaScript do navegador. A rota `/api/ai` usa as variáveis privadas da Vercel. Como essa rota é pública, considere adicionar autenticação, rate limiting ou algum limite de uso para evitar consumo inesperado da sua cota.

A API personalizada fica no navegador do visitante por escolha dele; o Noctools não recebe nem salva essa chave no servidor.

## Scott.M — recursos avançados v5

- Perfil visual da Scott.M usando a imagem incluída em `scott-avatar.webp`.
- Composer escuro inspirado em apps de conversa: câmera, anexos, voz, agendamento e envio.
- Upload de imagens e arquivos de código/texto.
- Análise visual quando o modelo/provedor configurado oferece visão.
- Perfil de programação para criação e correção de projetos.
- Quando a IA responde com blocos `@@FILE: caminho/arquivo.ext` + bloco de código, o chat oferece **Baixar projeto .zip**.
- Entregas agendadas ficam salvas no navegador e podem gerar notificações do sistema. Para executar com a página completamente fechada, é necessário um backend persistente/cron; o agendamento local não promete execução em segundo plano do navegador.
- APIs oficiais continuam protegidas por variáveis de ambiente da Vercel.

## Noctools v8

Scott.M ganhou uma camada de Workspace local: progresso de tarefas, projeto/notas, diagnóstico básico, linha do tempo de atividades, estatísticas locais, compartilhamento de conversa via link, exportação da conversa atual, rascunho automático, ações sobre texto selecionado, tela cheia e PWA básico. Também foram adicionados feedback por resposta e mensagens fixadas.

Observação: agendamentos e notificações locais continuam dependentes do navegador disponível; para execução garantida com o site fechado, use um scheduler no backend.


## Rotas do site
- `/ia` — Scott.M
- `/termo` — termos e privacidade
- `/sobre` — sobre o Noctools
- `/ajuda` — central de ajuda
- `/status` — status
- `/novidades` — novidades

A Vercel usa `vercel.json` para manter essas URLs limpas.

## Vercel: múltiplas chaves e provedores
O backend aceita até 20 chaves por provedor. Use `GROQ_API_KEY`, `GROQ_API_KEY_2`, `GROQ_API_KEY_3`...; o mesmo padrão vale para OpenAI, Gemini, Anthropic, Mistral, DeepSeek, xAI e OpenRouter. Em modo Automático, o backend tenta os provedores configurados e, dentro de cada provedor, as chaves na ordem configurada até obter uma resposta.

Você também pode definir `*_MODELS` como uma lista separada por vírgulas para limitar os modelos aceitos pelo backend.
