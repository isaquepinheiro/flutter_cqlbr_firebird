## Criteria Query Language Brasil (Dart/Flutter)

CQLBr é um framework opensource que provê escritas gerando o script SQL, através de uma interface, permitindo mapear de forma orientada a objeto, toda sintaxe de comandos SQL (SELECT, INSERT, UPDATE e DELETE), para banco de dados relacional.

Durante o desenvolvimento de software, é evidente a preocupação em que se tem em aumentar a produtividade e manter a compatibilidade entre os possíveis bancos que um sistema pode usar. No que se refere a sintaxe de banco de dados, temos em alguns casos, incompatibilidades entre comandos SQL, exigindo assim, a necessidade de um maior controle na escrita de cada banco, e foi para ajudar nesse ponto crítico que CQLBr nasceu, ele foi projetado para que a escrita de querys seja única, de forma funcional e orientada a objeto, possibilitando assim a mesma escrita feita pelo framework, gerar querys diferentes conforme o banco selecionado, o qual pode ser mudado de forma muito simples, bastando selecionar um dos modelos implementados no CQLBr Framework, sem ter que re-faturar diversas querys espalhadas pelas milhares de linhas de código.

## SELECT

```dart
  CQLBr cqlbr = CQLBr(select: CQLSelectFirebird());

  Expect : "SELECT ID_CLIENTE, NOME_CLIENTE, (CASE TIPO_CLIENTE WHEN 0 THEN 'FISICA' WHEN 1 THEN 'JURIDICA' ELSE 'PRODUTOR' END) AS TIPO_PESSOA FROM CLIENTES");

  String result = cqlbr
        .select$()
          .column$('ID_CLIENTE')
          .column$('NOME_CLIENTE')
          .column$('TIPO_CLIENTE')
          .case$(null)
            .when$('0').then$(Fun.q('FISICA'))
            .when$('1').then$(Fun.q('JURIDICA'))
                       .else$(Fun.q('PRODUTOR'))
          .end$()
        .as$('TIPO_PESSOA')
        .from$('CLIENTES')
    .asString();
```

## INSERT

```dart
Expect : "INSERT INTO CLIENTES (ID_CLIENTE, NOME_CLIENTE) VALUES ('1', 'MyName')";

String result = cqlbr
       .insert$()
       .into$('CLIENTES')
       .set$('ID_CLEINTE', 1)
       .set$('NOME_CLIENTE', 'MyName')
    .asString();
```

## Additional information

TODO: multi-database SQL syntax using object orientation, now in flutter.