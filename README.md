# Informations intéressantes

## Développer des rapports

- [Best Practice](https://communities.sas.com/html/assets/breports/know-your-audience.html)

## Data-Driven Content

- Example:
  - [screenshot](./images/DDCExample.png)
  - [Code](./formatTable.html)
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
