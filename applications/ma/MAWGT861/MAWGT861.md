---
title:  MAWGT861 UPN Weight
description: UPN Weight
published: true
date: 2020-09-02T07:35:27.206Z
tags: 
editor: undefined
---

## [Version](/applications/ma/weighting/MAWGT861/MAWGT861_VersionLog.md)

| **Revise date** | **Version** | **Modified by** | **Purpose**                                                  |
| --------------- | ----------- | --------------- | ------------------------------------------------------------ |
| 2020/06/19      | 2.0.4.9     | Winds Liang     | Fix Issue: "Conversion from string "--" to type 'Integer' is not valid" in `writeErrorMsg` function. |
| 2020/05/11      | 2.0.4.8     | Winds Liang     | 使称重入库程式实现同一791料号周转栈板(海运)与带栈板出货(空运). |

## Scope and Purpose   #####
**Scope:** SFCS.

**Purpose:** Weighting for pallet weight and Check compare item, for warehouse packing operation.

**Related Applications**:

- 1.[Weighting Module](../../../modules/Weighting.md)

- 2.[SMWGT861 Pallet Standard Weight Maintain](../../sm-system management/SMWGT861/SMWGT861.md)

- 3.[SMMOWGT001](../sm-system management/SMMOWGT001/SMMOWGT001.md)(Weight Maintain by MO for MAWGT861).

- 4.[MAWGT862 Auto Weight](../MAWGT862/MAWGT862.md)
 

## UI 

- **Login**
	![Login UI](/applications/m-a/mawgt861/mawgt861_login.png)
     
- **Main** 
(The main UI will have some differences depending on INI Settings)
   ![MAWGT861_MainUI](/applications/m-a/mawgt861/mawgt861_mainui.png)

##  Application Logic  #####
- [**Base Process Flow**](/applications/m-a/mawgt861/mawgt861_basicprocessflow.drawio)

  ![MAWGT861_BasicProcessFlow](/applications/m-a/mawgt861/mawgt861_basicprocessflow.png) 


## Key features

- 1.Check base data.
- 2.INI `SCANTRACTORWEIGHT`: 
```vb
'0/1:Disable/Enable need scan tractor weight.
```

- 3.Weight data source Setting:
```vb
'INI [WEIGHTMACHINETYPE]:-1.Regular expressions(new); 0.Weight Machine(old).
'INI [VALUEFROM]: 1. weight value from GetWeight.dll 2. weight value from COM port.
'INI [VALUEFORMAT]: Regular Expression: the position of weight value in input string from COM port. if empty, input string to be value.
'INI [POSITIVEREVERSE]: Scale data 0.Reverse; 1.Positive.
'INI [TENEXPONENT]: Set weight data to how many exponent of ten.
```

- 4.Need Weight

```vb
'INI NEEDWEIGHT: 1.Enable weight function; 0.Disable weight function.
```

- 5.满足同一料号2种运货方式(空运和海运)的入库，避免因重量差异导致报关异常
```plsql
--Get MO Shipping Type by PalletID, then get its corresponding Pallet Type;(Different pallet types have different standard weight)
--Check: a pallet cannot mix multiple Shipping Type.
--INI [AIRFREIGHTCMD]:
  --Set the Air Freight Shipping Type Command, Default ""(Empty):Disable Air Freight Mode;
  --Scan the Command to enable Air Freight mode weighing;
  --Check: AirFreight pallet, must scan the Command firstly; Not AirFreight pallet, shoud not scan it.
--INI [SHIPTYPEPALLETYPEMAP]: 
  --ShippingType:PalletType Map; Default ""; Ex:0:P; 1:P; 2:P; 3:A.  
  --(Shipping Type: 0.Not Defined, 1.Land Transportation, 2.Sea Shipping, 3.Air Freight).
```

- 6.Weighting Error Log
```plsql
SELECT * FROM SFCPALLETWEIGHTMSG;
```

- 7.Item Compare
```plsql
Scan carton/USN to Compare
```

- 8.Send Pallet Weight Info to LMS
```plsql
INSERT INTO SFCPALLETWEIGHT;
LmsWebService.SendPalletWeightInfo(PalletWeightToLMS).
```

------



## Interface (Web Service)   #####

| API  Module           | interface name                                               |
| --------------------- | ------------------------------------------------------------ |
| [DBConnWebService](#) | ExecuteScalar; FillDataSet;  ExecuteNonQuery; ExecuteNonQueryInSchema; ExecuteInTransaction. |
| [LogonWebService](#)  | loginByUserIDPassword; authenticateApIdByUserId.             |
| [WmsWebService](#)    | AllocateBinForFG; AddToInventoryBySn; SearchAvailableBinForPackentity |
| [LmsWebService](#)    | ReleaseByBarcodeCheck; SendPalletWeightInfo                  |
| [BasicWebService](#)  | GetWorkStationGenealogy; GetApplicationIni; GetPackageItem; GetLabelJobSetting; RequestLabelPrint |

## Configuration

- **configuration setting** ([MAWGT861.config](/applications/m-a/mawgt861/mawgt861.config.xml))

```xml
<add key="DBConnWebService" value="http://10.41.21.91:808/DBConnect.WebService/DBConnect.WebService.asmx" />
<add key="BasicWebService" value="http://10.41.21.91:808/basic.webservice/WebService.asmx" />
<add key="LogonWebService" value="http://10.41.21.91:808/portalwebservice/logon.asmx" />
<add key="WmsWebService" value="http://10.41.21.91:808/WM/Wms.Basic.WebService/WmsWebService.asmx" />
<add key="LmsWebService" value="http://10.41.21.91:808/PPExternalService/PPExternalService.svc" />
<add key="withCOM" value="0" />
<add key="MaxTractorWeight" value="90" /> <!--Add for deduct the tractor weight for F192-->
<add key="MinTractorWeight" value="60" /> <!--Add for deduct the tractor weight for F192-->
<add key="WorkstationIP" value="10.41.56.XXX" />
<add key="ClientSettingsProvider.ServiceUri" value="" />
```

- **initial settings**  

```plsql
SELECT * FROM cimapini WHERE apid='MAWGT861';
```

**Must:**

| #    | SECTION | ITEM                   | VALUE       | REMARK                                                       |
| ---- | ------- | ---------------------- | ----------- | ------------------------------------------------------------ |
| 1    | COM     | COM_INPUTLEN           | 0           | Comm Setting Input Length                                    |
| 2    | COM     | COM_PORT               | 1           | Comm setting Port                                            |
| 3    | COM     | COM_SETTINGS           | 2400,N,8,1  | Comm Settings                                                |
| 4    | COMPARE | CARTONFORMAT           | ..(.*)      | Carton format                                                |
| 5    | COMPARE | USNFORMAT              | .(.*)       | USN format                                                   |
| 6    | PROCESS | SOUNDPATH              | c:\Windows\ |                                                              |
| 7    | PROCESS | UNFULLPALLETWEIGHTCMD  | MWOEP       | Unfull Pallet Weght  Command. Default: MWOEP.                |
| 8    | PROCESS | UNFULLPALLETWEIGHTMODE | 0           | 0: Support multi  unfull pallets weight together (Default), Operation flow:  UnfullPalletWeightCMD.Value -> Pallet1…PalletN -> COMPLETE. 1: Single  unfull pallet weight, Operation flow: UnfullPalletWeightCMD.Value ->  Pallet1. |
| 9    | PROCESS | WITHOUTENDCOMMAND      | 1           | 0.input  "END" command to finish compare 1.auto complete compare no need  input "END" |
| 10   | WEIGHT  | VALUEFORMAT            |             | Regular Expression:  the position of weight value in input string from COM port. if empty, input  string to be value |
| 11   | WEIGHT  | VALUEFROM              | 1           | 1. weight value from  GetWeight.dll 2. weight value from COM port |
| 12   | WEIGHT  | WEIGHTMACHINETYPE      | 0           | -1 Regular  expressions(new);0 Weight Machine(old)           |

**Option:**

| #    | SECTION           | ITEM                 | VALUE                          | REMARK                                                       |
| ---- | ----------------- | -------------------- | ------------------------------ | ------------------------------------------------------------ |
| 1    | ALLOCATE          | PLANT                | F192                           | Allocate bin need set it.                                    |
| 2    | ALLOCATE          | WAREHOUSE            | W101                           | Allocate bin need set  it.                                   |
| 3    | LABEL             | PRINTLABEL           | 1                              | 1.Enable print label  function 0.Disable print label function |
| 4    | LANGUAGE          | LANGUAGE             | 1                              |                                                              |
| 5    | LEASTCOMPARETIMES | LEASTCOMPARETIMES    | 2                              | Setting least compare  times                                 |
| 6    | LOGIN             | LOGIN                | 0                              | 0 disable;1 Enable  Pop-up login UI when it is tail plate number and before save pallet weight |
| 7    | PROCESS           | AIRFREIGHTCMD        |                                | Air Freight Shipping  Type Command. Default: ""(Empty): Disable Air Freight Mode. |
| 8    | PROCESS           | ALLOCATEBIN          | 1                              | 1.Enable allocate bin  for F/G,0.Disabel allocate bin for F/G. |
| 9    | PROCESS           | ALLOWEDSTORAGELOC    |                                | If ALLOWEDSTORAGELOC  is empty then no need check storage Loc |
| 10   | PROCESS           | AUTOWEIGHTPALLETTYPE |                                | Maintain Pallet type  for Auto weight                        |
| 11   | PROCESS           | CHECK91PN            | 0                              | 0.Disable check 91  P/N; 1.Enable check 91 P/N               |
| 12   | PROCESS           | CHECKPYGIDIUMUPN     | 0                              | Check not allow mix  UPN when pygidium. 0 disable;1 Enable   |
| 13   | PROCESS           | CHECKUPNWEIGHTED     | 1                              | need check UPN weight  or not                                |
| 14   | PROCESS           | DISABLECOMPARE       | 0                              | 1.Disable compare  Carton/USN, 0.Enable compare Carton/USN   |
| 15   | PROCESS           | SCANTRACTORWEIGHT    | 1                              | 0/1:Disable/Enable  need scan tractor weight.                |
| 16   | PROCESS           | SHIPTYPEPALLETYPEMAP |                                | ShipType:PalletType;  Default ""; Ex:0:P; 1:P; 2:P; 3:A (ShipType: 0.Not Defined, 1.Land  Transportation, 2.Sea Shipping, 3.Air Freight) |
| 17   | UPDATEPPS         | HOLDREASON           | Label Not Check!               |                                                              |
| 18   | UPDATEPPS         | ISLMSGOLIVE          | 0                              | Control enable LMS  logic or old logic, default, old logic   |
| 19   | UPDATEPPS         | RELEASEREASON        | Check Label  Finished,Release! |                                                              |
| 20   | UPDATEPPS         | UPDATEPPSHOLD        | 1                              |                                                              |
| 21   | WEIGHT            | CHECKSTDWEIGHTBY91PN | 0                              | 0/1: Disable/Enable  check single pallet standard weight by internalPN. When it be used that  INI[UNFULLPALLETWEIGHTMODE] must equal 1. Default: 0 |
| 22   | WEIGHT            | DISABLECHECKWEIGHT   | 0                              | 0: enable check  weight when weight (original logic), default 0. 1: Disable check weight |
| 23   | WEIGHT            | KEYINWEIGHT          | 0                              | 0. not allow keyin  weight value; 1. allow keyin weight value |
| 24   | WEIGHT            | NEEDWEIGHT           | 1                              | 1.Enable weight  function 0.Disable weight function          |
| 25   | WEIGHT            | POSITIVEREVERSE      | 1                              | 0 Reverse;1 Positive                                         |
| 26   | WEIGHT            | TENEXPONENT          | -1                             | Config weight data to  how many exponent of ten;             |



## Related DB Objects

| Schema    | Table / View       | Description                         |
| --------- | ------------------ | ----------------------------------- |
| SFCFA/PCB | SFCPALLETSTDWEIGHT | UPN Standard weight                 |
| SFCFA/PCB | SFCPALLETWEIGHT    | Pallet weight by UPN                |
| SFCFA/PCB | SFCPALLET          | Pallet info                         |
| SFCFA/PCB | SFCPALLETITEM      | Pallet item info                    |
| SFCFA/PCB | SFCCARTONITEM      | Carton item info                    |
| SFCFA/PCB | SFCPALLETWEIGHTMSG | UPN Pallet Weight Error message LOG |
| SFCFA/PCB | SFCLABELJOBSETTING | Label job setting                   |
| SFCFA/PCB | UPN_WEIGHT_REPORT  | Check UPN has weighted              |
| SFCFA/PCB | cmpps133           | Now No Used. Use LMS                |
| SFCFA/PCB | SFCUSN             |                                     |
| SFCFA/PCB | SFCMO              |                                     |
| SFCFA/PCB | SFCMODEL           |                                     |
| CIMSFC    | SFCSTAGE           |                                     |
| CIMSFC    | CIMUSER            |                                     |

## Reference 

- [Version log](./MAWGT861_VersionLog.md)
- [SQL Log](/applications/ma/MAWGT861/MAWGT861_SqlLog.md)
- [MAWGT861 app.config](/applications/m-a/mawgt861/mawgt861.config.xml)