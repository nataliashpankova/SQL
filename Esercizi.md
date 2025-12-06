---------------------------------ESERCIZIO 1

CREATE DATABASED IF NOT EXISTS telegram;

CREATE TABLE users (
  id INT UNSIGNED NOT NULL AUTO_INCREMENT, --Pk
  nome VARCHAR(45),
  cognome VARCHAR(45),
  email VARCHAR(100),
  eta INT
);

INSERT INTO users (id, nome, cognome, email, eta)
VALUES (1, Natalia, Shpankova, nat@gmail.com, 27);

INSERT INTO users (id, nome, cognome, email, eta)
VALUES (2, Maria, Sole, mar@gmail.com, 18);

INSERT INTO users (id, nome, cognome, email, eta)
VALUES (3, Valentina, Nuvola, val@gmail.com, 30);


CREATE TABLE messages (
  id_send INT UNSIGNED NOT NULL,
  id_receive INT UNSIGNED NOT NULL,
  tempo DATETIME,
  body TEXT,
  
  FOREIGN KEY id_send REFERENCES users(id),
  FOREIGN KEY id_receive REFERENCES users(id),
);


-------------------------------ESERCIZIO 2

CREATE TABLE impiegato (
  id_impiegato SERIAL, --INT UNSIGNED NOT NULL AUTO_INCRIMENT,
  nome VARCHAR(20),
  titolo VARCHAR(15),
  eta Char(3),
  salario BIGINT unsigned,
  dipartimento Varchar(10)
);


CREATE TABLE acquisto (
  id_acquisto INT UNSIGNED NOT NULL,
  id_impiegato INT UNSIGNED NOT NULL,
  id_cliente INT UNSIGNED NOT NULL,
  dataDiOrdinazione DATETIME DEFAULT NOW(),
  item TEXT,
  quantita INT,
  prezo BIGINT,
  
  FOREIGN KEY (id_acquisto) REFERENCES (),
  FOREIGN KEY id_impiegato() REFERENCES impiegato(id_impiegato),
  FOREIGN KEY (id_cliente) REFERENCES cliente (id)
);


CREATE TABLE cliente (
  id INT UNSIGNED NOT NULL AUTO_INCRIMENT,
  nome VARCHAR(20),
  cognome VARCHAR(20),
  citta VARCHAR(20),
  stato ENUM ('ORDER', 'DELIVERY', 'DONE')
);

--1--------------------------------------------
SELECT nome, eta, salario
FROM impiegato
WHERE eta > 50;
--2--------------------------------------------
SELECT *
FROM acquisto
WHERE item IN "Tenda";
--3--------------------------------------------
SELECT item, prezzo, id_cliente
FROM acquisto
WHERE id = 10449;
--4--------------------------------------------
SELECT nome, titolo, dipartimento
FROM impiegati
WHERE title LIKE "Ing%";
--5--------------------------------------------
SELECT nome, titolo, salario
FROM impiegato
WHERE title IN "programmatore" and salario >= 50000;
--6--------------------------------------------
SELECT nome, salario
FROM impiegato
WHERE dipartimento IN ("Vendite", "Programmazione");
--7--------------------------------------------
SELECT distinct(eta)
FROM impiegato;
--8--------------------------------------------
SELECT avg(salario)
FROM impiegato;
--9--------------------------------------------
SELECT *
FROM impiegato
WHERE dipartimento = "Vendite"
ORDER BY salario;
--10--------------------------------------------
SELECT *
FROM impiegato
WHERE dipartimento = "Vendite"
ORDER BY salario ASC, eta DESC;
--11--------------------------------------------
SELECT *
FROM impiegato
WHERE nome IN ("Hernandez", "Jones", "Roberts", "Ruiz");
--12--------------------------------------------
SELECT *
FROM impiegato
WHERE eta BETWEEN 30 and 40;

