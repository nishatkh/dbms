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


<h2>SQL Subquery Practice Questions</h2>

<h3>1. List all courses offered by departments with a budget over $500,000.</h3>
<p><strong>Logic:</strong> Identify department IDs with a budget greater than $500,000, and then list the courses belonging to those departments.</p>
<pre><code>SELECT Course_Name
FROM Courses
WHERE Department_ID IN (
    SELECT Department_ID
    FROM Departments
    WHERE Budget > 500000
);
</code></pre>

<h3>2. Find the students with a CGPA higher than the average CGPA of all students.</h3>
<p><strong>Logic:</strong> Calculate the average CGPA of all students and select those whose individual CGPA is higher.</p>
<pre><code>SELECT Student_Name, CGPA
FROM Students
WHERE CGPA > (SELECT AVG(CGPA) FROM Students);
</code></pre>

<h3>3. Find the teacher(s) with the highest salary.</h3>
<p><strong>Logic:</strong> Find the maximum salary among all teachers, and select the teacher(s) who match that salary.</p>
<pre><code>SELECT Teacher_Name, Salary
FROM Teachers
WHERE Salary = (SELECT MAX(Salary) FROM Teachers);
</code></pre>

<h3>4. List all departments with more than the average number of faculty members.</h3>
<p><strong>Logic:</strong> Calculate the average number of faculty members across all departments and list the departments exceeding that average.</p>
<pre><code>SELECT Department_Name, Faculty_Count
FROM Departments
WHERE Faculty_Count > (SELECT AVG(Faculty_Count) FROM Departments);
</code></pre>

<h3>5. Find the courses in which students scored a grade of "A".</h3>
<p><strong>Logic:</strong> Identify the Course_IDs from the enrollments table where the grade is 'A', and then retrieve the names of those courses.</p>
<pre><code>SELECT Course_Name
FROM Courses
WHERE Course_ID IN (
    SELECT Course_ID
    FROM Course_Enrollments
    WHERE Grade = 'A'
);
</code></pre>

<h3>6. Find the names of professors earning above the average salary of all teachers.</h3>
<p><strong>Logic:</strong> Calculate the overall average salary and retrieve the names and salaries of teachers whose salary is greater than the average.</p>
<pre><code>SELECT Teacher_Name, Salary
FROM Teachers
WHERE Salary > (SELECT AVG(Salary) FROM Teachers);
</code></pre>

<h3>7. List all students not enrolled in any course.</h3>
<p><strong>Logic:</strong> Select students whose Student_ID is not present in the Course_Enrollments table.</p>
<pre><code>SELECT Student_Name
FROM Students
WHERE Student_ID NOT IN (SELECT Student_ID FROM Course_Enrollments);
</code></pre>

<h3>8. Find the departments offering more than 2 courses.</h3>
<p><strong>Logic:</strong> Use a subquery with GROUP BY and HAVING to count courses per department and filter those with a count greater than 2.</p>
<pre><code>SELECT Department_Name
FROM Departments
WHERE Department_ID IN (
    SELECT Department_ID
    FROM Courses
    GROUP BY Department_ID
    HAVING COUNT(Course_ID) > 2
);
</code></pre>

<pre><code class="language-sql">CREATE DATABASE Teachers_Students;
USE Teachers_Students;

CREATE TABLE Faculty (
    Faculty_ID VARCHAR(10),
    Faculty_Name VARCHAR(50),
    Dean VARCHAR(50),
    Email VARCHAR(100)
);

CREATE TABLE Teachers_Portal (
    Teacher_ID VARCHAR(10),
    Name VARCHAR(50),
    Email VARCHAR(100),
    Faculty_ID VARCHAR(10)
);

CREATE TABLE Students_Portal (
    Student_ID VARCHAR(10),
    Name VARCHAR(50),
    Address VARCHAR(50),
    Age INT,
    CGPA DECIMAL(3,2),
    Faculty_ID VARCHAR(10)
);

INSERT INTO Faculty (Faculty_ID, Faculty_Name, Dean, Email) VALUES
('F301', 'FSIT', 'Mr. Fokhray', 'fsit@diu.edu.bd'),
('F302', 'FBE', 'Mr. Rokibul', 'fbe@diu.edu.bd'),
('F303', 'FHLS', 'Mr. Majumder', 'fhls@diu.edu.bd'),
('F304', 'FE', 'Mr. Shamsul', 'fe@diu.edu.bd'),
('F305', 'FHSS', 'Ms. Liza', 'fhss@diu.edu.bd');

INSERT INTO Teachers_Portal (Teacher_ID, Name, Email, Faculty_ID) VALUES
('T201', 'Mr. Sohel', 'sohel@diu.edu.bd', 'F301'),
('T202', 'Mr. Mehedi', 'mehedi@diu.edu.bd', 'F302'),
('T203', 'Mr. Israfil', 'israfil@diu.edu.bd', 'F305'),
('T204', 'Mr. Faruk', 'faruk@diu.edu.bd', 'F304'),
('T205', 'Ms. Sonia', 'sonia@diu.edu.bd', 'F301');

INSERT INTO Students_Portal (Student_ID, Name, Address, Age, CGPA, Faculty_ID) VALUES
('S101', 'Shimu', 'Rajshahi', 24, 3.80, 'F301'),
('S102', 'Rayhan', 'Chittagong', 23, 3.20, 'F305'),
('S103', 'Samiul', 'Dhaka', 21, 3.95, 'F301'),
('S104', 'Shehabaul', 'Rajshahi', 22, 3.50, 'F304'),
('S105', 'Tanzil', 'Khulna', 24, 3.10, 'F302');</code></pre>



