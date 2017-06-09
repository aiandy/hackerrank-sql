#Amber's conglomerate corporation just acquired some new companies. Each of the companies follows this hierarchy:
SELECT c.company_code
    ,c.founder
    ,count(DISTINCT(e.lead_manager_code)) 
    ,count(DISTINCT(e.senior_manager_code))
    ,count(DISTINCT(e.manager_code))
    ,count(DISTINCT(e.employee_code))
    FROM Company AS c Inner JOIN  Employee AS e 
    ON c.company_code=e.company_code
GROUP BY c.company_code,c.founder
ORDER BY c.company_code;

#You are given a table, BST, containing two columns: N and P, where N represents the value of a node in Binary Tree, 
#and P is the parent of N.
select N, 
    case 
    when P is NULL then 'Root'
    when N in (select P from BST) then 'Inner' 
    else 'Leaf' end 
from BST 
order by N;


SELECT N,
    CASE
    WHEN P IS NULL THEN 'Root'
    WHEN (
    SELECT N FROM BST 
    WHEN count(p)>0
    ) THEN 'Inner'
    ELSE 'Leaf'
    END
    FROM BST
ORDER BY N;

#You are given two tables: Students and Grades. Students contains three columns ID, Name and Marks.
SELECT 
    CASE WHEN grade<8 THEN 'NULL'
         ELSE s.name END,g.Grade,s.Marks
FROM Students s INNER JOIN Grades g ON 1=1
where s.marks>=g.min_mark and s.marks<=g.max_mark 
ORDER BY g.grade desc,name;

#Julia just finished conducting a coding contest, and she needs your help assembling the leaderboard! 
#Write a query to print the respective hacker_id and name of hackers who achieved full scores for more than one challenge. 
#Order your output in descending order by the total number of challenges in which the hacker earned a full score. If more than one hacker received full scores in same number of challenges, then sort them by ascending hacker_id.
SELECT  s.hacker_id,h.name as col2   
    FROM Submissions s INNER JOIN Challenges c
    ON s.challenge_id=c.challenge_id
    INNER JOIN Difficulty d 
    ON d.difficulty_level=c.difficulty_level
    INNER JOIN Hackers h
    ON h.hacker_id=s.hacker_id
WHERE s.score=d.score 
GROUP BY s.hacker_id,h.name
HAVING count(h.name)>1
ORDER BY count(h.name) DESC,s.hacker_id ASC;

