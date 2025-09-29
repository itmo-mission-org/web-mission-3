# Mission 3

## Part 1

[Link to video](https://www.youtube.com/)

## Part2

[Link to video](https://www.youtube.com/)

## Part3

1. Получение списка юзернеймов пользователей

``SELECT username FROM users``

2. Получение количества отправленных сообщений каждым пользователем

``SELECT id, COUNT(*) AS number_of_sent_messages
FROM messages
GROUP BY id;``

3. Получение пользователя с максимальным количеством полученных сообщений

``SELECT 
    u.username,
    COUNT(m.id) AS "number of received messages"
FROM 
    users u
JOIN 
    messages m ON u.id = m."to"
GROUP BY 
    u.username
ORDER BY 
    COUNT(m.id) DESC
LIMIT 1;``

4. Получение среднего количества сообщений на пользователя

``SELECT 
    AVG(message_count) AS "average_messages_per_user"
FROM 
    (SELECT u.id,
        COUNT(m.id) AS message_count
    FROM 
        users u
    LEFT JOIN 
        messages m ON u.id = m."from"
    WHERE
        u.id IN (1, 2) 
    GROUP BY u.id
    ) 
AS 
    user_message_counts;``
