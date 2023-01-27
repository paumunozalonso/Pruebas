# Crear sentenciés SQL - Categoria 2

### 5 preguntes de consultes de combinacions de més d'una taula: INNER JOINS, LEFT JOINS.

>Treball realitzat per Pau

### Selecciona el codi de candidatura i el nom curt dels partits que superen la quantitat de 100 vots(mostra igualment la quantitat de vots):

```
SELECT c.codi_candidatura, c.nom_curt, v.vots
FROM candidatures c
INNER JOIN vots_candidatures_ca v ON v.candidatura_id=c.candidatura_id
WHERE v.vots>100; 
```

### Mostra el nom i el total de vots(vots emesos,vots valids,vots candidatures,vots blanc, vots nuls) del municipi Melilla en l'any 2019:

```
SELECT m.nom,e.vots_emesos,e.vots_valids,e.vots_candidatures,e.vots_blanc,e.vots_nuls 
FROM eleccions_municipis e 
INNER JOIN municipis m ON m.municipi_id=e.municipi_id
INNER JOIN eleccions el ON el.eleccio_id=e.eleccio_id
WHERE el.any=2019 AND m.nom='Melilla';
```
### Selecciona el nom complert (nom, 1cognom, 2cognom) dels candidats que siguin dones i titulars a les eleccions:

```
SELECT CONCAT(p.nom,' ', p.cog1,' ',p.cog2) AS "Nom complert"
FROM candidats c
INNER JOIN persones p ON p.persona_id=c.persona_id
WHERE p.sexe='F' AND c.tipus='T';
```

### Selecciona els noms dels 3 municipis amb més vots valids:
```
SELECT m.nom, em.vots_valids
FROM municipis m
INNER JOIN eleccions_municipis em ON em.municipi_id=m.municipi_id
ORDER BY em.vots_valids DESC
LIMIT 3;
```

### Mostra el nom llarg dels partits que contenen "PARTIDO" presentats a l'any 2019:
 
```
SELECT c.nom_llarg AS 'Nom complert partit', e.nom AS 'Nom eleccions'
FROM candidatures c 
INNER JOIN eleccions e ON e.eleccio_id=c.eleccio_id
WHERE c.nom_llarg like '%PARTIDO%' AND e.any=2019;
```
