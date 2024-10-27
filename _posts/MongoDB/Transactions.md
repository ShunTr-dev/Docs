Transactions - Fail together

```
// Necesitas crear una sesión, un objeto que permite agrupar todas las acciones
const sesion = db.getMongo().startSession()
session.startTransaction()
const usersC = session.getDatabases("blog")
const usersCol = session.getDatabases("blog").users
const postsCol = session.getDatabases("blog").posts
db.users.find.pretty()
usersCol.deleteOne()
postsCol.deleteMany()
session.commitTransaction()
session.abortTransaction()
```
