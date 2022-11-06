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
 选择一个dat文件：
 返回值如下：
 ```return fdat_data,Obj_Bcards,Obj_BQcards,Obj_BEcards,Obj_Tcards,Obj_Lcards,Obj_PZcards```
 





















   - 








  
