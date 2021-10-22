/*******************sequences**********************************************/
CREATE SEQUENCE seqART
 START WITH     1
 INCREMENT BY   1
 NOCACHE
 NOCYCLE;
CREATE SEQUENCE seqSPEC
 START WITH     1
 INCREMENT BY   1
 NOCACHE
 NOCYCLE;
 CREATE SEQUENCE seqLIEU
 START WITH     17
 INCREMENT BY   1
 NOCACHE
 NOCYCLE;
 CREATE SEQUENCE seqBIL
 START WITH     1
 INCREMENT BY   1
 NOCACHE
 NOCYCLE;
CREATE SEQUENCE seqRUB
 START WITH     1
 INCREMENT BY   1
 NOCACHE
 NOCYCLE;
CREATE SEQUENCE seqCLI
 START WITH     1
 INCREMENT BY   1
 NOCACHE
 NOCYCLE;

/***********************  CREATION DES TABLES WITH CONTRAINT  *************************/
CREATE TABLE CLIENT
	(idClt INTEGER  PRIMARY KEY,
	nomClt VARCHAR2(20) NOT NULL,
    prenomClt VARCHAR2(20) NOT NULL,
	tel NUMBER(10) NOT NULL,
	email VARCHAR(50) NOT NULL, 
    motP VARCHAR2(30) NOT NULL,    
CONSTRAINT chk_Emails_Check CHECK (email LIKE '%_@%_._%'),
CONSTRAINT chk_Tel CHECK(tel BETWEEN 10000000 AND 999999999),
CONSTRAINT chk_motP CHECK( motP like '%[0-9]%' AND motP  
like '%[A-Z]%' AND  motP  like '%[!@#$%^&*()-_+=.,;:~]%' AND LENGTH( motP )>=(8))
);
/*******************************Constraint*********************************/
ALTER TABLE LIEU ADD CONSTRAINT chk_cap_lieu  
CHECK (capacite BETWEEN 100 AND 2000 );
ALTER TABLE ARTISTE ADD CONSTRAINT chk_spec_artiste   
CHECK (specialite in('danseur','acteur','musicien','magicien','imitateur','humoriste','chanteur'));
ALTER TABLE RUBRIQUE ADD CONSTRAINT chk_type_rubrique 
CHECK(type in('comédie','theatre','dance',' imitation','magie', 'musique','chant'));
ALTER TABLE BILLET ADD CONSTRAINT chk_cat_billet 
CHECK(categorie in('gold','silver','normale'));
 /********************INSERT ARTISTE ***********************************/
INSERT INTO ARTISTE (IDART, NOMART,PRENOMART, SPECIALITE) 
VALUES (seqART.nextval,'Rochdi','Alouen','danseur');
INSERT INTO ARTISTE (IDART, NOMART, PRENOMART, SPECIALITE)
VALUES (seqART.nextval,'Hichem','Rostom','acteur');
INSERT INTO ARTISTE (IDART, NOMART, PRENOMART, SPECIALITE)
VALUES (seqART.nextval,'Fathi','Hadeoui','acteur');
INSERT INTO ARTISTE (IDART, NOMART, PRENOMART, SPECIALITE)
VALUES (seqART.nextval,'Kaouther','Bardi','acteur');
INSERT INTO ARTISTE (IDART, NOMART, PRENOMART, SPECIALITE)
VALUES (seqART.nextval,'Mahdi','Mweli','musicien');
INSERT INTO ARTISTE (IDART, NOMART, PRENOMART, SPECIALITE)
VALUES (seqART.nextval,'Lotfi ','Bouchnek','musicien');
INSERT INTO ARTISTE (IDART, NOMART, PRENOMART, SPECIALITE)
VALUES (seqART.nextval,'Kader ','Bweno','magicien');
INSERT INTO ARTISTE (IDART, NOMART, PRENOMART, SPECIALITE)
VALUES (seqART.nextval,'Wassim','Migalo','imitateur');
INSERT INTO ARTISTE (IDART, NOMART, PRENOMART, SPECIALITE)
VALUES (seqART.nextval,'Jaloul','Jlassi','imitateur');
INSERT INTO ARTISTE (IDART, NOMART, PRENOMART, SPECIALITE)
VALUES (seqART.nextval,'Karim ','Gharbi','humoriste');
INSERT INTO ARTISTE (IDART, NOMART, PRENOMART, SPECIALITE)
VALUES (seqART.nextval,'Jafer ','Gesmi','humoriste');
INSERT INTO ARTISTE (IDART, NOMART, PRENOMART, SPECIALITE)
VALUES (seqART.nextval,'wajiha','jandoubi','humoriste');
INSERT INTO ARTISTE (IDART, NOMART, PRENOMART, SPECIALITE)
VALUES (seqART.nextval,'amna','faket','chanteur');
INSERT INTO ARTISTE (IDART, NOMART, PRENOMART, SPECIALITE)
VALUES (seqART.nextval,'Yosra','Mahnouch','chanteur');
INSERT INTO ARTISTE (IDART, NOMART, PRENOMART, SPECIALITE)
VALUES (seqART.nextval,'Saber','Rbeai','chanteur');

/************************INSERT SPECTACLE*************************/
INSERT INTO SPECTACLE (IDSPEC, TITRE, DATES, H_DEBUT, DUREES, NBRSPECTATEUR, IDLIEU) 
VALUES (seqSPEC.nextval,'Big Bossa',TO_DATE('02/02/2021','dd/mm/yyyy'),10,2,300,15);
INSERT INTO SPECTACLE (IDSPEC, TITRE, DATES, H_DEBUT, DUREES, NBRSPECTATEUR, IDLIEU) 
VALUES (seqSPEC.nextval,'100 %Tunisia',TO_DATE('02/02/2021','dd/mm/yyyy'),15,2,300,15);
INSERT INTO SPECTACLE (IDSPEC, TITRE, DATES, H_DEBUT, DUREES, NBRSPECTATEUR, IDLIEU) 
VALUES (seqSPEC.nextval,'super star saber rbaii',TO_DATE('02/02/2021','dd/mm/yyyy'),17.10,3,300,15);
INSERT INTO SPECTACLE (IDSPEC, TITRE, DATES, H_DEBUT, DUREES, NBRSPECTATEUR, IDLIEU) 
VALUES (seqSPEC.nextval,'made in tunisia',TO_DATE('02/02/2021','dd/mm/yyyy'),21.20,2.30,300,15);

INSERT INTO SPECTACLE (IDSPEC, TITRE, DATES, H_DEBUT, DUREES, NBRSPECTATEUR, IDLIEU) 
VALUES (seqSPEC.nextval,'Big Bossa',TO_DATE('03/02/2021','dd/mm/yyyy'),10,2,1500,8);
INSERT INTO SPECTACLE (IDSPEC, TITRE, DATES, H_DEBUT, DUREES, NBRSPECTATEUR, IDLIEU) 
VALUES (seqSPEC.nextval,'100 %Tunisia',TO_DATE('03/02/2021','dd/mm/yyyy'),15,2,1500,8);
INSERT INTO SPECTACLE (IDSPEC, TITRE, DATES, H_DEBUT, DUREES, NBRSPECTATEUR, IDLIEU) 
VALUES (seqSPEC.nextval,'super star saber rbaii',TO_DATE('03/02/2021','dd/mm/yyyy'),17.10,3,1500,8);
INSERT INTO SPECTACLE (IDSPEC, TITRE, DATES, H_DEBUT, DUREES, NBRSPECTATEUR, IDLIEU) 
VALUES (seqSPEC.nextval,'made in tunisia',TO_DATE('03/02/2021','dd/mm/yyyy'),21.20,2.30,1500,8);



/*++++++++++++++++++++++++++++++++++++++++++++++lieu++++++++++++++++++++++++++++++++++++++++++++*/
/***********************triger ajouter lieu 100-2000 ******************/
CREATE OR REPLACE TRIGGER Tajoutlieu 
BEFORE INSERT ON lieu
FOR EACH ROW 
DECLARE
BEGIN
IF :NEW.capacite<100 OR :NEW.capacite>2000 then 
RAISE_APPLICATION_ERROR(-20100,'la capacité doit etre comprie entre 100 et 2000');
END IF;
END;
/*modifier lieu */
CREATE OR REPLACE PROCEDURE P_MODIFIER_LIEU (vidlieu lieu.idlieu%TYPE , vnomL  lieu.nomlieu%TYPE,vcapacite lieu.capacite%TYPE ) IS

id lieu.idlieu%TYPE ;
BEGIN
IF VNOML IS NOT NULL THEN 
UPDATE LIEU SET nomlieu =vnomL  WHERE vidlieu=IDLIEU;
END IF;
IF vcapacite IS NOT NULL THEN 
UPDATE LIEU SET capacite = vcapacite  WHERE vidlieu=IDLIEU;
END IF;

SELECT idlieu into id FROM LIEU WHERE vidlieu=IDLIEU ;
EXCEPTION WHEN NO_DATA_FOUND THEN 
RAISE_APPLICATION_ERROR(-20120,'le lieu n''est pas disponible ');
     
END;


/////////////////////////////////////////////////*recherhcier lieu *//////////////////////



CREATE OR REPLACE PROCEDURE P_CHERCHER_LIEU ( vnomL  lieu.nomlieu%TYPE,vcapacite lieu.capacite%TYPE  ) IS

 
CURSOR curLieu IS 
SELECT * FROM LIEU
WHERE(   vnomL is  NOT NULL  AND   UPPER(vnomL) LIKE UPPER(nomLieu)     );

CURSOR curLieuCAP IS 
SELECT * FROM LIEU
WHERE   ( vcapacite = CAPACITE AND  vcapacite IS NOT NULL );

CURSOR curLieuCAP_NOM IS 
SELECT * FROM LIEU
WHERE   ( vcapacite = CAPACITE AND  UPPER(vnomL) LIKE UPPER(nomLieu)  );


supp char(4) :='SUPP';
vcurLieuCAP_NOM curLieuCAP_NOM%ROWTYPE ;
vcurlieuCAP curLieuCAP%ROWTYPE ;
vcurlieu curLieu%ROWTYPE ;
exvide EXCEPTION;
BEGIN
IF vcapacite is null THEN
OPEN curLieu ;
DBMS_OUTPUT.PUT_LINE('Les caracteristiques des lieux  sont : ' );
LOOP
FETCH curLieu INTO vcurlieu ;
EXIT WHEN curLieu%NOTFOUND OR curLieu%NOTFOUND IS NULL ;
IF vcurlieu.SUPPLOGIC NOT LIKE supp or  vcurlieu.SUPPLOGIC  is null THEN 
DBMS_OUTPUT.PUT_LINE(' id : '|| vcurlieu.idlieu ||', nom :'|| vcurlieu.nomlieu|| ',adresse : '||
vcurlieu.adresse||' ville :'|| vcurlieu.ville|| ' capacité  '|| vcurlieu.capacite ||'') ;
END IF;
END LOOP ;
IF curLieu%NOTFOUND THEN RAISE exvide;
END IF;
CLOSE curLieu ;
END IF ;
IF vnomL IS NULL THEN
OPEN curlieuCAP ;
DBMS_OUTPUT.PUT_LINE('Les caracteristiques des lieux  sont : ' );
LOOP
FETCH curlieuCAP INTO vcurlieuCAP ;
EXIT WHEN curlieuCAP%NOTFOUND OR curlieuCAP%NOTFOUND IS NULL ;
IF vcurlieuCAP.SUPPLOGIC NOT LIKE supp or  vcurlieuCAP.SUPPLOGIC  is null THEN 
DBMS_OUTPUT.PUT_LINE(' id : '|| vcurlieuCAP.idlieu ||', nom :'|| vcurlieuCAP.nomlieu|| ',adresse : '||
vcurlieuCAP.adresse||' ville :'|| vcurlieuCAP.ville|| ' capacité  '|| vcurlieuCAP.capacite ||'') ;
END IF;
END LOOP ;
IF curlieuCAP%NOTFOUND THEN RAISE exvide;
END IF;
close curlieuCAP ;
END IF ;
IF vcapacite IS  NOT NULL AND vnomL IS NOT NULL  THEN
OPEN curLieuCAP_NOM ;
DBMS_OUTPUT.PUT_LINE('Les caracteristiques des lieux  sont : ' );
LOOP
FETCH curLieuCAP_NOM INTO vcurLieuCAP_NOM ;
EXIT WHEN curLieuCAP_NOM%NOTFOUND OR curLieuCAP_NOM%NOTFOUND IS NULL ;
IF VcurLieuCAP_NOM.SUPPLOGIC NOT LIKE supp or  VcurLieuCAP_NOM.SUPPLOGIC  is null THEN 
DBMS_OUTPUT.PUT_LINE(' id : '|| vcurLieuCAP_NOM.idlieu ||', nom :'|| vcurLieuCAP_NOM.nomlieu|| ',adresse : '||
vcurLieuCAP_NOM.adresse||' ville :'|| vcurLieuCAP_NOM.ville|| ' capacité  '|| vcurLieuCAP_NOM.capacite ||'') ;
END IF;
END LOOP ;
IF curLieuCAP_NOM%NOTFOUND THEN RAISE exvide;
END IF;
close curLieuCAP_NOM ;
END IF ;
EXCEPTION WHEN exvide THEN 
DBMS_OUTPUT.PUT_LINE('pas de lieu avec cette caracteristique ');
END ;
/************suprrimer lieu *///////////


CREATE OR REPLACE PROCEDURE SupprimerLieu (vidlieu lieu.idLieu%TYPE) IS
BEGIN
DELETE FROM LIEU 
WHERE vidlieu=idlieu ;
DBMS_OUTPUT.PUT_LINE('Le lieu a été supprimé PHYSIQUEMENT');
END;


CREATE OR REPLACE TRIGGER TRI_NOSPEC_DISPO
BEFORE DELETE
ON LIEU
FOR EACH ROW         
DECLARE
CURSOR CURLIEU IS
SELECT * 
FROM SPECTACLE
WHERE  IDLIEU = :NEW.IDLIEU  ;

BEGIN
OPEN CURLIEU ;
IF CURLIEU%FOUND THEN 
UPDATE LIEU SET SUPPLOGIC ='supp' WHERE IDLIEU=:OLD.IDLIEU;
 RAISE_APPLICATION_ERROR(-20115,'LE lieu et supprimer logiquement ');
END IF;
CLOSE CURLIEU ;
END; 
 

/********chercher un specatcle *///////////
CREATE OR REPLACE PROCEDURE P_CHERCHER_SPEC_TITRE (
            vtitre  SPECTACLE.TITRE%TYPE,
            vidspec  SPECTACLE.IDSPEC%TYPE) IS
CURSOR curtitre IS 
SELECT * FROM SPECTACLE
WHERE( UPPER(TITRE) LIKE UPPER(vtitre));
vcurtitre curtitre%ROWTYPE ;
CURSOR curid IS 
SELECT * FROM SPECTACLE
WHERE( vidspec=IDSPEC);
vcurid curid%ROWTYPE ;
CURSOR curidtitre IS 
SELECT * FROM SPECTACLE
WHERE( vidspec=IDSPEC and UPPER(TITRE) LIKE UPPER(vtitre) );
VCURIDTITRE curidtitre%ROWTYPE ;
exvide EXCEPTION;
BEGIN
if vidspec is null then 
 OPEN curtitre ;
  DBMS_OUTPUT.PUT_LINE('Les de specatacle sont  : ' );
LOOP
 FETCH curtitre INTO vcurtitre ;
 EXIT WHEN curtitre%NOTFOUND OR curtitre%NOTFOUND IS NULL ;
 DBMS_OUTPUT.PUT_LINE(' id : '|| vcurtitre.IDSPEC ||', TITRE :'|| vcurtitre.TITRE|| ',DATES : '||
 vcurtitre.DATES||' H_DEBUT :'|| vcurtitre.H_DEBUT|| ' DUREES  '|| vcurtitre.DUREES ||
 ' NBRSPECTATEUR'|| vcurtitre.NBRSPECTATEUR ||'' ) ;
 END LOOP ;
IF curtitre%NOTFOUND THEN RAISE exvide;
END IF;
CLOSE curtitre ;
end if ;
if vtitre is null then 
OPEN curid ; 
LOOP
 FETCH curid INTO vcurid ;
 EXIT WHEN curid%NOTFOUND OR curid%NOTFOUND IS NULL ;
 DBMS_OUTPUT.PUT_LINE(' id : '|| vcurid.IDSPEC ||', TITRE :'|| vcurid.TITRE|| ',DATES : '||
 vcurid.DATES||' H_DEBUT :'|| vcurid.H_DEBUT|| ' DUREES  '|| vcurid.DUREES ||
 ' NBRSPECTATEUR'|| vcurid.NBRSPECTATEUR ||'' ) ;
 END LOOP ;
IF curid%NOTFOUND THEN RAISE exvide;
END IF;
CLOSE curid ;
end if ;
if vidspec is not null and  vtitre is not null   then 
 OPEN curidtitre ;
  DBMS_OUTPUT.PUT_LINE('Les de specatacle sont  : ' );
LOOP
 FETCH curidtitre INTO vcuridtitre ;
 EXIT WHEN curtitre%NOTFOUND OR curidtitre%NOTFOUND IS NULL ;
 DBMS_OUTPUT.PUT_LINE(' id : '|| vcuridtitre.IDSPEC ||', TITRE :'|| vcuridtitre.TITRE|| ',DATES : '||
 vcuridtitre.DATES||' H_DEBUT :'|| vcuridtitre.H_DEBUT|| ' DUREES  '|| vcuridtitre.DUREES ||
 ' NBRSPECTATEUR'|| vcuridtitre.NBRSPECTATEUR ||'' ) ;
 END LOOP ;
IF curidtitre%NOTFOUND THEN RAISE exvide;
END IF;
CLOSE curtitre ;
end if ;
EXCEPTION WHEN exvide THEN 
DBMS_OUTPUT.PUT_LINE('pas de spectacle');
END;
/**************************triger pour le supprimer logic ************************/
CREATE OR REPLACE TRIGGER TRI_NOSPEC_DISPO
BEFORE DELETE
ON LIEU
FOR EACH ROW         
DECLARE
CURSOR CURLIEU IS
SELECT * 
FROM SPECTACLE
WHERE  IDLIEU = :OLD.IDLIEU  ;

BEGIN
OPEN CURLIEU ;
IF CURLIEU%FOUND THEN 
UPDATE LIEU SET SUPPLOGIC ='supp' WHERE IDLIEU=:OLD.IDLIEU;
 RAISE_APPLICATION_ERROR(-20115,'LE lieu et supprimer logiquement ');
END IF;
CLOSE CURLIEU ;
END; 
 

/*++++++++++++++++++++++++++++++++++++++++++++Spectacle +++++++++++++++++++++++++++++++++++++++++*/
/****************************ajouter spectacle *************************************/
CREATE OR REPLACE PROCEDURE P_AJOUTER_SPEC (
          vtitre IN SPECTACLE.TITRE%TYPE,
          vdate IN SPECTACLE.DATES%TYPE,
          vh_debut IN SPECTACLE.H_DEBUT%TYPE,
          vdurees IN SPECTACLE.DUREES%TYPE,
          vnbrSpectateur IN SPECTACLE.NBRSPECTATEUR%TYPE,
          vidlieu  IN SPECTACLE.IDLIEU%TYPE ) IS
BEGIN           
INSERT INTO spectacle 
VALUES (seqSPEC.NEXTVAL,vtitre,vdate,vh_debut,vdurees,vnbrSpectateur,vidlieu);
END;

/**************************triger (verifer capacité lieu  <  nombre spectacle  ) **********************/
CREATE OR REPLACE TRIGGER TRI_CAPACITE_NBRSPECTACLE 
BEFORE INSERT
ON spectacle
FOR EACH ROW         
DECLARE
vcapacite LIEU.CAPACITE%TYPE ;
BEGIN
SELECT CAPACITE INTO vcapacite 
FROM LIEU
WHERE IDLIEU = :NEW.IDLIEU;
IF vcapacite < :NEW.NBRSPECTATEUR THEN 
RAISE_APPLICATION_ERROR(-20110,'La capacité est inferieur au nombre des spectateurs');
END IF;
END;
/********************************triger spectacle insertionn (verification la disponibilté du lieu et spectacle )***************/

CREATE OR REPLACE TRIGGER TRI_SPECTACLE 
BEFORE INSERT
ON spectacle
FOR EACH ROW         
DECLARE
CURSOR CURSPEC IS SELECT TITRE,DATES,H_DEBUT,DUREES  
FROM SPECTACLE
WHERE TITRE LIKE :NEW.TITRE AND DATES = :NEW.DATES ;

CURSOR CURLIEU IS SELECT IDLIEU,DATES,H_DEBUT,DUREES  
FROM SPECTACLE
WHERE  IDLIEU = :NEW.IDLIEU  AND DATES = :NEW.DATES ;

vcurlieu CURLIEU%ROWTYPE ;
vcurspec CURSPEC%ROWTYPE ;

BEGIN
OPEN CURLIEU ;
LOOP
FETCH CURLIEU INTO vcurlieu ;
EXIT WHEN CURLIEU%NOTFOUND OR CURLIEU%NOTFOUND IS NULL ; 
IF (:NEW.H_DEBUT + :NEW.DUREES ) BETWEEN  vcurlieu.H_DEBUT AND (vcurlieu.H_DEBUT+vcurlieu.DUREES)
THEN  RAISE_APPLICATION_ERROR(-20111,'cette temps est  occupé ');
END IF;
END LOOP ;
CLOSE CURLIEU ;
 
OPEN CURSPEC ;
LOOP
FETCH CURSPEC INTO vcurspec ;
EXIT WHEN CURSPEC%NOTFOUND OR CURSPEC%NOTFOUND IS NULL ; 
IF (:NEW.H_DEBUT + :NEW.DUREES ) BETWEEN  vcurlieu.H_DEBUT AND (vcurlieu.H_DEBUT+vcurlieu.DUREES)
then  RAISE_APPLICATION_ERROR(-20112,'ce spectacle n''est pas disponible    ');
END IF;
END LOOP ;
CLOSE CURSPEC ;
END; 
/*************************triger(la date ajouter est supperieur au date d'aujourduit ******************/

CREATE OR REPLACE TRIGGER TRI_DATENOW 
BEFORE INSERT
ON SPECTACLE
FOR EACH ROW         
DECLARE
BEGIN 
IF CURRENT_DATE  > :NEW.DATES THEN 
RAISE_APPLICATION_ERROR(-20113,'la date est  dépassée ');
END IF;
END;

/******************************** procedure anuuler specatacle avec verification de disponibilité **************/
CREATE OR REPLACE PROCEDURE P_ANNULER_SPEC (
           vidspec SPECTACLE.IDSPEC%TYPE) IS

vvidspec SPECTACLE.IDSPEC%TYPE;
exvide EXCEPTION;
BEGIN
SELECT IDSPEC  INTO vvidspec
    FROM SPECTACLE
    WHERE IDSPEC = vidspec;       
IF vvidspec IS NULL  THEN RAISE exvide;
ELSE      
UPDATE SPECTACLE SET H_DEBUT = NULL
WHERE IDSPEC = vidspec;
dbms_output.put_line('le spectacle est anuulée');
END IF;
EXCEPTION WHEN exvide THEN 
DBMS_OUTPUT.PUT_LINE('pas de spectacle avec cette id ');        
END;
/*ALTER TABLE SPECTACLE
DROP CONSTRAINT SYS_C007522;*/

/************** recherche spectacle avec titre  ****************************
CREATE OR REPLACE PROCEDURE P_CHERCHER_SPEC_TITRE (
            vtitre  SPECTACLE.TITRE%TYPE) IS

CURSOR curtitre IS 
SELECT * FROM SPECTACLE
WHERE( UPPER(TITRE) LIKE UPPER(vtitre));
vcurtitre curtitre%ROWTYPE ;
exvide EXCEPTION;
BEGIN

 OPEN curtitre ;
  DBMS_OUTPUT.PUT_LINE('Les de specatacle sont  : ' );
LOOP
 FETCH curtitre INTO vcurtitre ;
 EXIT WHEN curtitre%NOTFOUND OR curtitre%NOTFOUND IS NULL ;
 DBMS_OUTPUT.PUT_LINE(' id : '|| vcurtitre.IDSPEC ||', TITRE :'|| vcurtitre.TITRE|| ',DATES : '||
 vcurtitre.DATES||' H_DEBUT :'|| vcurtitre.H_DEBUT|| ' DUREES  '|| vcurtitre.DUREES ||
 ' NBRSPECTATEUR'|| vcurtitre.NBRSPECTATEUR ||'' ) ;
 END LOOP ;
IF curtitre%NOTFOUND THEN RAISE exvide;
END IF;
CLOSE curtitre ;
EXCEPTION WHEN exvide THEN 
DBMS_OUTPUT.PUT_LINE('pas de spectacle');
END;
/*********************************recherche spectacle avec id ************************************/
set serveroutput on; 
CREATE OR REPLACE PROCEDURE P_CHERCHER_SPEC_ID (
            vidspec  SPECTACLE.IDSPEC%TYPE) IS

CURSOR curid IS 
SELECT * FROM SPECTACLE
WHERE( vidspec=IDSPEC);
vcurid curid%ROWTYPE ;
exvide EXCEPTION;
BEGIN

 OPEN curid ;
 
LOOP
 FETCH curid INTO vcurid ;
 EXIT WHEN curid%NOTFOUND OR curid%NOTFOUND IS NULL ;
 DBMS_OUTPUT.PUT_LINE(' id : '|| vcurid.IDSPEC ||', TITRE :'|| vcurid.TITRE|| ',DATES : '||
 vcurid.DATES||' H_DEBUT :'|| vcurid.H_DEBUT|| ' DUREES  '|| vcurid.DUREES ||
 ' NBRSPECTATEUR'|| vcurid.NBRSPECTATEUR ||'' ) ;
 END LOOP ;
IF curid%NOTFOUND THEN RAISE exvide;
END IF;
CLOSE curid ;
EXCEPTION WHEN exvide THEN 
DBMS_OUTPUT.PUT_LINE('pas de spectacle');
END ;


/******************* modifier spectacle*******************************/
CREATE OR REPLACE PROCEDURE P_MODIFIER_SPEC (   vidspec  SPECTACLE.IDSPEC%TYPE,
                                                vtitre  SPECTACLE.TITRE%TYPE,
                                                vDATES SPECTACLE.DATES%TYPE,                                             
                                                vH_DEBUT  SPECTACLE.H_DEBUT%TYPE,
                                                vDUREES SPECTACLE.DUREES%TYPE,
                                                vNBRSPECTATEUR  SPECTACLE.NBRSPECTATEUR%TYPE,
                                                vIDLIEU  SPECTACLE.IDLIEU%TYPE ) IS


id lieu.idlieu%TYPE ;
BEGIN
IF vtitre IS NOT NULL THEN 
UPDATE SPECTACLE SET titre =vtitre  WHERE vidspec=idspec;
END IF;
IF vDATES IS NOT NULL THEN 
UPDATE SPECTACLE SET DATES = vDATES  WHERE vidspec=idspec;
END IF;
IF vH_DEBUT IS NOT NULL THEN 
UPDATE SPECTACLE SET H_DEBUT =vH_DEBUT  WHERE vidspec=idspec;
END IF;
IF vDUREES IS NOT NULL THEN 
UPDATE SPECTACLE SET DUREES =vDUREES  WHERE vidspec=idspec;
END IF;

IF vNBRSPECTATEUR IS NOT NULL THEN 
UPDATE SPECTACLE SET NBRSPECTATEUR =vNBRSPECTATEUR  WHERE vidspec=idspec;
END IF;
IF vIDLIEU IS NOT NULL THEN 
UPDATE SPECTACLE s SET s.IDLIEU =vIDLIEU  WHERE vidspec=idspec;
END IF;

SELECT idspec into id FROM SPECTACLE WHERE vidspec=idspec;
EXCEPTION WHEN NO_DATA_FOUND THEN 
RAISE_APPLICATION_ERROR(-20120,'le spectacle  n''est pas disponible ');
     
END;

set serveroutput on;
BEGIN
P_AJOUTER_SPEC ('made in tunisia', TO_DATE('05/02/2021', 'DD/MM/YYYY'),21,2,500,9);/*insertion shih */
END;

set serveroutput on;
BEGIN
P_MODIFIER_SPEC(60,'&titre_spectacle','&date_spectacle',&heure_debut,&duree,&nbre_spectateurs,&id_lieu);/*on peut faire la modification par le nom ou/et la capacité */
END;    




 
 