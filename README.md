<h1>SQL Practice Queries with Examples</h1>

<h2>1️⃣ LIKE</h2>

<h3>Query 1: Find all students whose names start with 'A'</h3>
<pre><code>SELECT Student_Name
FROM Students
WHERE Student_Name LIKE 'A%';
</code></pre>

<p><strong>Example result:</strong></p>
<pre><code>Alice
</code></pre>

<h3>Query 2: Find all courses whose name contains 'Data'</h3>
<pre><code>SELECT Course_Name
FROM Courses
WHERE Course_Name LIKE '%Data%';
</code></pre>

<p><strong>Example result:</strong></p>
<pre><code>Data Structures
Database Management
</code></pre>

<hr>

<h2>2️⃣ LIMIT</h2>

<h3>Query 3: Display the first 3 students ordered by CGPA descending</h3>
<pre><code>SELECT Student_Name, CGPA
FROM Students
ORDER BY CGPA DESC
LIMIT 3;
</code></pre>

<p><strong>Example result:</strong></p>
<pre><code>Charlie   3.90
Alice     3.75
Eva       3.45
</code></pre>

<h3>Query 4: Show the first 2 teachers with the highest salary</h3>
<pre><code>SELECT Teacher_Name, Salary
FROM Teachers
ORDER BY Salary DESC
LIMIT 2;
</code></pre>

<p><strong>Example result:</strong></p>
<pre><code>Dr. Ahmed   120000
Dr. Anika   110000
</code></pre>

<hr>

<h2>3️⃣ DISTINCT</h2>

<h3>Query 5: List all distinct semesters in which students are enrolled</h3>
<pre><code>SELECT DISTINCT Semester
FROM Students;
</code></pre>

<p><strong>Example result:</strong></p>
<pre><code>Spring
Summer
Fall
</code></pre>

<h3>Query 6: List all distinct departments in the Courses table</h3>
<pre><code>SELECT DISTINCT Department_ID
FROM Courses;
</code></pre>

<p><strong>Example result:</strong></p>
<pre><code>101
102
103
</code></pre>

<hr>

<h2>4️⃣ BETWEEN</h2>

<h3>Query 7: Find all students whose CGPA is between 3.50 and 3.80</h3>
<pre><code>SELECT Student_Name, CGPA
FROM Students
WHERE CGPA BETWEEN 3.50 AND 3.80;
</code></pre>

<p><strong>Example result:</strong></p>
<pre><code>Alice   3.75
Bob     3.50
</code></pre>

<h3>Query 8: Find all teachers whose salary is between 90000 and 120000</h3>
<pre><code>SELECT Teacher_Name, Salary
FROM Teachers
WHERE Salary BETWEEN 90000 AND 120000;
</code></pre>

<p><strong>Example result:</strong></p>
<pre><code>Dr. Ahmed   120000
Dr. Karim   100000
Dr. Anika   110000
</code></pre>

<hr>

<h2>5️⃣ IN</h2>

<h3>Query 9: List all students who belong to Department 101 or 103</h3>
<pre><code>SELECT Student_Name
FROM Students
WHERE Department_ID IN (101, 103);
</code></pre>

<p><strong>Example result:</strong></p>
<pre><code>Alice
Charlie
Eva
David
</code></pre>

<h3>Query 10: Show all courses taught by Teacher_ID 201 or 202</h3>
<pre><code>SELECT Course_Name
FROM Courses
WHERE Teacher_ID IN (201, 202);
</code></pre>

<p><strong>Example result:</strong></p>
<pre><code>Introduction to Programming
Data Structures
Database Management
</code></pre>

<hr>

<h2>6️⃣ NOT IN</h2>

<h3>Query 11: Find all students not enrolled in course 'CSE101'</h3>
<pre><code>SELECT Student_Name
FROM Students
WHERE Student_ID NOT IN (
    SELECT Student_ID
    FROM Course_Enrollments
    WHERE Course_ID = 'CSE101'
);
</code></pre>

<p><strong>Example result:</strong></p>
<pre><code>Bob
Charlie
David
Eva
</code></pre>

<h3>Query 12: List all courses not belonging to Department 101</h3>
<pre><code>SELECT Course_Name
FROM Courses
WHERE Department_ID NOT IN (101);
</code></pre>

<p><strong>Example result:</strong></p>
<pre><code>ENG101
MAT101
</code></pre>

<hr>

<h2>7️⃣ ORDER BY</h2>

<h3>Query 13: List all courses ordered by Credit ascending and then by Course_Name ascending</h3>
<pre><code>SELECT Course_Name, Credit
FROM Courses
ORDER BY Credit ASC, Course_Name ASC;
</code></pre>

<p><strong>Example result:</strong></p>
<pre><code>ENG101   2
CSE101   3
CSE102   3
CSE103   3
MAT101   3
</code></pre>

<h3>Query 14: Display all students ordered by CGPA descending</h3>
<pre><code>SELECT Student_Name, CGPA
FROM Students
ORDER BY CGPA DESC;
</code></pre>

<p><strong>Example result:</strong></p>
<pre><code>Charlie   3.90
Alice     3.75
Eva       3.45
Bob       3.50
David     3.10
</code></pre>

<hr>

<h2>8️⃣ HAVING</h2>

<h3>Query 15: Find departments that have more than 1 course offered</h3>
<pre><code>SELECT Department_ID, COUNT(*) AS Course_Count
FROM Courses
GROUP BY Department_ID
HAVING COUNT(*) > 1;
</code></pre>

<p><strong>Example result:</strong></p>
<pre><code>Department_ID   Course_Count
101             3
</code></pre>

<h3>Query 16: Show teachers with a salary greater than 90000 in each department</h3>
<pre><code>SELECT Department_ID, COUNT(*) AS high_salary_teachers
FROM Teachers
WHERE Salary > 90000
GROUP BY Department_ID
HAVING COUNT(*) > 0;
</code></pre>

<p><strong>Example result:</strong></p>
<pre><code>Department_ID   high_salary_teachers
101             2
103             1
</code></pre>


1. List all courses offered by departments with a budget over $500,000.

Logic: Identify department IDs with a budget greater than $500,000, and then list the courses belonging to those departments.

SELECT Course_Name
FROM Courses
WHERE Department_ID IN (
    SELECT Department_ID
    FROM Departments
    WHERE Budget > 500000
);


2. Find the students with a CGPA higher than the average CGPA of all students.

Logic: Calculate the average CGPA of all students and select those whose individual CGPA is higher.

SELECT Student_Name, CGPA
FROM Students
WHERE CGPA > (SELECT AVG(CGPA) FROM Students);


3. Find the teacher(s) with the highest salary.

Logic: Find the maximum salary among all teachers, and select the teacher(s) who match that salary.

SELECT Teacher_Name, Salary
FROM Teachers
WHERE Salary = (SELECT MAX(Salary) FROM Teachers);


4. List all departments with more than the average number of faculty members.

Logic: Calculate the average number of faculty members across all departments and list the departments exceeding that average.

SELECT Department_Name, Faculty_Count
FROM Departments
WHERE Faculty_Count > (SELECT AVG(Faculty_Count) FROM Departments);


5. Find the courses in which students scored a grade of "A".

Logic: Identify the Course_IDs from the enrollments table where the grade is 'A', and then retrieve the names of those courses.

SELECT Course_Name
FROM Courses
WHERE Course_ID IN (
    SELECT Course_ID
    FROM Course_Enrollments
    WHERE Grade = 'A'
);


6. Find the names of professors earning above the average salary of all teachers.

Logic: Calculate the overall average salary and retrieve the names and salaries of teachers whose salary is greater than the average.

SELECT Teacher_Name, Salary
FROM Teachers
WHERE Salary > (SELECT AVG(Salary) FROM Teachers);


7. List all students not enrolled in any course.

Logic: Select students whose Student_ID is not present in the Course_Enrollments table.

SELECT Student_Name
FROM Students
WHERE Student_ID NOT IN (SELECT Student_ID FROM Course_Enrollments);


8. Find the departments offering more than 2 courses.

Logic: Use a subquery with GROUP BY and HAVING to count courses per department and filter those with a count greater than 2.

SELECT Department_Name
FROM Departments
WHERE Department_ID IN (
    SELECT Department_ID
    FROM Courses
    GROUP BY Department_ID
    HAVING COUNT(Course_ID) > 2
);


