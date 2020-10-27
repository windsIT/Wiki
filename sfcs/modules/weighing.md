---
title: Weighing Module
description: Weighing related Manufacture Applications
published: true
date: 2020-10-27T01:29:30.464Z
tags: weighing
editor: markdown
dateCreated: 2020-10-27T00:55:07.802Z
---

# Purpose 
* Purpose: Weigh and check the weight of USN/ Carton/ Pallet. 
* **Related Applications**:
  | APID                                                         | Description              |
  | ------------------------------------------------------------ | ------------------------ |
  | [MAWGT002](/en/sfcs/modules/weighing/mawgt002) | LCD Accessory Weight     |
  | [MAWGT003](/en/sfcs/modules/weighing/mawgt003) | Weighting                |
  | [MAWGT004](./weighing/mawgt004) | Unit Weight For WMS Ship |
  | [MAWGT861](./weighing/mawgt861) | UPN Weight               |
  | [MAWGT862](./weighing/mawgt862) | Auto Weight              |


# Process flow  

- [**Main Process Flow**](/sfcs/modules/weighing/weightingmodule-mainprocessflow.drawio)
![weightingmodule-mainprocessflow.png](/sfcs/modules/weighing/weightingmodule-mainprocessflow.png)

- [**Weight Process Flow**](/sfcs/modules/weighing/weightingmodule-weightprocessflow.drawio)
![Weighting Module Weight Process Flow](/sfcs/modules/weighing/weightingmodule-weightprocessflow.png)

 * **Main Process**

| **Main Process** | **Description**                                              |
| ---------------- | ------------------------------------------------------------ |
| Check Process    | Get and Check the Basic Data.                                |
| Weight Process   | Get/Calculate Total Weight and Standard Weight, then check  them. |
| SaveDataProcess  | Save Weight Information; Complete Process; [Throw Label Job;]  [Check Sampling;] Show Message. |

# Weight Machine

- 地磅，Ex: MAWGT861程式使用的 [天合牌TDI-300D3称重控制仪表(上海天合电子有限公司)]
 ![weight_machine-tdi-300d3.png](/sfcs/modules/weighing/weight_machine-tdi-300d3.png)
- 台湾电子秤称, Ex: Kingship GRW-15.
 ![台湾称-kingship-grw-15.png](/sfcs/modules/weighing/台湾称-kingship-grw-15.png)
- 上海电子秤称, Ex: 英展  AWH-15-SA.
 ![上海称-英展AWH-15-SA](/sfcs/modules/weighing/上海称-英展awh-15-sa.png)			


# Reference / Remark
- N/A 