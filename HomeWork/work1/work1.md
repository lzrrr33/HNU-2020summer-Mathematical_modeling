### 第一次：
附件1：区域高程数据.xlsx给出了某区域 （km）的高程数据，画出该区域的三维网格图和等高线图，在A（30，0）和B（43，30）（单位：km）点处建立了两个基地，在等高线图上标注出这两个点。并求该区域地表面积的近似值。  

----
**写完作业后，上传代码至work1文件夹 并且在work1.md文件中简要说明如何搞定的，以及一些参考资料的链接或者上传文档。**  

----
##### 数据读取
采用**pandas**读取Excel数据，并将数据保存为numpy数组data
##### 3D网格图
使用**matplotlib**中的**mpl_toolkits.mplot3d**工具包绘制3维图形。
```
ax3d.plot_surface(x, y, z, rstride=1, cstride=1, cmap=plt.cm.spring)  # 3D网格图绘制
```
##### 等高线图
用**plt.contourf**绘制等高线图
```
cset = plt.contourf(x,y,data.transpose([1,0])) # 等高线绘画
plt.colorbar(cset) # 设置颜色条
plt.plot(x1, y1, 'om') # A点标注
plt.plot(x2, y2, 'om') # B点标注
```
##### 求区域地表面积近似值

将每一个网格的地表面积近似为四个海拔点构成的四边形面积
四边形面积求解：
先求得四条边长度 `l1,l2,l3,l4` 和对角线长度`l5`
将四边形分为两个三角形，然后通过海伦公式求解。
```
tri_area1 = (p1*(p1-l1)*(p1-l3)*(p1-l5))**0.5
tri_area2 = (p2*(p2-l2)*(p2-l4)*(p2-l5))**0.5
```
其中`p1,p2`分别为三角形周长的一半
