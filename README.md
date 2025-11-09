# DevOps e Cloud Computing
## Foodly – Projeto Simples e Impactante

O aplicativo Foodly foi desenvolvido com o objetivo de promover práticas sustentáveis relacionadas à alimentação, contribuindo para a redução de desperdício de alimentos e minimizando a emissão de gases nocivos ao meio ambiente.
O sistema visa identificar e disponibilizar alimentos que estão próximos da data de vencimento, bem como produtos que não foram entregues ou foram cancelados, tornando-os acessíveis para consumo consciente. Os itens são organizados em categorias, como Salgados, Doces, Lanches, Bebidas e outros alimentos variados, podendo ser comercializados em kits sortidos a preços reduzidos, incentivando a compra consciente e sustentável. 

### Sprint2
Nessa sprint foi criada uma Máquina Virtual no prvedor de Nuvem(Azure) por Debian/Ubuntu. E a solução foi planejada e arquitetada por *containers docker* para e melhorar a experiência do projeto

## Como foi planejado a estrutura de deploy

* Virtualização --> **Containers em Docker** 
* Provedor de Nuvem --> Máquina Virtual Debian pelo **Microsoft Azure** 
* Webserver --> Por **Nginx** 

## Segue passo a passo dos comandos para o **deployment**

Execultar a sequência de comandos para o deploy

1️⃣ Criar um container Nginx inicial 
Primeiro, foi criado um container básico do Nginx para testar se o serviço estava rodando corretamente:

```bash
docker run --name AppFoodly -p 8082:80 -d nginx
```
* Esse comando cria um container chamado AppFoodly, mapeando a porta local 8082 para a porta 80 do Nginx.
* A página exibida é a padrão do Nginx.

2️⃣ Remover container duplicado (em caso de conflito)
Se já existir um container com o mesmo nome *AppFoodly*, o Docker exibirá o erro:

```bash
Error response from daemon: Conflict. The container name "/AppFoodly" is already in use
```
Para resolver, basta remover o container antigo:

```bash
docker rm -f AppFoodly
```

3️⃣ Subir o container com o site montado
Agora sim, monte o volume do seu projeto local no diretório padrão do Nginx (/usr/share/nginx/html):

```bash
docker run --name AppFoodly -p 8082:80 -v "C:\Users\lucas\Desktop\Sprint2\App:/usr/share/nginx/html" -d nginx
```

### Explicação dos parâmetros
| Parâmetro                                                       | Função                                                                         |
| --------------------------------------------------------------- | ------------------------------------------------------------------------------ |
| `--name AppFoodly`                                              | Define o nome do container                                                     |
| `-p 8082:80`                                                    | Mapeia a porta 8082 da máquina para a 80 do container                          |
| `-v "C:\Users\lucas\Desktop\Sprint2\App:/usr/share/nginx/html"` | Faz o *bind* da pasta local do projeto com a pasta onde o Nginx busca arquivos |
| `-d nginx`                                                      | Usa a imagem oficial do Nginx e executa em segundo plano                       |

4️⃣ Acessar o site
Abra no navegador:

```bash
http://localhost:8082
```

5️⃣ Parar ou remover o container

Para parar o container:

```bash
docker stop AppFoodly
```

Para removê-lo:

```bash
docker rm AppFoodly
```

6️⃣ Rode o container novamente, com o volume correto

Agora, execute este comando ajustado:

```bash
docker run --name AppFoodly -p 8082:80 -v "C:\Users\lucas\Desktop\Sprint2\App:/usr/share/nginx/html" -d nginx
```

# Resultado Final

O site Foodly está hospedado localmente via Nginx em um container Docker, acessível pela porta 8082, com o código-fonte sendo servido diretamente da pasta do projeto no seu computador.

## Vídeo demonstrativo do deploy do projeto em container docker

[![Vídeo de Demonstração da Sprint 2](https://img.youtube.com/vi/8wYvcyXgY-8/hqdefault.jpg)](https://youtu.be/8wYvcyXgY-8?si=gi5uPn0CYznZCZPl)

## Integrantes do projeto

Lucas Aurelio de Brito Chicote - RM: 559366

Henrique Marques Sladkevicius - RM: 560698

Lucas Gomes de Araujo Lopes - RM: 559607








