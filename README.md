Esercizio di oggi: Db University
nome repo: db-universityModellizzare la struttura di un database per memorizzare tutti i dati riguardanti una università:

    sono presenti diversi Dipartimenti (es.: Lettere e Filosofia, Matematica, Ingegneria ecc.);
    ogni Dipartimento offre più Corsi di Laurea (es.: Civiltà e Letterature Classiche, Informatica, Ingegneria Elettronica ecc..)
    ogni Corso di Laurea prevede diversi Corsi (es.: Letteratura Latina, Sistemi Operativi 1, Analisi Matematica 2 ecc.);
    ogni Corso può essere tenuto da diversi Insegnanti;
    ogni Corso prevede più appelli d'Esame;
    ogni Studente è iscritto ad un solo Corso di Laurea;
    ogni Studente può iscriversi a più appelli di Esame;
    per ogni appello d'Esame a cui lo Studente ha partecipato, è necessario memorizzare il voto ottenuto, anche se non sufficiente. Pensiamo a quali entità (tabelle) creare per il nostro database e cerchiamo poi di stabilirne le relazioni. Infine, andiamo a definire le colonne e i tipi di dato di ogni tabella.

Utilizzare https://www.drawio.com/ per la creazione dello schema. Esportare quindi il diagramma in jpg e caricarlo nella repo.

---------------------------------------------------- QUERY ----------------------------------------
1: 
SELECT *
FROM `students`
WHERE YEAR(`date_of_birth`) = '1990'

2:
SELECT *
FROM `courses`
WHERE `cfu` > '10'

3:
SELECT *
FROM `students`
WHERE year(`date_of_birth`) > '1995'

4:
SELECT * 
FROM `courses`
WHERE `period` = 'I semestre'
AND `year` = '1'

5: (non torna)
SELECT * 
FROM `exams`
WHERE `hour` LIKE '14%'
AND `date` = '2020-06-20'

6:
SELECT * 
FROM `degrees`
WHERE `level` = 'magistrale'

7:
SELECT COUNT(`id`)
FROM `departments`

8:
SELECT COUNT(`id`)
FROM `teachers`
WHERE `phone` IS NULL