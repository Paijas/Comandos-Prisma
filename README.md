# Comandos Prisma



Este repositório contém uma documentação detalhada e exemplos práticos de comandos Prisma, especialmente para desenvolvedores que já estão familiarizados com SQL. O objetivo deste repositório é servir como uma referência rápida, permitindo um entendimento claro e aplicação eficiente dos comandos Prisma.

### Estrutura do Repositório

- **Documentação de Comandos Prisma**: Um arquivo Markdown que descreve e explica cada comando Prisma, com uma visão geral e exemplos de uso.
- **Exemplos de Comandos Prisma**: Um arquivo separado contendo apenas os exemplos práticos de cada comando Prisma, organizados por tópicos.

### Comandos Prisma Cobertos

- **Filtros e Condições**: `AND`, `OR`, `NOT`, `equals`, `in`, `contains`, `startsWith`, `endsWith`
- **Funções de Agregação**: `count`, `avg`, `sum`, `min`, `max`
- **Ordenação e Limitação de Resultados**: `orderBy`, `take`, `skip`
- **Agrupamento e Filtragem de Grupos**: `groupBy`, `having`
- **Manipulação de Strings**: `contains`, `startsWith`, `endsWith`
- **Tratamento de Nulos**: `null`, `notNull`
- **Conexão de Tabelas**: `connect`, `disconnect`, `set`, `create`, `delete`
- **Combinação de Resultados**: Não aplicável diretamente, mas `findMany` pode ser usado para múltiplas consultas
- **Outras Funções e Comandos**: `findUnique`, `findFirst`, `create`, `update`, `delete`, `upsert`, `raw`, `transaction`, `executeRaw`

## Índice

- [AND](#and)
- [avg](#avg)
- [connect](#connect)
- [contains](#contains)
- [count](#count)
- [create](#create)
- [delete](#delete)
- [disconnect](#disconnect)
- [endsWith](#endswith)
- [equals](#equals)
- [findFirst](#findfirst)
- [findMany](#findmany)
- [findUnique](#findunique)
- [groupBy](#groupby)
- [having](#having)
- [in](#in)
- [max](#max)
- [min](#min)
- [NOT](#not)
- [null](#null)
- [orderBy](#orderby)
- [OR](#or)
- [raw](#raw)
- [set](#set)
- [skip](#skip)
- [startsWith](#startswith)
- [sum](#sum)
- [take](#take)
- [transaction](#transaction)
- [update](#update)
- [upsert](#upsert)

---

## Descrições de Comandos Prisma

### AND
- **Comando:** `AND`
  - **Descrição:** Combina condições múltiplas em uma cláusula `where`, retornando resultados que satisfaçam todas as condições.
  - **Exemplo:**
    ```ts
    const produtos = await prisma.produto.findMany({
      where: {
        AND: [
          { preco: { gt: 10 } },
          { estoque: { gt: 0 } }
        ]
      }
    });
    ```

### avg
- **Comando:** `avg`
  - **Descrição:** Calcula a média de um campo numérico.
  - **Exemplo:**
    ```ts
    const avgPreco = await prisma.produto.aggregate({
      _avg: {
        preco: true
      }
    });
    ```

### connect
- **Comando:** `connect`
  - **Descrição:** Conecta registros existentes em relações entre tabelas.
  - **Exemplo:**
    ```ts
    const pedido = await prisma.pedido.create({
      data: {
        cliente: {
          connect: { id: clienteId }
        }
      }
    });
    ```

### contains
- **Comando:** `contains`
  - **Descrição:** Filtra resultados que contêm uma string específica.
  - **Exemplo:**
    ```ts
    const produtos = await prisma.produto.findMany({
      where: {
        nome: { contains: 'produto' }
      }
    });
    ```

### count
- **Comando:** `count`
  - **Descrição:** Retorna o número total de registros que correspondem ao critério especificado.
  - **Exemplo:**
    ```ts
    const numProdutos = await prisma.produto.count({
      where: {
        preco: { gt: 20 }
      }
    });
    ```

### create
- **Comando:** `create`
  - **Descrição:** Cria um novo registro em uma tabela.
  - **Exemplo:**
    ```ts
    const novoProduto = await prisma.produto.create({
      data: {
        nome: 'Produto A',
        preco: 20.0
      }
    });
    ```

### delete
- **Comando:** `delete`
  - **Descrição:** Remove um registro de uma tabela com base em uma condição.
  - **Exemplo:**
    ```ts
    const produtoDeletado = await prisma.produto.delete({
      where: { id: produtoId }
    });
    ```

### disconnect
- **Comando:** `disconnect`
  - **Descrição:** Desconecta um registro relacionado, sem removê-lo do banco de dados.
  - **Exemplo:**
    ```ts
    const atualizacaoPedido = await prisma.pedido.update({
      where: { id: pedidoId },
      data: {
        cliente: {
          disconnect: true
        }
      }
    });
    ```

### endsWith
- **Comando:** `endsWith`
  - **Descrição:** Filtra resultados que terminam com uma string específica.
  - **Exemplo:**
    ```ts
    const produtos = await prisma.produto.findMany({
      where: {
        nome: { endsWith: 'final' }
      }
    });
    ```

### equals
- **Comando:** `equals`
  - **Descrição:** Filtra resultados que correspondem exatamente a um valor específico.
  - **Exemplo:**
    ```ts
    const produtos = await prisma.produto.findMany({
      where: {
        preco: { equals: 10.0 }
      }
    });
    ```

### findFirst
- **Comando:** `findFirst`
  - **Descrição:** Retorna o primeiro registro que corresponde ao critério especificado.
  - **Exemplo:**
    ```ts
    const primeiroProduto = await prisma.produto.findFirst({
      where: { preco: { gt: 10 } }
    });
    ```

### findMany
- **Comando:** `findMany`
  - **Descrição:** Retorna todos os registros que correspondem ao critério especificado.
  - **Exemplo:**
    ```ts
    const produtos = await prisma.produto.findMany({
      where: { preco: { gt: 10 } }
    });
    ```

### findUnique
- **Comando:** `findUnique`
  - **Descrição:** Retorna um único registro que corresponde ao critério especificado.
  - **Exemplo:**
    ```ts
    const produtoUnico = await prisma.produto.findUnique({
      where: { id: produtoId }
    });
    ```

### groupBy
- **Comando:** `groupBy`
  - **Descrição:** Agrupa registros por campos específicos e permite operações de agregação.
  - **Exemplo:**
    ```ts
    const produtosPorCategoria = await prisma.produto.groupBy({
      by: ['categoria'],
      _count: {
        _all: true
      }
    });
    ```

### having
- **Comando:** `having`
  - **Descrição:** Filtra os resultados de grupos formados pelo `groupBy`.
  - **Exemplo:**
    ```ts
    const categoriasComMuitosProdutos = await prisma.produto.groupBy({
      by: ['categoria'],
      having: {
        _count: {
          _all: { gt: 5 }
        }
      }
    });
    ```

### in
- **Comando:** `in`
  - **Descrição:** Filtra resultados que correspondem a qualquer valor dentro de um conjunto especificado.
  - **Exemplo:**
    ```ts
    const produtos = await prisma.produto.findMany({
      where: {
        categoria: { in: ['Eletrônicos', 'Móveis'] }
      }
    });
    ```

### max
- **Comando:** `max`
  - **Descrição:** Retorna o valor máximo de um campo.
  - **Exemplo:**
    ```ts
    const precoMaximo = await prisma.produto.aggregate({
      _max: {
        preco: true
      }
    });
    ```

### min
- **Comando:** `min`
  - **Descrição:** Retorna o valor mínimo de um campo.
  - **Exemplo:**
    ```ts
    const precoMinimo = await prisma.produto.aggregate({
      _min: {
        preco: true
      }
    });
    ```

### NOT
- **Comando:** `NOT`
  - **Descrição:** Exclui registros que correspondem ao critério especificado.
  - **Exemplo:**
    ```ts
    const produtosNaoBaratos = await prisma.produto.findMany({
      where: {
        NOT: {
          preco: { lt: 10 }
        }
      }
    });
    ```

### null
- **Comando:** `null`
  - **Descrição:** Filtra registros com valores nulos em um campo.
  - **Exemplo:**
    ```ts
    const produtosSemDescricao = await prisma.produto.findMany({
      where: {
        descricao: null
      }
    });
    ```

### orderBy
- **Comando:** `orderBy`
  - **Descrição:** Ordena os resultados da consulta.
  - **Exemplo:**
    ```ts
    const produtosOrdenados = await prisma.produto.findMany({
      orderBy: {
        preco: 'asc'
      }
    });
    ```

### OR
- **Comando:** `OR`
  - **Descrição:** Combina múltiplas condições em uma cláusula `where`, retornando resultados que satisfaçam qualquer uma das condições.
  - **Exemplo:**
    ```ts
    const produtosBaratosOuEmEstoque = await prisma.produto.findMany({
      where: {
        OR: [
          { preco: { lt: 10 } },
          { estoque: { gt: 0 } }
        ]
      }
    });
    ```

### raw
- **Comando:** `raw`
  - **Descrição:** Executa comandos SQL brutos diretamente no banco de dados.
  - **Exemplo:**
    ```ts
    const resultados = await prisma.$queryRaw`SELECT * FROM Produto WHERE preco > 10`;
    ```

### set
- **Comando:** `set`
  - **Descrição:** Define o valor de uma relação, substituindo qualquer valor anterior.
  - **Exemplo:**
    ```ts
    const pedidoAtualizado = await prisma.pedido.update({
      where: { id: pedidoId },
      data: {
        cliente: {
          set: { id: novoClienteId }
        }
      }
    });
    ```

### skip
- **Comando:** `skip`
  - **Descrição:** Ignora um número específico de registros antes de começar a retornar os resultados.
  - **Exemplo:**
    ```ts
    const produtos = await prisma.produto.findMany({
      skip: 5,
      take: 10
    });
    ```

### startsWith
- **Comando:** `startsWith`
  - **Descrição:** Filtra resultados que começam com uma string específica.
  - **Exemplo:**
    ```ts
    const produtos = await prisma.produto.findMany({
      where: {
        nome: { startsWith: 'Início' }
      }
    });
    ```

### sum
- **Comando:** `sum`
  - **Descrição:** Retorna a soma de todos os valores em um campo numérico.
  - **Exemplo:**
    ```ts
    const somaPrecos = await prisma.produto.aggregate({
      _sum: {
        preco: true
      }
    });
    ```

### take
- **Comando:** `take`
  - **Descrição:** Limita o número de registros retornados por uma consulta.
  - **Exemplo:**
    ```ts
    const produtos = await prisma.produto.findMany({
      take: 10
    });
    ```

### transaction
- **Comando:** `transaction`
  - **Descrição:** Executa um conjunto de operações como uma transação.
  - **Exemplo:**
    ```ts
    const [pedido, produtoAtualizado] = await prisma.$transaction([
      prisma.pedido.create({ data: { /* dados do pedido */ } }),
      prisma.produto.update({ where: { id: produtoId }, data: { estoque: { decrement: 1 } } })
    ]);
    ```

### update
- **Comando:** `update`
  - **Descrição:** Modifica os dados existentes em uma tabela.
  - **Exemplo:**
    ```ts
    const produtoAtualizado = await prisma.produto.update({
      where: { id: produtoId },
      data: { preco: { increment: 5.0 } }
    });
    ```

### upsert
- **Comando:** `upsert`
  - **Descrição:** Insere um novo registro ou atualiza um registro existente se um conflito ocorrer.
  - **Exemplo:**
    ```ts
    const produto = await prisma.produto.upsert({
      where: { id: produtoId },
      update: { preco: { increment: 5.0 } },
      create: { nome: 'Novo Produto', preco: 20.0 }
    });
    ```

---



