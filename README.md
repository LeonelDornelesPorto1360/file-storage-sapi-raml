# Projeto de Armazenamento de Arquivos

O projeto de armazenamento de arquivos é uma solução desenvolvida pela equipe de engenharia da OSF Digital para fornecer aos usuários uma plataforma segura e confiável para armazenar, gerenciar e compartilhar arquivos. A solução é projetada para atender às necessidades de empresas de todos os tamanhos, oferecendo uma interface intuitiva e funcionalidades avançadas.

## Funcionalidades Principais

- **Criar arquivos**: O serviço permite aos usuários criar arquivos no sistema de armazenamento através do endpoint `/files/{bucket}/create`.
- **Listar arquivos**: Os usuários podem listar os arquivos presentes em um diretório específico utilizando o endpoint `/files/{bucket}/list`.
- **Baixar arquivos**: É possível baixar um arquivo específico do serviço de armazenamento através do endpoint `/files/{bucket}/download`.
- **Excluir arquivos**: Os usuários podem excluir um arquivo do serviço de armazenamento utilizando o endpoint `/files/{bucket}/delete`.
- **Baixar conteúdo de um item**: É possível baixar o conteúdo de um item específico utilizando o endpoint `/files/{target}/{targetId}/content/download`.
- **Obter informações de um item**: Os usuários podem obter informações sobre um item específico, como nome, tamanho e URL de download, através do endpoint `/files/{target}/{targetId}/content`.
- **Atualizar conteúdo de um item**: É possível atualizar o conteúdo de um item específico utilizando o endpoint `/files/{target}/{targetId}/content` com uma requisição PUT.
- **Excluir conteúdo de um item**: Os usuários podem excluir o conteúdo de um item específico utilizando o endpoint `/files/{target}/{targetId}/content` com uma requisição DELETE.
- **Obter coleção de itens**: É possível obter uma coleção de itens relacionados a um determinado alvo utilizando o endpoint `/files/{target}/{targetId}/content/collection`.
- **Atualizar coleção de itens**: Os usuários podem atualizar a coleção de itens relacionados a um determinado alvo utilizando o endpoint `/files/{target}/{targetId}/content/collection` com uma requisição PUT.
- **Excluir coleção de itens**: É possível excluir a coleção de itens relacionados a um determinado alvo utilizando o endpoint `/files/{target}/{targetId}/content/collection` com uma requisição DELETE.
- **Obter conteúdo de um item específico**: Os usuários podem obter o conteúdo de um item específico utilizando o endpoint `/files/{target}/{targetId}/content/{fileName}`.
- **Excluir um item específico**: É possível excluir um item específico utilizando o endpoint `/files/{target}/{targetId}/content/{fileName}` com uma requisição DELETE.

## Segurança e Escalabilidade

A segurança é uma prioridade neste projeto. Todos os arquivos são armazenados de forma criptografada e protegidos por autenticação e autorização robustas. Os usuários têm controle total sobre as permissões de acesso aos arquivos, podendo definir quem pode visualizar, editar ou excluir os arquivos.

Além disso, o projeto de armazenamento de arquivos é altamente escalável e flexível, permitindo que os usuários armazenem uma grande quantidade de dados e acessem os arquivos de qualquer dispositivo, a qualquer momento. A solução é integrada com outras ferramentas e serviços, como o Salesforce, para fornecer uma experiência de usuário perfeita e uma maior produtividade.

Em resumo, o projeto de armazenamento de arquivos é uma solução completa e confiável para gerenciar arquivos de forma segura e eficiente. Com suas funcionalidades avançadas e foco na segurança, ele atende às necessidades de empresas que desejam armazenar, compartilhar e gerenciar seus arquivos de maneira eficaz.

## Tipos de Dados

- **teste**:
  - **files**: string (obrigatório)
  - **path**: string (obrigatório)

- **teste1**:
  - **path**: string (obrigatório)

- **teste2**:
  - **file**: string (obrigatório)

- **teste3**:
  - **files**: string (obrigatório)

## Endpoints

### /files/{bucket}/create

- Método: POST
- Body:
  - multipart/form-data:
    - Tipo: teste[]
- Respostas:
  - 204
  - 404:
    - Body:
      - application/json:
        - Exemplo: "Path '/files/ftp/test/1/1/arquivos' doesn't exist"

### /files/{bucket}/list

- Método: POST
- Body:
  - multipart/form-data:
    - Tipo: teste1[]
- Respostas:
  - 200:
    - Body:
      - application/json:
        - Exemplo:
          ```
          {
              "item": [
                  {
                      "href": "http://localhost:8081/files/test/1/1/arquivos/1.pdf",
                      "name": "1.pdf",
                      "size": 281826
                  },
                  {
                      "href": "http://localhost:8081/files/test/1/1/arquivos/2.pdf",
                      "name": "2.pdf",
                      "size": 245893
                  }
              ]
          }
          ```
  - 404:
    - Body:
      - application/json:
        - Exemplo: "Path '/files/ftp/test/1/1/arquivos' doesn't exist"

### /files/{bucket}/download

- Método: POST
- Respostas:
  - 200
  - 404:
    - Body:
      - application/json:
        - Exemplo: "Path '/files/test/1/1/arquivos' doesn't exist"

### /files/{bucket}/delete

- Método: POST
- Respostas:
  - 204
  - 404:
    - Body:
      - application/json:
        - Exemplo: "Path '/files/test/1/1/arquivos' doesn't exist"

### /files/{target}/{targetId}/content/download

- Método: GET
- Respostas:
  - 200
  - 404:
    - Body:
      - application/json:
        - Exemplo: "Path '/files/test/1/1/arquivos'"

### /files/{target}/{targetId}/content

- Método: GET
- Respostas:
  - 200:
    - Body:
      - application/json:
        - Exemplo:
          ```
          {
              "target": "order",
              "targetId": "123456",
              "item": {
                  "href": "http://localhost:8081/files/order/123456/collection/1.jfif",
                  "name": "1.jfif",
                  "size": 15552
              }
          }
          ```
  - 404:
    - Body:
      - application/json:
        - Exemplo: "Path '/files/test/1/1/arquivos'"

- Método: PUT
- Body:
  - multipart/form-data:
    - Tipo: teste2[]
- Respostas:
  - 204
  - 404:
    - Body:
      - application/json:
        - Exemplo: "Path '/files/test/1/1/arquivos'"

- Método: DELETE
- Respostas:
  - 204
  - 404:
    - Body:
      - application/json:
        - Exemplo: "Path '/files/test/1/1/arquivos'"

### /files/{target}/{targetId}/content/collection

- Método: GET
- Respostas:
  - 200:
    - Body:
      - application/json:
        - Exemplo:
          ```
          {
              "target": "order",
              "targetId": "123456",
              "items": [
                  {
                      "href": "http://localhost:8081/files/order/123456/collection/1.jfif",
                      "name": "1.jfif",
                      "size": 15552
                  },
                  {
                      "href": "http://localhost:8081/files/order/123456/collection/2.PDF",
                      "name": "2.PDF",
                      "size": 127714
                  },
                  {
                      "href": "http://localhost:8081/files/order/123456/collection/3.txt",
                      "name": "3.txt",
                      "size": 5
                  },
                  {
                      "href": "http://localhost:8081/files/order/123456/collection/4.xlsx",
                      "name": "4.xlsx",
                      "size": 3245
                  }
              ]
          }
          ```
  - 404:
    - Body:
      - application/json:
        - Exemplo: "Path '/files/test/1/1/arquivos'"

- Método: PUT
- Body:
  - multipart/form-data:
    - Tipo: teste3[]
- Respostas:
  - 204
  - 404:
    - Body:
      - application/json:
        - Exemplo: "Path '/files/ftp/test/1/1/arquivos' doesn't exist"

- Método: DELETE
- Respostas:
  - 204
  - 404:
    - Body:
      - application/json:
        - Exemplo: "Path '/files/test/1/1/arquivos'"

### /files/{target}/{targetId}/content/{fileName}

- Método: GET
- Respostas:
  - 200
  - 404:
    - Body:
      - application/json:
        - Exemplo: "Path '/files/test/1/1/arquivos'"

- Método: DELETE
- Respostas:
  - 204
  - 404:
    - Body:
      - application/json:
        - Exemplo: "Path '/files/test/1/1/arquivos'"
