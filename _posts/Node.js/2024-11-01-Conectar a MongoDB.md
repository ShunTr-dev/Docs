---
title: Conectar a MongoDb
date: 2024-11-01 00:00:00 -100
categories: [Node.js]
tags: [node, mongo, mongodb, db, database]
---

Para conectar una aplicación de Node.js a MongoDB, puedes usar el paquete `mongoose`, que facilita la interacción con MongoDB mediante una interfaz sencilla y orientada a objetos.

### 1. Crear un proyecto de Node.js
Si aún no tienes un proyecto de Node.js, crea uno yendo al directorio de tu proyecto y ejecutando:

```bash
mkdir nombre-de-tu-proyecto
cd nombre-de-tu-proyecto
npm init -y
```

### 1. Instalar Mongoose
Mongoose es una biblioteca de Node.js para MongoDB que facilita la interacción con la base de datos. Puedes instalarlo con:

```bash
npm install mongoose
```

### 2. Configurar la Conexión a MongoDB

#### Explicación:
- **URI de conexión**: 
    * Si estás usando MongoDB en tu máquina local, usa `mongodb://localhost:27017/nombre-de-tu-base-de-datos`.
    * Si usas MongoDB Atlas o un servidor remoto, la URI puede verse así: `mongodb+srv://usuario:password@cluster.mongodb.net/nombre-de-tu-base-de-datos?retryWrites=true&w=majority`.
  
    Puedes pasar la dirección como una variable de entorno pero necesitas usar un string template.

Ahora puedes usar `mongoose` en el archivo principal de tu aplicación (por ejemplo, `app.js` o `server.js`).

#### Archivo `app.js`:
```javascript
const express = require('express');
const mongoose = require('./db');

const app = express();

app.use(express.json());

app.get('/', (req, res) => {
    res.send('¡La conexión a MongoDB está funcionando!');
});

mongoose
    .connect('mongodb+srv://usuario:password@cluster.mongodb.net/nombre-de-tu-base-de-datos?retryWrites=true&w=majority')
    .then(() => {
        app.listen(process.env.PORT);
    })
    .catch(err => {
        console.log(err);
    });
```

### 3. Crear un Modelo de Ejemplo
Los modelos en Mongoose son representaciones de los documentos de MongoDB. Por ejemplo, si quieres un modelo para almacenar usuarios:

#### Archivo `models/User.js`:
```javascript
const mongoose = require('mongoose');
const uniqueValidator = require('mongoose-unique-validator');

const userSchema = new Schema({
    username: { type: String, required: false },
    groupId: { type: mongoose.Schema.Types.ObjectId, required: false , ref: 'UserGroup', default: '64be2e7090b134d92ec1b68a'},
    email: { type: String, required: true, unique: true },
    dateOfBirth: { type: Date, required: false, default: '' },
    mailing_addresses: [{
        name: { type: String, required: false },
        address: { type: String, required: false },
    }],
});

userSchema.plugin(uniqueValidator);
userSchema.set('timestamps', true);

const User = mongoose.model('User', userSchema);

module.exports = User;
```
