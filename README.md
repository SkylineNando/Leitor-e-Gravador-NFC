## 📱 **Leitor e Gravador NFC**

Este projeto permite ler e gravar dados em tags NFC (Near Field Communication) usando HTML, CSS e JavaScript com a **Web NFC API**.

### 🚀 **Funcionalidades**

- **Leitura de Tags NFC**: Escaneia e lê informações de tags NFC compatíveis.
- **Gravação em Tags NFC**: Grava texto simples em tags NFC.
- **Interface Simples**: Interface amigável com botões para interagir com as tags NFC.

---

### 📋 **Pré-requisitos**

- **Navegador Compatível**: Google Chrome para Android (versão 89 ou superior).
- **Conexão Segura**: O site precisa ser servido via **HTTPS**.
- **Dispositivo com NFC**: Smartphone ou tablet com suporte a NFC.
- **Tag NFC**: Use tags NFC regraváveis para testar a funcionalidade de gravação.

---

### 🛠️ **Como Usar**

#### **1. Clonar o Repositório**

```bash
git clone https://github.com/skylinenando/nfc-reader-writer.git
cd nfc-reader-writer
```

#### **2. Estrutura do Projeto**

```plaintext
nfc-reader-writer/
│-- index.html
│-- styles.css (opcional)
└-- README.md
```

#### **3. Hospedar o Projeto**

Use um servidor local ou uma plataforma de hospedagem como **GitHub Pages** para rodar o projeto em **HTTPS**.

- **GitHub Pages**:
  - Faça o commit e push para o branch `main`.
  - Ative o GitHub Pages em **Settings → Pages**.
  
#### **4. Acessar o Projeto**

Abra o projeto em um navegador compatível com NFC e acesse a URL hospedada.

---

### 🧑‍💻 **Código Principal**

#### **Leitura NFC (`index.html`)**

```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Leitor NFC</title>
</head>
<body>
    <h1>Leitura de NFC</h1>
    <button id="startButton">Iniciar Leitura NFC</button>
    <p id="output"></p>

    <script>
        const startButton = document.getElementById('startButton');
        const output = document.getElementById('output');

        startButton.addEventListener('click', async () => {
            if ('NDEFReader' in window) {
                try {
                    const ndef = new NDEFReader();
                    await ndef.scan();
                    output.textContent = 'Aguardando leitura da tag NFC...';

                    ndef.onreading = event => {
                        const decoder = new TextDecoder();
                        for (const record of event.message.records) {
                            output.textContent = `Dados lidos: ${decoder.decode(record.data)}`;
                        }
                    };
                } catch (error) {
                    output.textContent = `Erro: ${error}`;
                }
            } else {
                output.textContent = 'NFC não suportado neste navegador.';
            }
        });
    </script>
</body>
</html>
```

#### **Gravação NFC (`index.html`)**

```html
<input type="text" id="textInput" placeholder="Digite algo para gravar">
<button id="writeButton">Gravar na Tag NFC</button>

<script>
    const writeButton = document.getElementById('writeButton');
    const textInput = document.getElementById('textInput');
    const output = document.getElementById('output');

    writeButton.addEventListener('click', async () => {
        if ('NDEFReader' in window) {
            try {
                const ndef = new NDEFReader();
                await ndef.write(textInput.value);
                output.textContent = `Dados "${textInput.value}" gravados com sucesso!`;
            } catch (error) {
                output.textContent = `Erro: ${error}`;
            }
        } else {
            output.textContent = 'NFC não suportado neste navegador.';
        }
    });
</script>
```

---

### ⚠️ **Limitações**

- **Suporte apenas em Android**: A Web NFC API não é suportada no iOS.
- **HTTPS obrigatório**: O projeto só funciona em conexões seguras.
- **Gravação limitada**: Apenas dados em formato **NDEF** podem ser gravados.

---

### 📄 **Licença**

Este projeto está licenciado sob a **MIT License**.

---

### 🌐 **Links Úteis**

- [Documentação da Web NFC API](https://developer.mozilla.org/pt-BR/docs/Web/API/Web_NFC_API)
- [Suporte do Chrome para Android](https://caniuse.com/webnfc)

---

### 🤝 **Contribuições**

Contribuições são bem-vindas! Sinta-se à vontade para abrir **issues** ou enviar **pull requests**.
