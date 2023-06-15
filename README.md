# MongoDB

***Iniciar banco de dados:***
```
mongod.exe
```

> Utilizar o pront de comando!

***Se conectar com o banco de dados:***
```sql
mongosh
```
> Para se comunicar com o Mongo é necessário de ter executado o comando anterior!

***Ajuda:***
```
mongod --help
```

***Exibir bancos de dados disponiveis:***
```
show dbs
```

***Mudar para um banco de dados especifico:***
```
use meubd
```

**Extrutura do MongoDB:**
- **Database**
- **Collection**
- **Document**

***Verificar o banco de dados que está sendo utilizado no momento:***
```
db
```

***Criar coleção:***
```
db.alunos.insert(
    {
      "nome": "Toninho",
      "idade": 12,
      "gotoDe": [
        "futebol",
        "carrinho",
        "video game"
      ],
      "naEscola": true,
      "materias": {
        "português": 8.9,
        "matemática": 9.5,
        "história": 2.4 
      }
    }
  )
```

***Criar registro único:***
```
db.crud.insertOne({b: 234})
```

***Criar registro com vários items:***
```
db.crud.insertMany([{f: 123}, {e: 334}, {g: 234}])
```

***Criar registro com ordered false:***
```
db.crud.insertMany([{f: 123}, {e: 334}, {g: 234}], {ordered: false})
```

>  ***Por padrão o booleano ordered vem como verdadeiro, onde não é possivel inserir novos registros com dados repetidos porém caso ele seja configurado para vim como falso... items que não esteja de acordo com a ação esperada, serão irgnorados de forma automática! A ação execução irá pular para o próximo item da lista e irá adicionar o novo item no banco de dados, caso o mesmo esteja de acordo com as regras e definições do MongoDB.***
 
***Buscar coleção:***
```
db.alunos.find()
```

***Formatar Json:***
```
 db.alunos.find().pretty()
```

***Buscar documento com dados definidos:***
```
db.crud.find({ a: 1234 })
```

***Buscar primeiro item da coleção:***
```
db.alunos.findOne()
```

***Buscar primeiro item da coleção com findOne:***
```
db.crud.findOne({ a: 1234 })
```

***Buscar id:***
```
 db.alunos.findOne()._id
```

***Ver a data que o documento foi criado através do ISODate:***
```
escola> db.alunos.findOne()._id.getTimestamp()
```

***Atualizar documento:***
```
db.crud.updateOne({b:234}, { $set: {h: 555}})
```

***Atualizando vários documentos:***
```
db.crud.updateMany({a:1234}, { $set: {h: 20}})
```

***Trocar valor do documento:***
```
db.crud.replaceOne({e:334}, {outro: "documento"})
```

***Deletar um documento:***
```
db.crud.deleteOne({b: 555})
```

***Deletar mais de um documento:***
```
 db.crud.deleteMany({g: 234})
```

***Deletar documento da query updateOne ou updateMany:***
```
db.crud.deleteMany({h: {$exists: true}})
```

***Deletar todos os documentos da coleção:***
```
db.crud.deleteMany({})
```

# Relacionamento One To One

***Embedded documents:***
```
{
    "_id": 1,
    "cpf": "123456798",
    "nome": "Joãozinho",
    "cidade": "São Paulo",
    "carteirinha": {
        "_id": 8,
        "turma": "220A",
        "ra": 1245
    }
}
```
> ***No relacionamento um pra um, os dados são incorporados dentro do documento.***

# Relacionamento One To Many
***Um Para Muitos:***
```
{
    "_id": 3,
    "meta": 4000,
    "nome": "Vendas",
    "funcionarios": [
        {
            "_id": 8,
            "salario": 1400,
            "turno": "tarde",
            "cargo": "vendedor"
        },
        {
            "_id": 12,
            "salario": 1600,
            "turno": "noite",
            "cargo": "vendedor"
        }
    ]
}
```

# Relacionamento Many To Many 
***Muitos Para Muitos:***
```
{
    "_id": "f04",
    "cnpj": "165486984",
    "nome": "Fornecedor Legal",
    "cep": "1098465",
    "produto_ids": ["p16", "p21"]
}
 
{
    "_id": "f07",
    "cnpj": "98498151",
    "nome": "Fornecedor Maneiro",
    "cep": "198498",
    "produto_ids": ["p21", "p47"]
}
// Collection Produtos
{
    "_id": "p16",
    "descricao": "Panela",
    "preco": 45.50,
    "fornecedor_ids": ["f04"]
}
 
{
    "_id": "p21",
    "descricao": "Prato",
    "preco": 14,
    "fornecedor_ids": ["f04", "f07"]
} 
 
{
    "_id": "p47",
    "descricao": "Faqueiro",
    "preco": 127.46,
    "fornecedor_ids": ["f07"]
}
```
***Muitos Para Muitos | Híbrido de Referência com Embedded:***
```
// Collection Fornecedores
{
    "_id": "f04",
    "cnpj": "165486984",
    "nome": "Fornecedor Legal",
    "cep": "1098465",
    "produtos": [
        {
            "_id": "p16",
            "preco": 46.50
        },
        {
            "_id": "p21",
            "preco": 12
        }
    ]
}
 
{
    "_id": "f07",
    "cnpj": "98498151",
    "nome": "Fornecedor Maneiro",
    "cep": "198498",
    "produtos": [
        {
            "_id": "p21",
            "preco": 16
        },
        {
            "_id": "p47",
            "preco": 127.46
        }
    ]
}


// Collection Produtos
{
    "_id": "p16",
    "descricao": "Panela",
    "fornecedores": [
        {
            "_id": "f04",
            "preco": 46.50
        }
    ]
}
 
{
    "_id": "p21",
    "descricao": "Prato",
    "fornecedores": [
        {
            "_id": "f04",
            "preco": 12
        },
        {
            "_id": "f07",
            "preco": 16
        }
    ]
} 
 
{
    "_id": "p47",
    "descricao": "Faqueiro",
    "fornecedores": [
        {
            "_id": "f07",
            "preco": 127.46
        }
    ]
}
```

***Duplicar ou não duplicar? Segredos e vantagens desse modelo:***
```
// Collection Fornecedores
{
    "_id": "f04",
    "cnpj": "165486984",
    "nome": "Fornecedor Legal",
    "cep": "1098465",
    "produtos": [
        {
            "_id": "p16",
            "descricao": "Panela",
            "preco": 46.50
        },
        {
            "_id": "p21",
            "descricao": "Prato",
            "preco": 12
        }
    ]
}
 
{
    "_id": "f07",
    "cnpj": "98498151",
    "nome": "Fornecedor Maneiro",
    "cep": "198498",
    "produtos": [
        {
            "_id": "p21",
            "descricao": "Prato",
            "preco": 16
        },
        {
            "_id": "p47",
            "descricao": "Faqueiro",
            "preco": 127.46
        }
    ]
}
// Collection Produtos
{
    "_id": "p16",
    "descricao": "Panela",
    "fornecedores": [
        {
            "_id": "f04",
            "preco": 46.50,
            "cep": "1098465"
        }
    ],
    "peso": 4,
    "unidade_peso": "kg",
    "altura": 14,
    "largura": 15,
    "profundidade": 20
}
 
{
    "_id": "p21",
    "descricao": "Prato",
    "fornecedores": [
        {
            "_id": "f04",
            "preco": 12,
            "cep": "1098465"
        },
        {
            "_id": "f07",
            "preco": 16,
            "cep": "198498",
        }
    ]
} 
 
{
    "_id": "p47",
    "descricao": "Faqueiro",
    "fornecedores": [
        {
            "_id": "f07",
            "preco": 127.46,
            "cep": "198498",
        }
    ]
}
```

# Schema e Validation

***Apagar coleção:***
```
 db.cars.drop()
```

***Listar Coleções por nome:***
```
db.getCollectionNames()
```

***Criar coleção com validação:***
```
db.createCollection("cars", {
	validator: {
  		$jsonSchema: {
   			bsonType: "object",
			required: ["model", "year"],
			properties: {
				model: {
					bsonType: "string",
					description: "O Modelo é necessário e deve ser uma string"
				},
				madeBy: {				
					bsonType: "string",
					description: "O Modelo é necessário e deve ser uma string",
					minLength: 3
				},
				year: {
					bsonType: "int",
					description: "O Modelo é necessário e deve ser um inteiro",
					minimum: 1980,
					maximum: 2025
				}
			}
  		} 
	}
})
```

> O validator cria validações para os atributos do MongoDB! Diferente de bancos de dados relacionais, o MongoDB, aceita diferentes valores em um mesmo campo, onde isso pode gerar um problema. Para resolver o problema é necessário, criar validações manualmente e informar qual é o valor do campo.

***Capped Collections | Funciona como uma fila:***
```
db.createCollection("logs", {
    capped: true,
    size: 2048,
    max: 5
})
```

# Queries

***Buscando documento com dados especificos:***
```
 db.pokemon.find({ "legendary": true })
```

***Buscando documento com filtros e com a quantidade de items da coleção:***
```
 db.pokemon.find({ "legendary": true }).count()
```

***Buscar valores distintos:***
```
db.pokemon.distinct("generation")
```

***Buscando nome com Regex:***
```
db.pokemon.find({ name: /Pik/ })
```

***Buscar por nomes que começam com letras especificadas na query:***
```
db.pokemon.find({ name: /^Pik/ })
```

***Retornando apenas campos específicos da coleção com o projection:***
```
db.pokemon.find({ name: /^Pik/ }, {name: true })
```

***Buscando por letras  minúsculas:***
```
db.pokemon.find({ name: /^pik/i }, {name: true })
```

***Buscando valores que são iguais a um valor especificado default:***
```
db.pokemon.find({ attack: 85 }, {attack: true })
```

***Buscando valores que são iguais a um valor especificado:***
```
 db.pokemon.find({ attack: { $eq: 85 }  }, {attack: true })
```

***Buscando valores maiores que um valor especificado:***
```
pokemon_center> db.pokemon.find({ attack: { $gt: 85 }  }, {attack: true })
```

***Buscando valores maiores ou iguais a um valor especificado:***
```
db.pokemon.find({ attack: { $gte: 85 }  }, {attack: true })
```

***Buscando valores que são menores que um valor especificado:***
```
 db.pokemon.find({ attack: { $lt: 85 }  }, {attack: true })
```

***Buscando valores menores ou iguais a um valor especificado:***
```
db.pokemon.find({ attack: { $lte: 85 }  }, {attack: true })
```

***Buscando a todos os valores que não são iguais a um valor especificado:***
```
db.pokemon.find({ attack: { $ne: 85 }  }, {attack: true })
```

***Buscando strings dentro de arrays:***
```
db.pokemon.find({ types: "Fire" }, {name: true, types: true})
```

***Filtrando por dados específicos dentro de um array:***
```
db.pokemon.find({ types: { $in: ["Fire", "Rock"] } }, {name: true, types: true})
```

***Filtrando por dados distintos do dados Especificados dentro de um array:***
```
db.pokemon.find({ types: { $nin: ["Fire", "Rock"] } }, {name: true, types: true})
```
***Filtrando por dados na coleção:***
```
db.pokemon.find({ name: { $in: ["Pichu", "Pikachu"] } })
```

# Combinando operadores

***Combinando operadores:***
```
db.pokemon.find({ defense: { $gt: 60, $lte: 72 }}, {name: true, defense: true})
```

***Mesclando queries com operadores logicos $or:***
```
db.pokemon.find(
 {
   $or: [
     {
       defense: {
	$gte: 60,
	$lte: 72
       },
     },
     {
       defense: 100
     },
   ],
 },
 { name: true, defense: true }
)
```

***Filtrando mais de um campo com o $or***:
```
db.pokemon.find(
 {
   $or: [
     {
       defense: {
	$gte: 80
       },
     },
     {
       attack: {
        $gte: 80
       }
     },
   ],
 },
 { name: true, defense: true, attack: true }
)
```

***Encontrando pokemons fortes OU com muita defesa***:
```
db.pokemon.find(
 {
   $or: [
     {
       defense: {
	$gte: 80
       },
       hp: {
        $gte: 80
       }
     },
     {
       attack: {
        $gte: 80
       },
       speed: {
        $gte: 80
       }
     },
   ],
 },
 { name: true, defense: true, attack: true, speed: true }
)
```

***Ordenar dados de ordem crescente utilizando o sort:***
```
db.pokemon.find(
 {
   $or: [
     {
       defense: {
	$gte: 80
       },
       hp: {
        $gte: 80
       }
     },
     {
       attack: {
        $gte: 80
       },
       speed: {
        $gte: 80
       }
     },
   ],
 },
 { hp: true }
).sort({
   hp: 1
})
```

***Ordenar dados de ordem decrescente utilizando o sort:***
```
db.pokemon.find(
 {
   $or: [
     {
       defense: {
	$gte: 80
       },
       hp: {
        $gte: 80
       }
     },
     {
       attack: {
        $gte: 80
       },
       speed: {
        $gte: 80
       }
     },
   ],
 },
 { hp: true }
).sort({
   hp: -1
})
```

***Ordenar dados de ordem decrescente com combinação de valores no sort:***
```
db.pokemon.find(
 {
   $or: [
     {
       defense: {
	$gte: 80
       },
       hp: {
        $gte: 80
       }
     },
     {
       attack: {
        $gte: 80
       },
       speed: {
        $gte: 80
       }
     },
   ],
 },
 { hp: true }
).sort({
   {  hp: 1, defense: -1 }
})
```

***Retornando dados com Size caso a condição estabelecidade retorne os dados informados:***
```
db.pokemon.find({ types: { $size: 2 } }, { _id: false, name: true, types: true})
```

> Os dados informados no Size, também pode ser em formatado de String.

***Retornando dados com All caso as duas condições do filtro sejam verdadeiras:***
```
db.pokemon.find({ types: { $all: ["Rock", "Flying"] } }, { _id: false, name: true, types: true})
```

***Utilizando páginação com o limit:***
```
db.pokemon.find({ types: "Fire" }).sort({ attack: -1}).limit(5)
```

***Trocando de página através do skip:***
```
db.pokemon.find({ types: "Fire" }).sort({ attack: -1}).skip(5).limit(6)
```

> Para pular de uma página para outra é necessário pular a quantidade items referentes ao limit em questão.

***Verificar se um campo existe dentro da coleção:***
```
 db.pokemon.find({ battle_points: { $exists: true } })
```

***Filtrando em embeded documents com o dot notation:***
```
db.pokemon.find({ "battle_points.hp": { $lte: 40 } })
```

# Updates

***Adicionar novo campo dentro da coleção utilizando o  $set:***
```
db.pokemon.updateOne({ name: /^O/ }, { $set: { startsWithO: true }})
```

***Adicionar novo campo dentro das coleções que Condizem com as estruções da query informada usando o $set:***
```
db.pokemon.updateMany({ name: /^O/ }, { $set: { startsWithO: true }})
```

