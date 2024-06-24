# PSD-BPA-MANIPULATION
- 为bpa使用者提供基于Python的自动化操作
- 作者：倪程捷
- 2024年6月23日更新版本：3.0
- 文件：BPA_data_manipulation_3.pyd
- 新增功能：增加了直流卡：LD卡，DC卡；增加了PSD软件的稳定性文件(后缀为swi)的专门卡：M卡，MF卡。
- 关于M系列卡片的含义和填写要求：
  - MF卡是发电机模型基本参数数据卡，其中需要填写大部分发电机的相关变量，如动能、直轴和交轴的电抗和暂态电抗、时间常数、饱和等，当采用双轴模型时，都应该填写MF卡。
  - M卡主要用来填写发电机次暂态参数，对于一台发电机，如果考虑次暂态参数，应该填写M卡，M卡必须和MF卡或MG卡联合使用，即填写M卡必须同时填写MF卡或MG卡。
  - 如果发电机模型采用无穷大母线模型，则应该填写MC卡，同时在动能位置填写999999；如果采用Eq'恒定的模型，应该令Tdo'＝999。
- 上个版本包含的X0，XR卡主要用于检查文件是否缺失零序参数
- 本次新增的M卡，MF卡主要用于检查文件模型是否缺失用于计算短路电流的参数以及该参数是否准确。
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
 ```return fdat_data,Obj_Bcards,Obj_BQcards,Obj_BEcards,Obj_Tcards,Obj_Lcards,Obj_PZcards,Obj_LDcards,Obj_DCcards```
 - 注意：其中有发电能力的B卡被放在了```Obj_BQcards```变量中，`Obj_Bcards`只包含无发电能力的B卡
 ### create_swiCard_Obj()
 - 选择一个swi文件，返回值如下：
 - ```return Obj_X0cards,Obj_XRcards,Obj_MCard,Obj_MFCard```
 ### Power_Flow_SUM_GT500()
 - 选择pfo文件，输出一个pandas.DataFrame类型的表格，包含线路节点名字，线路电压等级，分区，潮流，网损，电压等信息
 - 输出范围为500kV和1000kV电压等级的线路
 ### Power_Flow_SUM_220()
 - 选择pfo文件，输出一个pandas.DataFrame类型的表格，包含线路节点名字，线路电压等级，分区，潮流，网损，电压等信息
 - 输出范围为220kV电压等级的线路
 ## 使用实例
 - 此版本使用python3.11版本，其他版本可能失效
 - 如果版本不一致，请建立虚拟环境，在cmd中输入：
 - ```
   conda create --name env311 python=3.11
   conda install ipykernel
   python -m ipykernel install --user --name env311 --display-name "env311"
   cd ....
   activate env311
   ```
- LD卡、DC卡的使用示例：
- 使用前，先将BPA_data_manipulation_3.pyd文件放置于juptyer-notebook文件同一路径下
```
In: import BPA_data_manipulation_3 as bd
In: filedata,B,BQ,BE,T,L,PZ,LD,DC =bd.create_Card_Obj()
In: X0,XR,M,MF =bd.create_swiCard_Obj
In: for i in (LD+DC):
    print(i.gen())
Out: LD    鄂团林P1210. 沪枫泾P2199.  3000 10.21901.760     R495.  500. 15. 17.     
     LD    鄂团林N1210. 沪枫泾N2199.  3000 10.21901.760     R495.  500. 15. 17.     
     LD    鄂宋家P1209. SNQ220P2198.  1200 25.87  917.0     R198.  500. 17. 17.     
     LD    鄂宋家N1209. SNQ220N2198.  1200 25.87  917.0     R198.  500. 17. 17.     
     LD    川复龙P1170. 沪奉贤P2158.  4000  12.6 1590.0     R1056. 800. 15. 17.     
     LD    川复龙N1170. 沪奉贤N2158.  4000  12.6 1590.0     R1056. 800. 15. 17.     
     LD    鄂宜都P1210. 沪华新P2201.  3000    8.  799.0     R495.  500. 15. 17.     
     LD    鄂宜都N1210. 沪华新N2201.  3000    8.  799.0     R495.  500. 15. 17.     
     LD    川锦屏P1171. 苏同里P2161.  450011.134 1405.0     I3315. 800. 15. 17.     
     LD    川锦屏N1171. 苏同里N2161.  450011.134 1405.0     I3315. 800. 15. 17.
     ......
In: for i in (LD):
    print(i.Bus_name1+" "+i.Bus_name2+' '+i.POWERset)
Out: 鄂团林P1 沪枫泾P2 495. 
     鄂团林N1 沪枫泾N2 495. 
     鄂宋家P1 SNQ220P2 198. 
     鄂宋家N1 SNQ220N2 198. 
     川复龙P1 沪奉贤P2 1056.
     川复龙N1 沪奉贤N2 1056.
     鄂宜都P1 沪华新P2 495. 
     鄂宜都N1 沪华新N2 495. 
     川锦屏P1 苏同里P2 3315.
     川锦屏N1 苏同里N2 3315.
     ......
In: for i in (DC):
    print(i.Rec_H_Name+" "+i.Inv_H_Name+i.Vol_RankIH+' '+i.Inv_L_Name+i.Vol_RankIL+' '+i.Inv_POWERset)
Out: 蒙锡换5N 国泰换5N525. 国泰换5F1050 4892. 
     蒙锡换5P 国泰换5P525. 国泰换5Z1050 4892. 
     新吉换7N 国皖换5N525. 国皖换5F1050  6000.
     新吉换7P 国皖换5P525. 国皖换5Z1050  6000.
     国布换DN 浙北换N 525. 浙北换NF525. 1333  
     国布换DP 浙北换P 525. 浙北换ZF525. 1333  
```
- Power_Flow_SUM_GT500()函数的示例
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
 

