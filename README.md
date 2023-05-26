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

