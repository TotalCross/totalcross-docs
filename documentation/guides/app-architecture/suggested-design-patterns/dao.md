# Data Persistence: DAO Pattern.

The DAO persistence pattern serves to isolate the persistence layer of the application layer, thus allowing both parts to evolve separately without knowing anything about the other.

### Structures

{% code title="Structures" %}
```text
└── src
    └── main
        └── java
            └── com.your_company_name.your_name_app
                .
                .
                .
                └── persistence
                    └──SampleDAO.java
```
{% endcode %}

You can see an example using DAO in TotalCross in the [SQLite documentation](https://app.gitbook.com/@totalcross/s/playbook/~/drafts/-Ld5U4zrEcGVLc5JZxHO/primary/learn-totalcross/how-to-store-data-sqlite#inserting-data-into-the-table)

## Referencies

* See more about DAO Pattern in [baeldung ](%20https://www.baeldung.com/java-dao-pattern)and [DevMedia](https://www.devmedia.com.br/dao-pattern-persistencia-de-dados-utilizando-o-padrao-dao/30999)

