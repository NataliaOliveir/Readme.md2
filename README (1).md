
# Resumo dos Seminários de SQL


Os seminários têm como objetivo educar e capacitar profissionais e estudantes na linguagem SQL, promovendo o entendimento sobre o gerenciamento de bancos de dados. Eles são importantes para compartilhar conhecimentos atualizados, melhorar habilidades práticas, facilitar o networking e contribuir para o avanço na carreira dos participantes.
 
# GRUPO 1:  Operadores de Agregação 
 Funções de agregação são ferramentas em bancos de dados que resumem e calculam informações de conjuntos de dados, operando em grupos de linhas e retornando um único valor, facilitando análises estatísticas.

    Exemplo
    SELECT departamento, COUNT(*) as total_funcionarios
    FROM funcionarios
    GROUP BY departamento;
# GRUPO 2: Joins em SQL 
 joins são operadores que combinam dados de duas ou mais tabelas com base em uma condição comum. Geralmente envolvendo chaves primárias e chaves estrangeiras. eles permitem que você consulte dados relacionados que estão distribuídos em diferentes tabelas 


***INNER JOIN:*** Retorna registros que têm correspondência em ambas as tabelas.

***LEFT JOIN:*** Retorna todos os registros da tabela à esquerda e os correspondentes da tabela à direita.

***RIGHT JOIN:*** Retorna todos os registros da tabela à direita e os correspondentes da tabela à esquerda.

***FULL JOIN:*** Retorna registros quando há correspondência em uma das tabelas.


      SELECT a.nome, b.nome_departamento
      FROM funcionarios a
      INNER JOIN departamentos b ON a.id_departamento = b.id;

# GRUPO 3: Operadores Lógicos

Operadores lógicos conectam expressões condicionais, formando condições compostas que são avaliadas como verdadeiras ou falsas. Em SQL, os principais operadores incluem: 

***CAND:*** Retorna verdadeiro se todas as condições forem verdadeiras. 
    
    SELECT * FROM funcionarios
    WHERE salario > 5000 AND departamento = 'TI';

***OR:*** Retorna verdadeiro se pelo menos uma das condições for verdadeira. 

    SELECT * FROM funcionarios
    WHERE departamento = 'TI' OR departamento = 'RH';


***NOT:*** Inverte o valor de verdade de uma condição. 

     SELECT * FROM funcionarios
     WHERE NOT departamento = 'Financeiro';


***IN:*** Verifica se um valor está presente em uma lista de valores. 
     
     SELECT * FROM funcionarios
     WHERE departamento IN ('TI', 'RH', 'Marketing');


***NOT IN:*** Verifica se um valor não está na lista de valores. 
     
     SELECT * FROM funcionarios
     WHERE departamento NOT IN ('Financeiro', 'Vendas');


***BETWEEN:*** Filtra resultados dentro de um intervalo específico, inclusivo. 

     SELECT * FROM funcionarios
    WHERE salario BETWEEN 3000 AND 7000;



***LIKE:*** Busca um padrão em uma coluna de texto.

     SELECT * FROM funcionarios
     WHERE nome LIKE 'A%';



***IS NULL:*** Verifica se um valor em uma coluna é nulo.  
    
    SELECT * FROM funcionarios
     WHERE data_demissao IS NULL;



# GRUPO 4: Subconsultas 

Subconsultas são consultas SQL dentro de outra consulta principal, com o objetivo de permitir a recuperação de dados mais específica, filtrada ou agregada. 

***Filtragem de Dados:*** Quando você precisa filtrar resultados com base em um conjunto de dados que não pode ser facilmente alcançado em uma única consulta.  

***Cálculos Agregados:*** Quando você precisa realizar cálculos que dependem de agregações de dados em outras tabelas. 

***Verificações de Existência:*** Quando você precisa verificar se um registro existe em outra tabela.  

***Atualizações Condicionais:*** Quando você deseja atualizar registros com base em condições que envolvem dados de outras tabelas. 

### Vantagens:
Maior clareza em consultas 

Complexas; Elimina a necessidade de tabelas temporárias; Flexibilidade na manipulação 

de dados. 

Desvantagens: Subconsultas correlacionadas podem ser mais lentas, pois são avaliadas para cada linha da consulta externa; Em consultas muito grandes, podem afetar o desempenho. 
    
     SELECT nome FROM funcionarios
     WHERE salario > (SELECT AVG(salario) FROM funcionarios);


 

# GRUPO 5: Funções de Agregação com GROUP BY 

Funções de agregação são ferramentas em bancos de dados que resumem e calculam informações de conjuntos de dados. A cláusula GROUP BY é essencial no SQL, pois agrupa linhas de uma tabela com base em valores comuns, permitindo cálculos e análises detalhadas.  

### A cláusula GROUP BY funciona da seguinte forma: 

***Especificação dos grupos:*** Indica as colunas para formar os grupos.  

***Aplicação de funções de agregação:*** As funções de agregação são aplicadas a cada grupo, gerando um valor único para cada um. 

***Combinação com outras cláusulas:*** Pode ser usada com WHERE e HAVING para filtrar dados e grupos. 

### POR QUE COMBINAR GROUP BY E HAVING? 
Permite filtrar os grupos resultantes da agregação com base em condições específicas. Permite realizar análises mais profundas, focando em grupos que atendem a critérios específicos. Permite criar relatórios personalizados, exibindo apenas os dados mais relevantes. 

      SELECT departamento, COUNT(*) as total_funcionarios
     FROM funcionarios
     GROUP BY departamento;


# GRUPO 6: Indexação e Performance

Um índice é uma estrutura auxiliar que melhora a velocidade de recuperação de registros em tabelas, sendo crucial em sistemas com grandes volumes de dados, como e-commerce e bancos de dados financeiros. 

### Estruturas de índice: 

***Árvores B e B+:*** Organizacionais balanceadas que permitem buscas eficientes; na B+, os valores estão nas folhas e os nós internos contêm apenas chaves. 

***Hashing:*** Mapeia valores para posições específicas, permitindo buscas rápidas, mas não é bom para consultas de intervalo. 

### Tipos de índices: 

***Índice Único:*** Garante a unicidade de valores. 

***Índice Composto:*** Ideal para consultas envolvendo várias colunas. 

***Índice Bitmap:*** Eficaz para colunas com poucos valores, mas caro em atualizações. 

***Full-Text Index:*** Otimiza buscas de texto completo. 

### Vantagens e desvantagens: 

Índices reduzem o tempo de consulta, evitam varreduras completas e melhoram a performance de operações de JOIN e ordenações. No entanto, consomem espaço, podem se fragmentar e lentificar operações de escrita, pois precisam ser atualizados com modificações nos dados. 

### Boas práticas: 

Focar em colunas frequentemente usadas em consultas e monitorar o uso de índices com ferramentas como EXPLAIN. Evitar a criação excessiva de índices é essencial para não prejudicar a performance em sistemas com alta carga de inserções e atualizações. 

 

# Grupo 7: Transações e Controle de Confiabilidade 

Uma transação em um banco de dados é um conjunto de operações que executam como uma unidade única. Para garantir integridade e consistência, elas devem seguir os princípios ACID: Atomicidade, Consistência, Isolamento e Durabilidade. 

A transação é iniciada com um comando específico que varia conforme o sistema de gerenciamento de banco de dados (SGBD), geralmente envolvendo uma instrução que sinaliza seu início. 

Durante a transação, uma ou mais operações, como inserções, atualizações ou exclusões, são realizadas em um contexto que permite a manipulação dos dados, mas sem aplicação permanente ainda. 

 

 

 
    