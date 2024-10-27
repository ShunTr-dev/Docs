```
mongod --auth //obliga a que todo el que se conecte tenga que estar autorizado
// cuando estás es localhost, y no tienes usuarios, tienes la opción de crear un usuario
use admin
db.createUser({user: "max", pwd: "pwd", roles["userAdminAnyDatabase"]})
deb.auth("max", "max")
```

```
mongo -u max -p max --authenticationDatabase admin
use shop
db.createUser({user: 'appdev', pwd: 'pwd', roles: ["readWrite"]}) // los usuarios se crean localmente en las BDD
db.logout()

// Para extender un rol a otra bdd
db.updateUser("appdev", {roles: ["readWrite", {role: "readWrite", db: "blog"} ]})
```
