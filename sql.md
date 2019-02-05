# SQL
1. Получить все договоры, имеющие статус “VIP”: 

    `SELECT * FROM contracts WHERE is_vip = '1';`
2. Получить договоры, которые были созданы в период с 2015-03-05 до 2016-10-12:

    `SELECT * FROM contracts_addresses WHERE date_start > '2015-03-05' AND date_start < '2016-10-12';`
3. Получить договоры, которые были активны в период с 2014-03-05 до 2018-10-11 хотя бы один день: 

    `SELECT * FROM contracts_addresses WHERE ((date_start >= '2014-03-05' AND date_start <= '2018-10-11') 
    AND (date_end <= '2018-10-11' OR date_end is NULL)) AND CURDATE() - date_start > 1;`
4. Получить все договоры, у которых за все время был хотя бы один адрес подключения:

    `SELECT * FROM contracts_addresses WHERE address_id IS NOT NULL;`
5. Получить последний адрес подключения для каждого договора:

    `SELECT id, name FROM addresses WHERE id IN (SELECT address_id FROM contracts_addresses ca 
     WHERE NOT EXISTS (SELECT * FROM contracts_addresses cad WHERE cad.contract_id = ca.contract_id 
    AND cad.date_start > ca.date_start));`
6. Получить кол-во адресов подключения для каждого договора:

    `SELECT contract_id, COUNT(address_id) FROM contracts_addresses GROUP BY contract_id;`
