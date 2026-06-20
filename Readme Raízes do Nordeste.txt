================================================================================
          REDE "RAÍZES DO NORDESTE" - ECOSSISTEMA CENTRAL DE SOFTWARE
     TRILHA: ENGENHARIA DE REQUISITOS E GARANTIA DA QUALIDADE DE SOFTWARE (QA)
================================================================================

1. VISÃO GERAL DO SISTEMA
--------------------------------------------------------------------------------
Este software simula o motor lógico e a camada de resiliência do Back-end central
da Rede "Raízes do Nordeste", projetado para sustentar a expansão multicanal da
franquia alimentícia (App, Totem e Balcão).

O foco principal desta implementação é validar de forma prática as diretrizes de
Qualidade de Software (QA Plan), tratando regras complexas de negócio como:
- Validação rigorosa e simultânea de estoque local por unidade (Franquias);
- Controle cronológico automático de cardápios sazonais (Ex: Período Junino);
- Logs imutáveis de segurança e auditoria (Garantia de conformidade);
- Tolerância a falhas (Fault Tolerance) e desacoplamento assíncrono com gateways
  de pagamento externos através de um sistema interno de mensageria por fila.


2. TECNOLOGIAS UTILIZADAS
--------------------------------------------------------------------------------
- Linguagem de Programação: TypeScript (Versão 5.x)
- Ambiente de Execução: Node.js (Recomendado v18+)
- Mecanismo de Simulação: Suíte de Execução de QA Integrada (Caixa-Cinza)


3. COMO EXECUTAR O CÓDIGO
--------------------------------------------------------------------------------

OPÇÃO A: EXECUÇÃO ONLINE (RÁPIDA E SEM INSTALAÇÃO)
1. Abra o navegador e acesse: https://www.typescriptlang.org/play
2. Copie o código fonte completo do arquivo principal do sistema.
3. Cole o código na janela localizada no lado esquerdo da tela do site.
4. Clique no botão "Run" (Executar) situado no menu superior.
5. Os resultados de usabilidade e logs de teste serão exibidos imediatamente
   no painel de console ("Logs") do lado direito.

OPÇÃO B: EXECUÇÃO LOCAL (VIA TERMINAL / COMPUTADOR)
1. Certifique-se de ter o Node.js instalado na sua máquina (https://nodejs.org).
2. Abra o terminal do seu computador (Prompt de Comando ou PowerShell).
3. Instale o executor global do TypeScript rodando o comando:
   npm install -g ts-node typescript
4. Crie um arquivo chamado "index.ts" e cole o código fonte fornecido.
5. Pelo terminal, navegue até a pasta do arquivo e execute o comando:
   ts-node index.ts


4. CENÁRIOS DE TESTE COBERTOS NA EXECUÇÃO (USABILIDADE DE QA)
--------------------------------------------------------------------------------
Ao executar o script, o sistema rodará de forma autônoma uma bateria automática
de testes de sistema e de arquitetura, gerando as seguintes saídas:

[CENÁRIO 1] - Pedido via App com Sucesso (Baseado no CT-01)
- Objetivo: Testar a integração do fluxo perfeito de compra.
- Saída: O sistema valida o estoque, retém o pedido na fila assíncrona, faz a
  chamada simulada ao gateway de pagamento (Online) e envia para a cozinha.

[CENÁRIO 2] - Bloqueio por Falha de Estoque Local (Baseado no CT-02)
- Objetivo: Testar o comportamento negativo ao tentar vender item sem estoque.
- Saída: O sistema bloqueia a transação na origem e dispara a mensagem de erro
  esperada: "HTTP 422: Produto indisponível nesta unidade."

[CENÁRIO 3] - Resiliência com Gateway de Pagamento Offline (Baseado no CT-04)
- Objetivo: Testar a tolerância a falhas caso o parceiro de pagamento caia.
- Saída: O sistema não crasha. Ele mantém o pedido protegido na fila de
  mensageria, preserva o estoque provisório local e emite um alerta seguro
  para o dispositivo móvel do usuário ("HTTP 503").

[CENÁRIO 4] - Segurança e Imutabilidade de Auditoria (Baseado no CT-09)
- Objetivo: Impedir que fraudes ou deleções manuais de logs aconteçam nas lojas.
- Saída: O sistema rejeita categoricamente qualquer tentativa de deleção ou
  alteração de registros históricos, gerando um erro de segurança "HTTP 403".


5. EVIDÊNCIAS E MONITORAMENTO (FOCO NA BANCA EXAMINADORA)
--------------------------------------------------------------------------------
Todas as ações geradas na execução disparam logs em formato JSON padronizado
pelo "ServiçoAuditoria", simulando perfeitamente os insumos técnicos que alimentam
os painéis de monitoramento (Grafana/Prometheus) detalhados no plano de métricas 
do projeto multidisciplinar da UNINTER.

--------------------------------------------------------------------------------
      Desenvolvido para o Estudo de Caso Multidisciplinar - Ano 2026
================================================================================