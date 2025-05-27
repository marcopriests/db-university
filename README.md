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

---------------------------------------------------- QUERY 1 ----------------------------------------
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

5: 
SELECT * 
FROM `exams`
WHERE `hour` <= 14
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


-------------------------------------------- QUERY JOIN ----------------------------------------
1:
SELECT `students`.`id` AS 'studenti'
FROM `degrees`
INNER JOIN `students`
ON `degrees`.`id` = `students`.`degree_id`
WHERE `degrees`.`name` = 'Corso di Laurea in Economia'

2:
SELECT `degrees`.`id`, `degrees`.`name`
FROM `departments`
INNER JOIN `degrees`
ON `departments`.`id` = `degrees`.`department_id`
WHERE `degrees`.`level` = 'Magistrale'
AND `departments`.`name` = 'Dipartimento di Neuroscienze'

3:
SELECT `courses`.`id`, `courses`.`name`, `teachers`.`id` AS 'Fulvio_Amato_ID'
FROM `courses`
INNER JOIN `course_teacher` ON `course_teacher`.`course_id` = `courses`.`id`
INNER JOIN `teachers` ON `course_teacher`.`teacher_id` = `teachers`.`id`
WHERE `teachers`.`name` = 'Fulvio'
AND `teachers`.`surname` = 'Amato'

4:
SELECT `students`.`id` AS 'student_id',
`students`.`name`,
`students`.`surname`,
`degrees`.*,
`departments`.`name`
FROM `departments`
INNER JOIN `degrees` ON `departments`.`id` = `degrees`.`department_id`
INNER JOIN `students` ON `degrees`.`id` = `students`.`degree_id`
ORDER BY `students`.`surname` ASC

5:
SELECT `degrees`.`id` AS 'degree_id',
`degrees`.`name`,
`courses`.`id` AS 'course_id',
`courses`.`name`,
`courses`.`period`,
`courses`.`cfu`,
`teachers`.`id` AS 'teacher_id',
`teachers`.`name`,
`teachers`.`surname`
FROM `degrees`
INNER JOIN `courses` ON `degrees`.`id` = `courses`.`degree_id`
INNER JOIN `course_teacher` ON `course_teacher`.`course_id` = `courses`.`id`
INNER JOIN `teachers` ON `course_teacher`.`teacher_id` = `teachers`.`id`
ORDER BY `degrees`.`id` ASC

6:
SELECT `teachers`.`id`, `teachers`.`name`, `teachers`.`surname`
FROM `departments`
INNER JOIN `degrees` ON `departments`.`id` = `degrees`.`department_id`
INNER JOIN `courses` ON `degrees`.`id` = `courses`.`degree_id`
INNER JOIN `course_teacher` ON `courses`.`id` = `course_teacher`.`course_id`
INNER JOIN `teachers` ON `course_teacher`.`teacher_id` = `teachers`.`id`
WHERE `departments`.`name` = 'Dipartimento di Matematica'

7:


-------------------------------------------- QUERY GROUP BY ----------------------------------------
1:
SELECT COUNT(*) AS `numero_studenti`, YEAR(`enrolment_date`) AS `anno_iscrizione`
FROM `students`
GROUP BY `anno_iscrizione` 

2:
SELECT COUNT(*) AS `numero_insegnanti`, `office_address` AS `edificio`
FROM `teachers`
GROUP BY `edificio` 

3:

4:
