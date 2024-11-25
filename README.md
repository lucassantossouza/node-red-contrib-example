# **Node-RED Contrib Example**

Este repositório é um **template** para criação de nós customizados no **Node-RED**. Ele inclui uma estrutura organizada, exemplos de código e scripts úteis para facilitar o desenvolvimento e a reutilização.

---

## **Características do Template**
- Estrutura modular para nós customizados.
- Scripts de desenvolvimento configurados para maior produtividade.
- Exemplo de nó com lógica e interface para o Node-RED.
- Carregamento dinâmico de nós com base na pasta `nodes/`.

---

## **Como Usar Este Template**

### **1. Clone o Repositório**
Faça o clone do template para iniciar seu projeto:
```bash
git clone https://github.com/lucassantossouza/node-red-contrib-example.git
cd node-red-contrib-example
```

### **2. Instale as Dependências**
Certifique-se de que o Node.js (versão 14 ou superior) está instalado. Depois, execute:
```bash
npm install
```

### **3. Personalize o Template**
1. Altere o nome do pacote no `package.json`:
   ```json
   "name": "node-red-contrib-seu-novo-no"
   ```
2. Atualize as informações do autor, descrição e outras configurações, se necessário.

### **4. Inicie o Ambiente de Desenvolvimento**
Inicie o Node-RED no modo de desenvolvimento:
```bash
npm run dev
```

### **5. Adicione Seus Nós**
1. Crie uma nova pasta dentro de `src/nodes` com o nome do seu nó.
2. Adicione os arquivos `.js` e `.html` na pasta para definir a lógica e a interface do nó.

---

## **Estrutura do Projeto**

A estrutura do template é organizada da seguinte forma:

```plaintext
node-red-contrib-example/
├── src/
│   ├── config/             # Configurações do Node-RED (opcional)
│   │   └── settings.js
│   ├── nodes/              # Nós customizados
│   │   ├── exemplo/        # Nó "exemplo" (base para novos nós)
│   │   │   ├── exemplo.js    # Lógica do nó
│   │   │   ├── exemplo.html  # Interface do nó
│   │   │   └── assets/       # Ícones ou outros arquivos opcionais
│   │   └── ...
│   ├── index.js            # Registro central de nós
├── .nvmrc                  # Versão do Node.js
├── .eslintrc.json          # Configuração do ESLint
├── .gitignore              # Arquivos ignorados pelo Git
├── package.json            # Dependências e scripts
└── README.md               # Documentação do template
```

---

## **Scripts Disponíveis**

Os scripts estão definidos no `package.json` para facilitar o uso:

| Comando          | Descrição                                                                           |
|-------------------|-------------------------------------------------------------------------------------|
| `npm run link`    | Cria links simbólicos para o pacote local.                                         |
| `npm run dev`     | Inicia o Node-RED em modo de desenvolvimento e verifica o código.     |
| `npm run start`   | Inicia o Node-RED.                                                    |

---

## **Adicionando Nós Customizados**

Para adicionar um novo nó:
1. Crie uma nova pasta dentro de `src/nodes`, com o nome do nó.
2. Adicione os seguintes arquivos:
   - **`<nome>.js`**: Define a lógica do nó.
   - **`<nome>.html`**: Configura a interface no editor do Node-RED.

**Exemplo de Arquivo `.js`:**
```javascript
module.exports = function (RED) {
    function ExampleNode(config) {
        RED.nodes.createNode(this, config);
        const node = this;

        node.on('input', (msg) => {
            msg.payload = `Mensagem processada: ${msg.payload}`;
            node.send(msg);
        });
    }

    RED.nodes.registerType('example', ExampleNode);
};
```

**Exemplo de Arquivo `.html`:**
```html
<script type="text/javascript">
  RED.nodes.registerType('example', {
      category: 'function',
      color: '#a6bbcf',
      defaults: {
          name: { value: "" }
      },
      label: function () {
          return this.name || "Example Node";
      },
      icon: "icon.png"
  });
</script>
```

---

## **Carregamento Dinâmico de Nós**

O `index.js` está configurado para carregar automaticamente os nós dentro da pasta `nodes/`. Ele procura por arquivos `.js` que correspondam ao nome da pasta.

**Exemplo do `index.js`:**
```javascript
const fs = require('fs');
const path = require('path');
const nodesPath = path.join(__dirname, 'nodes');

// Carrega dinamicamente todos os nós
fs.readdirSync(nodesPath).forEach((dir) => {
  const nodePath = path.join(nodesPath, dir, `${dir}.js`);
  if (fs.existsSync(nodePath)) {
    require(nodePath)(RED);
  }
});
```

---

## **Publicando o Pacote**

1. Teste o nó no Node-RED para garantir que tudo está funcionando.
2. Atualize a versão no `package.json`:
   ```bash
   npm version <major|minor|patch>
   ```
3. Publique no npm:
   ```bash
   npm publish
   ```

---

## **Contribuições**

Sinta-se à vontade para abrir **Issues** ou enviar **Pull Requests** para melhorias.

---

## **Licença**

Este projeto está licenciado sob a licença ISC.