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
