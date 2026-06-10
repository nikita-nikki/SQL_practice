DROP TABLE scores;

CREATE TABLE scores (
    student_id  INT PRIMARY KEY,
    name        VARCHAR(100),
    subject     VARCHAR(50),
    score       INT,
    exam_date   DATE,
    grade       VARCHAR(5)
);
 
INSERT INTO scores VALUES
(1,  'Amit',  'Maths',   92, '2026-01-15', 'A'),
(2,  'Sara',  'Maths',   85, '2026-01-15', 'B'),
(3,  'Ravi',  'Maths',   92, '2026-01-15', 'A'),
(4,  'Neha',  'Maths',   78, '2026-01-15', 'B'),
(5,  'Karan', 'Maths',   65, '2026-01-15', 'C'),
(6,  'Amit',  'Science', 88, '2026-02-10', 'A'),
(7,  'Sara',  'Science', 91, '2026-02-10', 'A'),
(8,  'Ravi',  'Science', 74, '2026-02-10', 'C'),
(9,  'Neha',  'Science', 88, '2026-02-10', 'A'),
(10, 'Karan', 'Science', 55, '2026-02-10', 'D'),
(11, 'Amit',  'English', 79, '2026-03-05', 'B'),
(12, 'Sara',  'English', 95, '2026-03-05', 'A'),
(13, 'Ravi',  'English', 82, '2026-03-05', 'B'),
(14, 'Neha',  'English', 79, '2026-03-05', 'B'),
(15, 'Karan', 'English', 88, '2026-03-05', 'A');


--RUNNING TOTAL
SELECT 
    *,
	SUM(score) OVER (PARTITION BY name ORDER BY exam_date ) AS total_score
FROM scores;





	