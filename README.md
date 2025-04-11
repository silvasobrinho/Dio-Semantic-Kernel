# Azure OpenAI API & Semantic Kernel

## ✨ Visão Geral
Este repositório documenta os principais conceitos relacionados ao uso da **Azure OpenAI API** e do **Semantic Kernel**, dois componentes fundamentais para o desenvolvimento de soluções modernas baseadas em IA generativa com recursos do Microsoft Azure.

---

## 🔧 Arquitetura da Azure OpenAI API

Segundo a [documentação oficial da Microsoft](https://learn.microsoft.com/en-us/azure/ai-services/openai/reference), a Azure OpenAI API é estruturada em três camadas principais:

### 1. Control Plane
Responsável pela gestão e administração dos recursos:
- Criação de recursos
- Instanciação de modelos
- Painel de configurações e controle

### 2. Data Plane - Authoring
Foco em customização e preparação de modelos:
- Fine-tuning
- Upload de arquivos
- Jobs de ingestão de dados
- Processamento em lote

### 3. Data Plane - Inference
Execução e inferência dos modelos:
- Completions e Chat Completions
- Embeddings
- Geração de imagens com DALL-E
- Reconhecimento de voz (Whisper)
- Geração de fala (Text-to-Speech)

Essas três camadas possibilitam aos desenvolvedores acessarem todo o potencial da plataforma Azure OpenAI.

---

## 🔐 Autenticação na API
A API da Azure OpenAI oferece dois métodos de autenticação:

### 1. API Key
- Requisição HTTP com cabeçalho `api-key`.

### 2. Microsoft Entra ID (OAuth)
- Requisição com token Bearer via header:

```http
Authorization: Bearer YOUR_AUTH_TOKEN
```

Referência: [REST API Reference](https://learn.microsoft.com/en-us/azure/ai-services/openai/reference)

---

## 🔄 Exemplo de Chamada para a API

### URL da Requisição
```http
POST https://{endpoint}/openai/deployments/{deployment-id}/completions?api-version=2024-10-21
```

### Corpo da Requisição
```json
{
  "prompt": ["tell me a joke about mango"],
  "max_tokens": 32,
  "temperature": 1.0,
  "n": 1
}
```

### Principais Parâmetros
- **prompt**: Entrada textual.
- **max_tokens**: Limita o comprimento da resposta.
- **temperature**: Controla a aleatoriedade da resposta.
- **n**: Quantidade de respostas geradas.
- **top_p, presence_penalty, frequency_penalty**: Opções adicionais de controle da geração.

### Saída
As respostas são recebidas em formato JSON, permitindo ao desenvolvedor construir a interface conforme os campos de interesse.

---

## 📃 Desenvolvimento: SDKs e Linguagens Suportadas

A Azure OpenAI oferece SDKs e bibliotecas auxiliares para facilitar a integração:

- Python
- Go
- Java
- C#
- JavaScript *(descontinuado)*

### Exemplo com Python - Criação de um Assistente
```python
from openai import AzureOpenAI

client = AzureOpenAI(
    api_key=os.getenv("AZURE_OPENAI_API_KEY"),  
    api_version="2024-08-01-preview",
    azure_endpoint=os.getenv("AZURE_OPENAI_ENDPOINT")
)

assistant = client.beta.assistants.create(
    instructions="You are an AI assistant that can write code to help answer math questions",
    model="<REPLACE WITH MODEL DEPLOYMENT NAME>",
    tools=[{"type": "code_interpreter"}]
)
```

---

## 🪄 Introdução ao Semantic Kernel

O [Semantic Kernel](https://learn.microsoft.com/en-us/semantic-kernel/overview/) é um SDK leve e open-source desenvolvido pela Microsoft para facilitar a criação de **AI agents**, com suporte para:
- Modularidade
- Observabilidade
- Extensão para serviços como Microsoft 365 Copilot

### Características
- Middleware para orquestração de IA
- Plug-ins e funções reutilizáveis
- Suporte a linguagens: **C#**, **Python**, **Java**

> "You as a developer have a single place where you can configure and monitor your AI agents."

### Fluxo de Execução
1. Seleciona o melhor serviço para o prompt
2. Constrói o prompt
3. Envia para o modelo
4. Recebe e interpreta a resposta
5. Retorna para a aplicação


### Funcionalidades e Plugins
- Chat Completion
- Text Generation
- Embeddings *(experimental)*
- Text-to-Image *(experimental)*
- Audio-to-Text *(experimental)*
- Text-to-Audio *(experimental)*
- Realtime *(experimental)*


---

## 🔗 Referências
1. [Azure OpenAI Service REST API](https://learn.microsoft.com/en-us/azure/ai-services/openai/reference)
2. [Introduction to Semantic Kernel](https://learn.microsoft.com/en-us/semantic-kernel/overview/)
