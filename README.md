# Notícias Diárias
Este repositório contém o workflow de automação para curadoria e resumo de notícias utilizando IA Generativa. O sistema monitora feeds RSS, processa o conteúdo via Google Gemini e entrega um resumo executivo diretamente no WhatsApp.

A solução foi desenhada com foco em soberania de dados e segurança, rodando inteiramente em uma infraestrutura Self-Hosted.

## Arquitetura e Tecnologias
### Core da Aplicação
- n8n: Orquestrador de workflow low-code para integração de serviços.
- Google Gemini (Pro/Flash): Modelo de IA utilizado para sumarização de texto.
- Evolution API: Instância de API para integração profissional com o ecossistema WhatsApp.
### Infraestrutura & DevOps
- Oracle Cloud Infrastructure (OCI): Hospedagem em instâncias Always Free (aarch64).
- Docker & Docker Compose: Gerenciamento de containers para portabilidade e isolamento de dependências.
- Nginx Reverse Proxy: Gerenciamento de tráfego de entrada com terminação TLS/SSL.

## Segurança
- Controle de Acesso: Implementação de Network Security Groups (NSG) na OCI para bloqueio de IPs e controle granular de portas.
- Criptografia: Certificados SSL/TLS ativos para comunicação segura via domínio personalizado.
- Isolamento: Containers rodando em redes Docker internas, expondo apenas o necessário via Proxy.

## Workflow
1. Schedule: Gatilho configurado para execução diária automática.
1. RSS Reader: Captura as últimas 10 notícias de feeds selecionados (ex: TechCrunch).
1. HTML Extract: Realiza requisições HTTP para extrair o conteúdo textual bruto das páginas.
1. AI Processing: O Gemini analisa o texto e gera um resumo objetivo de até 10 linhas.
1. JS Format: Um nó de código (JavaScript) formata os dados para o envio.
1. WhatsApp Delivery: Envio via POST para a Evolution API.

## Pré-requisitos
- Instância n8n ativa.
- Instância Evolution API configurada e conectada a um dispositivo WhatsApp.
- Chave de API do Google Gemini (PaLM/Google AI Studio).

## Configuração
1. Importe o arquivo Noticias_Diarias.json no seu n8n.
1. googlePalmApi: Sua chave do Google Gemini.
1. Ajuste o nó HTTP Request1 com a URL da sua Evolution API e sua apikey.
