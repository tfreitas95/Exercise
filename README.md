1)

A) Pesquise os itens que foram vendidos sem desconto. As colunas presentes no 
resultado da consulta são: ID_NF, ID_ITEM, COD_PROD E VALOR_UNIT.

select
id_nf,
id_item,
cod_prod,
valor_unit

from `q.id`

where desconto is null

-------------------------------------------------------------------------------------------------------
B) Pesquise os itens que foram vendidos com desconto. As colunas presentes no 
resultado da consulta são: ID_NF, ID_ITEM, COD_PROD, VALOR_UNIT E O VALOR 
VENDIDO. OBS: O valor vendido é igual ao VALOR_UNIT -
(VALOR_UNIT*(DESCONTO/100)).

select 
id_nf,
id_item,
cod_prod,
valor_unit,
valor_vendido

 from (
select
id_nf,
id_item,
cod_prod,
valor_unit,
valor_unit - (valor_unit*(desconto/100)) as valor_vendido

from q.id

where desconto is not null

)

------------------------------------------------------------------------------------------------------
C) Altere o valor do desconto (para zero) de todos os registros onde este campo é nulo.

select 
id_nf,
id_item,
cod_prod,
valor_unit,
ifnull (desconto, 0)

from q.id
------------------------------------------------------------------------------------------------------
D) Pesquise os itens que foram vendidos. As colunas presentes no resultado da consulta 
são: ID_NF, ID_ITEM, COD_PROD, VALOR_UNIT, VALOR_TOTAL, DESCONTO, 
VALOR_VENDIDO. OBS: O VALOR_TOTAL é obtido pela fórmula: QUANTIDADE * 
VALOR_UNIT. O VALOR_VENDIDO é igual a VALOR_UNIT -
(VALOR_UNIT*(DESCONTO/100)).

select 
id_nf,
id_item,
cod_prod,
valor_unit,
quantidade*valor_unit as valor_total,
desconto,
valor_unit - (valor_unit*((ifnull (desconto, 0))/100)) as valor_vendido

from q.id
------------------------------------------------------------------------------------------------------
E) Pesquise o valor total das NF e ordene o resultado do maior valor para o menor. As 
colunas presentes no resultado da consulta são: ID_NF, VALOR_TOTAL. OBS: O 
VALOR_TOTAL é obtido pela fórmula: ∑ QUANTIDADE * VALOR_UNIT. Agrupe o 
resultado da consulta por ID_NF.
select 
count(id_nf),
sum(quantidade*valor_unit) as valor_total 

from q.id
--------------------------------------------------------------------------------------------------------
F) Pesquise o valor vendido das NF e ordene o resultado do maior valor para o menor. As 
colunas presentes no resultado da consulta são: ID_NF, VALOR_VENDIDO. OBS: O 
VALOR_TOTAL é obtido pela fórmula: ∑ QUANTIDADE * VALOR_UNIT. O 
VALOR_VENDIDO é igual a ∑ VALOR_UNIT - (VALOR_UNIT*(DESCONTO/100)). Agrupe 
o resultado da consulta por ID_NF
select 
id_nf,
valor_unit - (valor_unit*((ifnull (desconto, 0))/100)) as valor_vendido

from q.id
order by (id_nf)
---------------------------------------------------------------------------------------------------------
G) Consulte o produto que mais vendeu no geral. As colunas presentes no resultado da 
consulta são: COD_PROD, QUANTIDADE. Agrupe o resultado da consulta por 
COD_PROD.
select 
cod_prod,
sum(quantidade) as qtd

from q.id
group by (cod_prod) 
---------------------------------------------------------------------------------------------------------
H) Consulte as NF que foram vendidas mais de 10 unidades de pelo menos um produto. 
As colunas presentes no resultado da consulta são: ID_NF, COD_PROD, QUANTIDADE.
Agrupe o resultado da consulta por ID_NF, COD_PROD.
select
id_nf,
sum(quantidade) qtd,
sum(cod_prod) codigo_produto

from q.id

where quantidade > 9
group by (id_nf)
--------------------------------------------------------------------------------------------------------
I) Pesquise o valor total das NF, onde esse valor seja maior que 500, e ordene o 
resultado do maior valor para o menor. As colunas presentes no resultado da consulta 
são: ID_NF, VALOR_TOT. OBS: O VALOR_TOTAL é obtido pela fórmula: ∑ QUANTIDADE 
* VALOR_UNIT. Agrupe o resultado da consulta por ID_NF.
select
id_nf,
quantidade*valor_unit as valor_total 

from q.id

where quantidade*valor_unit > 500
order by quantidade*valor_unit desc
--------------------------------------------------------------------------------------------------------
J) Qual o valor médio dos descontos dados por produto. As colunas presentes no 
resultado da consulta são: COD_PROD, MEDIA. Agrupe o resultado da consulta por 
COD_PROD.
select
cod_prod,
avg(desconto) as desco

from q.id

group by cod_prod
-------------------------------------------------------------------------------------------------------
K) Qual o menor, maior e o valor médio dos descontos dados por produto. As colunas 
presentes no resultado da consulta são: COD_PROD, MENOR, MAIOR, MEDIA. Agrupe 
o resultado da consulta por COD_PROD.
select
cod_prod,
avg(desconto) as descomedio,
min(desconto) as minimo,
max(desconto) as maximo

from q.id

group by cod_prod 
-------------------------------------------------------------------------------------------------------
L) Quais as NF que possuem mais de 3 itens vendidos. As colunas presentes no resultado 
da consulta são: ID_NF, QTD_ITENS. OBS:: NÃO ESTÁ RELACIONADO A QUANTIDADE 
VENDIDA DO ITEM E SIM A QUANTIDADE DE ITENS POR NOTA FISCAL. Agrupe o 
resultado da consulta por ID_NF
select
id_nf,
sum(quantidade) as qtd

from q.id

where quantidade >=3

group by id_nf
-------------------------------------------------------------------------------------------------------
-------------------------------------------------------------------------------------------------------
2)


















