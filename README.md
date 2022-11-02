# Challenge12

  - [Exercise 1](#1)
  - [Exercise 2](#2)
  - [Exercise 3](#3)
  - [Exercise 4](#4)
  - [Exercise 5](#5)
  - [Exercise 6](#6)
## 1. 
__Add 10 documents with diferent values to the messages and products collection__

```
db.messages.insertMany([
  {
    email: 'alexander@gmail.com',
    date: new Date('2022-11-01T18:37:53Z'),
    text: 'Hola, hablas inglés?'
  },
  {
    email: 'amelia@gmail.com',
    date: new Date('2022-11-01T18:38:24Z'),
    text: 'A little bit hehe'
  },
  {
    email: 'alexander@gmail.com',
    date: new Date('2022-11-01T18:38:58Z'),
    text: 'Me too, a little bit Spanish'
  },
  {
    email: 'amelia@gmail.com',
    date: new Date('2022-11-01T18:40:12Z'),
    text: 'Great! Where are you from?'
  },
  {
    email: 'alexander@gmail.com',
    date: new Date('2022-11-01T18:41:38Z'),
    text: 'I am from Canada, and you?'
  },
  {
    email: 'amelia@gmail.com',
    date: new Date('2022-11-01T18:41:59Z'),
    text: 'Cool, I am originally from India'
  },
  {
    email: 'amelia@gmail.com',
    date: new Date('2022-11-01T18:43:18Z'),
    text: 'But I lived in Paris for two years'
  },
  {
    email: 'alexander@gmail.com',
    date: new Date('2022-11-01T18:58:23Z'),
    text: 'Nice!'
  },
  {
    email: 'alexander@gmail.com',
    date: new Date('2022-11-01T19:02:47Z'),
    text: 'That's great buddy'
  },
  {
    email: 'alexander@gmail.com',
    date: new Date('2022-11-01T19:02:59Z'),
    text: 'Take care'
  }
])
```

```
db.products.insertMany([
  {
    title: 'Clock',
    price: 190.9,
    thumbnail: 'https://cdn3.iconfinder.com/data/icons/education-209/64/clock-stopwatch-timer-time-128.png'
  },
  {
    title: 'Ruler',
    price: 124.8,
    thumbnail: 'https://cdn3.iconfinder.com/data/icons/education-209/64/ruler-triangle-stationary-school-256.png'
  },
  {
    title: 'Apple',
    price: 24.2,
    thumbnail: 'https://cdn3.iconfinder.com/data/icons/education-209/64/apple-fruit-science-school-128.png'
  },
  {
    title: 'Calculator',
    price: 234.5,
    thumbnail: 'https://cdn3.iconfinder.com/data/icons/education-209/64/calculator-math-tool-school-256.png'
  },
  {
    title: 'Globe',
    price: 345.6,
    thumbnail: 'https://cdn3.iconfinder.com/data/icons/education-209/64/globe-earth-geograhy-planet-school-128.png'
  },
  {
    title: 'Pencil',
    price: 80.7,
    thumbnail: 'https://cdn3.iconfinder.com/data/icons/education-209/64/pencil-pen-stationery-school-128.png'
  },
  {
    title: 'Backpack',
    price: 200.6,
    thumbnail: 'https://cdn3.iconfinder.com/data/icons/education-209/64/bag-pack-container-school-128.png'
  },
  {
    title: 'Bus',
    price: 4900.7,
    thumbnail: 'https://cdn3.iconfinder.com/data/icons/education-209/64/bus-vehicle-transport-school-128.png'
  },
  {
    title: 'Folder',
    price: 68.5,
    thumbnail: 'https://cdn1.iconfinder.com/data/icons/Futurosoft%20Icons%200.5.2/128x128/filesystems/folder_image.png'
  },
  {
    title: 'Paper Plane',
    price: 12,
    thumbnail: 'https://cdn3.iconfinder.com/data/icons/education-209/64/plane-paper-toy-science-school-128.png'
  }
])
```

## 2. 
__Define the documents keys in relation to the fields of the tables for that base. In the case of products, put values ​​in the price field between 100 and 5000 pesos__

## 3. 
__List all documents of each collection__
```
db.messages.find()
db.products.find()
```

## 4. 
__Show the total number of documents of each collection__
```
db.messages.estimatedDocumentCount()
db.products.estimatedDocumentCount()
```

## 5. 
__CRUD on products collection__

### 5.1. Add a new product
```
db.products.insertOne({
  title: 'Gif',
  price: 45.2,
  thumbnail: 'https://cdn3.iconfinder.com/data/icons/pleasant/GIF-Image.png'
})
```

### 5.2. Find with filters

#### 5.2.1. Find products with price lower than 1000
```
db.products.find({ price: { $lt: 1000 } })
```
#### 5.2.2. Find products with price between 1000 and 3000
```
db.products.find({ $and: [{ price: { $gt: 1000 } }, { price: { $lt: 3000 } }] })
```
#### 5.2.3. Find products with price greater than 3000
```
db.products.find({ price: { $gt: 3000 } })
```
#### 5.2.4. Find the title of the third most cheaper product
```
db.products.find({}, { title: 1 }).sort({ price: 1 }).limit(1).skip(2)
```

### 5.3. Update all products, adding a new field called stock with a value of 100
```
db.products.updateMany({}, { $set: { stock: 100 } })
```

### 5.4. Update all products with a price greater than 4000, setting the stock to 0
```
db.products.updateMany({ price: { $gt: 4000 } }, { $set: { stock: 0 } })
```

### 5.5. Delete all products with a price lower than 1000
```
db.products.deleteMany({ price: { $lt: 1000 } })
```

## 6. 
__Create an user called 'pepe' with password 'asd456' that can only read the database__
```
use admin
db.createUser({
  user: 'pepe',
  pwd: 'asd456',
  roles: [
    {
      role: 'read',
      db: 'ch-challenges-ecommerce'
    }
  ]
})
```