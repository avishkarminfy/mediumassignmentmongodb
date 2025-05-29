# Medium Assignment: MongoDB

## 1. Total Quantity of Products by Supplier

### Command
```js
db.products.aggregate([
  {
    $group: {
      _id: "$supplier.name",
      totalQuantity: { $sum: "$quantity" }
    }
  }
])
```
### Output
```js
[
  { "_id": "GadgetPro", "totalQuantity": 125 },
  { "_id": "HomeBest", "totalQuantity": 30 },
  { "_id": "ActiveLife", "totalQuantity": 90 },
  { "_id": "SoundWave", "totalQuantity": 60 },
  { "_id": "TechGlobe", "totalQuantity": 60 },
  { "_id": "FashionHub", "totalQuantity": 280 },
  { "_id": "StyleCraft", "totalQuantity": 120 }
]
```

### 2. Average Price of Products per Tag

### Command
```js
db.products.aggregate([
  { $unwind: "$tags" },
  {
    $group: {
      _id: "$tags",
      averagePrice: { $avg: "$price" }
    }
  },
  {
    $sort: {
      averagePrice: -1
    }
  }
])
```
### Output
```js
[
  { "_id": "work", "averagePrice": 1200 },
  { "_id": "portable", "averagePrice": 493 },
  { "_id": "computer", "averagePrice": 433.33 },
  { "_id": "kitchen", "averagePrice": 250 },
  { "_id": "appliance", "averagePrice": 250 },
  { "_id": "coffee", "averagePrice": 250 },
  { "_id": "gadget", "averagePrice": 199 },
  { "_id": "wearable", "averagePrice": 199 },
  { "_id": "audio", "averagePrice": 80 },
  { "_id": "mechanical", "averagePrice": 75 },
  { "_id": "denim", "averagePrice": 60 },
  { "_id": "wireless", "averagePrice": 52.5 },
  { "_id": "peripheral", "averagePrice": 50 },
  { "_id": "leather", "averagePrice": 45 },
  { "_id": "fashion", "averagePrice": 45 },
  { "_id": "clothing", "averagePrice": 40 },
  { "_id": "fitness", "averagePrice": 30 },
  { "_id": "exercise", "averagePrice": 30 },
  { "_id": "casual", "averagePrice": 20 },
  { "_id": "cotton", "averagePrice": 20 }
]
```

### 3. Products Added in February 2023

### Command
```js
db.products.aggregate([
  {
    $match: {
      date_added: {
        $gte: new ISODate("2023-02-01T00:00:00Z"),
        $lt: new ISODate("2023-03-01T00:00:00Z")
      }
    }
  },
  {
    $project: {
      name: 1,
      category: 1,
      formattedDateAdded: {
        $dateToString: {
          format: "%Y-%m-%d",
          date: "$date_added"
        }
      }
    }
  }
])
```
### Output
<img width="644" alt="image" src="https://github.com/user-attachments/assets/9324eb02-9457-4281-af7d-0420c9788d83" />


