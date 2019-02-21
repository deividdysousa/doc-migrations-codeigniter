# Documentação auxiliar das Migrations do Codigniter 3
obs: documentação criada para auxiliar no desenvolvimento das aplicações com Codeigniter (não oficial)


### Metodos
- Criar tabela
  - Adicionando uma chave primaria
  - Adicionando uma chave estrangeira
  - Adicionando colunas a uma tabela existente
- Remover Tabelas
  - Remover colunas
  - Renomear colunas
- Renomear tabela



---
#### Criar Tabela
```php
$columns = [
    'codigo'    =>  [
        'type'              =>  'INT',
        'auto_increment'    =>  true
    ],
    'nome'    =>  [
        'type'              =>  'VARCHAR',
        'constraint'        =>  100
    ],
    'telefone'    =>  [
        'type'              =>  'VARCHAR',
        'constraint'        =>  20
    ]
];
$this->dbforge->create_table ('Clientes');
```

##### Adicionando uma chave primaria
```php
$this->dbforge->add_key ('codigo', TRUE);
```

##### Adicionando uma chave estrangeira
```php
$this->dbforge->add_field('FOREIGN KEY(codigo_cliente) REFERENCES Clientes(codigo) on delete cascade');
```

##### Adicionando colunas a uma tabela existente
```php
$columns = [
  'email'    =>  [
    'type'              =>  'VARCHAR',
    'constraint'        =>  50
  ]
];

$this->dbforge->add_column ('Clientes', $columns);
```

---
#### Remover Tabelas
```php
$this->dbforge->drop_table ('Fone');
```
Para Verificar se a mesma existe:  
```php
$this->dbforge->drop_table ('Fone', TRUE)
```

##### Remover colunas
```php
$this->dbforge->drop_column ('Clientes', 'email');
```

##### Renomear colunas
```php
$sql = "ALTER TABLE Clientes CHANGE email new_email varchar(255) not null";
$this->db->query($sql);
```
