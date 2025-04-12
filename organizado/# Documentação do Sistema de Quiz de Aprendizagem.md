# Documentação do Sistema de Quiz de Aprendizagem

## 1. Parâmetros de URL

O aplicativo de Quiz suporta vários parâmetros de URL para personalizar a configuração inicial e o carregamento do quiz:

### 1.1 Parâmetro de URL do JSON
- **Parâmetro**: `json-url`
- **Descrição**: Especifica a URL do arquivo JSON contendo os dados do quiz
- **Exemplo**: 
  ```
  https://seuaplicativo.com/quiz.html?json-url=https://exemplo.com/dados-quiz.json
  ```

### 1.2 Parâmetro de Idioma
- **Parâmetro**: `language`
- **Descrição**: Define o idioma inicial do quiz
- **Valores Suportados**: `pt` (Português), `en` (Inglês), `es` (Espanhol)
- **Exemplo**: 
  ```
  https://seuaplicativo.com/quiz.html?json-url=https://exemplo.com/quiz.json&language=en
  https://seuaplicativo.com/quiz.html?json-url=https://exemplo.com/quiz.json&language=es
  ```

### 1.3 Parâmetro de Carregamento de Arquivo de Salvamento
- **Parâmetro**: `load-save-file`
- **Descrição**: Carrega um estado de jogo salvo anteriormente a partir de uma URL específica
- **Exemplo**:
  ```
  https://seuaplicativo.com/quiz.html?load-save-file=https://exemplo.com/jogo-salvo.json
  ```

### 1.4 Combinação de Parâmetros
- **Exemplo Completo**:
  ```
  https://seuaplicativo.com/quiz.html?json-url=https://exemplo.com/quiz.json&language=en&load-save-file=https://exemplo.com/jogo-salvo.json
  ```
  - Carrega o quiz de uma URL específica
  - Define o idioma inicial como inglês
  - Carrega um arquivo de jogo salvo

## 2. Configuração do JSON

O arquivo JSON para o quiz suporta várias opções de configuração:

### 2.1 Estrutura Básica do JSON
```json
{
  "words": [
    {
      "word": "Olá",
      "translation": "Hello",
      "type": "substantivo",
      "imageUrl": "https://exemplo.com/imagem-olá.jpg"
    }
  ],
  "config": {
    "showWordTextWithImage": true,
    "sidebar": {
      "items": [...]
    },
    "translations": {
      "pt": {...},
      "en": {...},
      "es": {...}
    }
  }
}
```

### 2.2 Propriedades do Objeto de Palavra
| Propriedade | Tipo | Descrição | Opcional |
|-------------|------|------------|----------|
| `word` | String | A palavra original | Obrigatório |
| `translation` | String | A tradução da palavra | Obrigatório |
| `type` | String | Tipo gramatical da palavra | Opcional |
| `imageUrl` | String | URL de uma imagem associada à palavra | Opcional |

### 2.3 Opções de Configuração

#### 2.3.1 Configuração Geral
- `showWordTextWithImage` (Booleano)
  - Controla se o texto da palavra é exibido quando uma imagem está presente
  - Padrão: Detectado automaticamente com base na prevalência de imagens

#### 2.3.2 Configuração da Barra Lateral
```json
"sidebar": {
  "items": [
    {
      "id": "id-unico",
      "title": "Título do Item",
      "content": "Conteúdo em markdown",
      "contentUrl": "https://exemplo.com/conteudo.md",
      "color": "#3b82f6"
    }
  ]
}
```

Propriedades do Item da Barra Lateral:
- `id`: Identificador único do item
- `title`: Título de exibição do item da barra lateral
- `content`: Conteúdo em markdown (opcional)
- `contentUrl`: URL para carregar conteúdo markdown externo (opcional)
- `color`: Cor de destaque para o item da barra lateral

#### 2.3.3 Traduções Personalizadas
```json
"translations": {
  "pt": {
    "appTitle": "Quiz do Aprendizado",
    "definitions": {
      "substantivo": "Uma palavra que representa um objeto, pessoa ou conceito"
    }
  },
  "en": {
    "appTitle": "Learning Quiz",
    "definitions": {
      "noun": "A word representing an object, person, or concept"
    }
  }
}
```

### 2.4 Estrutura do Arquivo de Salvamento
```json
{
  "jsonUrl": "https://exemplo.com/dados-quiz.json",
  "wordQueue": [...],
  "wordList": [...],
  "sidebarItems": [...],
  "score": {
    "correct": 10,
    "wrong": 5
  },
  "timer": 300,
  "config": {...},
  "date": "2024-04-12T10:30:00Z"
}
```

## 3. Exemplo de JSON Completo

```json
{
  "words": [
    {
      "word": "Gato",
      "translation": "Cat",
      "type": "substantivo",
      "imageUrl": "https://exemplo.com/gato.jpg"
    },
    {
      "word": "Correr",
      "translation": "To run",
      "type": "verbo",
      "imageUrl": "https://exemplo.com/correr.jpg"
    }
  ],
  "config": {
    "showWordTextWithImage": false,
    "sidebar": {
      "items": [
        {
          "id": "guia-gramatical",
          "title": "Guia de Gramática",
          "contentUrl": "https://exemplo.com/gramatica.md",
          "color": "#3b82f6"
        }
      ]
    },
    "translations": {
      "pt": {
        "appTitle": "Quiz de Aprendizado",
        "definitions": {
          "substantivo": "Uma palavra que representa um objeto, pessoa ou conceito",
          "verbo": "Uma palavra que descreve uma ação ou estado"
        }
      },
      "en": {
        "appTitle": "Learning Quiz",
        "definitions": {
          "noun": "A word representing an object, person, or concept",
          "verb": "A word describing an action or state"
        }
      }
    }
  }
}
```

## 4. Recomendações

1. Certifique-se de que todas as URLs estejam publicamente acessíveis
2. Use servidores com CORS habilitado para conteúdo externo
3. Valide a estrutura do JSON antes do uso
4. Mantenha os tamanhos das imagens otimizados
5. Forneça traduções para todos os idiomas suportados
