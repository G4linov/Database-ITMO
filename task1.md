# Отчёт о проделанной работе в PostgreSQL

## Создание базы данных и таблиц

создали базу данных с названием project_db и таблицы teams, projects, и tasks, представляющие информацию о командах, проектах и задачах соответственно. Ниже приведен пример SQL-кода для создания базы данных и таблиц:

-- Создание базы данных
CREATE DATABASE project_db;

-- Подключение к созданной базе данных
\c project_db;

-- Создание таблицы teams
CREATE TABLE teams (
    team_id SERIAL PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    description TEXT
);

-- Создание таблицы projects
CREATE TABLE projects (
    project_id SERIAL PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    start_date DATE,
    end_date DATE,
    team_id INTEGER,
    FOREIGN KEY (team_id) REFERENCES teams(team_id)
);

-- Создание таблицы tasks
CREATE TABLE tasks (
    task_id SERIAL PRIMARY KEY,
    description TEXT NOT NULL,
    status VARCHAR(50),
    priority INTEGER,
    due_date DATE,
    project_id INTEGER,
    FOREIGN KEY (project_id) REFERENCES projects(project_id)
);

## Обновление данных в таблице с операторами UPDATE и WHERE

Для обновления данных в базе данных project_db и таблице tasks. хотим обновить статус задач для определённого проекта. В качестве примера, предположим, что нужно изменить статус всех задач, принадлежащих проекту с project_id равным 2, на "Completed".

-- Обновление статуса задач в проекте с project_id = 2 на "Completed"
UPDATE tasks
SET status = 'Completed'
WHERE project_id = 2;

## Удаление данных из таблицы с операторами DELETE и WHERE

Предположим, что нужно удалить все задачи, которые были завершены и имеют дату выполнения (due_date) до определённой даты, например, до 1 января 2024 года.

-- Удаление задач, которые были завершены и имеют дату выполнения до 1 января 2024 года
DELETE FROM tasks
WHERE status = 'Completed'
AND due_date < '2024-01-01';

## Получение данных из таблицы с операторами SELECT и WHERE

выбрать все проекты, которые начались после 1 января 2023 года. Используя операторы SELECT и WHERE, вы можете легко извлечь эту информацию. Вот пример SQL-кода, который демонстрирует, как это сделать:

-- Выборка проектов, которые начались после 1 января 2023 года
SELECT *
FROM projects
WHERE start_date > '2023-01-01';

## Result

 project_id |               name                | start_date |  end_date  | team_id 
------------+------------------------------------+------------+------------+---------
          2 | Веб-платформа электронной коммерции| 2023-02-01 | 2023-12-01 |       1
          3 | Система управления задачами        | 2023-03-15 | 2024-01-15 |       3
          4 | Разработка игры на Unity           | 2023-01-15 | 2023-11-20 |       4
