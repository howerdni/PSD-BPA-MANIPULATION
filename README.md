# PSD-BPA-MANIPULATION
为bpa使用者提供基于Python的自动化操作

## BPA卡片的类名称和类成员变量，成员函数：
### PZ卡：  
- name:PZCard   
- attributes:   
  - CardType:str
  - Dist:str
  - FPload:str
  - FQload:str
  - FPgen:str
  - FQgen:str
  - FOwner:str(如果不填所有者，所有者是三个空字符)
  - gen():str(返回该卡片的字符串，可以直接复制到bap软件中使用)
### B0卡：
- name:B0(该卡为B类卡片的父类)
- attributes:
  - Owner:str
  - Bus_name:str
  - Vol_Rank:str
  - Dist:str
  - Mw_load:str
  - Mvar_load:str
  - Shunt_Mw:str
  - Shunt_var:str
  - Capacity:str
  - Pout:str
  - Qout:str
  - Qout_min:str
  - Vmax_pu:str
  - Vmin_pu:str
  - gen():str(返回该卡片的字符串，可以直接复制到bap软件中使用)
  - Mw_load,Mvar_load,Shunt_Mw,Shunt_var,Capacity,Pout,Qout,Qout_min,Vmax_pu,Vmin_pu其中任何一个填的不是数字的话，会被认为填写有误
 ### B卡： 
 - name:BCard
 - attributes:
   - CardType：str
   - 其余与B0卡相同
 ### BQ卡： 
 - name:BQCard
 - attributes:
   - CardType：str
   - 其余与B0卡相同
 ### BE卡： 
 - name:BECard
 - attributes:
   - CardType：str
   - 其余与B0卡相同
 ### T卡：
 - name:TCard
 - attributes：
   - strTCard:str
   - CardType:str
   - Owner:str
   - Bus_name1:str
   - Vol_Rank1:str
   - test_point:str
   - Bus_name2:str
   - Vol_Rank2:str
   - parallel:str
   - series:str
   - Capacity:str
   - p_num:str
   - r_pu:str
   - x_pu:str
   - iron_pu:str
   - jb_pu:str
   - tap_vol1:str
   - tap_vol2:str
   - beg_op_m:str
   - beg_op_y:str
   - stp_op_m:str
   - stp_op_y:str
   - gen():str(返回该卡片的字符串，可以直接复制到bap软件中使用)
   - Vol_Rank1,Vol_Rank2,Capacity,p_num,r_pu,x_pu,iron_pu,jb_pu,tap_vol1,tap_vol2其中任何一个填的不是数字的话，会被认为填写有误
 ### L卡：
 - name:LCard
 - attributes：
   - strLCard:str
   - CardType:str
   - Owner:str
   - Bus_name1:str
   - Vol_Rank1:str
   - test_point:str
   - Bus_name2:str
   - Vol_Rank2:str
   - parallel:str
   - series:str
   - Irate:str
   - p_num:str
   - r_pu:str
   - x_pu:str
   - g2_pu:str
   - b2_pu:str
   - length:str
   - notes:str
   - beg_op_m:str
   - beg_op_y:str
   - stp_op_m:str
   - stp_op_y:str
   - gen():str(返回该卡片的字符串，可以直接复制到bap软件中使用)
   - Vol_Rank1,Vol_Rank2,Irate,r_pu,x_pu,g2_pu,b2_pu其中任何一个填的不是数字的话，会被认为填写有误
 ### X0卡：
 - name:X0Card
 - attributes：
 - CardType:str
 - Bus_name1:str
 - Vol_Rank1:str
 - Bus_name2:str
 - Vol_Rank2:str
 - Connect_type:str
 - parallel:str
 - X0:str
 - R0:str
 - gen():str(返回该卡片的字符串，可以直接复制到bap软件中使用)
 ### XR卡：
 - name:XRCard
 - attributes：
 - CardType:str
 - Bus_name1:str
 - Vol_Rank1:str
 - R0:str
 - X0:str
 - gen():str(返回该卡片的字符串，可以直接复制到bap软件中使用)
 ### create_Card_Obj()
 - 选择一个dat文件，返回值如下：
 ```return fdat_data,Obj_Bcards,Obj_BQcards,Obj_BEcards,Obj_Tcards,Obj_Lcards,Obj_PZcards```
 - 注意：其中有发电能力的B卡被放在了```Obj_BQcards```变量中，B卡只包含无发电能力的B卡
 ### create_swiCard_Obj()
 - 选择一个swi文件，返回值如下：
 - ```return Obj_X0cards,Obj_XRcards```
 ### Power_Flow_SUM_GT500()
 - 选择pfo文件，输出一个pandas.DataFrame类型的表格，包含线路节点名字，线路电压等级，分区，潮流，网损，电压等信息
 - 输出范围为500kV和1000kV电压等级的线路
 ### Power_Flow_SUM_220()
 - 选择pfo文件，输出一个pandas.DataFrame类型的表格，包含线路节点名字，线路电压等级，分区，潮流，网损，电压等信息
 - 输出范围为220kV电压等级的线路
 ## 使用实例
 ```
 import BPA_data_manipulation as Bdm
 Bdm.Power_Flow_SUM_GT500()
 	Bus1	Voltage1	Bus2	Voltage2	Parallel	Dist1	Dist2	Power_flow	Ploss	Voltage_r
0	国芜湖B1	525.0	国芜湖1_	525.0	1		GD	473.6	0.046	522.25
1	国芜湖B1	525.0	国芜湖_1	115.0	1		GD	0.0	0.000	522.25
2	国芜湖B1	525.0	国芜湖__	1050.0	1		GD	-473.6	0.682	522.25
3	国芜湖B2	525.0	国芜湖2_	525.0	1		GD	475.1	0.049	522.15
4	国芜湖B2	525.0	国芜湖_2	115.0	1		GD	0.0	0.000	522.15
...	...	...	...	...	...	...	...	...	...	...
32204	浙舟燃__	525.0	浙舟山__	525.0	1	ZS	N	936.5	1.838	526.33
32205	浙舟三__	525.0	浙舟三_1	20.0		ZS	C	-502.4	0.496	524.44
32206	浙舟三__	525.0	浙舟三_2	20.0		ZS	C	-502.4	0.495	524.44
32207	浙舟三__	525.0	浙舟山__	525.0	1	ZS	N	502.4	0.180	524.44
32208	浙舟三__	525.0	浙舟山__	525.0	2	ZS	N	502.4	0.180	524.44
```
 
 filedata,B,BQ,BE,T,L,PZ=Bdm.create_Card_Obj()





















   - 








  
