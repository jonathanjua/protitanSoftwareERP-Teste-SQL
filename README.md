# Teste de SQL - protitanSoftwareERP

## 1. Inserir o registro na tabela de produtos
```sql
INSERT INTO produtos (cod_prod, loj_prod, desc_prod, dt_inclu_prod, preco_prod)
VALUES (170, 2, 'LEITE CONDENSADO MOCOCA', '2010-12-30', 45.40);
```

## 2. Alterar o preço do produto para R$95,40
```sql
UPDATE produtos
SET preco_prod = 95.40
WHERE cod_prod = 170 AND loj_prod = 2;
```

## 3. Selecionar todos os registros das lojas 1 e 2
```sql
SELECT *
FROM produtos
WHERE loj_prod IN (1, 2);
```

## 4. Selecionar a maior e a menor data de inclusão
```sql
SELECT 
    MIN(dt_inclu_prod) AS menor_data_inclusao,
    MAX(dt_inclu_prod) AS maior_data_inclusao
FROM produtos;
```

## 5. Quantidade total de registros na tabela
```sql
SELECT COUNT(*) AS total_registros
FROM produtos;
```

## 6. Selecionar todos os produtos que começam com a letra "L"
```sql
SELECT *
FROM produtos
WHERE desc_prod LIKE 'L%';
```
## 7. Soma dos preços totalizados por loja
```sql
SELECT 
    loj_prod,
    SUM(preco_prod) AS soma_precos
FROM produtos
GROUP BY loj_prod;
```

## 8. Soma dos preços totalizados por loja que seja maior que R$100.000
```sql
SELECT 
    loj_prod,
    SUM(preco_prod) AS soma_precos
FROM produtos
GROUP BY loj_prod
HAVING SUM(preco_prod) > 100000;
```

## 9. Selecionar dados combinados entre a tabela
```sql
SELECT 
    l.loj_prod, 
    l.desc_loj, 
    p.cod_prod, 
    p.desc_prod, 
    p.preco_prod, 
    e.qtd_prod
FROM produtos p
JOIN estoque e ON p.cod_prod = e.cod_prod AND p.loj_prod = e.loj_prod
JOIN lojas l ON e.loj_prod = l.loj_prod
WHERE e.loj_prod = 1;
```
## 10. Produtos na tabela produtos que não existem na tabela estoque
```sql
SELECT p.cod_prod, p.desc_prod
FROM produtos p
LEFT JOIN estoque e ON p.cod_prod = e.cod_prod AND p.loj_prod = e.loj_prod
WHERE e.cod_prod IS NULL;
```

## 11. Produtos na tabela estoque que não existem na tabela produtos
```sql
SELECT e.cod_prod, e.loj_prod
FROM estoque e
LEFT JOIN produtos p ON e.cod_prod = p.cod_prod AND e.loj_prod = p.loj_prod
WHERE p.cod_prod IS NULL;
```
