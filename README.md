# 🎙️ Assistente de Voz Multi-Idiomas com Whisper e ChatGPT

Projeto desenvolvido no **Bootcamp Bradesco – GenAI & Dados**, da **DIO (Digital Innovation One)**.

É um assistente de voz em Python: você **fala uma pergunta**, a IA **transcreve**, **responde** e **lê a resposta em voz alta**.

🔗 **Notebook no Google Colab:** [Abrir projeto](https://colab.research.google.com/drive/1rHGq5N-sbEGtZsNUiQFT8q60BhRbj99b?usp=sharing)

> **Google Colab** é um "caderno" de Python que roda na nuvem do Google, direto no navegador, sem precisar instalar nada.

---

## 📍 Contexto

O bootcamp propôs integrar diferentes modelos de **Inteligência Artificial Generativa** em um único fluxo, para entender na prática como essas ferramentas se conectam.

## ❗ Problema

Cada IA resolve **uma parte** da tarefa: uma entende fala, outra gera texto e outra produz voz. O desafio era **ligar essas peças** para que a pessoa converse com o assistente só usando a voz, em mais de um idioma.

## 🛠️ Solução (o que e como fiz)

Montei um fluxo em 4 etapas, em que cada uma recebe o resultado da anterior:

```
 🎤 Voz  ──▶  📝 Texto  ──▶  💬 Resposta  ──▶  🔊 Voz
 Gravação     Whisper        ChatGPT          gTTS
```

| Etapa | Ferramenta | O que faz |
|---|---|---|
| **1. Gravação** | Python + JavaScript | Grava a voz pelo microfone do navegador (o Colab roda na nuvem e não acessa o microfone sozinho) |
| **2. Voz → Texto** | **Whisper** (OpenAI) | Transcreve o áudio em texto |
| **3. Texto → Resposta** | **API do ChatGPT** (OpenAI) | Gera a resposta para a pergunta |
| **4. Resposta → Voz** | **gTTS** (Google Text-to-Speech) | Converte a resposta em áudio e toca automaticamente |

O idioma é definido em uma única variável, usada em todas as etapas:

```python
language = 'pt'   # troque para 'en', 'es'... e o assistente muda de idioma
```

**Analogia:** é como uma central de atendimento com três funcionários. Um **anota** o que o cliente falou (Whisper), outro **pensa na resposta** (ChatGPT) e o terceiro **liga de volta e lê a resposta** (gTTS).

## 📊 Resultado (Antes × Depois)

| Antes | Depois |
|---|---|
| Para usar o ChatGPT era preciso **digitar** a pergunta | A pergunta é feita **por voz** |
| A resposta só aparecia **em texto** | A resposta é **falada** pelo assistente |
| Cada IA funcionava isolada | Três IAs trabalhando juntas em um único fluxo |
| Um idioma fixo | Troca de idioma alterando **uma variável** |

**Exemplo real do teste:**

- 🎤 Pergunta falada: *"Em poucas palavras, quem é a Digital Innovation One?"*
- 🔊 Resposta: o assistente explicou, em áudio, que a DIO é uma plataforma de educação online em tecnologia.

---

## ▶️ Como executar

1. Abra o [notebook no Colab](https://colab.research.google.com/drive/1rHGq5N-sbEGtZsNUiQFT8q60BhRbj99b?usp=sharing).
2. Gere uma **API Key** em [platform.openai.com](https://platform.openai.com/account/api-keys). A API da OpenAI é paga.
3. Substitua o `'TODO'` pela sua chave (nunca publique sua chave real).
4. Execute as células **em ordem**, de cima para baixo, e permita o uso do microfone.

## ⚠️ Observação

O notebook usa a sintaxe antiga da biblioteca `openai` (`openai.ChatCompletion.create`). Nas versões atuais, o formato é:

```python
from openai import OpenAI
client = OpenAI()
response = client.chat.completions.create(model="gpt-4o-mini", messages=[...])
```

## 🧰 Tecnologias

Python · Google Colab · JavaScript · OpenAI Whisper · OpenAI API (ChatGPT) · gTTS
