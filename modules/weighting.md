---
title: Weighting Module 
description: Weighting Module Introduction
published: true
date: 2020-09-02T06:30:53.057Z
tags: 
editor: undefined
---

## Scope and Purpose 
* Scope: SFCS.
* Purpose: Weigh and check the weight of USN/ Carton/ Pallet. 
* **Related Applications**:
  | APID                                                         | Description              |
  | ------------------------------------------------------------ | ------------------------ |
  | [MAWGT002](/en/applications/ma/weighting/mawgt002) | LCD Accessory Weight     |
  | [MAWGT003](/en/applications/ma/weighting/mawgt003) | Weighting                |
  | [MAWGT004](/en/applications/ma/weighting/mawgt004) | Unit Weight For WMS Ship |
  | [MAWGT861](/en/applications/ma/weighting/mawgt861) | UPN Weight               |
  | [MAWGT862](/en/applications/ma/weighting/mawgt862) | Auto Weight              |


## Process flow  

- [**Main Process Flow**](/modules/weighting/weightingmodule-mainprocessflow.drawio)
![weightingmodule-mainprocessflow.png](/modules/weighting/weightingmodule-mainprocessflow.png)

- [**Weight Process Flow**](/modules/weighting/weightingmodule-weightprocessflow.drawio)
![Weighting Module Weight Process Flow](/modules/weighting/weightingmodule-weightprocessflow.png)

 * **Main Process**

| **Main Process** | **Description**                                              |
| ---------------- | ------------------------------------------------------------ |
| Check Process    | Get and Check the Basic Data.                                |
| Weight Process   | Get/Calculate Total Weight and Standard Weight, then check  them. |
| SaveDataProcess  | Save Weight Information; Complete Process; [Throw Label Job;]  [Check Sampling;] Show Message. |

## Weight Machine

- 地磅，Ex: MAWGT861程式使用的 [天合牌TDI-300D3称重控制仪表(上海天合电子有限公司)]
   ![weight_machine-tdi-300d3.png](/modules/weighting/weight_machine-tdi-300d3.png)
- 台湾电子秤称, Ex: Kingship GRW-15.
​					![台湾称-Kingship-GRW-15](/modules/weighting/台湾称-kingship-grw-15.png)
- 上海电子秤称, Ex: 英展  AWH-15-SA.
   ![上海称-英展AWH-15-SA](/modules/weighting/上海称-英展awh-15-sa.png)			


## Reference / Remark
- N/A 