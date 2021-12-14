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

## API Endpoints:

### **Terminais de API(API Endpoints)** são as URLs públicas expostas pelo servidor que um aplicativo cliente usa para acessar recursos e dados.

### Por causa deste tutorial, usaremos a API REST da Fake Store. Mais especificamente, usaremos os endpoints abaixo:

| METODO HTTP |	  TERMINAIS DA API      | DESCRIÇÃO                         |
|-------------|-------------------------|-----------------------------------|
|    GET	    | /products	              | Obtenha uma lista de produtos.    |
|    GET	    | /products?limit=x	      | Obtenha apenas 5 produtos.        |
|    GET	    | /products/<product_id>	| Obtenha um único produto.         |
|    POST	    | /products	              | Cria um novo produto.             |
|    PUT	    | /products/<product_id>	| Atualiza um produto.              |
|    PATCH	  | /products/<product_id>	| Atualiza parcialmente um produto. |
|    DELETE	  | /products/<product_id>	| Deleta um produto.                |

### Cada um dos terminais acima executa uma ação diferente com base no método HTTP. Para cada URL da API, o URL base é: `https://fakestoreapi.com`. Vamos explorá-los um após o outro.

### Mas primeiro precisamos instalar uma biblioteca externa para consumir essas APIs. A maioria dos desenvolvedores Python usa a biblioteca `requests` para interagir com os serviços da web. Você pode instalar essa biblioteca usando o comando `pip` como este:

```
$ pip install requests
```

### Assim que a biblioteca estiver instalada, estamos prontos para prosseguir!

## Como fazer uma solicitação GET:

### Este é um dos métodos de solicitação HTTP mais comuns que você encontrará. É uma operação **somente leitura(read only)** que permite recuperar dados da API.

### Vamos experimentar a solicitação GET no primeiro endpoint mencionado acima, que responde com uma lista de produtos.

```python
import requests

BASE_URL = 'https://fakestoreapi.com'

response = requests.get(f"{BASE_URL}/products")
print(response.json())
```

### O script acima usa o método `requests.get()` para enviar uma solicitação GET no endpoint `/products` da API. Ele responde com uma lista de todos os produtos. Em seguida, chamamos `.json()` para visualizar a resposta JSON, que se parece com isto:

```
Veja o arquivo: file_api.json
```

### Se você olhar de perto, a resposta JSON parece uma lista de dicionários Python. JSON é um formato de intercâmbio de dados muito popular para APIs REST.

### Você também pode imprimir outros atributos relacionados à resposta, como o código de status.

```python
print(response.status_code)

# OUTPUT:
# >>> 200
```

### Como sabemos, o código de status 200 significa uma resposta de sucesso.

### Como o endpoint `/products` retorna muitos dados, vamos limitar esses dados a apenas 3 produtos.

### Para fazer isso, temos um ponto final `/products?limit=x` onde x é um número inteiro positivo. O `limit` é chamado de parâmetro de consulta. Vamos ver como podemos adicionar este parâmetro de consulta na solicitação.

### O método `requests.get()` usa um parâmetro chamado `params`, onde podemos especificar nossos parâmetros de consulta na forma de um dicionário Python. Assim, criamos um dicionário chamado `query_params` e passamos `limit` como chave e `3` como valor. Em seguida, passamos esse `query_params` no `request.get()`. A saída agora se parece com isto:

```JSON
[
  {
    "id": 1,
    "title": "Fjallraven - Foldsack No. 1 Backpack, Fits 15 Laptops",
    "price": 109.95,
    "description": "Your perfect pack for everyday use and walks in the forest. Stash your laptop (up to 15 inches) in the padded sleeve, your everyday",
    "category": "men's clothing",
    "image": "https://fakestoreapi.com/img/81fPKd-2AYL._AC_SL1500_.jpg",
    "rating": { "rate": 3.9, "count": 120 }
  },
  {
    "id": 2,
    "title": "Mens Casual Premium Slim Fit T-Shirts ",
    "price": 22.3,
    "description": "Slim-fitting style, contrast raglan long sleeve, three-button henley placket, light weight & soft fabric for breathable and comfortable wearing. And Solid stitched shirts with round neck made for durability and a great fit for casual fashion wear and diehard baseball fans. The Henley style round neckline includes a three-button placket.",
    "category": "men's clothing",
    "image": "https://fakestoreapi.com/img/71-3HjGNDUL._AC_SY879._SX._UX._SY._UY_.jpg",
    "rating": { "rate": 4.1, "count": 259 }
  },
  {
    "id": 3,
    "title": "Mens Cotton Jacket",
    "price": 55.99,
    "description": "great outerwear jackets for Spring/Autumn/Winter, suitable for many occasions, such as working, hiking, camping, mountain/rock climbing, cycling, traveling or other outdoors. Good gift choice for you or your family member. A warm hearted love to Father, husband or son in this thanksgiving or Christmas Day.",
    "category": "men's clothing",
    "image": "https://fakestoreapi.com/img/71li-ujtlUL._AC_UX679_.jpg",
    "rating": { "rate": 4.7, "count": 500 }
  }
]
```

### Agora temos os dados de resposta limitados a apenas 3 produtos. Vamos tentar obter apenas um produto com o `id` 18.

### Como temos um endpoint `/products /<product_id>`, podemos passar o `id` 18 na URL da API e fazer uma solicitação GET nele. A resposta é parecida com esta:

```JSON
{
  "id": 18,
  "title": "MBJ Women's Solid Short Sleeve Boat Neck V ",
  "price": 9.85,
  "description": "95% RAYON 5% SPANDEX, Made in USA or Imported, Do Not Bleach, Lightweight fabric with great stretch for comfort, Ribbed on sleeves and neckline / Double stitching on bottom hem",
  "category": "women's clothing",
  "image": "https://fakestoreapi.com/img/71z3kpMAYsL._AC_UY879_.jpg",
  "rating": {
      "rate": 4.7,
      "count": 130
  }
}
```

## Como fazer uma solicitação POST:

### Usamos a solicitação POST para adicionar novos dados à API REST. Os dados são enviados ao servidor no formato JSON, que se parece com um dicionário Python. De acordo com a documentação da API da Fake Store, um produto possui os seguintes atributos: `title`, `price`, `description`, `image` e `category`. Portanto, um novo produto se parece com isto:

```JSON
new_product = {
    "title": "test product",
    "price": 13.5,
    "description": "lorem ipsum set",
    "image": "https://i.pravatar.cc",
    "category": "electronic"
}
```

### Podemos enviar uma solicitação POST usando o método `requests.post()` assim:

```Python
import requests

BASE_URL = 'https://fakestoreapi.com'

new_product = {
    "title": 'test product',
    "price": 13.5,
    "description": 'lorem ipsum set',
    "image": 'https://i.pravatar.cc',
    "category": 'electronic'
}

response = requests.post(f"{BASE_URL}/products", json=new_product)
print(response.json())
```

### No método `requests.post()`, podemos passar dados JSON usando o argumento `json`. O uso do argumento `json` define automaticamente o `Content-Type` como `Application/JSON` no cabeçalho da solicitação.

### Depois de fazer uma solicitação POST no endpoint `/products`, obtemos um objeto de produto com o `id` na resposta. A resposta é parecida com esta:

```JSON
{
  "_id": "61b45067e087f30012c45a45",
  "id": 21,
  "title": "test product",
  "price": 13.5,
  "description": "lorem ipsum set",
  "image": "https://i.pravatar.cc",
  "category": "electronic"
}
```

### Se não usarmos o argumento `json`, temos que fazer a solicitação POST assim:

```Python
import requests
import json

BASE_URL = 'https://fakestoreapi.com'

new_product = {
    "title": 'test product',
    "price": 13.5,
    "description": 'lorem ipsum set',
    "image": 'https://i.pravatar.cc',
    "category": 'electronic'
}

headers = {
    "Content-Type": "application/json"
}

response = requests.post(f"{BASE_URL}/products", data=json.dumps(new_product), headers=headers)
print(response.json())
```

### Nesse caso, em que usamos o argumento de `data` em vez de `json`, precisamos definir o `Content-Type` como `application/json` no cabeçalho explicitamente. Enquanto no caso do argumento `json`, não precisamos serializar os dados - mas precisamos serializar os dados usando `json.dumps()` neste caso.

## Como fazer uma solicitação PUT:

### Freqüentemente, precisamos atualizar os dados existentes na API. Usando a solicitação PUT, podemos atualizar os dados completos. Isso significa que, quando fazemos uma solicitação PUT, ela substitui os dados antigos pelos novos.

### Na solicitação POST, criamos um novo produto cujo `id` era 21. Vamos atualizar o produto antigo com um novo produto fazendo uma solicitação PUT no ponto de extremidade `products/<product_id>`.

```Python
import requests

BASE_URL = 'https://fakestoreapi.com'

updated_product = {
    "title": 'updated_product',
    "category": 'clothing'
}

response = requests.put(f"{BASE_URL}/products/21", json=updated_product)
print(response.json())
```

### Quando fazemos a solicitação PUT com o `updated_product` usando o método `requests.put()`, ele responde com os seguintes dados JSON:

```JSON
{
  "id": "21",
  "title": "updated_product",
  "category": "clothing"
}
```

### Observe que o produto antigo foi completamente substituído pelo produto atualizado.

## Como fazer uma solicitação PATCH:

### Às vezes, não precisamos substituir os dados antigos completamente. Em vez disso, desejamos modificar apenas alguns campos. Nesse caso, usamos a solicitação PATCH.

### Vamos atualizar a categoria do produto de volta de **vestuário(clothing)** para **eletrônico(electronic)**, fazendo uma solicitação PATCH no endpoint `products/<product_id>`.

```Python
import requests

BASE_URL = 'https://fakestoreapi.com'

updated_product = {
    "category": 'electronic'
}

response = requests.patch(f"{BASE_URL}/products/21", json=updated_product)
print(response.json())
```

### Observe que, desta vez, os dados inteiros não foram alterados - apenas o campo da categoria foi atualizado.

## Como fazer uma solicitação DELETE:

### Como o nome sugere, se você deseja excluir um recurso da API, pode usar uma solicitação DELETE. Vamos deletar este produto com `id` 21.

```Python
import requests

BASE_URL = 'https://fakestoreapi.com'

response = requests.delete(f"{BASE_URL}/products/21")
print(response.json())
```

### O método `requests.delete()` nos ajuda a fazer uma solicitação DELETE no `endpoint/products/<product_id>`.

## Empacotando

### Neste tutorial, aprendemos como podemos interagir com serviços da web usando uma ferramenta incrível chamada de **solicitações(requests)** em Python.

### Espero que tenham gostado - e obrigado pela leitura!
