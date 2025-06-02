```sql
 -- Создать базу данных
CREATE DATABASE
  university;

-- Таблица групп
CREATE TABLE
  groups (
    id SERIAL PRIMARY KEY,
    group_name VARCHAR(10) UNIQUE
  );

-- Таблица студентов
CREATE TABLE
  students (
    id SERIAL PRIMARY KEY,
    full_name VARCHAR(100),
    age INT CHECK (age >= 16),
    group_id INT REFERENCES groups (id) ON DELETE CASCADE
  );

-- Таблица преподавателей
CREATE TABLE
  teachers (
    id SERIAL PRIMARY KEY,
    full_name VARCHAR(100),
    degree VARCHAR(50)
  );

-- Таблица курсов
CREATE TABLE
  courses (
    id SERIAL PRIMARY KEY,
    title VARCHAR(100) NOT NULL,
    credits INT CHECK (credits > 0)
  );

-- Кто что преподаёт (связь преподавателей с курсами)
CREATE TABLE
  teaches (
    teacher_id INT REFERENCES teachers (id) ON DELETE CASCADE,
    course_id INT REFERENCES courses (id) ON DELETE CASCADE,
    PRIMARY KEY (teacher_id, course_id)
  );

-- Записи на курсы
CREATE TABLE
  enrollments (
    student_id INT REFERENCES students (id) ON DELETE CASCADE,
    course_id INT REFERENCES courses (id) ON DELETE CASCADE,
    grade INT CHECK (
      grade >= 0
      AND grade <= 100
    ),
    PRIMARY KEY (student_id, course_id)
  );

------------------------------------------------------------
-- Группы
INSERT INTO
  groups (group_name)
VALUES
  ('CS101'),
  ('DS202'),
  ('AI303');

-- Преподаватели
INSERT INTO
  teachers (full_name, degree)
VALUES
  ('Dr. Smith', 'PhD'),
  ('Prof. Müller', 'Doctor of Science');

-- Курсы
INSERT INTO
  courses (title, credits)
VALUES
  ('Databases', 5),
  ('Algorithms', 4),
  ('AI Fundamentals', 6);

-- Кто что преподаёт
INSERT INTO
  teaches (teacher_id, course_id)
VALUES
  (1, 1),
  (1, 2),
  (2, 3);

-- Студенты
INSERT INTO
  students (full_name, age, group_id)
VALUES
  ('Alice Johnson', 20, 1),
  ('Bob Müller', 21, 2),
  ('Carlos Gómez', 22, 1),
  ('Dana Schmidt', 19, 3);

-- Записи студентов на курсы
INSERT INTO
  enrollments (student_id, course_id, grade)
VALUES
  (1, 1, 90),
  (1, 2, 85),
  (2, 1, 78),
  (2, 3, 88),
  (3, 2, 95),
  (4, 3, 92);

----------------------------------------------
-- средний возраст студентов
SELECT
  AVG(age)
FROM
  students;

-- общее количество студентов
SELECT
  COUNT(*)
FROM
  students;

-- минимальный возраст студента
SELECT
  MIN(age)
FROM
  students;

-- максимальное количество кредитов по курсам
SELECT
  MAX(credits)
FROM
  courses;

-- количество курсов, которые ведут преподаватели
SELECT
  COUNT(*)
FROM
  courses;

-- сколько студентов в каждой группе
SELECT
  group_id,
  COUNT(*) AS student_count
FROM
  students
GROUP BY
  group_id;

-- среднее количество кредитов по всем курсам
SELECT
  AVG(credits)
FROM
  courses;

-- сколько курсов ведёт каждый преподаватель
SELECT
  teacher_id,
  COUNT(*) AS course_count
FROM
  teaches
GROUP BY
  teacher_id;
```