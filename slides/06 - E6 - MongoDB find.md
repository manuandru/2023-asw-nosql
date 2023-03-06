# MongoDB  - Esercitazione (Find)

## Restaurants
1. Visualizzare tutti i ristoranti.
```javascript
db = db.getSiblingDB("exercises");
db.restaurants
  .find({});
```


2. Visualizzare quartiere (borough) e tipo di cucina (cuisine) di tutti i ristoranti. 
```javascript
db = db.getSiblingDB("exercises");
db.restaurants
  .find({}, {borough:1, cuisine:1});
```

3. Visualizzare quartiere (borough) e tipo di cucina (cuisine) di tutti i ristoranti, ma senza _id. 
```javascript
db = db.getSiblingDB("exercises");
db.restaurants
  .find({}, {borough:1, cuisine:1, _id:0});
```

4. Visualizzare quartiere (borough), tipo di cucina (cuisine) e via (address.street) di tutti i ristoranti. 
```javascript
db = db.getSiblingDB("exercises");
db.restaurants
  .find({}, {borough:1, cuisine:1, "address.zipcode":1});
```

5. Visualizzare iI ristorante il cui zipcode è 11225
```javascript
db = db.getSiblingDB("exercises");
db.restaurants
  .find({"address.zipcode":"11225"});
```


6. Visualizzare i ristoranti il cui tipo di cucina è Hamburgers 
```javascript
db = db.getSiblingDB("exercises");
db.restaurants
  .find({"cuisine":"Hamburgers"});
```


7. Visualizzare i ristoranti il cui tipo di cucina NON è Hamburgers 
```javascript
db = db.getSiblingDB("exercises");
db.restaurants
  .find({"cuisine":{"$ne":"Hamburgers"}});
```


8. Visualizzare i ristoranti il cui tipo di cucina è tra Hamburgers, Bakery o Irish 
```javascript
db = db.getSiblingDB("exercises");
db.restaurants
  .find({"cuisine":{"$in":["Hamburgers", "Bakery", "Irish"]}});

```


9. Visualizzare i ristoranti il cui tipo di cucina NON è tra Hamburgers, Bakery o Irish 
```javascript
db = db.getSiblingDB("exercises");
db.restaurants
  .find({"cuisine":{"$not":{"$in":["Hamburgers", "Bakery", "Irish"]}}});
```


10. Visualizzare i ristoranti il cui tipo di cucina non esiste 
```javascript
db = db.getSiblingDB("exercises");
db.restaurants
  .find({"cuisine":{"$exists":false}});
```


## Yelp business
11. Visualizzare tutti i business che hanno ricevuto almeno 10 recensioni (review_count) E si trovano in Arizona o in Nevada (state = NV o AZ) 
```javascript
db.getCollection("yelp-business")
  .find({
      "$and":[
          {"review_count": {"$gte":10}},
          {"state": {"$in":["NV", "AZ"]}}
      ]
  })
```


12. Visualizzare tutti i business che hanno ricevuto almeno 10 recensioni (review_count) O si trovano in Arizona o in Nevada (state = NV o AZ) 
```javascript
db.getCollection("yelp-business")
  .find({
      "$or":[
          {"review_count": {"$gte":10}},
          {"state": {"$in":["NV", "AZ"]}}
      ]
  })
```


13. Visualizzare tutti i business che hanno Grocery tra le categorie 
```javascript
db.getCollection("yelp-business")
  .find({
      categories:"Grocery"
  })
```


14. Visualizzare tutti i business che hanno Grocery E Food tra le categorie 
```javascript
db.getCollection("yelp-business")
  .find({
      categories:{
          $all: ["Grocery", "Food"]
      }
  })
```


15. Visualizzare tutti i business che hanno Grocery O Food tra le categorie 
```javascript
db.getCollection("yelp-business")
  .find({
      $or: [
          {categories: "Grocery"},
          {categories: "Food"}
      ]
  })
```


16. Visualizzare tutti i business che hanno SOLAMENTE Grocery E Food tra le categorie 
```javascript
db.getCollection("yelp-business")
  .find({
      categories:["Grocery", "Food"]
  })
```


17. Visualizzare tutti i business che hanno 5 categorie 
```javascript
db.getCollection("yelp-business")
  .find({
      categories: {
          $size: 5
      }
  })
```


18. Visualizzare tutti i business che hanno 5 categorie e la quinta categoria è Food 
```javascript
db.getCollection("yelp-business")
  .find({
      $and: [
          {categories: {$size: 5}},
          {"categories.4": "Food"}
      ]
  })
```


19. Visualizzare le prime due categorie di ogni business 
```javascript
db.getCollection("yelp-business")
  .find({}, {"_id":1, categories:{$slice: 2}})
```


20. Visualizzare unicamente le categorie dei business del Nevada 
```javascript
db.getCollection("yelp-business")
  .distinct("categories", {state: "NV"})
```


21. Visualizzare i valori distinti del campo city
```javascript
db.getCollection("yelp-business")
  .distinct("city")
```


22. Visualizzare i valori distinti del campo city nello stato del Nevada
```javascript
db.getCollection("yelp-business")
  .distinct("city", {state: "NV"})
```


23. Visualizzare i valori distinti dell’array categories
```javascript
db.getCollection("yelp-business")
  .distinct("categories")
```


## Games

24. Visualizzare le partite disputate nel 2010. (1239 risultati). Formato data: "anno-mese-giorno"
```javascript
```


25. Visualizzare le partite in cui una delle squadre ha totalizzato almeno 160 punti (6 risultati)
```javascript
```


26. Visualizzare le partite in cui la squadra di casa ha perso (12197 risultati)
```javascript
```


27. Visualizzare le partite in cui ha giocato Michael Jordan (990 risultati)
```javascript
```


28. Visualizzare le partite in cui Michael Jordan ha segnato più di 60 punti (4 risultati)
```javascript
```


29. Visualizzare le prime 10 partite memorizzate nella collection (10 risultati)
```javascript
```


30. Visualizzare le prime 10 partite in ordine di data (10 risultati)
```javascript
```


31. Visualizzare le prime 10 partite del 2010 in ordine di data (10 risultati)
```javascript
```


32. Visualizzare le seconde 10 partite (dalla 11°) del 2010 in ordine di data (10 risultati)
```javascript
```


## Esercizi aggiuntivi

33. [Restaurants] Visualizzare i ristoranti che hanno ricevuto almeno un punteggio (grades.score) maggiore di 10
```javascript
```


34. [Restaurants] Visualizzare i ristoranti che hanno ricevuto almeno un punteggio (grades.score) maggiore di 10 nel 2014
```javascript
```


35. [Yelpbusiness] Contare i business di categoria Yoga che hanno ricevuto almeno 4 di punteggio (stars) e che sono aperti (is_open=1)
```javascript
```


36. [Games] Visualizzare le partite in cui la squadra di casa ha perso pur totalizzando più di 120 punti
```javascript
```


37. [Games] Visualizzare l’elenco distinto di date in cui una delle squadre ha totalizzato almeno 160 punti
```javascript
```


38. [Games] Visualizzare le partite in cui una delle due squadre ha sbagliato tutti i tiri liberi (box.team.ft=0) pur avendone provati almeno 2 (box.team.fta>=2)
```javascript
```
