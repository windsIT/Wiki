---
title: SFCS
description: SFCS Home: Introduction to the SFCS
published: true
date: 2020-10-26T07:20:35.259Z
tags: sfcs
editor: markdown
dateCreated: 2020-08-25T07:34:52.818Z
---

- [:link:SFCS Docs Wiki.js Guide Page *:arrow_forward:*](/en/sfcs/guide)
{.links-list}

# Introduction to the SFCS
- These SFCS docs help you learn and use SFCS, no matter beginner or expert. 

- If you are beginner, please use [getting started]().

- If you are expert, you can use [applications]() for more detail.

---

## SFCS Navigation
## Tabs {.tabset}
### SFCS
### Started 
- [:globe_with_meridians: Getting Started *Getting Started with SFCS.* *:white_check_mark:*](/sfcs/started/gettingstarted)
- [:package: Permission Setting *Applications Permission Setting.* *:x:*](/sfcs/started/permissionsetting)
- [:clipboard: Base Data Setting *Base Data Setting(for common flow)* *:x:*](/sfcs/started/basedatasetting)
- [:clipboard: SFCS Flow *SFCS Common Flow* *:x:*](/sfcs/started/sfcscommonflow)
{.links-list}
### Modules 
- [:house: Modules Content *Modules Menu* *:arrow_forward:*](/en/sfcs/modules)
- [:office: MO Download *:x:*](/en/sfcs/modules/mo_download)
- [:curly_loop: MO Readiness Check *:x:*](/en/sfcs/modules/mo_readiness_check)
- [:house: SN Generator *:x:*](/en/sfcs/modules/sn_generator)
- [:curly_loop: SMO *:x:*](/en/sfcs/modules/smo)   
- [:house: Function Test *:x:*](/en/sfcs/modules/function_test)
- [:package: Packing *:white_check_mark:*](/en/sfcs/modules/packing)
- [:house: Item Compare *:x:*](/en/sfcs/modules/item_compare)
- [:office: Weighing *:white_check_mark:*](/en/sfcs/modules/weighing)
- [:ship: Store In *:x:*](/en/sfcs/modules/store_in)
- [:house: Labeling *:x:*](/en/sfcs/modules/labeling)
- [:repeat: Repair *:x:*](/en/sfcs/modules/repair)   
- [:house: Sampling *:x:*](/en/sfcs/modules/sampling)
- [:curly_loop: OOB *Out Of Box* *:x:*](/en/sfcs/modules/oob)
- [:house: P2L *:x:*](/en/sfcs/modules/p2l)
- [:curly_loop: Prewarning *:x:*](/en/sfcs/modules/prewarning)
- [:house: Auto Line Shut Down *:x:*](/en/sfcs/modules/autolineshutdown)
{.links-list}
### Applications
- [:office: WebServices *:white_check_mark:*](/en/sfcs/applications/webservices)
- [:curly_loop: MA *Manufature Application* *:white_check_mark:*](/en/sfcs/applications/ma)
- [:house: SM *System Management* *:white_check_mark:*](/en/sfcs/applications/sm)
- [:office: Super APP *:white_check_mark:*](/en/sfcs/applications/superapp)
- [:curly_loop: P2L *Pick-to-Light* *:white_check_mark:*](/en/sfcs/modules/p2l)
{.links-list}
### Projects 
- [:office: Annie *Annie Non KC* *:x:*](/en/sfcs/project/annienonkc)
- [:curly_loop: BeltLine *:x:*](/en/sfcs/project/beltline) 
- [:house:Iris *Iris EDI Project* *:x:*](/en/sfcs/project/iris)
- [:curly_loop: Lily *:x:*](/en/sfcs/project/lily)   
- [:house:Rosa *Rosa Auto Scheduling* *:x:*](/en/sfcs/project/rosa)
- [:curly_loop: Sandra *:x:*](/en/sfcs/project/sandra)
- [:house:SCT *Squeegee* *:x:*](/en/sfcs/project/sct)
- [:curly_loop: WW *:x:*](/en/sfcs/project/ww)
- [:house:Yama *:x:*](/en/sfcs/project/yama)
{.links-list}
### IT Guide 
- [:office: Doc Guide *:x:*](/en/sfcs/it_guide/docguide)
- [:curly_loop: Development Guide *:x:*](/en/sfcs/it_guide/devguide)
- [:house: Installation *:x:*](/en/sfcs/it_guide/installation)
{.links-list}
### About
- [:office: Message ID *:x:*](/en/sfcs/about/message_id)
- [:curly_loop: Interfaces *:x:*](/en/sfcs/about/interfaces)
- [:house: DB Object *:x:*](/en/sfcs/about/dbobj)
- [:curly_loop: DB Object SQL *:x:*](/en/sfcs/about/dbobjsql)
{.links-list}

---

## What's SFCS

- SFCS stands for **S**hop **F**loor **C**ontrol **S**ystem
  \- MES (Manufacturing Execution System)​
  \- CIM (Computer Integrated Manufacturing)​

- Why we need SFCS?
![1569468517395.png](/sfcs/index/1569469669300.png){.align-left}
- Wistron SFCS  in WW ([Wistron Portal](https://portal.wistron.com/weip/web/EIP_F_4001Q.aspx))
![1569468517395.png](/1569468517395.png){.align-left}
## IT System Architecture

- ![1569469996568.png](/sfcs/index/1569469996568.png =90%x)

## SFCS Architecture & Interfaces

- ![1569470041192](/sfcs/index/1569470041192.png =90%x)

## SFCS Basic Terminology

- ![1583398858326](/sfcs/index/1583398858326.png =90%x)

- ![1583398906722](/sfcs/index/1583398906722.png =90%x)

- ![1583398941375](/sfcs/index/1583398941375.png =90%x)

## SFCS Portal

- ![1583397638748](/sfcs/index/1583397638748.png =90%x)

## SFCS Environment

### AP Environment

- ![1583397731286](/sfcs/index/1583397731286.png =90%x)

### DB Environment

#### Schema

1. CIMSFC + Plant Code
2. SFCFA + Plant Code
3. SFCPCB + Plant Code
4. SFCMIFA + Plant Code
5. SFCMIPCB + Plant Code
6. TIBCOEAI + Plant Code

## SFCS Testing Station Integration

- ![1583397768594](/sfcs/index/1583397768594.png =90%x)

## SFCS Modules

1. SM: System Management, base data maintain module
2. MA: Manufacture Application, for production used
3. MI: Manufacture Information, reports
4. PP: PD Performance
5. Kanban: Production Kanban

### SM Module

**1. Application Management**

| Modules                  | Application ID | Description                |
| ------------------------ | -------------- | -------------------------- |
| Application   Management | SMAP001        | User Management            |
| Application   Management | SMAP002        | Group Management           |
| Application Management   | SMAP003        | Application Management     |
| Application Management   | SMAP005        | Application INI Management |
| Application Management   | SMAP006        | Message Management         |
| Application Management   | SMAP007        | Department Management      |

**2. Base Data Management**

| Modules              | Application ID | Description                       |
| -------------------- | -------------- | --------------------------------- |
| Base Data Management | SMBASE001      | Line Management                   |
| Base Data Management | SMBASE002      | Stage Management                  |
| Base Data Management | SMBASE003      | Error code Management             |
| Base Data Management | SMBASE004      | Reason code Management            |
| Base Data Management | SMBASE005      | Model/Model Family Management     |
| Base Data Management | SMBASE006      | Material Category Management      |
| Base Data Management | SMBASE009      | Workstation Management            |
| Base Data Management | SMBASE012      | Hold Management                   |
| Base Data Management | SMBASE017      | Gateway Management                |
| Base Data Management | SMBASE018      | Carry System Management           |
| Base Data Management | SMBASE019      | Serial ID Management              |
| Base Data Management | SMBASE020      | Manufacture Order Type Management |
| Base Data Management | SMBASE021      | Profit Center Management          |

**3. Component Management**

| Modules                | Application ID | Description                      |
| ---------------------- | -------------- | -------------------------------- |
| Component   Management | SMCPN001       | Barcode Status                   |
| Component   Management | SMCPN002       | Non-Standard Barcode Rule        |
| Component Management   | SMCPN003       | Software Rack                    |
| Component Management   | SMCPN004       | Derive Item Management           |
| Component Management   | SMCPN005       | Specify Item                     |
| Component Management   | SMCPN006       | Sequence Control                 |
| Component Management   | SMCPN007       | Alternative Item Management      |
| Component Management   | SMCPN008       | ERP/SFCS CPN Mapping             |
| Component Management   | SMCPN009       | ESOP                             |
| Component Management   | SMCPN010       | RoHS Pair                        |
| Component Management   | SMCPN011       | Check Code                       |
| Component Management   | SMCPN012       | Exclude Item                     |
| Component Management   | SMCPN013       | Component Barcode Rule           |
| Component Management   | SMCPN014       | Component Information Management |
| Component Management   | SMCPN015       | New Item Status                  |
| Component Management   | SMCPN016       | CPN Category for Check available |
| Component Management   | SMCPN017       | CPN Weight                       |
| Component Management   | SMCPN018       | Forbid/Limit Item                |
| Component Management   | SMCPN021       | MO Check Component               |
| Component Management   | SMCPN022       | Component Constraint             |
| Component Management   | SMCPN708       | Compare Setting Management       |

**4. Unit Management**

| Modules           | Application ID | Description                        |
| ----------------- | -------------- | ---------------------------------- |
| Unit   Management | SMUNIT001      | Model Family Configuration         |
| Unit   Management | SMUNIT021      | Model Family Configuration Revise  |
| Unit Management   | SMUNIT002      | Standard Barcode Rule              |
| Unit Management   | SMUNIT003      | S/N Range                          |
| Unit Management   | SMUNIT004      | Unit P/N Configuration             |
| Unit Management   | SMUNIT005      | Unit Routing                       |
| Unit Management   | SMUNIT006      | Unit Package                       |
| Unit Management   | SMUNIT007      | Unit Information                   |
| Unit Management   | SMUNIT008      | Exception Route                    |
| Unit Management   | SMUNIT009      | Sampling                           |
| Unit Management   | SMUNIT010      | Unit Weight                        |
| Unit Management   | SMUNIT011      | Unit Route Change                  |
| Unit Management   | SMUNIT012      | Route Redirect                     |
| Unit Management   | SMUNIT015      | Repair Location Restriction        |
| Unit Management   | SMUNIT016      | Unit P/N Restriction By Line Stage |
| Unit Management   | SMUNIT017      | X-Ray Standard Time                |
| Unit Management   | SMUNIT018      | AOI Side Mapping                   |
| Unit Management   | SMUNIT019      | Sub Unit Weight                    |
| Unit Management   | SMUNIT020      | Unit Information Confirmation      |
| Unit Management   | SMUNIT713      | Assembly Group                     |
| Unit Management   | SMUNIT714      | Assembly Group Revise              |

**5. Manufacture Order Management**

| Modules                        | Application ID | Description              |
| ------------------------------ | -------------- | ------------------------ |
| Manufacture   Order Management | SMMO001        | MO/MO Item               |
| Manufacture   Order Management | SMMO002        | MO Readiness             |
| Manufacture Order Management   | SMMO003        | MO S/N, ID Viewer        |
| Manufacture Order Management   | SMMO004        | Manual S/N Generator     |
| Manufacture Order Management   | SMMO005        | MO Barcode Validation    |
| Manufacture Order Management   | SMMO006        | Sub MO/MO Item           |
| Manufacture Order Management   | SMMO007        | MO ID Readiness          |
| Manufacture Order Management   | SMMO008        | Manual ID Generator      |
| Manufacture Order Management   | SMMO009        | MO Line Restriction      |
| Manufacture Order Management   | SMMO010        | Batch Generate Rework MO |
| Manufacture Order Management   | SMMO012        | MO Picking Filter        |
| Manufacture Order Management   | SMMO013        | MO Picking List          |
| Manufacture Order Management   | SMMO014        | SFCS ERP MO              |
| Manufacture Order Management   | SMMO015        | SFCS ERP SO              |

**6. ID Management**

| Modules         | Application ID | Description               |
| --------------- | -------------- | ------------------------- |
| ID   Management | SMID001        | ID Range Management       |
| ID   Management | SMID002        | ID Specification          |
| ID Management   | SMID003        | ID Reusable               |
| ID Management   | SMID005        | ID Type                   |
| ID Management   | SMID006        | ID Label File Upload      |
| ID Management   | SMID007        | ID Usage Report           |
| ID Management   | SMID008        | ID Range List             |
| ID Management   | SMID009        | Rosa ID Range List Upload |

**7. Basic Info Query**

| Modules            | Application ID | Description                         |
| ------------------ | -------------- | ----------------------------------- |
| Basic Info   Query | SMQUERY001     | MO Download Status                  |
| Basic Info   Query | SMQUERY002     | S/N Generation Status               |
| Basic Info Query   | SMQUERY003     | Unit S/N Information                |
| Basic Info Query   | SMQUERY004     | Lot Information                     |
| Basic Info Query   | SMQUERY005     | Pallet Result Query                 |
| Basic Info Query   | SMQUERY006     | Force Store in Query Report         |
| Basic Info Query   | SMQUERY007     | MO Check Log and Detail Information |
| Basic Info Query   | SMQUERY008     | MO Data Condense Status             |
| Basic Info Query   | SMQUERY009     | Sub USN Query                       |
| Basic Info Query   | SMQUERY101     | USN Data Query                      |
| Basic Info Query   | SMQUERY102     | Pallet Data  Query                  |
| Basic Info Query   | SMQUERY103     | Carton Data Query                   |
**8. CIM Change notice Management**

| Modules                      | Application ID        | Description    |
| ---------------------------- | --------------------- | -------------- |
| CIM Change notice Management | SMCREV001(SMSUPER001) | Code Review    |
| CIM Change notice Management | SMCIMCR001            | Change Notice  |
| CIM Change notice Management | SMCIMCR002            | CR Application |

### MA Module

### On line Applications

| Modules      | Application ID                                               | Description                                                  |
| ------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| P2L          | Console<br>P2L_Console<br>BTO_console<br>CTO_Console<br>P2LService<br>Process_base<br>Process_Kitting0 | - Picking to light off                                       |
| Assembly     | [MASMO001]() <br>[MASMO002]()                                | - Routing control<br>- Serial number collection              |
| ESOP         | MASMO001<br>MASMO002<br>SMCPN009                             | - Show assembly SOP                                          |
| Sampling/OOB | MAOOB001<br>SFCUSN_SAMPLING(Trigger)<br>SMUNIT009            | - Accessory Inspection<br/>- Carton and Unit S/N comparison  |
| Testing      | TesterWS                                                     | \- Flat File / XML / CSV / Dll, etc.<br>\- Web Service / Socket / Restful API, etc. |
| Weight       | MAWGT001<br>MAWGT003<br>MAWGT004<br>MAWGT861<br>MAWGT862     | \- Get weight from weighing machine<br/>- Check weight of Unit/Carton<br>- Routing control |
| Packing      | MAPACK001<br>MAPACK002                                       | - Accessory material scanning<br>- Carton label printing     |
| Store In     | MASTORE001<br/>MASTORE002<br/>MASTORE003<br/>MASTORE004<br/>MASTORE005 | - Grouping by Pallet<br/>- Outbound GR info to ERP           |
| Check In/Out | MACHECK001<br>MACHECK002                                     | - Unit route to FAE check in/out control<br/>- Unit/Repair info reminding |

### Off line Applications

| Modules       | Application ID                                               | Description                                                 |
| ------------- | ------------------------------------------------------------ | ----------------------------------------------------------- |
| MO Download   | [MAMODWN001]()                                               | - Download MO from SAP                                      |
| MO Readiness  | MAMOCHK001                                                   | - Check MO status                                           |
| USN Generator | MASNGEN001                                                   | - Generate USN for production                               |
| Repair        | MARPR001                                                     | - Component replacement<br>- Repair result record           |
| Rework        | MAWORK001/002                                                | - Clear unit assembly info<br>- Re-route to production line |
| Labeling      | MALABEL001<br>MALABEL002<br/>MALABEL003<br/>MALABEL704<br/>MALABEL705 | - Codesoft / Bartender template<br>- Label variable setting |

### MI Module

| Modules                   | Application ID | Description                   |
| ------------------------- | -------------- | ----------------------------- |
| Manufacture   information | MIBASIC001     | Yield Rate                    |
| Manufacture   information | MIBASIC002     | WIP Report                    |
| Manufacture information   | MIBASIC003     | Unit Genealogy                |
| Manufacture information   | MIBASIC004     | Unit S/N  Genealogy (Shipped) |
| Manufacture information   | MIBASIC006     | Function Test Error           |
| Manufacture information   | MIBASIC008     | Product Output                |
| Manufacture information   | MIBASIC009     | Solder Paste Error            |
| Manufacture information   | MIBASIC010     | Force Store in                |
| Manufacture information   | MIBASIC011     | Not Pass WIP                  |
| Manufacture information   | MIBASIC012     | AOI PIcture                   |
| Manufacture information   | MIBASIC013     | MIC Data Query                |
| Manufacture information   | MIBASIC017     | OOB Unit Report               |
| Manufacture information   | MIBASIC018     | MO Weight                     |
| Manufacture information   | MIBASIC020     | WIP Aging summary report      |
| Manufacture information   | MIBASIC021     | WIP Aging Status Kanban       |
| Manufacture information   | MIRPR001       | Repair report                 |
| Manufacture information   | MISPC006       | SPC XBAR-R Control Chart      |
| Manufacture information   | MISPC007       | SPC X-R Chart Jobs            |
| Manufacture information   | MISPC008       | SPC Control Chart             |

## SFCS Manufacture Process

### CTO Process

![1583399357196](/sfcs/index/1583399357196.png =90%x)

[Process Reference (Cindy)](/sfcs/index/cindy_server_routing.xlsx)

### FA Process

![1583480842985](/sfcs/index/1583480842985.png =90%x)

### PCB Process

![1583480899571](/sfcs/index/1583480899571.png =90%x)

## SFCS Major Features

1. **In-House Design**
     *- Various integration mechanism and new IT technology usage*

2. **Web-Based Platform**

3. **MO** **Download & Readiness Check**

4. **System core function is centralized control**

5. **SN Generator**
     *- By setting to generate unit serial number*

6. **Alert Mail**
     *- Quickly build up alert logic & provide Mfg. info/warning*

7. **ESOP**

8. **Label Printing**
     *- Flexible solution to fulfill label spec change*

9. **Various Hold Condition & Sampling Setting**

## Reference:

- [Wistron SFCS Introduction](https://wistron.sharepoint.com/:p:/r/teams/SFCSDevTeam/Shared%20Documents/Training%20Material/Wistron%20SFCS%20Introduction%20V1_%2020190911.pptx?d=w5db6520193414ee387076cdd8603fcac&csf=1&e=lzyWOf )
