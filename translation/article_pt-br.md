![LogoFCC](https://github.com/CarlosViniMSouza/Python-BackEnd-Django/blob/main/Images/freecodecamp.png)

# Isso é um resumo sobre *Requisições Python – Como Interagir com Serviços Web usando Python*

## Artigo por: Ashutosh Krishna

![EmblemArticle](https://www.freecodecamp.org/news/content/images/size/w2000/2021/12/Black-Moon-Blog-Banner--2-.png)

## Introdução:

### Uma API, ou **Interface de Programação de Aplicativo**, é um servidor que permite recuperar e enviar dados usando código. Geralmente usamos APIs para recuperar dados, e esse será o foco deste tutorial para iniciantes.

### Quando queremos receber dados de uma API, precisamos fazer uma **solicitação(request)**. As solicitações são usadas em toda a web. Por exemplo, quando você visitou esta postagem do blog, seu navegador fez uma solicitação ao servidor da freeCodeCamp, que respondeu com o conteúdo desta página da web.

<p align="center">
  <a href="https://github.com/CarlosViniMSouza">
    <img src="https://res.cloudinary.com/dlomjljb6/image/upload/v1/media/blog/uploads/2021/06/04/api-request_rlwgao"/>
  </a>
</p>

### As solicitações de API funcionam exatamente da mesma maneira - você faz uma solicitação de dados a um servidor de API e ele responde à sua solicitação.

## Diferentes Metodos HTTP e Estados de Código:

### Existem vários métodos HTTP para <ins>APIs REST</ins>. Esses métodos informam à API quais operações precisam ser executadas nos dados. Embora existam muitos métodos HTTP, os cinco métodos listados abaixo são os mais comumente usados com APIs REST:

|HTTP METODO |	DESCRIÇÃO                                  |
|------------|---------------------------------------------|
|   GET	     |  Recuperar dados existentes                 |
|   POST	   |  Add novos dados                            |
|   PUT	     |  Atualiza dados existentes                  |
|   PATCH    |	Atualiza parcialmente os dados existentes  |
|   DELETE   |	Apaga dados                                |

### Depois que uma API REST recebe e processa uma solicitação HTTP, ela retorna uma resposta com um código de status HTTP. Este código de status fornece informações sobre a resposta e ajuda o aplicativo cliente a saber que tipo de resposta é.

### Os códigos de status são numerados com base na categoria do resultado:

|INTER. CODE | CATEGORIA              |
|------------|------------------------|
|    1xx	   | Resposta informativa   |
|    2xx	   | Operação bem sucedida  |
|    3xx	   | Redirecionando         |
|    4xx	   | Erro do Cliente        |
|    5xx	   | Erro do Servidor       |

### Você pode aprender mais sobre os códigos de status HTTP no [MDN Web Docs](https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Status).