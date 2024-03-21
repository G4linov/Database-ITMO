```sql
-- Создание таблицы users
CREATE TABLE users (
    user_id SERIAL PRIMARY KEY,
    email VARCHAR(255),
    name VARCHAR(255) NOT NULL,
    lastname VARCHAR(255)
);
-- Создание таблицы chats
CREATE TABLE chats (
    chat_id SERIAL PRIMARY KEY,
    chat_name VARCHAR(255) UNIQUE NOT NULL
);
-- Создание таблицы messages
CREATE TABLE messages (
    message_id SERIAL PRIMARY KEY,
    message_text TEXT NOT NULL,
    user_id INTEGER,
    chat_id INTEGER,
    FOREIGN KEY (user_id) REFERENCES users(user_id),
    FOREIGN KEY (chat_id) REFERENCES chats(chat_id)
);
```
```sql
-- Добавление пользователей
INSERT INTO users (email, name, lastname) VALUES
('user1@mail.com', 'User1', 'Lastname1'),
('user2@mail.com', 'User2', 'Lastname2');
-- Добавление чатов
INSERT INTO chats (chat_name) VALUES
('Chat1'),
('Chat2');
-- Добавление сообщений
INSERT INTO messages (message_text, user_id, chat_id) VALUES
('Hello from User1', 1, 1),
('Reply from User2', 2, 1),
('Another message from User1', 1, 2),
('Final message from User2', 2, 2);
```
```sql
SELECT
    u.user_id AS "userId",
    u.name AS "userName",
    u.lastname AS "userLastname",
    c.chat_id AS "chatId",
    c.chat_name AS "chatName",
    m.message_id AS "lastMessageId",
    m.message_text AS "lastMessageText"
FROM
    users u
JOIN
    messages m ON u.user_id = m.user_id
JOIN
    chats c ON m.chat_id = c.chat_id
WHERE
    m.message_id IN (
        SELECT MAX(message_id)
        FROM messages
        GROUP BY chat_id
    )
ORDER BY
    c.chat_id;
```

```sql
| userId | userName | userLastname | chatId | chatName | lastMessageId |      lastMessageText       |
|--------|----------|--------------|--------|----------|---------------|----------------------------|
|      1 | User1    | Lastname1    |      1 | Chat1    |             2 | Reply from User2           |
|      1 | User1    | Lastname1    |      2 | Chat2    |             4 | Final message from User2   |

```
