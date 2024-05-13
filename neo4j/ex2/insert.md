# Insert Statement in neo4j for building plan database
```
// Erdgeschoss
CREATE
  (Aufenthaltsraum:Raum {name: 'Aufenthaltsraum', plätze: 30}),
  (TreppeSüdUnten:Treppe {name: 'Treppe Süd Unten', rollstuhlfahrer: false}),
  (AufzugUnten:Aufzug {name: 'Aufzug Unten', rollstuhlfahrer: true}),
  (PcPool0002:Raum {name: 'Pc Pool 0002', plätze: 56}),
  (BehindertenToillette:Raum {name: '0092 Behinderten Toillette'}),
  (FakultätIN0003:Raum {name: '0003 Fakultät IN'}),
  (FakultätIN0004:Raum {name: '0004 Fakultät IN'}),
  (TreppeNordUnten:Treppe {name: 'Treppe Nord Unten'}),
  (PCPool0007:Raum {name: '0007 PC Pool'}),
  (WCHerren:Raum {name: '0091 WC Herren'}),
  (Gebäudemanagement:Raum {name: '0010 Gebäudemanagement'}),
  (Rechenzentrum:Raum {name: '0009 Rechenzentrum'}),
  (PCPool0008:Raum {name: '0008 PC-Pool'}),
  (Ausgang:Raum {name: 'Ausgang'});

// Relationships
CREATE
  (Aufenthaltsraum)-[:NACHBAR {zeit: 1}]->(TreppeSüdUnten),
  (TreppeSüdUnten)-[:NACHBAR {zeit: 1}]->(AufzugUnten),
  (AufzugUnten)-[:NACHBAR {zeit: 3}]->(PcPool0002),
  (PcPool0002)-[:NACHBAR {zeit: 2}]->(BehindertenToillette),
  (BehindertenToillette)-[:NACHBAR {zeit: 3}]->(FakultätIN0003),
  (FakultätIN0003)-[:NACHBAR {zeit: 2}]->(FakultätIN0004),
  (FakultätIN0004)-[:NACHBAR {zeit: 3}]->(TreppeNordUnten),
  (TreppeNordUnten)-[:NACHBAR {zeit: 2}]->(PCPool0007),
  (PCPool0007)-[:NACHBAR {zeit: 2}]->(WCHerren),
  (WCHerren)-[:NACHBAR {zeit: 1}]->(Gebäudemanagement),
  (Gebäudemanagement)-[:NACHBAR {zeit: 1}]->(Rechenzentrum),
  (Rechenzentrum)-[:NACHBAR {zeit: 3}]->(PCPool0008),
  (PCPool0008)-[:NACHBAR {zeit: 2}]->(Ausgang);

// 1. Stock
CREATE
  (Seminarraum:Raum {name: '0101 Seminarraum', plätze: 20}),
  (TreppeSüdOben:Treppe {name: 'Treppe Süd Oben', rollstuhlfahrer: false}),
  (AufzugOben:Aufzug {name: 'Aufzug Oben', rollstuhlfahrer: true}),
  (Hörsaal0102:Raum {name: 'Hörsaal 0102', plätze: 60}),
  (FakultätINTeeküche:Raum {name: '0111 Fakultät IN Teeküche'}),
  (Hörsaal0103:Raum {name: '0103 Hörsaal', plätze: 60}),
  (FakultätIN0104:Raum {name: '0104 Fakultät IN'}),
  (FakultätIN0105:Raum {name: '0105 Fakultät IN'}),
  (FakultätIN0106:Raum {name: '0106 Fakultät IN'}),
  (TreppeNordOben:Treppe {name: 'Treppe Nord Oben'}),
  (FakultätINDruckerraum:Raum {name: '0112 Fakultät IN Druckerraum'}),
  (ToiletteFrauen:Raum {name: '0191 Toilette Frauen'}),
  (PCPool0107:Raum {name: '0107 PC Pool'}),
  (Gebäudemanagement2:Raum {name: '0110 Gebäudemanagement'}),
  (Rechenzrentrum:Raum {name: '0109 Rechenzrentrum'}),
  (PCPool0108:Raum {name: '0108 PC Pool'});

// Relationships
CREATE
  (Seminarraum)-[:NACHBAR {zeit: 1}]->(TreppeSüdOben),
  (TreppeSüdOben)-[:NACHBAR {zeit: 1}]->(AufzugOben),
  (AufzugOben)-[:NACHBAR {zeit: 2}]->(Hörsaal0102),
  (Hörsaal0102)-[:NACHBAR {zeit: 2}]->(FakultätINTeeküche),
  (FakultätINTeeküche)-[:NACHBAR {zeit: 2}]->(Hörsaal0103),
  (Hörsaal0103)-[:NACHBAR {zeit: 2}]->(FakultätIN0104),
  (FakultätIN0104)-[:NACHBAR {zeit: 1}]->(FakultätIN0105),
  (FakultätIN0105)-[:NACHBAR {zeit: 1}]->(FakultätIN0106),
  (FakultätIN0106)-[:NACHBAR {zeit: 2}]->(TreppeNordOben),
  (TreppeNordOben)-[:NACHBAR {zeit: 2}]->(FakultätINDruckerraum),
  (FakultätINDruckerraum)-[:NACHBAR {zeit: 1}]->(ToiletteFrauen),
  (ToiletteFrauen)-[:NACHBAR {zeit: 2}]->(PCPool0107),
  (PCPool0107)-[:NACHBAR {zeit: 2}]->(Gebäudemanagement2),
  (Gebäudemanagement2)-[:NACHBAR {zeit: 1}]->(Rechenzrentrum),
  (Rechenzrentrum)-[:NACHBAR {zeit: 4}]->(PCPool0108),
  (PCPool0108)-[:NACHBAR {zeit: 4}]->(Seminarraum);
```