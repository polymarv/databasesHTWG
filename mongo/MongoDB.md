# 2)
## a)
```
db.studiengaenge.find({ abschluss: "Bachelor" }, { kuerzel: 1, _id: 0 })
```

## b)
```
db.vorlesungen.find({ studiengang: ObjectId("662772c5176f1fa75bd337d7"), sws: { $lt: 5 } }, { name: 1, _id: 0 }).sort({ name: 1 })
```

## c)
```
db.vorlesungen.find({ sws: { $gt: "$ects" } })
```

## d)
```
db.vorlesungen.aggregate([
    { $match: { studiengang: ObjectId("662772c5176f1fa75bd337d7") } },
    { $group: { _id: "$dozent", total_sws: { $sum: "$sws" } } }
])
```

## e)
```
db.vorlesungen.aggregate([
    { $match: { studiengang: ObjectId("662772c5176f1fa75bd337d7") } },
    { $group: { _id: "$dozent", total_sws: { $sum: "$sws" } } },
    { $sort: { total_sws: -1 } },
    { $limit: 1 }
])
```

# 3)
## a)
```
db.abt.aggregate([
    {
        $lookup: {
            from: "pers",
            localField: "_id",
            foreignField: "abteilung.$id",
            as: "mitarbeiter"
        }
    },
    {
        $match: {
            mitarbeiter: { $size: 0 }
        }
    },
    {
        $project: {
            _id: 1,
            name: 1,
            ort: 1
        }
    }
])
```

## b)
```
db.pers.aggregate([
    {
        $lookup: {
            from: "pers",
            localField: "vorgesetzter.$id",
            foreignField: "_id",
            as: "chef"
        }
    },
    {
        $match: {
            chef: { $ne: [] }, // Mitarbeiter eines Vorgesetzten
            $expr: { $gt: ["$jahrg", { $arrayElemAt: ["$chef.jahrg", 0] }] } // Vergleich der Geburtsjahre 
        }
    },
    {
        $project: {
            _id: 0,
            mitarbeiter: "$name",
            vorgesetzter: { $arrayElemAt: ["$chef.name", 0] }
        }
    }
])
```

### in SQL:
```
SELECT Mitarbeiter.name AS Mitarbeiter, Vorgesetzter.name AS Vorgesetzter
FROM pers AS Mitarbeiter
JOIN pers AS Vorgesetzter ON Mitarbeiter.vorgesetzter = Vorgesetzter.pnr
WHERE Mitarbeiter.jahrg > Vorgesetzter.jahrg;
```

### Unterschiede:
- Lookup vs join
- Dokumentorientiert vs relational

## c)
```
db.pers.aggregate([
    {
        $group: {
            _id: "$abteilung.$id",
            durchschnittsalter: { $avg: "$jahrg" }
        }
    },
    {
        $lookup: {
            from: "abt",
            localField: "_id",
            foreignField: "_id",
            as: "abteilung"
        }
    },
    {
        $unwind: "$abteilung"
    },
    {
        $sort: { durchschnittsalter: 1 }
    },
    {
        $project: {
            _id: "$abteilung.anr",
            abteilungsname: "$abteilung.name"
        }
    },
    {
        $limit: 1
    }
])
```
