# Examen-SQL-Databases-
Examen SQL Databases 


1 Geef de namen van de Franstalige personen van wie de naam begint met een 'M'.

SELECT persoon_naam 
FROM persoon
WHERE persoon_taal = 'F'
AND persoon_naam LIKE 'M%'


2 Geef de referenties en de namen van de personen, gesorteerd volgens het referentienummer van hoog naar laag. Gebruik bij het sorteren een nummer in plaats van een kolomnaam.

SELECT persoon_id, persoon_naam
FROM persoon
ORDER BY  1 DESC


3 Geef de productcode en het productnummer van de producten waarbij een locatie is ingevuld.

SELECT product_code, product_nr
FROM product
WHERE locatie_nr IS NOT NULL


4 Geef de productcode en het productnummer van de producten met een productnummer tussen de 5 en 15 en de producten met een productnummer tussen de 30 en 50.

SELECT product_code, product_nr
FROM product
WHERE product_nr BETWEEN 5 AND 15
OR product_nr BETWEEN 30 AND 50


5 Geef de productcode en het productnummer van de producten met productnummer 5,10,20,25. Maak gebruik van IN.

SELECT product_code, product_nr
FROM product
WHERE product_nr IN(5, 10, 15, 20, 25)


6 Geef de naam en voornaam van de personen waarbij de laatste letter van de achternaam een 's' is en de eerste letter van de voornaam een 'f' of een 'p'.

SELECT persoon_naam, persoon_voornaam
FROM persoon
WHERE RIGHT(UPPER(persoon_naam),1) = 'S'
AND LEFT(UPPER(persoon_voornaam),1) IN ('F','P')


7 Geef de namen van de personen van de Nederlandstalige en/of Franstalige taalgroep, hun geslacht ('man' of 'vrouw') en hun taal ('Nederlandstalig' of 'Franstalig').

SELECT persoon_naam Naam, 'man' Geslacht, 'Nederlandstalig' Taal
FROM persoon
WHERE persoon_geslacht = 1
AND persoon_taal = 'N'
UNION
SELECT persoon_naam Naam, 'vrouw' Geslacht, 'Nederlandstalig' Taal
FROM persoon
WHERE persoon_geslacht = 2
AND persoon_taal ='N'
UNION
SELECT persoon_naam Naam, 'man' Geslacht, 'Franstalig' Taal
FROM persoon
WHERE persoon_geslacht = 1
AND persoon_taal = 'F'
UNION
SELECT persoon_naam Naam, 'vrouw' Geslacht, 'Franstalig' Taal
FROM persoon
WHERE persoon_geslacht = 2
AND persoon_taal ='F'

8 Hoeveel Franstalige personen zijn er?

SELECT COUNT(*) persoon_taal
FROM persoon
WHERE persoon_taal = 'F'


9 Geef de productcode en het productnummer van de producten waarbij geen oorsprong is ingevuld.

SELECT product_code, product_nr
FROM product
WHERE oorsprong_nr IS NULL


10 Geef de productcode, het productnummer en de naam van de locatie. In de gevallen dat de naam van de locatie niet is ingevuld, moet er in die plaats geen worden vermeld.

SELECT product.product_code, product.product_nr, coalesce(locatie.locatie_naam, 'geen')
FROM product LEFT OUTER JOIN locatie
ON (product.locatie_nr = locatie.locatie_id)


11 geef de namen van de locaties waarvan de naam uit 16 letters bestaat, maar waarin het woord 'Magazijn' voorkomt.

SELECT locatie_naam
FROM locatie
WHERE LENGTH(locatie_naam) = 16
AND locatie_naam LIKE '%Magazijn%'


12 Geef de productcode en het productnummer van de producten met productcode 'HA' of 'NE' maar waarvan het productnummer kleiner is dan 15.

SELECT product_code, product_nr
FROM product
WHERE product_code IN ('HA', 'NE')
AND product_nr < 15

    
13 Geef de productcode en het nummer van die producten waarbij de naam van de locatie begint met 'maga'. Maak gebruik van de principes van Subquery.

SELECT product.product_code, product.product_nr
FROM product
WHERE EXISTS 	(SELECT locatie.locatie_naam
		FROM locatie 
		WHERE locatie.locatie_id = product.locatie_nr
		AND LOWER(locatie.locatie_naam) LIKE 'maga%')


14 Verhuis alle producten van magazijn 1 naar magazijn 2.

UPDATE product
SET locatie_nr = 2
WHERE locatie_nr = 1


15 Verwijder alle producten van Millie.

DELETE FROM product 
WHERE oorsprong _nr = 14

