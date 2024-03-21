```json
// Документы в коллекции users
[
  {
    "_id": ObjectId("..."),
    "login": "user1",
    "name": "User One",
    "email": "user1@example.com"
  },
  {
    "_id": ObjectId("..."),
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
    "_id": ObjectId("..."),
    "login": "user1",
    "message": "Hello from User One",
    "timestamp": ISODate("...")
  },
  {
    "_id": ObjectId("..."),
    "login": "user2",
    "message": "User Two's message",
    "timestamp": ISODate("...")
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
  "_id": ObjectId("..."),
  "login": "user1",
  "name": "User One",
  "email": "user1@example.com",
  "user_messages": [
    {
      "_id": ObjectId("..."),
      "login": "user1",
      "message": "Hello from User One",
      "timestamp": ISODate("...")
    }
  ]
}

```
