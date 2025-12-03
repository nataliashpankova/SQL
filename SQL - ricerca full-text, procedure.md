Utilizzando la ricerca full-text, restituisci tutti i record della tabella dei canali che contengono la parola ' sql ' nel campo del titolo ma non ' server '.
Ordina la selezione in base al campo del titolo .

SELECT id, title
FROM channels
WHERE match(title) AGAINST('+sql -server' IN BOOLEAN MODE)
ORDER BY title;


# cancellare la procedura con controllo di esistenza 
DROP PROCEDURE IF EXISTS my_procedure;

# impostare nuovo delimiter
DELIMITER //
	
# creare la procedura propria
CREATE PROCEDURE my_procedure()
BEGIN
	SELECT 456;
	SELECT 456;
	SELECT 456;
END//

# impostare delimiter al suo standard
DELIMITER ;	
	
# chiamare la procedura
CALL my_procedure();

##########################################################################

# процедура, возвращающая указанное число случайных групп или каналов
DROP PROCEDURE IF EXISTS telegram.random_society;

DELIMITER $$
$$
CREATE PROCEDURE telegram.random_society(cnt int)
BEGIN
	SELECT id, title , invite_link , 'channel' AS community_type
	FROM channels 
		UNION 
	SELECT id, title , invite_link , 'group' AS community_type
	FROM `groups`  
	ORDER BY rand()
	LIMIT cnt;
END $$
DELIMITER ;


# chiamare la procedura 
CALL random_society(3);
