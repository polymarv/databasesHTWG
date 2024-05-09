# Insert Statement in neo4j for building plan database
```
// Erdgeschoss
CREATE 
  (Aufenthaltsraum:Raum {Name:'0001 Aufenthaltsraum', Plätze:30, Sofa:true, Etage:'Erdgeschoss'}),
  (TreppeSüd:Raum {Name:'Treppe Süd', Etage:'Erdgeschoss'}),
  (Aufzug:Raum {Name:'Aufzug', Etage:'Erdgeschoss'}),
  (PcPool0002:Raum {Name:'Pc Pool 0002', Plätze:56, Etage:'Erdgeschoss'}),
  (BehindertenToilette:Raum {Name:'0092 Behinderten Toillette', Etage:'Erdgeschoss'}),
  (FakultätIN1:Raum {Name:'0003 Fakultät IN', Personen:['Sahin Karakoc', 'Johannes Dierkes'], Etage:'Erdgeschoss'}),
  (FakultätIN2:Raum {Name:'0004 Fakultät IN', Personen:['Klaus Eiermann', 'Mamaduo Kane'], Etage:'Erdgeschoss'}),
  (TreppeNord:Raum {Name:'Treppe Nord', Etage:'Erdgeschoss'}),
  (PCPool0007:Raum {Name:'0007 PC-Pool', Etage:'Erdgeschoss'}),
  (WCHerren:Raum {Name:'0091 WC-Herren', Etage:'Erdgeschoss'}),
  (Gebäudemanagement:Raum {Name:'0010 Gebäudemanagement', Etage:'Erdgeschoss'}),
  (Rechenzentrum:Raum {Name:'0009 Rechenzentrum', Etage:'Erdgeschoss'}),
  (PCPool0008:Raum {Name:'0008 PC-Pool', Plätze:30, Beamer:1, Tafeln:3, Etage:'Erdgeschoss'}),
  (Ausgang:Raum {Name:'Ausgang', Etage:'Erdgeschoss'});

// 1. Stock
CREATE 
  (Seminarraum:Raum {Name:'0101 Seminarraum', Plätze:20, Beamer:1, Tafeln:3, Etage:'1. Stock'}),
  (Hörsaal0102:Raum {Name:'Hörsaal 0102', Plätze:60, Beamer:1, Tafeln:3, Etage:'1. Stock'}),
  (FakultätINTeeküche:Raum {Name:'0111 Fakultät IN Teeküche', Etage:'1. Stock'}),
  (Hörsaal0103:Raum {Name:'0103 Hörsaal', Plätze:60, Beamer:1, Tafeln:3, Etage:'1. Stock'}),
  (FakultätIN3:Raum {Name:'0104 Fakultät IN', Personen:['Prof. Dr. Renato Dambe', 'Prof. Dr. Christian Wache'], Etage:'1. Stock'}),
  (FakultätIN4:Raum {Name:'0105 Fakultät IN', Personen:['Prof. Dr. Ralf-Dieter Schimkat', 'Prof. Dr. Stefan Sohn'], Etage:'1. Stock'}),
  (FakultätIN5:Raum {Name:'0106 Fakultät IN', Personen:['Prof. Dr. Ing. Jürgen Wäsch', 'Prof. Dr. Oliver Eck'], Etage:'1. Stock'}),
  (Druckerraum:Raum {Name:'0112 Fakultät IN Druckerraum', Etage:'1. Stock'}),
  (ToiletteFrauen:Raum {Name:'0191 Toilette Frauen', Etage:'1. Stock'}),
  (PCPool0107:Raum {Name:'0107 PC Pool', Plätze:70, Beamer:1, Tafeln:3, Etage:'1. Stock'}),
  (Gebäudemanagement2:Raum {Name:'0110 Gebäudemanagement', Etage:'1. Stock'}),
  (Rechenzentrum2:Raum {Name:'0109 Rechenzrentrum', Etage:'1. Stock'}),
  (PCPool0108:Raum {Name:'0108 PC Pool', Plätze:18, Beamer:1, Tafeln:4, Etage:'1. Stock'});

// Relations
CREATE 
  (Aufenthaltsraum)-[:NACHBAR {Zeit:1}]->(TreppeSüd),
  (TreppeSüd)-[:NACHBAR {Zeit:1}]->(Aufzug),
  (Aufzug)-[:NACHBAR {Zeit:3}]->(PcPool0002),
  (PcPool0002)-[:NACHBAR {Zeit:2}]->(BehindertenToilette),
  (BehindertenToilette)-[:NACHBAR {Zeit:3}]->(FakultätIN1),
  (FakultätIN1)-[:NACHBAR {Zeit:2}]->(FakultätIN2),
  (FakultätIN2)-[:NACHBAR {Zeit:3}]->(TreppeNord),
  (TreppeNord)-[:NACHBAR {Zeit:2}]->(PCPool0007),
  (PCPool0007)-[:NACHBAR {Zeit:2}]->(WCHerren),
  (WCHerren)-[:NACHBAR {Zeit:1}]->(Gebäudemanagement),
  (Gebäudemanagement)-[:NACHBAR {Zeit:1}]->(Rechenzentrum),
  (Rechenzentrum)-[:NACHBAR {Zeit:3}]->(PCPool0008),
  (PCPool0008)-[:NACHBAR {Zeit:2}]->(Ausgang),
  (Seminarraum)-[:NACHBAR {Zeit:1}]->(TreppeSüd),
  (TreppeSüd)-[:NACHBAR {Zeit:1}]->(Aufzug),
  (Aufzug)-[:NACHBAR {Zeit:2}]->(Hörsaal0102),
  (Hörsaal0102)-[:NACHBAR {Zeit:2}]->(FakultätINTeeküche),
  (FakultätINTeeküche)-[:NACHBAR {Zeit:2}]->(Hörsaal0103),
  (Hörsaal0103)-[:NACHBAR {Zeit:2}]->(FakultätIN3),
  (FakultätIN3)-[:NACHBAR {Zeit:1}]->(FakultätIN4),
  (FakultätIN4)-[:NACHBAR {Zeit:1}]->(FakultätIN5),
  (FakultätIN5)-[:NACHBAR {Zeit:2}]->(TreppeNord),
  (TreppeNord)-[:NACHBAR {Zeit:2}]->(Druckerraum),
  (Druckerraum)-[:NACHBAR {Zeit:1}]->(ToiletteFrauen),
  (ToiletteFrauen)-[:NACHBAR {Zeit:2}]->(PCPool0107),
  (PCPool0107)-[:NACHBAR {Zeit:2}]->(Gebäudemanagement2),
  (Gebäudemanagement2)-[:NACHBAR {Zeit:1}]->(Rechenzentrum2),
  (PCPool0108)-[:NACHBAR {Zeit:4}]->(Seminarraum);

```