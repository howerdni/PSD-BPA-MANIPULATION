# PSD-BPA-MANIPULATION
- 为bpa使用者提供基于Python的自动化操作
- 作者：倪程捷
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
 - 注意：其中有发电能力的B卡被放在了```Obj_BQcards```变量中，`Obj_Bcards`只包含无发电能力的B卡
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
 - Power_Flow_SUM_GT500()函数的示例（此版本使用python3.11版本，其他版本可能失效）
 - 如果版本不一致，请建立虚拟环境，在cmd中输入：
 - ```
   conda create --name env311 python=3.11
   conda install ipykernel
   python -m ipykernel install --user --name env311 --display-name "env311"
   cd ....
   activate env311
   ```
 ```
In: import BPA_data_manipulation as Bdm
In: Bdm.Power_Flow_SUM_GT500()
Out:
     	Bus1	Voltage1	Bus2 Voltage2 Parallel	Dist1	Dist2	Power_flow	Ploss	Voltage_r
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
- Power_Flow_SUM_220()函数的示例
```
In: Bdm.Power_Flow_SUM_220()
Out:
    	Bus1	Voltage1	Bus2	Voltage2	Parallel	Dist1	Dist2	Power_flow	Ploss	Voltage_r
    81	苏茶庵21	230.0	苏茶光2P	230.0		11	GH	0.0	0.001	219.70
    82	苏茶庵21	230.0	苏茶庵B1	1.0		11	11	0.0	0.000	219.70
    83	苏茶庵21	230.0	苏贺村21	230.0	1	11	11	95.2	0.151	219.70
    84	苏茶庵21	230.0	苏三堡21	230.0	1	11	11	-138.9	0.137	219.70
    89	苏常店21	230.0	苏常店1P	230.0		11	GH	0.0	0.000	216.75
    ...	...	...	...	...	...	...	...	...	...	...
    32217	浙岑山ZD	230.0	浙岑山Z_	230.0		ZS	ZS	11.7	0.000	227.09
    32218	浙岑山Z_	230.0	浙六横__	230.0	1	ZS	ZS	-64.1	0.021	227.09
    32219	浙岑山Z_	230.0	浙六横__	230.0	2	ZS	ZS	-65.6	0.022	227.09
    32220	浙岑山Z_	230.0	浙普计Z_	230.0	1	ZS	C6	0.0	0.008	227.09
    32221	浙岑山Z_	230.0	浙岑山ZD	230.0		ZS	ZS	-11.7	0.000	227.09
```
- 列出浙江所有对外联络线的潮流
```
In: rows=[]
    bus1=['国芜湖','国练塘','沪林海','国榕城','闽宁德','皖广德','皖河沥']
    bus2=['国安吉','国吴江','浙汾湖','浙丽西','国莲都','浙瓶窑','浙富阳']
    x=Bdm.Power_Flow_SUM_GT500()
    for i in x.index:
        if ((x.loc[i,'Bus2'][0:3] in bus1 ) &(x.loc[i,'Bus1'][0:3] in bus2)) or ((x.loc[i,'Bus2'] in ['国吴江51','国吴江52']) & (x.loc[i,'Bus1'] in ['国吴江B1','国吴江B3'])) :
            rows.append(i)
    WS=x.loc[rows,:]
    WS
Out: 
    	Bus1	Voltage1	Bus2	Voltage2	Parallel	Dist1	Dist2	Power_flow	Ploss	Voltage_r
    13697	国安吉__	1050.0	国芜湖__	1050.0	1	GD	GD	-3889.0	15.662	36.02
    13699	国安吉__	1050.0	国芜湖__	1050.0	2	GD	GD	-3889.0	15.662	36.02
    13884	国莲都__	1050.0	国榕城__	1050.0	1	GD	M1	374.8	0.290	49.10
    13886	国莲都__	1050.0	国榕城__	1050.0	2	GD	M1	374.8	0.290	49.10
    14027	国吴江B1	525.0	国吴江51	525.0	1	GD	GD	302.4	0.092	521.85
    14033	国吴江B3	525.0	国吴江52	525.0	1	GD	GD	297.4	0.091	522.21
    14040	国吴江T1	1050.0	国练塘__	1050.0	1	GD	JG	1159.5	1.321	41.11
    14042	国吴江T1	1050.0	国练塘__	1050.0	2	GD	JG	1159.5	1.321	41.11
    14986	浙富阳__	525.0	皖河沥__	525.0	1	H	WE	-1138.9	7.819	501.72
    14987	浙富阳__	525.0	皖河沥__	525.0	2	H	WE	-1140.9	7.848	501.72
    15339	浙瓶窑__	525.0	皖广德__	525.0	1	H	WE	-942.7	7.152	500.50
    17121	浙汾湖__	525.0	沪林海__	525.0	1	JX	SK	549.7	1.431	508.57
    17122	浙汾湖__	525.0	沪林海__	525.0	2	JX	SK	549.7	1.431	508.57
    17685	浙丽西__	525.0	闽宁德51	525.0	1	L	M9	-393.0	3.080	511.65
    17687	浙丽西__	525.0	闽宁德51	525.0	2	L	M9	-389.1	4.067	511.65
```
- 以下例子为统计浙江省电力受入总量
``` 
In:
    #统计出力
    filedata,B,BQ,BE,T,L,PZ=Bdm.create_Card_Obj()
    GEN=0
    GEN1=0
    for i in BQ:
        for j in PZ:
            if (i.CardType=='BQ') & ((i.Dist.strip() in ["ct","Ct","cc","cr","c1","c2","c3","C","C5","C6","C7","H","JX","HZ","N","S","J","Q","L","T","W","ZS"])) & (j.Dist.strip() ==  i.Dist.strip()):
                n=float(i.Pout)*float(j.FPgen)
                GEN=GEN+n
    
    for i in BQ:
        for j in PZ:
            if (i.CardType=='BQ') & ((i.Dist.strip() in ["HD"])) & (j.Dist.strip() ==  i.Dist.strip()) & (j.FOwner.strip() ==  i.Owner.strip()) & (i.Owner.strip() in ["H1","H2","H7"]):
                n=float(i.Pout)*float(j.FPgen)
                GEN1=GEN1+n
    #全浙江网络送出潮流（本地机组+华东机组-负荷-网损+直流）
    GEN+GEN1-(load_BQ+load_B+load_BQHD)*1.008+7660*2+7660*2*1/3
Out:
    -6159.581141778069
```
 

