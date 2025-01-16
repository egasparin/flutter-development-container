# Flutter Development Container

Este repositório configura um ambiente de desenvolvimento Docker para projetos Flutter, utilizando o VS Code e Dev Containers. Ele permite que você desenvolva, teste e depure aplicações Flutter de maneira isolada e consistente, independentemente do sistema operacional local.

---

## **Requisitos**

### **Softwares Necessários**

- [Docker](https://www.docker.com/) (com suporte a Docker Compose)
- [Visual Studio Code](https://code.visualstudio.com/)
- [Extensão Remote - Containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)

## **Como clonar o repositório**

1. Certifique-se de que o Docker esteja instalado no seu sistema.
2. Instale a extensão **Dev Containers** no Visual Studio Code.
3. Clone este repositório:
   ```bash
   git clone https://github.com/egasparin/flutter-development-container.git
   cd flutter-development-container
   ```
---

## **Sobre o projeto**

### **Dockerfile**

O arquivo `Dockerfile` cria um contêiner baseado no Debian, contendo todo o ambiente necessário para o desenvolvimento com Flutter. Isso inclui o SDK do Flutter e ferramentas adicionais para possibilitar o desenvolvimento.

### **devcontainer.json**

O arquivo `devcontainer.json` configura o Visual Studio Code para:

- Instalar extensões úteis para Flutter e Dart.
- Permitir que o contêiner utilize o motor gráfico do sistema host, através do `.X11`.
- Mapear o navegador Google Chrome do host para o contêiner, possibilitando o desenvolvimento e depuração de aplicações Flutter Web.

### **Teste do ambiente**

Após iniciar o contêiner, você pode verificar se o ambiente está corretamente configurado utilizando o comando:

```bash
flutter doctor
```

A saída deve ser semelhante à seguinte imagem:

<img src="/readme/doctor-summary.png" alt="Texto Alternativo">

---

## **Executar o projeto Flutter**

Este repositório já inclui um projeto Flutter configurado. Para executá-lo no navegador do usuário, utilize o comando:

```bash
flutter run -d web-server
```

---

## **Contribuig**[r](https://flutter.dev/docs)

- [Docker Compose](https://docs.docker.com/compose/)
- [Dev Containers](https://code.visualstudio.com/docs/remote/containers)

Se precisar de ajuda, entre em contato ou abra uma issue no repositório!

