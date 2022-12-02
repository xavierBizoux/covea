# Informations intéressantes

## Développer des rapports

- [Best Practice](https://communities.sas.com/html/assets/breports/know-your-audience.html)

## Data-Driven Content

- Examples:
  - Simple avec format numérique
    - [Screenshot](./images/DDCExample.png)
    - [Code](./formatTable.html)
  - Tableau en escalier
    - [Screenshot](./images/Stairs.png)
    - [Code](./stairsTable.html)
- [Documentation](https://go.documentation.sas.com/doc/en/vacdc/8.5/varef/n109mqtyl6quiun1mwfgtcn2s68b.htm)
- [Bootstrap Framework](https://getbootstrap.com/)
- [Apprendre HTML](https://www.w3schools.com/html/)
- [Outil de développement HTML en ligne](https://jsfiddle.net/)

## Formats

- Définir une librairie de formats dans Viya: [blog](https://communities.sas.com/t5/SAS-Communities-Library/SAS-Viya-Managing-User-defined-Formats/ta-p/518884)
- Créer un format dans une librairie existante:

  ```sas
  /* Créer une session CAS*/
  cas casauto;

  /* Créer un format dans une librairie existante */
  proc format lib=work.formats casfmtlib="covea";
    picture invoice low-high='$99k' (prefix='$' multiplier=.001);
  run;

  /* Mettre à disposition de tous les utilisateurs */
  cas casauto promotefmtlib fmtlibname=covea replace;

  /* Charger les données avec le format */
  proc casutil;
  format invoice invoice.;
  droptable casdata="cars" quiet;
  load data=sashelp.cars casdata="cars" promote;
  run;
  ```

## Charger des tables en utilisant un job

- [Documentation](https://go.documentation.sas.com/doc/en/pgmsascdc/9.4_3.5/jobexecug/titlepage.htm )
- Code example: [blog](https://blogs.sas.com/content/sgf/2019/06/21/learn-the-three-easiest-ways-to-load-data-into-cas-tables/)
- [Filename filesrvc](https://go.documentation.sas.com/doc/en/pgmsascdc/9.4_3.5/lestmtsglobal/p0qapul7pyz9hmn0zfoefj0c278a.htm)
- Sample code: load a table into CAS

```sas
filename import filesrvc "&_WEBIN_FILEURI";

cas mySession sessopts=(caslib="casuser");
libname casuser cas caslib="casuser";

proc casutil;
droptable casdata="import" quiet;
run;
proc import datafile=import out=casuser.import (promote=yes) dbms=csv;
run;
options obs=10;
proc print data=casuser.import ;
run;
```