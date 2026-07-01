# PSIII — Auditoria Automatizada de Segurança SSL/TLS
## Automação de Diagnóstico de Vulnerabilidades com IA para Servidor Web

Workflow n8n que analisa a segurança de um host (SSL/TLS, certificado digital), usa uma IA para interpretar os resultados e gera um relatório em PDF enviado por e-mail.

## O que o fluxo faz

1. **Início e definição do alvo**: o fluxo é disparado manualmente e o hostname a ser analisado é configurado.
2. **Varredura SSL Labs**: solicita uma análise à API do SSL Labs e aguarda em loop até que o processamento esteja concluído.
3. **Análise dos dados**: os resultados são processados em paralelo — verificação de protocolos SSL/TLS e análise do certificado digital — e depois unificados.
4. **Interpretação por IA**: um agente de IA (modelo DeepSeek) analisa os dados técnicos e gera um relatório em Markdown, com classificação de risco e recomendações, usando um parser de saída estruturada.
5. **Geração e envio do relatório**: o Markdown é convertido em HTML, transformado em PDF e enviado por e-mail ao destinatário configurado.

## Principais integrações

- **SSL Labs API** — coleta de dados técnicos de SSL/TLS.
- **DeepSeek (via LangChain/n8n)** — geração do relatório de análise.
- **PDFShift** — conversão do relatório HTML em PDF.
- **E-mail (SMTP)** — envio do relatório final ao destinatário.

## Requisitos

- Instância n8n com os pacotes `@n8n/n8n-nodes-langchain` instalados.
- Credenciais configuradas para: SSL Labs (não requer chave, mas respeita rate limit), DeepSeek (API key), PDFShift (API key) e envio de e-mail (SMTP).

## Como usar

1. Importe o arquivo `PSIII.json` no n8n.
2. Configure as credenciais dos serviços acima.
3. Ajuste o hostname alvo no nó de definição do alvo, se necessário.
4. Execute o fluxo manualmente pelo gatilho inicial.
