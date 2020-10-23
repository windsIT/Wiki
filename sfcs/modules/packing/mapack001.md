---
title: MAPACK001  Packing (Win Form)
description:  Packing (Win Form)
published: true
date: 2020-10-23T09:01:16.215Z
tags: packing
editor: markdown
dateCreated: 2020-10-23T09:01:16.215Z
---

# Purpose
1. Avoid NG products shipping to  customer(避免 NG的产品出货给客户)
2. Ensure proper and fast packing（确保包装正确、快速）
3. To package the qualified product together, one box can be set to package one USN or more USNs(将符合条件的机台包装在一起，可以设置一个箱子包一个机台或者多个机台)
4. To support print Carton Label(支持打印 Carton Label)
5. SFCS Record history for user tracking.( SFCS 记录历史数据方便追踪)
6. Sampling warning(抽样)
7. Support carton weighing(支持包装并称重)——Win Form Application

# Process Flow
- `Packing` stage in SFCS flow
![Packing Architecture](/sfcs/modules/packing/mapack001/packing_architecture.png)
## Packing Flow
- `Packing` Basic Process flow[^1]
![Sample flow](/sfcs/modules/packing/mapack001/packing_sample_flow.png)
[^1]: 注：需要改为在线画DrawIO图.

- `Packing` Detail Process flow
![Packing Detail Flow 01](/sfcs/modules/packing/mapack001/packing_detail_flow01.png)
![Packing Detail Flow 02](/sfcs/modules/packing/mapack001/packing_detail_flow02.png)

# Operation 
## Packing Command
Different command will call different function.
| Command | Description                        | Function    |
| ------- | ---------------------------------- | ----------- |
| LGN     | Login                              | CMD_LGN()   |
| WGT     | Weight                             | CMD_WGT()   |
| %%%     | Administrator                      | CMD_ADMIN() |
| CHC     | Check  lost component Qty          | CMD_CHC()   |
| CMP     | Compare barcode                    | CMD_CMP()   |
| ERR     | Test Error                         | CMD_ERR()   |
| REP     | Replace component                  | CMD_REP()   |
| TOK     | Test OK                            | CMD_TOK()   |
| MIP     | MO input                           | CMD_MIP()   |
| CID     | Scan Customer Carton  ID           | CMD_CID()   |
| MCT     | To maintain MO line  restrict data | CMD_MCT()   |
## Basic Operation
### Normal Packing
Normal packing in `Packing` view: In this view have many functions.
![Packing view](/sfcs/modules/packing/mapack001/packing_ui.png)
1. **Assembly Component (Optional) and Generate Carton ID** 
  - If **need assembly component**, the operation flow is: **SCAN USN ---> CSN ---> CSN1....--->CSNX--->Generate CartonID ---> Scan next USN**
    - Scan CSN:
    	![Assembly Component](/sfcs/modules/packing/mapack001/input_csn.png)
  - If **need <font color="red">not</font> assembly component**, the operation flow is:  **SCAN USN --->Generate CartonID ---> Scan next USN-->.......  ---> Unit Carton ID close**    
    - Scan USN:
    	![Scan USN](/sfcs/modules/packing/mapack001/scan_usn.png)

2. **Compare item**
  - The operation flow is: **SCAN USN --->Scan compare item value--->...---> Until compare completed---> Generate Carton ID**
    ![Compare item](/sfcs/modules/packing/mapack001/compare_item.png)
    
### (Force) Manual Close Carton
- (1) When user click the button `Show unfinished carton` in the Packing view, it will jump to the view `Unfinished Carton`, and query unfinished carton by follwed SQL statement:
  ```SQL
   SELECT * FROM SFCCARTON WHERE WORKSTATION=':WorkstationValue' AND STATUS=0
  ```
  ![Unfinished Carton](/sfcs/modules/packing/mapack001/unfinished_carton.png)
  
- (2) When user click the `Close` button, it will close the carton by follwed SQL statement:
   (Pay attention, if enable INI `CARTONCLOSEUSERGROUP`, it will check the close Authority.)
  ```SQL
   UPDATE SFCCARTON SET STATUS=1,TRNDATE=SYSDATE WHERE CARTONID=':CartonValue'
  ```
### Merge Carton
- Scan Carton ID, it will merge these cartons into one carton, as long as the total quantity is valid. 
 If check the `Master Carton`, others will merge into it, instead of generating a new carton ID.
 ![Meger Carton](/sfcs/modules/packing/mapack001/meger_carton.png)

### Split Carton
1. Input the original Carton that will being splited, its USN will be displayed in the Original Carton list box;
2. Input USN to split from original carton, it will be displayed in the New Carton list box;
3. After splited. Lastly, click `Close New Carton` button, then other USN will be displayed in another New Carton list box.
 ![Split Carton](/sfcs/modules/packing/mapack001/split_carton_ui.png)

# Key features (Customization)


# Interface (Web Service)
it will call webservice([Basic.WebService]()/[LCSWebService]()/[WmsWebService]()) function.
| Reference         | Fucntion                      | Description                                                  |
| ----------------- | ----------------------------- | ------------------------------------------------------------ |
| Basic  Webservice | GetApplicationIni()           | Get WorkStation INI                                          |
| Basic Webservice  | GetWorkStationGenealogy()     | Get WorkStation information                                  |
| Basic Webservice  | IsRoHSItem()                  | Check ROHS                                                   |
| Basic Webservice  | GetMoGenealogy()              | Get mo Genealogy                                             |
| Basic Webservice  | GetUsnGenealogy()             | Get Unit Genealogy                                           |
| Basic Webservice  | [ApproveProcessStart()]()     | Approve SFC Process  Start,Routing Check                     |
| Basic Webservice  | GetLinkUSN()                  | Get Multi-Board Link  All USN                                |
| Basic Webservice  | [BarcodeValidation()]()       | Check Barcode  validation                                    |
| Basic Webservice  | IsCPNComplete()               | Check the CPN in the  Stage is Completed                     |
| Basic Webservice  | GetUPNPackage()               | Get Package  Information by Package ID                       |
| Basic Webservice  | GeneratePackageID()           | Generate Package ID                                          |
| Basic Webservice  | GetPackageItem()              | Get Package Item By  Package ID and Package Level            |
| Basic Webservice  | [CompleteProcess()]()         | Complete SFC  Process,Record Log                             |
| Basic Webservice  | CheckSampling()               | Check Unit Sampling  after this stage                        |
| Basic Webservice  | GetCompareSetting()           | Get compare setting                                          |
| Basic Webservice  | GetItemValue()                | Get Item Value                                               |
| Basic Webservice  | GenerateLotNo()               | Generate Lot No, For  Hold Shipment(used with ini[GENERATELOTNO]) |
| Basic Webservice  | RequestLabelPrint()           | Request a Label Print  Command                               |
| Basic Webservice  | HoldOperation()               | Hold SFC Operation                                           |
| Basic Webservice  | BoardExceedRequiredHours()    | Board Exceed Required  Hours                                 |
| Basic Webservice  | AssignTempLocation()          | Assign temporary  Location                                   |
| Basic Webservice  | ReleaseTempLocation()         | Release temporary  Location                                  |
| Basic Webservice  | RaisePackRackRequest()        | Raise Pack Rack  Request                                     |
| Basic Webservice  | SetLightForUnit()             | Set K2L Light On for  Unit(used with INI[EnableCombinePTL])  |
| Basic Webservice  | SetLightsForUnitPTL()         | Set P2L Light On for  Unit((used with INI[SkipPTLFlag]))     |
| Basic Webservice  | SetLightForComponent()        | Set KTL Light for  Special CPN(used with INI[EnableCombinePTL]) |
| Basic Webservice  | SetLightsForComponentPTL()    | Set P2L Light for  Special CPN((used with INI[SkipPTLFlag])) |
| Basic Webservice  | SetCOA()                      | Process COA                                                  |
| LCSWebService     | Get_SSN_Rack_by_Workstation() |                                                              |
| WmsWebService     | AllowMergeSplitInSFCS()       |                                                              |

# Config and INI
- **Configuration Setting** ([MAPACK001 App.config](/sfcs/modules/packing/mapack001/mapack001.config.xml))
  ```xml
	<add key="LogonWebService" value="http://10.41.21.91:808/PortalWebService/Logon.asmx"/>
	<add key="BasicWebService" value="http://10.41.21.91:808/Basic.WebService/WebService.asmx"/>
	<add key="DBConnectWebService" 	value="http://10.41.21.91:808/DBConnect.WebService/DBConnect.WebService.asmx"/>
	<add key="P2L" value="http://10.42.23.30/P2Lservice/SFC.asmx" />
	<add key="LCSWebService" value="http://10.42.23.30/LCS.webService/LCS_Service.asmx" />
	<add key="WmsWebService" value="http://wms232.wks.wistron.com.cn/Wms.Basic.WebService/WmsWebService.asmx" />
	<!-- Max Component Q'ty, Default is 99, can not be null, add by Daryl Guo 20151119 -->
	<add key="MaxComponentQty" value="99" />
	<add key="AllowMultiAP" value="1" />
	<add key="withCOM" value="0" /> <!-- Weight command:WGT; default value is 0-->
	<add key="virtualWorkstationIP" value="10.41.56.119" /> <!-- 2012/08/12 Add for Debug -->
	<add key="EnableSaveErrorLog" value="0" /><!--When Message ID equals SFCF01451, record Error Log to DB; default value is 0-->
  ```

- **Initial Settings** ( [SMAP005: Application Initial Setting Management](/sfcs/applications/sm/smap000/smap005)) 
  1. **Must**
  
  
  2. **Optional**



# Related DB Objects[^2]
| Schema    | Table / View  | Description           |
| --------- | ------------- | --------------------- |
| SFCFA/PCB | SFCCARTON     | SFCS Carton header    |
| SFCFA/PCB | SFCCARTONITEM | SFCS Carton item info |
| SFCFA/PCB | SFCUPNPACKAGE | Unit package          |
| SFCFA/PCB | SFCLABELJOB   | SFCS Label Job        |

[^2]: 注：待补充其他表

# Reference
- [Version log](./mapack001/versionlog)
- [SQL Log](./mapack001/sqllog)
- [MAPACK001 App.config](/sfcs/modules/packing/mapack001/mapack001.config.xml)

