```json
// Документы в коллекции users
[
  {
    "_id": ,
    "login": "user1",
    "name": "SadWorker",
    "email": "sad@example.com"
  },
  {
    "_id": ,
    "login": "user2",
    "name": "HappyWorker",
    "email": "happy@example.com"
  }
]
```
```json
// Документы в коллекции messages
[
  {
    "_id": ,
    "login": "user1",
    "message": "Hello from Sad",
  },
  {
    "_id": ,
    "login": "user2",
    "message": "Happy message",
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
  "name": "SadWorker",
  "email": "sad@example.com",
  "user_messages": [
    {
      "_id": ,
      "login": "user1",
      "message": "Hello from Sad",
    }
  ]
}

```
