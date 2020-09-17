---
title: MAWGT862 Auto Weight
description: Auto Weight
published: true
date: 2020-09-02T08:05:15.307Z
tags: 
editor: undefined
---

## [Version](MAWGT862.assets/MAWGT862_VersionLog.md) ###

| **Revise date** | **Version** | **Modified by** | **Purpose**                                                  |
| --------------- | ----------- | --------------- | ------------------------------------------------------------ |
| 2020/07/08      | 2.0.17.4    | Winds Liang     | Enhancement: Support weighing of multi plant pallets by one program. |
| 2020/04/30      | 2.0.17.3    | Winds Liang     | Pallet ID对应的Warehouse的值要以Pallet ID在`sfcPalletItem`的`StorageLoc`为准. |

## Scope and Purpose   #####
**Scope:** SFCS.

**Purpose:** Auto Weighting for pallet weight, for warehouse packing operation. 

**Related Applications**:

- 1.[Weighting Module](../../../modules/Weighting.md)

- 2.[SMWGT861 Pallet Standard Weight Maintain](../../sm-system management/SMWGT861/SMWGT861.md) 

- 3.[SMMOWGT001](../../sm-system management/SMMOWGT001/SMMOWGT001.md)(MO Weight Maintain)

- 4.[MAWGT861 UPN Weight](../MAWGT861/MAWGT861.md)

  

## UI 

- **Login** 
		  	![Login UI](/applications/m-a/weighting/mawgt862/mawgt862_login.png)
        

- **Main** 
    (The main UI will have some differences depending on INI Settings)
   ![MAWGT862_MainUI](/applications/m-a/weighting/mawgt862/mawgt862_mainui.png)

## Application Logic
- [**Base Process Flow**](/applications/m-a/weighting/mawgt862/mawgt862_basicprocessflow.drawio)

  ![MAWGT862_BasicProcessFlow](/applications/m-a/weighting/mawgt862/mawgt862_basicprocessflow.png) 



## Key features

- 1.Check (base) data.

```plsql
(1) Check Pallet ID exist or not.
(2) Check the pallet Status is closed.
(3) Check Palletid whether exist in sfcpalletcompare. -- INI [DISABLECOMPARE]
(4) Check whether scan twice.
(5) Get Pallet's sotrage location, and check it.
(6) Check standard weight exist or not; and Check pallet weight whether is standard.
(7) check upn has weighted. -- INI [CHECKUPNWEIGHTED] 
...
```


- 2.Support multiple languages by INI `LANGUAGE` setting: 
```plsq
1.en-US; 2.zh-TW; 3.zh-CN
```

- 3.Weight data source Setting:
```plsql
1.INI [WEIGHTMACHINETYPE]:-1.Regular expressions(new); 0.Weight Machine(old).
2.INI [VALUEFROM]: 1. weight value from GetWeight.dll 2. weight value from COM port.
3.INI [WEIGHTVALUEFORMAT]: Regular Expression: get value from input string from COM port when Weight machine type is -1. like ".......(.*).." to get " 5.815" from "ST,GS,+ 5.815kg".
4.INI [POSITIVEREVERSE]: Scale data 0.Reverse; 1.Positive.
5.INI [TENEXPONENT]: Set weight data to how many exponent of ten.
```

- 4.Support scan multi pallet ID, scan "END" as complete scan pallet symbol，by INI `MULTISCANPALLETID` setting：

```plsql
INI [MULTISCANPALLETID], [FORBIDKEYBOARD], [SCANNERTIMESPAN]
1. Input栏位允许刷入多个栈板ID，再刷 “end” 作为终止表明该栏位完成input；
2. 当上述1动作完成后，光标自动跳到Total weight栏位；添加时间卡关防止手动key in重量
3. 当Total weight输入数值后，与Standard Weight进行比较检查时重量是否在标准范围内。
4. 如果Input栏位刷入2个以上栈板ID，则每个栈板重量平分=Total weight / Input的栈板ID个数
5. 输入palletid的时候需要开刷多个palletid是同一个料号而且展板的数量必须一致，也就是说输入第一个展板后刷第二个展板的料号（sfcpallet 的料号）和数量（ sfcpalletitem 的数量 ）必须跟第一个一致
6. 遇到未满展板和尾数展板的时候，不能推叠展板，需单独称重
```

- 5.Support weighing of multi plant pallets by one program, by INI `MULTIPLANTWEIGHT` setting:
```plsql
INI: [MULTIPLANTWEIGHT], [GETWMSAVAILABLEBIN]
Config: [FXXX_DBConnWebService], [FXXX_BasicWebService], [FXXX_LmsWebService]
1. 扫不同厂别的栈板单号的时候，需要切换不同厂别的SFCS程序，而且有且只能打开一个; 希望只用一个称重程式实现对不同厂别的栈板进行称重过账.
2. 栈板对应的LMS的储位因库别的不同而不同，但程序目前只能设定同一个; 希望根据栈板单号自动获取到储位:
  --Old Process: INI[STORAGELOCATION] 为储位的信息(WMS.Bin) --> Post Bin information to WMS;
  --New process: Get Warehouse from SFCPALLETITEM, by PALLETID --> Get WMS.Bin by WareHouse  --> Post Bin information to WMS.
Action
 1. New INI[MULTIPLANTWEIGHT] to support weighing of multi plant pallets by one program;
 2. Add Reference [LmsEPWebService], call its SFCGETPALLETINFO() function to get Plant;
 3. Add config [FXXX_DBConnWebService] and [FXXX_BasicWebService] to get DBConnWebService and BasicWebService by the corresponding Plant;  (while preserving the original BasicWebService and DBConnWebService to get workstaion and LoadINI);
 4. New INI [GETWMSAVAILABLEBIN]:
     --0(Default): INI[STORAGELOCATION] setting regard as WMS.Bin, then Post it to WMS; 
     --1: Call WMS.GetAutoGRBinForSFCS(), get and Post the first WMS.Bin to WMS.
```

- 6.Save and Send Pallet Weight Info to LMS
```plsql
INSERT INTO SFCPALLETWEIGHT;
LmsWebService.SendPalletWeightInfo(PalletWeightToLMS).
```

------



## Interface (Web Service)

| API  Module           | interface name                                               |
| --------------------- | ------------------------------------------------------------ |
| [DBConnWebService](#) | ExecuteScalar; FillDataSet;  ExecuteNonQuery; ExecuteNonQueryInSchema; ExecuteInTransaction. |
| [LogonWebService](#)  | loginByUserIDPassword; authenticateApIdByUserId.             |
| [BasicWebService](#)  | GetWorkStationGenealogy; GetApplicationIni; GetPackageItem; GetUPNPackage |
| [WmsWebService](#)    | CheckInventoryByPallet; GetAutoGRBinForSFCS; AddToInventoryBySn |
| [LmsWebService](#)    | ReleaseByBarcodeCheck; SendPalletWeightInfo                  |
| [LmsEPWebService](#)  | SFCSGetPalletInfo                                            |

​		P. S.: LMS is mainly divided into two parts: PP (warehouse packing operation) and EP (customs declaration);

​		注：LMS的主要分两部分PP(库房打包作业)和EP(关务报关);

## Configuration and INI

- **configuration setting** ([MAWGT862.config](MAWGT862.assets/MAWGT862.config.xml))

```xml
   <!--Must-->
<add key="DBConnWebService" value="http://10.41.21.91:808/DBConnect.WebService/DBConnect.WebService.asmx"/>
<add key="BasicWebService" value="http://10.41.21.91:808/basic.webservice/WebService.asmx"/>
<add key="LogonWebService" value="http://10.41.21.91:808/portalwebservice/logon.asmx"/>
<add key="WmsWebService" value="http://10.41.20.182/WM/Wms.Basic.WebService/WmsWebService.asmx"/>  
<add key="LmsWebService" value="http://10.41.20.191/PPExternalService/PPExternalService.svc"/>
<add key="LmsEPWebService" value="http://10.41.20.182/EPExternalService/EPExternalService.svc"/>
<add key="withCOM" value="0"/>
<add key="withPLCCOM" value="0"/>
<add key="WorkstationIP" value="10.41.56.119"/>
   <!--Optional-->
<add key="FXXX_DBConnWebService" value="http://localhost/DBConnect.WebService/DBConnect.WebService.asmx"/> 
<!-- For different plant set different DBConnWebService -->
<add key="FXXX_BasicWebService" value="http://localhost/basic.webservice/WebService.asmx"/> 
<!-- For different plant set different BasicWebService -->
<add key="FXXX_LmsWebService" value="http://localhost/PPExternalService/PPExternalService.svc"/> 
<!-- For different plant set different LmsWebService(PP) -->
```

- **initial settings**  ([SMAP005: Application Initial Setting Management](../../sm-system management/SMAP000/SMAP005.md))

> **Must:** 

| #    | SECTION | ITEM              | VALUE         | REMARK                                                       |
| ---- | ------- | ----------------- | ------------- | ------------------------------------------------------------ |
| 1    | COM     | COM_INPUTLEN      | 0             | Comm Setting:Input Length                                    |
| 2    | COM     | COM_PORT          | 1             | Comm setting:Port                                            |
| 3    | COM     | COM_SETTINGS      | 2400,N,8,1    | Comm Settings                                                |
| 4    | COM     | PLCCOM_INPUTLEN   | 0             | PLC Comm Setting:Input Length                                |
| 5    | COM     | PLCCOM_PORT       | 1             | PLC Comm setting:Port                                        |
| 6    | COM     | PLCCOM_SETTINGS   | 2400,N,8,1    | PLC Comm Settings                                            |
| 7    | PROCESS | PLANT             | F192          | Plant code.                                                  |
| 8    | PROCESS | SCANNERTIMESPAN   | 50            | Set scanner scan time span, unit is ms (1000ms = 1s)         |
| 9    | PROCESS | SOUNDPATH         | 0             | Maintain Sound Path                                          |
| 10   | PROCESS | STORAGELOCATION   | 0             | Maintain Storage Location                                    |
| 11   | WEIGHT  | VALUEFROM         | 2             | 1. Weight value from GetWeight.dll; 2. Weight value from COM port |
| 12   | WEIGHT  | WEIGHTMACHINETYPE | 0             | -1 Regular expressions(new);0 Weight Machine(old)            |
| 13   | WEIGHT  | WEIGHTVALUEFORMAT | .......(.*).. | get value from input string from COM port when Weight machine type is  -1     like ".......(.*).." to get " 5.815" from "ST,GS,+ 5.815kg" |

> **Optional:**

| #    | SECTION   | ITEM                       | VALUE | REMARK                                                       |      |
| ---- | --------- | -------------------------- | ----- | ------------------------------------------------------------ | ---- |
| 1    | LANGUAGE  | LANGUAGE                   | 1     | 1.en-US 2.zh-TW 3.zh-CN                                      |      |
| 2    | PROCESS   | ALLOCATEBIN                | 0     | 1.Enable allocate bin for  F/G,0.Disabel allocate bin for F/G. |      |
| 3    | PROCESS   | ALLOWEDSTORAGELOC          |       | If ALLOWEDSTORAGELOC is empty then  no need check storage Loc |      |
| 4    | PROCESS   | CHECK91PN                  | 0     | 0.Disable check 91 P/N; 1.Enable  check 91 P/N               |      |
| 5    | PROCESS   | DISABLECOMPARE             | 0     | 1: Disable compare function. 0:  Enable compare function(default) |      |
| 6    | PROCESS   | FORBIDKEYBOARD             | 0     | 0: Allow key in with key board  (default); 1: Forbid key in. |      |
| 7    | PROCESS   | GETWMSAVAILABLEBIN         | 0     | 0(Default): WMS.Bin from  INI[STORAGELOCATION],     1:WMS.Bin from WMS.GetAutoGRBinForSFCS() |      |
| 8    | PROCESS   | ISLMSGOLIVE                | 0     | Enable LMS logic or old logic,  default,0.old logic          |      |
| 9    | PROCESS   | MULTIPLANTWEIGHT           | 0     | 0.Disabel(Default)/1.Enable: support  weighing of multi plant pallets by one program |      |
| 10   | PROCESS   | MULTISCANPALLETID          | 0     | 0:Disabel, 1:Enable scan multi pallet                        |      |
| 11   | PROCESS   | SLEEPTIMEFORCLEANPLCCOM    | 0     | Sleep time before clean PLC COM,  default(0 s)               |      |
| 12   | PROCESS   | SUPPORTFAPCB               | 0     | 1: Enable support FA and PCB schema  at the same time 0: Disable |      |
| 13   | PROCESS   | SUPPORTFAPCBSTAGE          |       | Set stage to get DB schema in basic  web service when enable ini SUPPORTFAPCB. Format:  schema1:stage1\|schema2:stage2, for example: FA:SN\|PCB:SA |      |
| 14   | UPDATEPPS | HOLDREASON                 |       | Hold reason                                                  |      |
| 15   | UPDATEPPS | RELEASEREASON              |       | Release reason                                               |      |
| 16   | UPDATEPPS | UPDATEPPSHOLD              | 0     | Update PPS, 0:Disable 1:Enable                               |      |
| 17   | WEIGHT    | BYPASSREDUPLICATEDPALLETID | 0     | 0:Disabel, 1:Enable pass  reduplicated pallet ID             |      |
| 18   | WEIGHT    | CHECKINVENTORYBYPALLET     | 0     | 0:Disabel, 1:Enable check inventory  by pallet               |      |
| 19   | WEIGHT    | CHECKUPNWEIGHTED           | 1     | need check UPN weight or not                                 |      |
| 20   | WEIGHT    | POSITIVEREVERSE            | 1     | 0 Reverse;1 Positive                                         |      |
| 21   | WEIGHT    | TENEXPONENT                | 0     | Config weight data to multiply how  many ten;                |      |

------

## Related DB Objects

| Schema    | Table /View        | Description            |
| --------- | ------------------ | ---------------------- |
| SFCFA/PCB | SFCPALLETSTDWEIGHT | UPN Standard weight    |
| SFCFA/PCB | SFCPALLETWEIGHT    | Pallet weight by UPN   |
| SFCFA/PCB | SFCPALLET          |                        |
| SFCFA/PCB | SFCPALLETITEM      | Pallet item            |
| SFCFA/PCB | SFCCARTON          |                        |
| SFCFA/PCB | SFCCARTONITEM      | Carton item            |
| SFCFA/PCB | SFCPALLETCOMPARE   | Pallet Compare         |
| SFCFA/PCB | SFCUPNPACKAGE      | UPN package            |
| SFCFA/PCB | UPN_WEIGHT_REPORT  | Check UPN has weighted |
| SFCFA/PCB | SFCUSN             |                        |
| SFCFA/PCB | SFCMO              |                        |
| SFCFA/PCB | SFCMODEL           |                        |
| CIMSFC    | SFCSTAGE           |                        |
| CIMSFC    | CIMUSER            |                        |

## Reference 

- [Version log](./MAWGT862_VersionLog.md)
- [SQL Log](./MAWGT862_SqlLog.md)
- [MAWGT862 app.config](/applications/m-a/weighting/mawgt862/mawgt862.config.xml)