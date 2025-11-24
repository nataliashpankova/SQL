# SQL
Repository dedicata a esercizi, query e approfondimenti SQL per migliorare le competenze in gestione e interrogazione di database.
-----------------------------------------------------------------------------------------------------------------------------------

CREATE TABLE attore(
nome VARCHAR(50),
cognome VARCHAR(50) UNIQUE,
cod_attore INT PRIMARY KEY
);

CREATE TABLE film(
titolo VARCHAR(50),
annoProd DATE NOT NULL,
regista VARCHAR(20),
genere VARCHAR(20),
cod_film VARCHAR(3) PRIMARY KEY,
durata INT
);

CREATE TABLE recita(
cod_film VARCHAR(3),
cod_attore INT,
FOREIGN KEY (cod_film) REFERENCES film(cod_film),
FOREIGN KEY (cod_attore) REFERENCES attore(cod_attore)
);

CREATE TABLE cinema(
nome VARCHAR(20),
codiceFilm VARCHAR(3),
cod_cinema VARCHAR(3) PRIMARY KEY,
FOREIGN KEY (codiceFilm) REFERENCES film(cod_film)
);

INSERT INTO attore (nome, cognome, cod_attore) VALUES ('Tom', "Cruise", 123);
INSERT INTO attore (nome, cognome, cod_attore) VALUES ('Al', "Pacino", 852);
INSERT INTO attore (nome, cognome, cod_attore) VALUES ('Timothée', "Chalamet", 963);
INSERT INTO attore (nome, cognome, cod_attore) VALUES ('Robert', "Downey", 741);
INSERT INTO attore (nome, cognome, cod_attore) VALUES ('Tom', "Hanks", 554);


INSERT INTO film(titolo, annoProd, regista, genere, cod_film, durata) VALUES ("Aquaman", "2020-05-11", "Wan", "Fantasy", "zxc", 200);
INSERT INTO film(titolo, annoProd, regista, genere, cod_film, durata) VALUES ("Top Gun", "2022-07-13", "Kosinski", "Azione", "abc", 150);
INSERT INTO film(titolo, annoProd, regista, genere, cod_film, durata) VALUES ("Il Padrino", "1972-11-27", "Coppola", "Drammatico", "qwe", 170);

INSERT INTO cinema (nome, codiceFilm, cod_cinema) VALUES ("The Space", "abc", "A01");

INSERT INTO recita (cod_film, cod_attore) VALUES ("abc", 123);


--1-- Elenca i titoli dei film e i codici degli attori che vi hanno recitato.

SELECT film.titolo, cod_attore
FROM recita
INNER JOIN film USING (cod_film);

--2--Elenca tutti gli attori e i codici dei film a cui hanno partecipato.

SELECT attore.nome, attore.cognome, recita.cod_film
FROM attore
INNER JOIN recita USING (cod_attore);

--3--Elenca i titoli dei film di genere 'Commedia' insieme ai cinema che li proiettano.

SELECT titolo, cinema.cod_cinema
FROM film
INNER JOIN cinema ON film.cod_film = cinema.codiceFilm
WHERE genere = "Commedia";

--4--Elenca i registi e il numero di film che hanno diretto in ordine decrescente.

SELECT regista, count(*) AS numeroDiFilm
FROM film
GROUP BY regista
ORDER BY count(*) DESC;

--5--Elenca tutti i cinema e i titoli dei film proiettati.

SELECT nome, film.titolo
FROM cinema
INNER JOIN film ON film.cod_film = cinema.codiceFilm;

--6--Mostra i primi 3 film più lunghi insieme al cinema che li proietta.

SELECT titolo, cinema.nome
FROM film
LEFT JOIN cinema ON film.cod_film = cinema.codiceFilm
ORDER BY film.durata DESC
LIMIT 3;

--7--Elenca gli attori che hanno recitato in almeno 2 film.

SELECT cognome, COUNT(recita.cod_film)
FROM attore
INNER JOIN recita USING (cod_attore)
GROUP BY cognome
HAVING count(recita.cod_film) >= 2;

--8--Elenca i titoli dei film con una durata maggiore di 120 minuti, e il nome del cinema che li proietta.

SELECT titolo, durata, cinema.nome
FROM film
INNER JOIN cinema ON film.cod_film = cinema.codiceFilm
WHERE durata >= 120;

--9--Conta quanti attori hanno recitato in ciascun film.

SELECT film.titolo, count(cod_attore)
FROM recita
RIGHT JOIN film USING (cod_film)
GROUP BY cod_film;

--10--Mostra il film più recente per ciascun regista.

SELECT regista, MAX(annoProd)
FROM film
GROUP BY regista;

--11--Elenca il nome del cinema e il genere del film proiettato.

SELECT nome, film.genere
FROM cinema
LEFT JOIN film ON cinema.codiceFilm = film.cod_film;

--12--Elenca i titoli dei film che sono stati proiettati in almeno un cinema oppure in cui ha recitato almeno un attore. Ogni titolo deve comparire una sola volta, anche se soddisfa entrambe le condizioni.

SELECT titolo
FROM film 
INNER JOIN cinema ON film.cod_film = cinema.codiceFilm

UNION

SELECT titolo
FROM film 
INNER JOIN recita USING (cod_film);

