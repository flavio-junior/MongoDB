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

***Buscar coleção:***
```
db.alunos.find()
```

***Buscar primeiro item da coleção:***
```
db.alunos.findOne()
```

***Buscar id:***
```
 db.alunos.findOne()._id
```

***Ver a data que o documento foi criado através do ISODate:***
```
escola> db.alunos.findOne()._id.getTimestamp()
```

***Formatar Json:***
```
 db.alunos.find().pretty()
```

