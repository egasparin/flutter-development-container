# Flutter Development Container

Este repositório configura um ambiente de desenvolvimento Docker para projetos Flutter, utilizando o VS Code e Dev Containers. Ele permite que você desenvolva, teste e depure aplicações Flutter de maneira isolada e consistente, independentemente do sistema operacional local.

---

## **Requisitos**

### **Softwares Necessários**

- [Docker](https://www.docker.com/) (com suporte a Docker Compose)
- [Visual Studio Code](https://code.visualstudio.com/)
- [Extensão Remote - Containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)

### **Imagem docker referenciada**
A imagem docker pode ser baixada (pull) ou diretamente linkada no projeto por meio do comando abaixo
```bash
docker pull egasparin/flutter:latest
 ```
---
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

Para conectar o dispositivo ao container, é necessário realizar a depuração por wifi, todo o processo inicia-se com o container inativo
No dispositivo, acesse as Opções de desenvolvedor > Depuração por Wi-fi.
Na sequência, encontre o endereço ip do dispositivo, por meio do Wifi > Configurações > Avançado > Endereço IP
No sistema Host, mate o serviço adb com o comando ```adb kill-server ```.
Inicie o container e conecte via tcp ```adb connect XXX.XXX.X.XXX:5555```
O dispositivo estará disponível para uso no container.
Para acessar o dispositivo pelo SCRCPY, instale esse no host ```apt install scrcpy ``` e depois que o dispositivo estiver acessivel pelo container, rode no host o comando ```scrcpy```
Com isso, a tela do celular será exibida pelo SCRCPY mesmo que o dispositivo esteja conectado no container
---

## **Conectar smartphone**

Este repositório já inclui um projeto Flutter configurado. Para executá-lo no navegador do host, utilize o comando:

```bash
flutter run -d web-server
```

---

## **Contribuig**[r](https://flutter.dev/docs)

- [Docker Compose](https://docs.docker.com/compose/)
- [Dev Containers](https://code.visualstudio.com/docs/remote/containers)

Se precisar de ajuda, entre em contato ou abra uma issue no repositório!

