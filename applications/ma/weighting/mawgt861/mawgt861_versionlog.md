---
title: MAWGT861 Version Log
description: 
published: true
date: 2020-08-26T03:51:10.392Z
tags: 
editor: undefined
---

MAWGT861, v2.0.4.9, 2020/06/19, UPN Weight, by Winds Liang  
=========================================================
Issue: [WZS F138] [`CR.NO`: F138_PR20200618001]
1. Issue: "Conversion from string "--" to type 'Integer' is not valid" in `writeErrorMsg` function.

Action:
1. Modify its parameter[weight] data type(from 'Int32' to 'String'); If `weight`(Ex."--") is not Number format, Insert NULL to SFCPALLETWEIGHTMSG.WEIGHT

MAWGT861, v2.0.4.8, 2020/05/11, UPN Weight, by Winds Liang  
=========================================================
Requirement: [WZS F138] [CR.NO: F138_CR20200416001]
1. 希望F138 称重入库程式可满足同一791料号周转栈板(海运)与带栈板出货(空运), 即满足同一料号2种运货方式的入库，避免因重量差异导致报关异常.

Action:
1. New INI[AIRFREIGHTCMD]:
    --Set the Air Freight Shipping Type Command, Default ""(Empty):Disable Air Freight Mode;
    --Scan the Command to enable Air Freight mode weighing;
    --Check: AirFreight pallet, must scan the Command firstly; Not AirFreight pallet, shoud not scan it.
2. New INI[SHIPTYPEPALLETYPEMAP]: ShippingType:PalletType Map; Default ""; Ex:0:P; 1:P; 2:P; 3:A.  
(Shipping Type: 0.Not Defined, 1.Land Transportation, 2.Sea Shipping, 3.Air Freight).
3. Add the logic:
    --Get MO Shipping Type by PalletID, then get its corresponding Pallet Type;(Different pallet types have different standard weight)
    --Check: a pallet cannot mix multiple Shipping Type.


MAWGT861, v2.0.4.7, 2019/04/18, UPN Weight, by Mark M Zhou 
=========================================================
Requirement/Action: [WZS F138] [`CR.NO`: F138_CR20190307001] [Project: Internal PN for Weighting]
1. Modify the logic to calculate 791PN in standard weight.

MAWGT861, v2.0.4.6, 2019/04/16, UPN Weight, by Mark M Zhou 
=========================================================
Requirement: [WZS F138] [CR.NO: F138_CR20190307001] [Project: Internal PN for Weighting]
1. Abnormal weight of different 791PN in Storage, support check a palletid weight by 791PN to store in.

Action:
1. Add INI['CHECKSTDWEIGHTBY91PN] to check single pallet standard weight by internalPN. When it be used that INI[UNFULLPALLETWEIGHTMODE] must equal, SFCS以791料号设置base data称重入库----WMS按客户料号入账----SAP按客户料号入账
2. Modify StandardWeight, support check a palletid weight by 791PN to store in.

MAWGT861, v2.0.4.5, 2018/10/15, UPN Weight, by Poppy Zhou
=========================================================
Requirement: [WZS F138] [CR.NO: F138_CR20181010001] [Project: Internal PN for Weighting]
1. Change 91PN datasource from SFCMO.LONGTEXT to SFCMO.INTERNALPN.

Action:
1. Alter TABLE SFCMO column INTERNALPN to store in 91 PN.
2. Get 91PN from SFCMO.INTERNALPN.

MAWGT861, v2.0.4.4, 2018/09/18, UPN Weight, by Poppy Zhou
=========================================================
Requirement: [WZS F138] [CR.NO: F138_CR20180914001]
1. Adjust COMMAND “MWOEP” process, to support Single unfull pallet weight.
	If Enable Single mode, operation: MWOEP -> Pallet1
	Else if Multi mode, operation: MWOEP -> Pallet1…PalletN -> COMPLETE

Action:
1. Add INI[PROCESS]/[UNFULLPALLETWEIGHTCMD] to set Unfull Pallet Weight Command.
2. Add INI[PROCESS]/[UNFULLPALLETWEIGHTMODE] to set Unfull pallet weight work mode.

MAWGT861, v2.0.4.3, 2018/05/18, UPN Weight, by Epson Chen
=========================================================
Requirement: [WZS F130] [F130_CR20180425006,F130_CR20180510005]
1. Add Pallet type to distinguish normal pallet and special pallet and get standard weight by UPN+QTY+PALLETTYPE.
2. Add INI to control disable compare carton/usn.
3. Add INI to setup default pallet type for Auto weight
Action:
1. Add Pallet type to distinguish normal pallet and special pallet and get standard weight by UPN+QTY+PALLETTYPE.
2. Add INI[DISABLECOMPARE] to control disable compare carton/usn.
3. Add INI[AUTOWEIGHTPALLETTYPE] to setup default pallet type for Auto weight 

MAWGT861, v2.0.4.2, 2018/04/04, UPN Weight, by Poppy Zhou
=========================================================
Requirement: [WZS F130] [CR.NO: F130_CR20180322001]
1. Needn't check standard pallet weight when user assess pallet's weight is ok.

Action:
1. Add ini [WEIGHT/DISABLECHECKWEIGHT] to control whether need to check UPN weight.

MAWGT861, v2.0.4.1, 2018/02/27, UPN Weight, by Lucky Z Li 
=========================================================
Issue: [WZS F130] [F130_PR20180208001_IT]
1. INI Check91PN = 0, but still get 91PN to send to LMS.
    Expect Check91PN = 0, then no need check/Get 91PN, and no need send 91PN to LMS.
Action:
1. Modify SavePalletWeight, if Check91PN = 0, then no need check/Get 91PN, and no need send 91PN to LMS.

MAWGT861, v2.0.4.0, 2018/1/23, UPN Weight, by Aglaia Shi
=========================================================
Issue: [WZS F138]
1. For a while, the call WMS passed in the parameter USNQty to the PalletItemQty, resulting in an exception.
Action:
1. When call WMS, send the USNQty are not PalletItemQty.

MAWGT861, v2.0.3.0, 2015/4/29, UPN Weight, by Epson Chen
=========================================================
Issue: [WZS F192]
1.The weight of LMS and the quantity of LMS are 0.
2.The program not release PPS hold by LMS 
Action:
1.Change the character type of LMS weight and LMS quantity to String type.
2.Delete 'i=i+1' in get USN list logic.

MAWGT861, v2.0.2.0, 2015/4/27, UPN Weight, by Epson Chen
=========================================================
Issue: [WZS F192]
1.The weight of LMS and the quantity of LMS are 0.
Action:
1.Change the character type of LMS weight and LMS quantity to double type

MAWGT861, v2.0.1.0, 2015/4/22, UPN Weight, by Epson Chen
=========================================================
Issue: [WZS F192]
1.The program call WMS and LMS. But when 91 P/N(from sfcmo.Longtext) is empty and call LMS web service,it will wrong. But it call WMS succeed.
Action:
1.Add ini [PROCESS/CHECK91PN] to control whether to check 91 P/N is empty or not.
2.ini AllowedStorageLoc support multi storage

MAWGT861, v2.0.0.0, 2015/4/1, UPN Weight,by Joyce Lv
=========================================================
Requirement: [WZS F192]
1. SFCS Call LMS Webservice to release PPS Hold (New ini: ISLMSGOLIVE control enable LMS logic or old logic, default, old logic)
2. Move table SFCPALLETWEIGHT to SFC CIMSFC schema. Program insert data to CIMSFC.SFCPALLETWEIGHT, 
it need add new column: 91P/N (from Longtext ) SFCS get 91 P/N from SFCMO.LONGTEXT to sfcpalletweight.InternalPN
 (New ini: ISLMSGOLIVE control enable LMS logic or old logic, default, old logic).Then sync CIMSFC.SFCPALLETWEIGHT to LMS DB
3. Add INI [PROCESS/ALLOWEDSTORAGELOC], if SFCPALLETITEM.STORAGELOC is different from this INI setting, show error message. If INI setting is empty, then don't check it.
Action:
1.Add INI setting:[UPDATEPPS/ISLMSGOLIVE] for F192 LMS project to control enable LMS logic or old logic, default, old logic.
2.New Message "SFCF07718" to show "LmsWebService URL is empty or not find LmsWebService URL".
3.New Message "SFCF07719" to show "SFCS send pallet[%$] weight Info. to LMS NG:%$".
4.New Message "SFCF07720" to show "Release LMS hold NG:%$"
5.Add Web.config "LmsWebService" which value is Web reference URL.
6. Add INI [PROCESS/ALLOWEDSTORAGELOC], if SFCPALLETITEM.STORAGELOC is different from this INI setting, show error message. If INI setting is empty, then don't check it.
7.New Message "SFCF07721" to show "The SFCPALLETITEM.StorageLoc can not be empty, PalletID[%$]".
8.New Message "SFCF07722" to show "The Pallet[%$] can not be put in this storage[%$]"
9. Initial release.
        * Build with VS2008
        * Target framework: .NET Framework 3.5



MAWGT861, v1.0.17.0, 2014/10/20,UPN Weight,by Epson Chen
=========================================================
Requirement: [WZS F192]
1.Add check not allow mix UPN.
2.Expect: Post weight data to WMS after compare ok
Action:
1.Add ini setting:[PROCESS/CHECKPYGIDIUMUPN],Check not allow mix UPN when pygidium.
2.After compare ok,then post weight data to WMS.

MAWGT861, v1.0.16.0, 2014/07/21,UPN Weight,by Epson Chen
================================================================================
issue: [WZS F192]
1.F192 稱重程式抛WMS quantity 时出现异常:60A3UAR2US這個料號的問題，是因為SFCS的稱重程式對於一Carton包多PCS的情況。入庫WMS時寫WMSINVENTORY的quantity是Carton的數量導致。
2. 抓标准重量时, 也是按Carton数量计算
Action:
1.Modify:Change AddToInventory into AddToInventoryBySn and change SerchAvailableBin into SearchAvailableBinForPackentity
2.Modify:Through the Qty of USN to find the standard weight when only input a pallet
3.Modify:Change quantity from Carton Qty to USN Qty when AddToInventoryBySn and MWOEP

MAWGT861, v1.0.15.0, 2014/05/22,UPN Weight,by Epson Chen
================================================================================
Requirement: [WZS F192]
1.刷油压车重量时，系统弹出一个对话框获取地磅秤重量值，程式没有减去铁牛重量
2.刷Palletid后程式会再次获取一次重量，并且会将前一次获取的重量覆盖.
Action:
1.Modify that reduce Tractor Weight when check Pallet Weight or input complete

MAWGT861, v1.0.14.0, 2014/05/15, Weight by Pallet,by Epson Chen
================================================================================
Requirement: [WZS F192]
1.程式减掉Pallet Weight重量目前发现并板时问题点是基本资料维护的Pallet Weight是8，而Total Weight减掉却是16.
2.同一个Palletid可以连续输入两次，并且刷入complete程式将两个相同的Palletid计算了重量.
3.整板时，Total Weight 有减去Pallet Weight 的话那么Standard Weight 也应该同时减去Pallet Weight 
4.如果上一笔并板未完成，再次输入并板指令MWOEP重新并板则会发现Standard Weight上一笔记录并没有清空.是当前重量和上一笔重量的累加.
5.在并板发现有问题时，把这个板拉走入其他正常的栈板时，需要把程式重开.不重开的话会就会一直在MWOEP这个指令下面死循环
Action:
1.Modify that Total Weight Subtract Pallet Weight one times
2.Check same Palletid when MWOEP
3.Modify that Standard Weight Subtract the Pallet Weight when compare with the total weight
4.Clear out Standard Weight when MWOEP
5.Modify that when MWOEP and NG,it can handle next Pallet

MAWGT861, v1.0.13.1, 2014/05/05, Weight by Pallet,by Epson Chen
================================================================================
Requirement: [WZS F192]
1.修改并板程式输入指令MWOEP->刷油压车重量->第一个Palletid->库位->第二个Palletid->Complete->系统计算两个Palletid机台数量获取数据比对Pallet Standard Weight Maintain 对应UPN数量的设定重量上下限，在设定值内Pass进入下一环节->Cartonid->àEnd.
2.Pallet Standard Weight Maintain 维护的栈板和机台的重量，不包含油压车重量.系统在界面上在刷油压车重量时直接将油压车重量扣除只得到栈板和机台的总量马上传重量资料和维护的实际资料做比对.同时将资料上传WMS.
Action:
1.Modify the logic that when MWOEP and complete input Palletid,then compare with Pallet Standard Weight
2.Modify that calculate the Pallet Standard Weight when MWOEP 

MAWGT861, v1.0.13.0, 2014/04/30, Weight by Pallet,by Epson Chen
================================================================================
Requirement: [WZS F192]
1.修改并板程式输入指令MWOEP->刷油压车重量->第一个Palletid->库位->第二个Palletid->Complete->系统计算两个Palletid机台数量获取数据比对Pallet Standard Weight Maintain 对应UPN数量的设定重量上下限，在设定值内Pass进入下一环节->Cartonid->àEnd.
2.Pallet Standard Weight Maintain 维护的栈板和机台的重量，不包含油压车重量.系统在界面上在刷油压车重量时直接将油压车重量扣除只得到栈板和机台的总量马上传重量资料和维护的实际资料做比对.同时将资料上传WMS.
Action:
1.add a ini[LOGIN/LOGIN]
2.Modify that when input the tractor weight,the total weight minus the tractor weight ,then compare with Pallet Standard Weight
3.Add a logic to check Pallet Weight when it is tail plate number
4.Add a logic that Pop-up login UI when it is tail plate number and before save pallet weight

MAWGT861, v1.0.12.0, 2014/04/30, Weight by Pallet,by Epson Chen
================================================================================
Requirement: [WZS F130]
As-is:
MAWGT861 目前有两种type get weight :ValueFrom /1. weight value from GetWeight.dll 2. weight value from COM port 
目前新进一种秤不能通过dll get weight, 使用get weight from COM Port时也得不到正确的重量，但是使用MAWGT003/MAWGT004 WEIGHTMACHINETYPE=’-1’时可以通过设定WEIGHTVALUEFORMAT得到正确的重量
To-be:
1.修改程式使其支持MAWGT003/MAWGT004 WEIGHTMACHINETYPE=’-1’相同的抓重量逻辑.
2.能够抓取正向/反向数据，通过正向/反向设置以及WEIGHTVALUEFORMAT设置可以灵活抓取多种数据格式满足不同的需求.
Action:
1.Add a ini:[WEIGHT/WEIGHTMACHINETYPE] to select the weight machine type
2.Add a ini:[WEIGHT/POSITIVEREVERSE]  to get the result of positive or the result of reverse 
3.Add a judge to get result of positive or reverse.
4.Add a key:WorkstationIP
5.Add for Win form get IP v4 Address in OS Win7

MAWGT861, v1.0.11.1, 2013/07/15, Weight by Pallet,by Jaden Chen
================================================================================
Requirement: [F192]
1.MAWGT861 系统称重 称出了 负数
Action:
1. Add check before Save SFCPalletWeight, Check Weight Data must >0, if Weight Data <=0, show Error.

MAWGT861, v1.0.11.0, 2013/03/06, Weight by Pallet,by Aimee Lu 
================================================================================
1.Change quantity from Carton Qty. to USN Qty. when AllocateBinForFG/AddToInventory.

MAWGT861, v1.0.10.0, 2012/04/20, Weight by Pallet, 
================================================================================
1.Modify:when checked tractor weight not check again when input is number;
2.Modify:turn string to double when compare tractor weight and maxweight or minweight;


MAWGT861, v1.0.9.0, 2011/11/01, Weight by Pallet, 
================================================================================
1.Modify:position of cursor when input the command of MWOEP; 
2.Modify:并板时 scanned each 2D Barcode of all Palletid;
3.Modify:The Record about weight and allocate bin

MAWGT861, v1.0.8.0, 2011/10/26, Weight by Pallet, 
================================================================================
1.Add: Command to distinguish multiple pallet; 
2.add: Clip the tractor weight;
3.Modify: DB SQL to auto to calculate the pallet weight
<!-- Tractor weight-->
<add key="MaxTractorWeight" value="90" />
  <add key="MinTractorWeight" value="80" />

MAWGT861, v1.0.6.0, 2011/01/10, Weight by Pallet, by Key Zhang
================================================================================
1.Fix:Remove spaces of SQL; 
2.Fix:When NG message,show red color. 

MAWGT861, v1.0.5.0, 2010/12/30, Weight by Pallet, by Key Zhang
================================================================================
1.当秤称取的重量不符合标准，需要手动输入重量时，则必须使用权限，点击权限后，系统只抓取输入的重量值；
2.记录了四个error message到DB中，messageID：SFCF07714,SFCF07713,SFCF07712,SFCF07709;
3.WMS分配储位失败，则不会解除PPS hold。

MAWGT861, v1.0.4.4, 2010/10/20, Weight by Pallet
================================================================================
1.Modify UI Performance.

MAWGT861, v1.0.4.3, 2010/10/15, Weight by Pallet
================================================================================
1.Add function for Getting the same material of the latest used bin for Move in.

MAWGT861, v1.0.4.2, 2010/10/12, Weight by Pallet
================================================================================
1.Modify show WMS Bin logic,When open INI:ALLOCATEBIN.

MAWGT861, v1.0.4.1, 2010/09/27, Weight by Pallet
================================================================================
1.Add new form show all available bin,user can select bin for manaul allocate bin  -F192 WMS

MAWGT861, v1.0.4.0, 2010/09/27, Weight by Pallet
================================================================================
1.Modify the way of reference WmsWebService  -F192 WMS

MAWGT861, v1.0.3.6, 2010/09/03, Weight by Pallet
================================================================================
1.Add check if UPN has weight record or not  -F192
