```json
// Документы в коллекции users
[
  {
    "_id": ,
    "login": "user1",
    "name": "User One",
    "email": "user1@example.com"
  },
  {
    "_id": ,
    "login": "user2",
    "name": "User Two",
    "email": "user2@example.com"
  }
]
```
```json
// Документы в коллекции messages
[
  {
    "_id": ,
    "login": "user1",
    "message": "Hello from User One",
  },
  {
    "_id": ,
    "login": "user2",
    "message": "User Two's message",
  }
]

```
```json
db.users.aggregate([
  {
    $lookup: {
      from: "messages",
      localField: "login",
      foreignField: "login",
      as: "user_messages"
    }
  }
])

```
```json
{
  "_id": ,
  "login": "user1",
  "name": "User One",
  "email": "user1@example.com",
  "user_messages": [
    {
      "_id": ,
      "login": "user1",
      "message": "Hello from User One",
    }
  ]
}

```
