---
title: MAWGT862 SQL Log
description: MAWGT862 Auto Weight -- SQL log
published: true
date: 2020-09-02T08:07:58.014Z
tags: 
editor: undefined
---

# MAWGT862 Auto Weight -- SQL log

```plsql
-- ===========================================================
-- MAWGT862, v2.0.17.4, 2020/07/08
-- ===========================================================
-- CIMSFC
UPDATE CIMAPPLICATION SET VERSION='2.0.17.4', VERSIONDATE='2020/07/08' WHERE APID='MAWGT862';
COMMIT;

-- ===========================================================
-- MAWGT862, v2.0.17.3, 2020/04/30
-- ===========================================================
-- CIMSFC
UPDATE CIMAPPLICATION SET VERSION='2.0.17.3', VERSIONDATE='2020/04/30' WHERE APID='MAWGT862';
COMMIT;

-- ===========================================================
-- MAWGT862, v2.0.17.2, 2020/04/27
-- ===========================================================
-- CIMSFC
UPDATE CIMAPPLICATION SET VERSION='2.0.17.2', VERSIONDATE='2020/04/27' WHERE APID='MAWGT862';
COMMIT;

-- Update INI Remark
UPDATE CIMAPINI SET Remark='0(Default): WMS.Bin from INI[STORAGELOCATION], 
1:WMS.Bin from WMS.GetAutoGRBinForSFCS()' 
WHERE APID='MAWGT862' AND SECTION ='PROCESS' AND ITEM ='GETWMSAVAILABLEBIN';
COMMIT;

-- ===========================================================
-- MAWGT862, v2.0.17.1, 2020/04/21
-- ===========================================================
-- CIMSFC
UPDATE CIMAPPLICATION SET VERSION='2.0.17.1', VERSIONDATE='2020/04/21' WHERE APID='MAWGT862';
COMMIT;

-- New INI 
INSERT INTO CIMAPINI(APID, SECTION, ITEM, VALUE, REMARK) 
  VALUES('MAWGT862', 'PROCESS', 'MULTIPLANTWEIGHT', '0', '0.Disabel(Default)/1.Enable: support weighing of multi plant pallets by one program');  
INSERT INTO CIMAPINI(APID, SECTION, ITEM, VALUE, REMARK) 
  VALUES('MAWGT862', 'PROCESS', 'GETWMSAVAILABLEBIN', '0', '0(Default): WMS.Bin from INI[STORAGELOCATION], 
1:WMS.Bin from WMS.SearchAvailableBinForPackentity()');
COMMIT;

-- New Message 
INSERT INTO CIMMESSAGE(MESSAGEID, LANGUAGE, MODULE, DESCRIPTION)
 VALUES('SFCF16148', 1, 'SFC', 'Can Not Get Plant by this PalletID[%$]');
INSERT INTO CIMMESSAGE(MESSAGEID, LANGUAGE, MODULE, DESCRIPTION)
 VALUES('SFCF16149', 1, 'SFC', 'The palletID[%$] plant[%$] is different last pallet ID, can not multi scan pallet id for different plant'); 
COMMIT;

-- ===========================================================
-- MAWGT862, v2.0.17.0, 2018/10/26
-- ===========================================================
-- CIMSFC
UPDATE CIMAPPLICATION SET VERSION='2.0.17.0', VERSIONDATE='2018/10/26' WHERE APID='MAWGT862';
COMMIT;

--FA/PCB
ALTER TABLE SFCMO ADD INTERNALPN VARCHAR2(18 CHAR);
COMMENT ON COLUMN SFCMO.INTERNALPN IS 'Internal PN.';
   
-- ===========================================================
-- MAWGT862, v2.0.16.0, 2018/10/05
-- ===========================================================
-- CIMSFC
UPDATE CIMAPPLICATION SET VERSION='2.0.16.0', VERSIONDATE='2018/10/05'
WHERE APID='MAWGT862';
COMMIT;

-- ===========================================================
-- MAWGT862, v2.0.15.0, 2018/09/18
-- ===========================================================
-- CIMSFC
UPDATE CIMAPPLICATION SET VERSION='2.0.15.0', VERSIONDATE='2018/09/18'
WHERE APID='MAWGT862';
COMMIT;

-- ===========================================================
-- MAWGT862, v2.0.14.0, 2017/06/19
-- ===========================================================
-- CIMSFC
UPDATE CIMAPPLICATION SET VERSION='2.0.14.0', VERSIONDATE='2017/06/19'
WHERE APID='MAWGT862';
COMMIT;

-- ===========================================================
-- MAWGT862, v2.0.13.0, 2017/05/12
-- ===========================================================
-- CIMSFC
UPDATE CIMAPPLICATION SET VERSION='2.0.13.0',VERSIONDATE='2017/05/12',DESCRIPTION='AUTO WEIGHT' 
WHERE APID='MAWGT862';
COMMIT;

-- ===========================================================
-- MAWGT862, v2.0.12.0, 2016/11/28
-- ===========================================================
-- CIMSFC
UPDATE CIMAPPLICATION SET VERSION='2.0.12.0',VERSIONDATE='2016/11/28',DESCRIPTION='AUTO WEIGHT' 
WHERE APID='MAWGT862';
COMMIT;

-- ===========================================================
-- MAWGT862, v2.0.11.0, 2016/11/16
-- ===========================================================
-- CIMSFC
UPDATE CIMAPPLICATION SET VERSION='2.0.11.0',VERSIONDATE='2016/11/16',DESCRIPTION='AUTO WEIGHT' 
WHERE APID='MAWGT862';
--New INI
INSERT INTO CIMAPINI(APID, SECTION, ITEM, VALUE, REMARK)
VALUES('MAWGT862', 'WEIGHT', 'CHECKINVENTORYBYPALLET', '0', '0:Disabel, 1:Enable check inventory by pallet');
INSERT INTO CIMAPINI(APID, SECTION, ITEM, VALUE, REMARK)
VALUES('MAWGT862', 'WEIGHT', 'BYPASSREDUPLICATEDPALLETID', '0', '0:Disabel, 1:Enable pass reduplicated pallet ID');
COMMIT;

-- ===========================================================
-- MAWGT862, v2.0.10.0, 2016/10/24
-- ===========================================================
-- CIMSFC
UPDATE CIMAPPLICATION SET VERSION='2.0.10.0',VERSIONDATE='2016/10/24',DESCRIPTION='AUTO WEIGHT' 
WHERE APID='MAWGT862';
COMMIT;

-- ===========================================================
-- MAWGT862, v2.0.9.0, 2016/07/06
-- ===========================================================
-- CIMSFC
UPDATE CIMAPPLICATION SET VERSION='2.0.9.0',VERSIONDATE='2016/07/06',DESCRIPTION='AUTO WEIGHT' 
WHERE APID='MAWGT862';
COMMIT;

-- ===========================================================
-- MAWGT862, v2.0.8.0, 2016/07/01
-- ===========================================================
-- CIMSFC
UPDATE CIMAPPLICATION SET VERSION='2.0.8.0',VERSIONDATE='2016/07/01',DESCRIPTION='AUTO WEIGHT' 
WHERE APID='MAWGT862';
INSERT INTO CIMMESSAGE(MESSAGEID, LANGUAGE, MODULE, DESCRIPTION)
VALUES('SFCF16147', 1, 'SFC', 'Pallet has been scan already, please another pallet.');
COMMIT;

-- ===========================================================
-- MAWGT862, v2.0.7.0, 2016/06/24
-- ===========================================================
-- CIMSFC
UPDATE CIMAPPLICATION SET VERSION='2.0.7.0',VERSIONDATE='2016/06/24',DESCRIPTION='AUTO WEIGHT' 
WHERE APID='MAWGT862';
--New INI
INSERT INTO CIMAPINI(APID, SECTION, ITEM, VALUE, REMARK)
VALUES('MAWGT862', 'PROCESS', 'MULTISCANPALLETID', '0', '0:Disabel, 1:Enable scan multi pallet');
INSERT INTO CIMAPINI(APID, SECTION, ITEM, VALUE, REMARK)
VALUES('MAWGT862', 'PROCESS', 'FORBIDKEYBOARD', '0', '0: Allow key in with key board (default); 1: Forbid key in.');
INSERT INTO CIMAPINI(APID, SECTION, ITEM, VALUE, REMARK)
VALUES('MAWGT862', 'PROCESS', 'SCANNERTIMESPAN', '50', 'Set scanner scan time span, unit is ms (1000ms = 1s)');
--New Message, Sequence: 16141-16160
INSERT INTO CIMMESSAGE(MESSAGEID, LANGUAGE, MODULE, DESCRIPTION)
VALUES('SFCI16141', 1, 'SFC', 'Please scan next pallet or command "END".');
INSERT INTO CIMMESSAGE(MESSAGEID, LANGUAGE, MODULE, DESCRIPTION)
VALUES('SFCI16142', 1, 'SFC', 'Pallets weight completed, Next pallet?');
INSERT INTO CIMMESSAGE(MESSAGEID, LANGUAGE, MODULE, DESCRIPTION)
VALUES('SFCF16143', 1, 'SFC', 'The Pallet UPN is not equal the last one.');
INSERT INTO CIMMESSAGE(MESSAGEID, LANGUAGE, MODULE, DESCRIPTION)
VALUES('SFCF16144', 1, 'SFC', 'The PalletItem count is not equal the last one.');
INSERT INTO CIMMESSAGE(MESSAGEID, LANGUAGE, MODULE, DESCRIPTION)
VALUES('SFCF16145', 1, 'SFC', 'Unfull pallet can not be pile up.');
INSERT INTO CIMMESSAGE(MESSAGEID, LANGUAGE, MODULE, DESCRIPTION)
VALUES('SFCI16146', 1, 'SFC', 'Scan pallet finish, please scan pallet weight.');
COMMIT;

-- ===========================================================
-- MAWGT862, v2.0.6.0, 2015/08/21
-- ===========================================================
-- CIMSFC
UPDATE CIMAPPLICATION SET VERSION='2.0.6.0',VERSIONDATE='2015/08/21',DESCRIPTION='AUTO WEIGHT' 
WHERE APID='MAWGT862';
COMMIT;

INSERT INTO CIMAPINI
   (APID, SECTION, ITEM, VALUE, REMARK)
 VALUES
   ('MAWGT862', 'PROCESS', 'SUPPORTFAPCB', '0', '1: Enable support FA and PCB schema at the same time  0: Disable(default)');
COMMIT;

INSERT INTO CIMAPINI
   (APID, SECTION, ITEM, VALUE, REMARK)
 VALUES
   ('MAWGT862', 'PROCESS', 'DISABLECOMPARE', '0', '1: Disable compare function. 0: Enable compare function(default)');
COMMIT;

INSERT INTO CIMAPINI
   (APID, SECTION, ITEM, VALUE, REMARK)
 VALUES
   ('MAWGT862', 'PROCESS', 'SUPPORTFAPCBSTAGE', '', 'Set stage to get DB schema in basic web service when enable ini SUPPORTFAPCB. Format: schema1:stage1|schema2:stage2, for example: FA:SN|PCB:SA');
COMMIT;

-- ===========================================================
-- MAWGT862, v2.0.4.0, 2015/04/22
-- ===========================================================
-- CIMSFC
UPDATE CIMAPPLICATION SET VERSION='2.0.4.0',VERSIONDATE='2015/04/27',DESCRIPTION='AUTO WEIGHT' 
WHERE APID='MAWGT862';
COMMIT;

INSERT INTO CIMAPINI
   (APID, SECTION, ITEM, VALUE, REMARK)
 VALUES
   ('MAWGT862', 'PROCESS', 'CHECK91PN', '0', '0.Disable check 91 P/N; 1.Enable check 91 P/N');
COMMIT;

-- ===========================================================
-- MAWGT862, v2.0.3.1, 2015/04/03
-- ===========================================================
-- CIMSFC
UPDATE CIMAPPLICATION SET VERSION='2.0.3.1',VERSIONDATE='2015/04/03',DESCRIPTION='AUTO WEIGHT' 
WHERE APID='MAWGT862';
COMMIT;

-- ===========================================================
-- MAWGT862, v2.0.3.0, 2015/03/31
-- ===========================================================
-- CIMSFC
UPDATE CIMAPPLICATION SET VERSION='2.0.3.0',VERSIONDATE='2015/03/31',DESCRIPTION='AUTO WEIGHT' 
WHERE APID='MAWGT862';
COMMIT;

--New ini setting
INSERT INTO CIMAPINI
   (APID, SECTION, ITEM, VALUE, REMARK)
 VALUES
   ('MAWGT862', 'PROCESS', 'ISLMSGOLIVE', '0', 'Enable LMS logic or old logic, default,0.old logic');
COMMIT;

INSERT INTO CIMAPINI
   (APID, SECTION, ITEM, VALUE, REMARK)
 VALUES
   ('MAWGT862', 'PROCESS', 'ALLOWEDSTORAGELOC', '', 'If ALLOWEDSTORAGELOC is empty then no need check storage Loc');
COMMIT;

INSERT INTO CIMAPINI
   (APID, SECTION, ITEM, VALUE, REMARK)
 VALUES
   ('MAWGT862', 'PROCESS', 'ALLOCATEBIN', '0', '1.Enable allocate bin for F/G,0.Disabel allocate bin for F/G.');
COMMIT;

--Message
INSERT INTO CIMMESSAGE
   (MESSAGEID, LANGUAGE, MODULE, DESCRIPTION)
 VALUES
   ('SFCF00357', 1, 'SFC', 'The Pallet [%$] has no unit');
COMMIT;

INSERT INTO CIMMESSAGE
   (MESSAGEID, LANGUAGE, MODULE, DESCRIPTION)
 VALUES
   ('SFCF00358', 1, 'SFC', 'The SFCPALLETITEM.StorageLoc can not be empty, PalletID[%$]');
COMMIT;

INSERT INTO CIMMESSAGE
   (MESSAGEID, LANGUAGE, MODULE, DESCRIPTION)
 VALUES
   ('SFCF00359', 1, 'SFC', 'The Pallet[%$] can not be put in this storage[%$]');
COMMIT;

-- ===========================================================
-- MAWGT862, v2.0.1.0, 2014/12/01
-- ===========================================================
-- CIMSFC
UPDATE CIMAPPLICATION SET VERSION='2.0.2.0',VERSIONDATE='2014/12/01',DESCRIPTION='AUTO WEIGHT' 
WHERE APID='MAWGT862';
COMMIT;

--New ini setting
INSERT INTO CIMAPINI
   (APID, SECTION, ITEM, VALUE, REMARK)
 VALUES
   ('MAWGT862', 'PROCESS', 'SLEEPTIMEFORCLEANPLCCOM', '0', 'Sleep time before clean PLC COM, default(0 s)');
COMMIT;

-- ===========================================================
-- MAWGT862, v2.0.1.0, 2014/11/14
-- ===========================================================
-- CIMSFC
UPDATE CIMAPPLICATION SET VERSION='2.0.1.0',VERSIONDATE='2014/11/14',DESCRIPTION='AUTO WEIGHT' 
WHERE APID='MAWGT862';
COMMIT;

INSERT INTO CIMAPINI
   (APID, SECTION, ITEM, VALUE, REMARK)
 VALUES
   ('MAWGT862', 'COM', 'PLCCOM_PORT', '1', 'PLC Comm setting:Port');
INSERT INTO CIMAPINI
   (APID, SECTION, ITEM, VALUE, REMARK)
 VALUES
   ('MAWGT862', 'COM', 'PLCCOM_SETTINGS', '2400,N,8,1', 'PLC Comm Settings');
COMMIT;
   
-- ===========================================================
-- MAWGT862, v2.0.0.0, 2014/11/05
-- ===========================================================
-- CIMSFC
INSERT INTO CIMAPPLICATION
(APID, VERSION, VERSIONDATE, DESCRIPTION, PARENTAPID, URL, PARAMETER, ENABLE, MENUITEM, MENUITEMSEQ, CHANGENOTICE, UPDATETYPE, NEWWINDOW)
VALUES
('MAWGT862', '2.0.0.0', '2014/11/05', 'AUTO WEIGHT', 'MA', '', NULL, 1, 1, 0, NULL, 0, 0);
COMMIT;

-- CIMSFC, Message
INSERT INTO CIMMESSAGE
   (MESSAGEID, LANGUAGE, MODULE, DESCRIPTION)
 VALUES
   ('SFCF00355', 1, 'SFC', 'The PalletID [%$] has not compared!');
COMMIT;

INSERT INTO CIMMESSAGE
   (MESSAGEID, LANGUAGE, MODULE, DESCRIPTION)
 VALUES
   ('SFCI00356', 1, 'SFC', 'Pallet:[%$] weight completed,Next pallet?');
COMMIT;

-- New initial setting
INSERT INTO CIMAPINI
   (APID, SECTION, ITEM, VALUE, REMARK)
 VALUES
   ('MAWGT862', 'PROCESS', 'PLANT', 'F192', 'Plant code.');
   
INSERT INTO CIMAPINI
(APID,SECTION,ITEM,VALUE,REMARK)
VALUES
('MAWGT862','WEIGHT','CHECKUPNWEIGHTED','1','need check UPN weight or not');

INSERT INTO CIMAPINI
   (APID, SECTION, ITEM, VALUE, REMARK)
 VALUES
   ('MAWGT862', 'WEIGHT', 'POSITIVEREVERSE', '1', '0 Reverse;1 Positive');
   
INSERT INTO CIMAPINI
   (APID, SECTION, ITEM, VALUE, REMARK)
 VALUES
   ('MAWGT862', 'WEIGHT', 'WEIGHTMACHINETYPE', '0', '-1 Regular expressions(new);0 Weight Machine(old)'); 
INSERT INTO CIMAPINI
   (APID, SECTION, ITEM, VALUE, REMARK)
 VALUES
   ('MAWGT862', 'PROCESS', 'STORAGELOCATION', '', 'Maintain Storage Location'); 
INSERT INTO CIMAPINI
   (APID, SECTION, ITEM, VALUE, REMARK)
 VALUES
   ('MAWGT862', 'COM', 'COM_INPUTLEN', '0', 'Comm Setting:Input Length');
INSERT INTO CIMAPINI
   (APID, SECTION, ITEM, VALUE, REMARK)
 VALUES
   ('MAWGT862', 'COM', 'COM_PORT', '1', 'Comm setting:Port');
INSERT INTO CIMAPINI
   (APID, SECTION, ITEM, VALUE, REMARK)
 VALUES
   ('MAWGT862', 'COM', 'COM_SETTINGS', '2400,N,8,1', 'Comm Settings');
 INSERT INTO CIMAPINI
   (APID, SECTION, ITEM, VALUE, REMARK)
 VALUES
   ('MAWGT862', 'WEIGHT', 'TENEXPONENT', '0', 'Config weight data to multiply how many ten;');
 INSERT INTO CIMAPINI
   (APID, SECTION, ITEM, VALUE, REMARK)
 VALUES
   ('MAWGT862', 'PROCESS', 'SOUNDPATH', '0', 'Maintain Sound Path');
 INSERT INTO CIMAPINI
   (APID, SECTION, ITEM, VALUE, REMARK)
 VALUES
   ('MAWGT862', 'WEIGHT', 'VALUEFROM', '2', '1. Weight value from GetWeight.dll; 2. Weight value from COM port');
INSERT INTO CIMAPINI
 (APID, SECTION, ITEM, VALUE, REMARK)
 VALUES
   ('MAWGT862', 'WEIGHT', 'WEIGHTVALUEFORMAT', '.......(.*)..' , 'get value from input string from COM port when Weight machine type is -1
like ".......(.*).." to get "  5.815" from "ST,GS,+  5.815kg"');
 INSERT INTO CIMAPINI
   (APID, SECTION, ITEM, VALUE, REMARK)
 VALUES
   ('MAWGT862', 'UPDATEPPS', 'UPDATEPPSHOLD', '0', '0:Disable 1:Enable');
 INSERT INTO CIMAPINI
   (APID, SECTION, ITEM, VALUE, REMARK)
 VALUES
   ('MAWGT862', 'UPDATEPPS', 'RELEASEREASON', '', 'Release reason');
 INSERT INTO CIMAPINI
   (APID, SECTION, ITEM, VALUE, REMARK)
 VALUES
   ('MAWGT862', 'UPDATEPPS', 'HOLDREASON', '', 'Hold reason');
 INSERT INTO CIMAPINI
   (APID, SECTION, ITEM, VALUE, REMARK)
 VALUES
   ('MAWGT862', 'LANGUAGE', 'LANGUAGE', '1', '1.en-US 2.zh-TW 3.zh-CN');
 COMMIT;
```