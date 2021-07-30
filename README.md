# Banco de dados - Mongo DB
Criação de um banco de dados no Mongo DB com rotas de 
pesquisa, inclusão, alteração e exclusão de ítens.

#### Demandas de negócio
- Inserção de documentos;
- Atualização de documentos;
- Exclusão de documentos;
- Consulta com projeção;
- Consulta utilizando combinação entre os seletores;
- Consulta paginada e ordenada (utilizar skip, limit e sort).


## Banco de dados - Rotas usadas para as demandas

#### Buscando Séries

```http
db.getCollection('series').find({})
```
#### Inserindo uma série

```http
  db.series.insertMany
```

#### Atualizando a quantidade de temporadas de uma série

```http
  db.getCollection('series').update(
    {
        "title" : "Game of Thrones"
    },
    
    {
        $set:{'seasons': '8'}
    },
    
    {
        "multi" : false
    }
);
```

#### Excluindo uma série

```http
  db.getCollection('series').remove({
    "genre": { $ne: "sci-fi" }
})
```

#### Consulta com projeção - Séries de drama ordenadas de forma decrescente de acordo com o número de temporadas

```http
  db.getCollection('series').find({genre:'drama'}).sort({seasons: 1})
```

#### Consulta combinando informações - Séries de drama com mais de 1 temporada

```http
  db.getCollection('series').find({'genre':'drama', 'seasons':{$gt:1}})
```

#### Consulta ordenada com (skip, limit e sort) - Série de drama com a 3° menor quantidade de temporadas

```http
db.getCollection('livros').find({'categoria':'Aventura'}).sort({seasons: 1}).skip(2).limit(1)
```
