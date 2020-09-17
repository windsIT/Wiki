---
title: MAWGT861 SQL Log
description: 
published: true
date: 2020-09-02T07:29:34.834Z
tags: 
editor: undefined
---

```plsql
-- CIMSFC, Message ID ( '07701' - '07799' , Max Use: 07733)

-- =========================================================================================================
-- MAWGT861,v2.0.4.9,2020/06/19
-- =========================================================================================================
-- CIMSFC
UPDATE CIMAPPLICATION SET VERSION ='2.0.4.9',versiondate='2020/06/19' WHERE APID='MAWGT861';
COMMIT;

-- =========================================================================================================
-- MAWGT861,v2.0.4.8,2020/05/11
-- =========================================================================================================
-- CIMSFC
UPDATE CIMAPPLICATION SET VERSION ='2.0.4.8',versiondate='2020/05/11' WHERE APID='MAWGT861';
COMMIT;

-- New INI 
INSERT INTO CIMAPINI(APID, SECTION, ITEM, VALUE, REMARK)
  VALUES('MAWGT861', 'PROCESS', 'AIRFREIGHTCMD', '', 'Air Freight Shipping Type Command. Default ""(Empty): Disable Air Freight Mode.');

INSERT INTO CIMAPINI(APID, SECTION, ITEM, VALUE, REMARK)
  VALUES('MAWGT861', 'PROCESS', 'SHIPTYPEPALLETYPEMAP', '', 'ShipType:PalletType Map; Default ""; Ex:0:P; 1:P; 2:P; 3:A
(ShipType: 0.Not Defined, 1.Land Transportation, 2.Sea Shipping, 3.Air Freight)'); 
COMMIT;

-- New Message
INSERT INTO CIMMESSAGE(MESSAGEID, LANGUAGE, MODULE, DESCRIPTION)
 VALUES('SFCF07728', 1, 'SFC', 'Please go through the Airfreight weighing process, input [%$] command Firstly!');

INSERT INTO CIMMESSAGE(MESSAGEID, LANGUAGE, MODULE, DESCRIPTION)
 VALUES('SFCI07729', 1, 'SFC', 'IF Air Freight,Please scan Air Command[%$] firstly; Else Please scan palletid...'); 
INSERT INTO CIMMESSAGE(MESSAGEID, LANGUAGE, MODULE, DESCRIPTION)
 VALUES('SFCI07729', 3, 'SFC', '如果是空运栈板,请先输入空运指令[%$],否则请直接输入PalletID.....');

 INSERT INTO CIMMESSAGE(MESSAGEID, LANGUAGE, MODULE, DESCRIPTION)
 VALUES('SFCF07730', 1, 'SFC', 'Can not find MO Shipping Type by PalletID[%$] !'); 

 INSERT INTO CIMMESSAGE(MESSAGEID, LANGUAGE, MODULE, DESCRIPTION)
 VALUES('SFCF07731', 1, 'SFC', 'The same pallet[%$] cannot mix multiple Shipping Type !');

 INSERT INTO CIMMESSAGE(MESSAGEID, LANGUAGE, MODULE, DESCRIPTION)
 VALUES('SFCF07732', 1, 'SFC', 'Input Airfreight Command[%$], But did not maintain its Pallet Type in INI[PROCESS]/[SHIPTYPEPALLETYPEMAP]!');

 INSERT INTO CIMMESSAGE(MESSAGEID, LANGUAGE, MODULE, DESCRIPTION)
 VALUES('SFCF07733', 1, 'SFC', 'Not AirFreight, should not input the AirFreight command[%$]!');
 COMMIT;

-- =========================================================================================================
-- MAWGT861,v2.0.4.7,2019/04/18
-- =========================================================================================================
-- CIMSFC
UPDATE CIMAPPLICATION SET VERSION ='2.0.4.7',versiondate='2019/04/18' WHERE APID='MAWGT861';
COMMIT;

-- =========================================================================================================
-- MAWGT861,v2.0.4.6,2019/04/16
-- =========================================================================================================
-- CIMSFC
UPDATE CIMAPPLICATION SET VERSION ='2.0.4.6',versiondate='2019/04/16' WHERE APID='MAWGT861';
COMMIT;

-- New INI
INSERT INTO CIMAPINI
  (APID, SECTION, ITEM, VALUE, REMARK)
VALUES
  ('MAWGT861',
   'WEIGHT',
   'CHECKSTDWEIGHTBY91PN',
   '0',
   '0/1: Disable/Enable check single pallet standard weight by internalPN. When it be used that INI[UNFULLPALLETWEIGHTMODE] must equal 1. Default: 0')
COMMIT;

INSERT INTO CIMMESSAGE ( MESSAGEID, LANGUAGE, MODULE, DESCRIPTION)
VALUES ('SFCF07727',1,'SFC','When ini[%$] is enable only support Single unfull pallet weight,Pls Modify ini[%$] value');
COMMIT;
INSERT INTO CIMMESSAGE ( MESSAGEID, LANGUAGE, MODULE, DESCRIPTION)
VALUES ('SFCF07727',2,'SFC','When ini[%$] is enable only support Single unfull pallet weight,Pls Modify ini[%$] value');
COMMIT;
INSERT INTO CIMMESSAGE ( MESSAGEID, LANGUAGE, MODULE, DESCRIPTION)
VALUES ('SFCF07727',3,'SFC','When ini[%$] is enable only support Single unfull pallet weight,Pls Modify ini[%$] value');
COMMIT;

-- =========================================================================================================
-- MAWGT861,v2.0.4.5,2018/10/15
-- =========================================================================================================
-- CIMSFC
UPDATE CIMAPPLICATION SET VERSION ='2.0.4.5',versiondate='2018/10/15' WHERE APID='MAWGT861';
COMMIT;

-- SFCFA/SFCPCB
ALTER TABLE SFCMO ADD INTERNALPN VARCHAR2(18 CHAR);
COMMENT ON COLUMN SFCMO.INTERNALPN IS 'Internal PN.';

-- =========================================================================================================
-- MAWGT861,v2.0.4.4,2018/09/18
-- =========================================================================================================
-- CIMSFC
UPDATE CIMAPPLICATION SET VERSION ='2.0.4.4',versiondate='2018/09/18' WHERE APID='MAWGT861';
COMMIT;

-- New INI
INSERT INTO CIMAPINI
   (APID, SECTION, ITEM, VALUE, REMARK)
 VALUES
   ('MAWGT861', 'PROCESS', 'UNFULLPALLETWEIGHTCMD', 'MWOEP', 'Unfull Pallet Weight Command. Default “MWOEP”.');
INSERT INTO CIMAPINI
   (APID, SECTION, ITEM, VALUE, REMARK)
 VALUES
   ('MAWGT861', 'PROCESS', 'UNFULLPALLETWEIGHTMODE', '0', '0: Support multi unfull pallets weight together (Default), Operation flow: UnfullPalletWeightCMD.Value -> Pallet1…PalletN -> COMPLETE. 1: Single unfull pallet weight, Operation flow: UnfullPalletWeightCMD.Value -> Pallet1.');
COMMIT;


-- =========================================================================================================
-- MAWGT861,v2.0.4.3,2018/05/15
-- =========================================================================================================
-- CIMSFC
UPDATE CIMAPPLICATION SET VERSION ='2.0.4.3',versiondate='2018/04/14' WHERE APID='MAWGT861';
COMMIT;

-- INI
INSERT INTO CIMAPINI
   (APID, SECTION, ITEM, VALUE, REMARK)
 VALUES
   ('MAWGT861', 'PROCESS', 'DISABLECOMPARE', '0', '1.Disable compare Carton/USN, 0.Enable compare Carton/USN ');
COMMIT;

INSERT INTO CIMAPINI
   (APID, SECTION, ITEM, VALUE, REMARK)
 VALUES
   ('MAWGT861', 'PROCESS', 'AUTOWEIGHTPALLETTYPE', 'P', 'Maintain Pallet type for Auto weight ');
COMMIT;

-- CIMSFC, Message ( '07715' - '07799',MAX '07726')
INSERT INTO CIMMESSAGE
   (MESSAGEID, LANGUAGE, MODULE, DESCRIPTION)
 VALUES
   ('SFCF07724', 1, 'SFC', 'Cannot find Pallet Type[%$] in SFCPALLETSTDWEIGHT');
COMMIT;

INSERT INTO CIMMESSAGE
   (MESSAGEID, LANGUAGE, MODULE, DESCRIPTION)
 VALUES
   ('SFCI07725', 1, 'SFC', 'Please scan Pallet Type.');
COMMIT;

INSERT INTO CIMMESSAGE
   (MESSAGEID, LANGUAGE, MODULE, DESCRIPTION)
 VALUES
   ('SFCF07726', 1, 'SFC', 'UPN [%$];Qty [%$];Pallet Type [%$] Standard weight does not exist!');
COMMIT;

--Modify SFCPALLETSTDWEIGHT
ALTER TABLE SFCPALLETSTDWEIGHT MODIFY PALLETWEIGHT NUMBER(13,3);
ALTER TABLE SFCPALLETSTDWEIGHT MODIFY STANDARDWEIGHT NUMBER(13,3);
ALTER TABLE SFCPALLETSTDWEIGHT MODIFY MINWEIGHT NUMBER(13,3);
ALTER TABLE SFCPALLETSTDWEIGHT MODIFY MAXWEIGHT NUMBER(13,3);
ALTER TABLE SFCPALLETSTDWEIGHT ADD PALLETTYPE VARCHAR2(1) DEFAULT 'P';

ALTER TABLE SFCPALLETSTDWEIGHT DROP CONSTRAINT PK_SFCPALLETSTDWEIGHT;
ALTER TABLE SFCPALLETSTDWEIGHT
  ADD CONSTRAINT PK_SFCPALLETSTDWEIGHT PRIMARY KEY (UPN, QTY, PALLETTYPE); 

-- =========================================================================================================
-- MAWGT861,v2.0.4.2,2018/04/04
-- =========================================================================================================
-- CIMSFC
UPDATE CIMAPPLICATION SET VERSION ='2.0.4.2',versiondate='2018/04/04' WHERE APID='MAWGT861';
COMMIT;

INSERT INTO CIMAPINI
   (APID, SECTION, ITEM, VALUE, REMARK)
 VALUES
   ('MAWGT861', 'WEIGHT', 'DisableCheckWeight', '0', '0: enable check weight when weight (original logic), default 0. 1: Disable check weight');
COMMIT;

-- =========================================================================================================
-- MAWGT861,v2.0.4.1,2018/02/27
-- =========================================================================================================
-- CIMSFC
UPDATE CIMAPPLICATION SET VERSION ='2.0.4.1',versiondate='2018/02/27' WHERE APID='MAWGT861';
COMMIT;

-- =========================================================================================================
-- MAWGT861,v2.0.4.0,2018/1/23
-- =========================================================================================================
-- CIMSFC
UPDATE CIMAPPLICATION SET VERSION ='2.0.4.0',versiondate='2018/01/23' WHERE APID='MAWGT861';
COMMIT;

-- =========================================================================================================
-- MAWGT861,v2.0.3.0,2015/4/29
-- =========================================================================================================
-- CIMSFC
UPDATE CIMAPPLICATION SET VERSION ='2.0.3.0',versiondate='2015/04/29' WHERE APID='MAWGT861';
COMMIT;

-- =========================================================================================================
-- MAWGT861,v2.0.2.0,2015/4/27
-- =========================================================================================================
-- CIMSFC
UPDATE CIMAPPLICATION SET VERSION ='2.0.2.0',versiondate='2015/04/27' WHERE APID='MAWGT861';
COMMIT;

-- =========================================================================================================
-- MAWGT861,v2.0.1.0,2015/4/22
-- =========================================================================================================
-- CIMSFC
UPDATE CIMAPPLICATION SET VERSION ='2.0.1.0',versiondate='2015/04/22' WHERE APID='MAWGT861';
COMMIT;

INSERT INTO CIMAPINI
   (APID, SECTION, ITEM, VALUE, REMARK)
 VALUES
   ('MAWGT861', 'PROCESS', 'CHECK91PN', '0', '0.Disable check 91 P/N; 1.Enable check 91 P/N');
COMMIT;

-- CIMSFC, Message ( '07715' - '07799',MAX '07723')
INSERT INTO CIMMESSAGE
   (MESSAGEID, LANGUAGE, MODULE, DESCRIPTION)
 VALUES
   ('SFCF07723', 1, 'SFC', 'The 91 P/N is not maintain, please check. PalletID:[%$]');
COMMIT;

-- =========================================================================================================
-- MAWGT861,v2.0.0.0,2015/4/1
-- =========================================================================================================

-- CIMSFC
UPDATE CIMAPPLICATION SET VERSION ='2.0.0.0',versiondate='2015/04/01' WHERE APID='MAWGT861';
COMMIT;

-- CIMSFC(New INI:ISLMSGOLIVE to control enable LMS logic or old logic, default, old logic)
INSERT INTO CIMAPINI
   (APID, SECTION, ITEM, VALUE, REMARK)
 VALUES
   ('MAWGT861', 'UPDATEPPS', 'ISLMSGOLIVE', '0', 'Control enable LMS logic or old logic, default, old logic');
COMMIT;
INSERT INTO CIMAPINI
   (APID, SECTION, ITEM, VALUE, REMARK)
 VALUES
   ('MAWGT861', 'PROCESS', 'ALLOWEDSTORAGELOC', '', 'If ALLOWEDSTORAGELOC is empty then no need check storage Loc');
COMMIT;
-- CIMSFC, Message ( '07715' - '07799')
INSERT INTO CIMMESSAGE
   (MESSAGEID, LANGUAGE, MODULE, DESCRIPTION)
 VALUES
   ('SFCF07718', 1, 'SFC', 'LmsWebService URL is empty or not find LmsWebService URL,Please check!');
COMMIT;
-- CIMSFC, Message ( '07715' - '07799' )
INSERT INTO CIMMESSAGE
   (MESSAGEID, LANGUAGE, MODULE, DESCRIPTION)
 VALUES
   ('SFCF07719', 1, 'SFC', 'SFCS send pallet[%$] weight Info. to LMS NG:%$');
COMMIT;
-- CIMSFC, Message ( '07715' - '07799')
INSERT INTO CIMMESSAGE
   (MESSAGEID, LANGUAGE, MODULE, DESCRIPTION)
 VALUES
   ('SFCF07720', 1, 'SFC', 'Release LMS hold NG:%$');
COMMIT;
-- CIMSFC, Message ( '07715' - '07799' )
INSERT INTO CIMMESSAGE
   (MESSAGEID, LANGUAGE, MODULE, DESCRIPTION)
 VALUES
   ('SFCF07721', 1, 'SFC', 'The SFCPALLETITEM.StorageLoc can not be empty, PalletID[%$]');
COMMIT;
-- CIMSFC, Message ( '07715' - '07799' , max use: 07722)
INSERT INTO CIMMESSAGE
   (MESSAGEID, LANGUAGE, MODULE, DESCRIPTION)
 VALUES
   ('SFCF07722', 1, 'SFC', 'The Pallet[%$] can not be put in this storage[%$]');
COMMIT;


-- =========================================================================================================
-- MAWGT861,v1.0.17.0,2014/10/20
-- =========================================================================================================
-- CIMSFC
UPDATE CIMAPPLICATION SET VERSION ='1.0.17.0',versiondate='2014/10/20' WHERE APID='MAWGT861';
COMMIT;

INSERT INTO CIMAPINI
   (APID, SECTION, ITEM, VALUE, REMARK)
 VALUES
   ('MAWGT861', 'PROCESS', 'CHECKPYGIDIUMUPN', '0', 'Check not allow mix UPN when pygidium. 0 disable;1 Enable');
COMMIT;

-- =========================================================================================================
-- MAWGT861,v1.0.16.0,2014/07/18
-- =========================================================================================================
-- CIMSFC
UPDATE CIMAPPLICATION SET VERSION ='1.0.16.0',versiondate='2014/07/21' WHERE APID='MAWGT861';
COMMIT;

-- =========================================================================================================
-- MAWGT861,v1.0.15.0,2014/05/22
-- =========================================================================================================
-- CIMSFC
UPDATE CIMAPPLICATION SET VERSION ='1.0.15.0',versiondate='2014/05/22' WHERE APID='MAWGT861';
COMMIT;

-- =========================================================================================================
-- MAWGT861,v1.0.14.0,2014/05/15
-- =========================================================================================================
-- CIMSFC
UPDATE CIMAPPLICATION SET VERSION ='1.0.14.0',versiondate='2014/05/15' WHERE APID='MAWGT861';

-- CIMSFC, Message ( '07715' - '07799', max use: 07717)
INSERT INTO CIMMESSAGE
   (MESSAGEID, LANGUAGE, MODULE, DESCRIPTION)
 VALUES
   ('SFCF07717', 1, 'SFC', 'The Pallet %$ have already inputted!');
COMMIT;

-- =========================================================================================================
-- MAWGT861,v1.0.13.1,2014/05/05
-- =========================================================================================================
-- CIMSFC
UPDATE CIMAPPLICATION SET VERSION ='1.0.13.1',versiondate='2014/05/05' WHERE APID='MAWGT861';

-- =========================================================================================================
-- MAWGT861,v1.0.13.0,2014/04/23
-- =========================================================================================================
-- CIMSFC
UPDATE CIMAPPLICATION SET VERSION ='1.0.13.0',versiondate='2014/04/30' WHERE APID='MAWGT861';

Insert into CIMAPINI
   (APID, SECTION, ITEM, VALUE, REMARK)
 Values
   ('MAWGT861', 'LOGIN', 'LOGIN', '0', '0 disable;1 Enable');

-- =========================================================================================================
-- MAWGT861,v1.0.12.0,2014/04/23
-- =========================================================================================================
-- CIMSFC
UPDATE CIMAPPLICATION SET VERSION ='1.0.12.0',versiondate='2014/04/2' WHERE APID='MAWGT861';

Insert into CIMAPINI
   (APID, SECTION, ITEM, VALUE, REMARK)
 Values
   ('MAWGT861', 'WEIGHT', 'POSITIVEREVERSE', '1', '0 Reverse;1 Positive');

   Insert into CIMAPINI
   (APID, SECTION, ITEM, VALUE, REMARK)
 Values
   ('MAWGT861', 'WEIGHT', 'WEIGHTMACHINETYPE', '0', '-1 Regular expressions(new);0 Weight Machine(old)');

-- =========================================================================================================
-- MAWGT861,v1.0.11.1,2013/07/15
-- =========================================================================================================
-- CIMSFC
UPDATE CIMAPPLICATION SET VERSION ='1.0.11.1',versiondate='2013/07/15' WHERE APID='MAWGT861';


-- CIMSFC, Message ( '07715' - '07799', max use: 07716)
Insert INTO CIMMESSAGE
   (MESSAGEID, LANGUAGE, MODULE, DESCRIPTION)
 Values
   ('SFCF07716', 1, 'SFC', 'Weight error,PalletWeight:%$ minus Tractor Weight:%$ <=0,Please check!');
COMMIT;

-- =========================================================================================================
-- MAWGT861,v1.0.11.0,2013/03/06
-- =========================================================================================================
-- CIMSFC
UPDATE CIMAPPLICATION SET VERSION ='1.0.11.0',versiondate='2013/03/06' WHERE APID='MAWGT861';
COMMIT;

-- =========================================================================================================
-- MAWGT861,v1.0.10.0,2012/04/20
-- =========================================================================================================
-- CIMSFC
Insert into CIMMESSAGE
------CIMSFC
UPDATE CIMAPPLICATION SET VERSION ='1.0.10.0',versiondate='2012/04/20' WHERE APID='MAWGT861';
COMMIT;

--MAWGT861,v1.0.9.0,2011/11/01
--=========================================================================================================
------CIMSFC
Insert into CIMMESSAGE
------CIMSFC
UPDATE CIMAPPLICATION SET VERSION ='1.0.9.0',versiondate='2011/11/01' WHERE APID='MAWGT861';
COMMIT;

--MAWGT861,v1.0.8.0,2011/10/26
--=========================================================================================================
------CIMSFC
Insert into CIMMESSAGE
   (MESSAGEID, LANGUAGE, MODULE, DESCRIPTION)
 Values
   ('SFCF07715', 1, 'SFC', 'Tractor weight: %$ is out of range %$ - %$!');

--MAWGT861,v1.0.7.0,2011/03/23
--=========================================================================================================
------CIMSFC
UPDATE CIMAPPLICATION SET VERSION ='1.0.7.0',versiondate='2011/03/23' WHERE APID='MAWGT861';
COMMIT;

Insert into CIMAPINI
   (APID, SECTION, ITEM, VALUE, REMARK)
 Values
   ('MAWGT861', 'PROCESS', 'SCANTRACTORWEIGHT', '0', '0/1:Disable/Enable scan tractor(铁牛) weight.');
Insert into CIMMESSAGE
   (MESSAGEID, LANGUAGE, MODULE, DESCRIPTION)
 Values
   ('SFCF00320', 1, 'SFC', 'Weight Data: %$ Error, must be number!');
Insert into CIMMESSAGE
   (MESSAGEID, LANGUAGE, MODULE, DESCRIPTION)
 Values
   ('SFCF10930', 1, 'SFC', 'The tractor weight should be < pallet weight.');
Insert into CIMMESSAGE
   (MESSAGEID, LANGUAGE, MODULE, DESCRIPTION)
 Values
   ('SFCI10929', 1, 'SFC', 'Please scan palletid.....');
Insert into CIMMESSAGE
   (MESSAGEID, LANGUAGE, MODULE, DESCRIPTION)
 Values
   ('SFCI10928', 1, 'SFC', 'Please scan tractor weight.....');
COMMIT;

--MAWGT861,v1.0.6.0,2011/01/10
--=========================================================================================================
------CIMSFC
UPDATE CIMAPPLICATION SET VERSION ='1.0.6.0',versiondate='2011/01/10' WHERE APID='MAWGT861';
COMMIT;

--MAWGT861,v1.0.5.0,2010/12/30 
--=========================================================================================================
------CIMSFC
UPDATE CIMAPPLICATION SET VERSION ='1.0.5.0',versiondate='2010/12/30' WHERE APID='MAWGT861';
COMMIT;
------SFCFA
CREATE TABLE SFCPALLETWEIGHTMSG(
	UPN VARCHAR2(20) NOT NULL,
	PALLETID VARCHAR2(20) NOT NULL,
	QUANTITY NUMBER(4),
	USERID VARCHAR2(10),
	WEIGHT NUMBER(10,2),
	ERRORMESSAGE VARCHAR2(400),
	TRNDATE DATE DEFAULT SYSDATE);
------CMS
ALTER TABLE SFCPALLETWEIGHT MODIFY(WEIGHT NUMBER(10,3));

--MAWGT861,v1.0.4.5,2010/10/21 
--=========================================================================================================
------CIMSFC
UPDATE CIMAPPLICATION SET VERSION ='1.0.4.5',versiondate='2010/10/21' WHERE APID='MAWGT861';
COMMIT;

--MAWGT861,v1.0.4.4,2010/10/18 
--=========================================================================================================
------CIMSFC
UPDATE CIMAPPLICATION SET VERSION ='1.0.4.4',versiondate='2010/10/18' WHERE APID='MAWGT861';
COMMIT;

--MAWGT861,v1.0.4.3,2010/10/15 
--=========================================================================================================
------CIMSFC
UPDATE CIMAPPLICATION SET VERSION ='1.0.4.3',versiondate='2010/10/15' WHERE APID='MAWGT861';
COMMIT;

--MAWGT861,v1.0.4.2,2010/10/12 
--=========================================================================================================
------CIMSFC
UPDATE CIMAPPLICATION SET VERSION ='1.0.4.2',versiondate='2010/10/12' WHERE APID='MAWGT861';
COMMIT;

--MAWGT861,v1.0.4.1,2010/09/03 
--=========================================================================================================
------CIMSFC
UPDATE CIMAPPLICATION SET VERSION ='1.0.4.1',versiondate='2010/10/09' WHERE APID='MAWGT861';
COMMIT;

--MAWGT861,v1.0.4.0,2010/09/03 
--=========================================================================================================
------CIMSFC
UPDATE CIMAPPLICATION SET VERSION ='1.0.4.0',versiondate='2010/09/27' WHERE APID='MAWGT861';
COMMIT;
Insert into CIMAPINI
   (APID, SECTION, ITEM, VALUE, REMARK)
 Values
   ('MAWGT861', 'ALLOCATE', 'PLANT', 'F192', 'Allocate bin need  set it.');
Insert into CIMAPINI
   (APID, SECTION, ITEM, VALUE, REMARK)
 Values
   ('MAWGT861', 'ALLOCATE', 'WAREHOUSE', 'W101', 'Allocate bin need set it.');
Insert into CIMAPINI
   (APID, SECTION, ITEM, VALUE, REMARK)
 Values
   ('MAWGT861', 'ALLOCATE', 'WMSWORKMODE', '1', '1.Allocate bin;2.Suggest bin;3.Allocate bin and Confirm bin.');
COMMIT;
Insert into CIMAPINI
   (APID, SECTION, ITEM, VALUE, REMARK)
 Values
   ('MAWGT861', 'PROCESS', 'ALLOCATEBIN', '1', '1.Enable allocate bin for F/G,0.Disabel allocate bin for F/G.');
COMMIT;

Insert into CIMMESSAGE
   (MESSAGEID, LANGUAGE, MODULE, DESCRIPTION)
 Values
   ('SFCI10713', 1, 'SFC', 'Pallet:[%$] compare completed,Please Move it to Bin:[%$] Next pallet?');
Insert into CIMMESSAGE
   (MESSAGEID, LANGUAGE, MODULE, DESCRIPTION)
 Values
   ('SFCF10717', 1, 'SFC', 'WmsWebService URL is empty or not find WmsWebService URL,Please check!');
COMMIT;

--MAWGT861,v1.0.3.6,2010/09/03 
--=========================================================================================================
------CIMSFC
UPDATE CIMAPPLICATION SET VERSION ='1.0.3.6',versiondate='2010/09/03' WHERE APID='MAWGT861';
COMMIT;
INSERT INTO CIMAPini
(APID,SECTION,ITEM,VALUE,REMARK)
VALUES
('MAWGT861','PROCESS','CHECKUPNWEIGHTED','1','need check UPN weight or not');
COMMIT;

INSERT INTO cimsfc.cimmessage
(MESSAGEID,LANGUAGE,MODULE,DESCRIPTION)
VALUES
('SFCF07714',1,'SFC','UPN [%$] has no weight record!');
COMMIT;
```