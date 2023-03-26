# GAMES101 note

* 计算机视觉与计算机图形学的区别与联系：

![image-20230104160948534](./images/image-20230104160948534.png)

## Linear Algebra

### Vectors

* Direction and length

* Unit vector

  * <img src="./images/image-20230104162157023.png" alt="image-20230104162157023" style="zoom:50%;" />

  #### Dot product **(give a number)**

  * basic 
    * <img src="./images/image-20230104162511564.png" alt="image-20230104162511564" style="zoom:33%;" />
  * Properties
    * <img src="./images/image-20230104162642312.png" alt="image-20230104162642312" style="zoom:33%;" />
    * <img src="./images/image-20230104162726286.png" alt="image-20230104162726286" style="zoom:33%;" />
    * for projection(投影)
      * <img src="./images/image-20230104162840604.png" alt="image-20230104162840604" style="zoom: 50%;" />
    * application
      * <img src="./images/image-20230104163206488.png" alt="image-20230104163206488" style="zoom:50%;" />

  #### Cross Product **(give a vector)**

  * basic
    * <img src="./images/image-20230104163417250.png" alt="image-20230104163417250" style="zoom: 50%;" />
  * Properties
    * <img src="./images/image-20230104163513227.png" alt="image-20230104163513227" style="zoom:33%;" />
    * in Linear Algebra
      * <img src="./images/image-20230104163617224.png" alt="image-20230104163617224" style="zoom:33%;" />
    * application
      * determine left or right for the vector 
      * **可以判断一个点在不在一个三角形内**（在做光栅化时要判断一个三角形覆盖了那些像素，这时候需要用到这个基本的算法）

### Matrices 

* Multiplication
  * <img src="./images/image-20230104165111197.png" alt="image-20230104165111197" style="zoom:33%;" />
* 对向量做变换操作（向量乘以一个变换矩阵）
* Properties
  * <img src="./images/image-20230104165513170.png" alt="image-20230104165513170" style="zoom:33%;" />
  * 单位矩阵 （定义矩阵的逆矩阵）
    * <img src="./images/image-20230104165548412.png" alt="image-20230104165548412" style="zoom: 33%;" />
  * 向量的点乘和叉乘都可以转换为矩阵的乘法
    * <img src="./images/image-20230104165701793.png" alt="image-20230104165701793" style="zoom:33%;" />

### Transform

（根据坐标点的变化写出变换矩阵）（这里列出二维的变换，三维的变换矩阵可以进行类比）

#### 2D 线性变换：<img src="./images/image-20230104171401727.png" alt="image-20230104171401727" style="zoom:33%;" />

* 缩放变换
  * <img src="./images/image-20230104170543340.png" alt="image-20230104170543340" style="zoom:33%;" />
* 镜像变换
  * <img src="./images/image-20230104170635991.png" alt="image-20230104170635991" style="zoom:33%;" />
* 切边
  * <img src="./images/image-20230104170830882.png" alt="image-20230104170830882" style="zoom:33%;" />
* 旋转变换
  * <img src="./images/image-20230104171159509.png" alt="image-20230104171159509" style="zoom:33%;" />
  * <img src="./images/image-20230104171225033.png" alt="image-20230104171225033" style="zoom:33%;" />
* 平移变换
  * **需要强调的是，平移变换不是线性变换，但是我们希望利用一个矩阵形式就包含掉所有的变换，而不让平移变换成为特例，所以之后人们引入的齐次坐标来进行统一**![image-20230104171724145](./images/image-20230104171724145.png)

* **引入齐次坐标 来统一所有变换的矩阵乘法变换** （先进行线性变换再平移）
  * <img src="./images/image-20230104171952458.png" alt="image-20230104171952458" style="zoom:50%;" />
  * 引入一个新的维度的意义：
    * <img src="./images/image-20230104172154424.png" alt="image-20230104172154424" style="zoom:50%;" />
    * 使用齐次坐标，二维情况下的变换矩阵
      * <img src="./images/image-20230104172407767.png" alt="image-20230104172407767" style="zoom:50%;" />

#### 3D Transform

三维空间中利用齐次坐标写出的变换矩阵

* <img src="./images/image-20230105160944121.png" alt="image-20230105160944121" style="zoom:50%;" />
* 旋转<img src="./images/image-20230105161215586.png" alt="image-20230105161215586" style="zoom:50%;" />
  * （罗德里格斯旋转公式）任意旋转的变换矩阵<img src="./images/image-20230105161613361.png" alt="image-20230105161613361" style="zoom:50%;" />
  * 四元数的引入：因为旋转矩阵不太好做差值（比如，一个旋转15°的旋转矩阵与一个旋转25°的旋转矩阵做平均，得不到我们想要的旋转20°的旋转矩阵），所以引入四元数

**MVP：（Model，View，Projection）**

![image-20230106161014841](./images/image-20230106161014841.png)

##### 视图变换（View）

* 规定相机在一个标准位置上（以相机为中心，不管最开始相机于模型的位置怎么摆，先把相机通过变换移动到规定的位置（position在原点，朝向-Z轴看，向上的位置为Y轴），模型随之变换）<img src="./images/image-20230105163103934.png" alt="image-20230105163103934" style="zoom:50%;" />
* **正交矩阵的逆矩阵与他的转置矩阵相同**，在解一个旋转矩阵遇到困难时，可以考虑他的逆矩阵，先写出逆矩阵，在求这个旋转矩阵

##### 投影变换（Projection）

* 正交投影（没有近大远小的视觉效果）
  * <img src="./images/image-20230105164350925.png" alt="image-20230105164350925" style="zoom:50%;" />
  * <img src="./images/image-20230105164717675.png" alt="image-20230105164717675" style="zoom:50%;" />
    * **对应的变换矩阵：**<img src="./images/image-20230105164835174.png" alt="image-20230105164835174" style="zoom:50%;" />
* 透视投影（有近大远小的效果）
  * <img src="./images/image-20230105164334499.png" alt="image-20230105164334499" style="zoom:50%;" />
  * 如何做透视投影：分两步
    * <img src="./images/image-20230105165452539.png" alt="image-20230105165452539" style="zoom:50%;" />
    * “挤压变换矩阵”：<img src="./images/image-20230105170628515.png" alt="image-20230105170628515" style="zoom:50%;" />

## Rasterization(光栅化)

### 定义：

​	**将三维空间的几何形体显示在二维的屏幕上**

​	在计算机图形学中：

​	**屏幕**：一个二维的数组（一个元素为一个像素）

​	**屏幕空间**：建立一个XY坐标系，以像素的左下角坐标描述像素的位置，但	需要注意的是，像素的中心点不是整数

​	**视口变换**：

<img src="./images/image-20230106161722841.png" alt="image-20230106161722841" style="zoom:50%;" />

<img src="./images/image-20230106162124672.png" alt="image-20230106162124672" style="zoom:50%;" />

​	**光栅化过程**：把之前经过MVP过程的一个立方体再经过视口变换得到多变形的输入，之后再将其把“画”到屏幕上（用像素来呈现）

<img src="./images/image-20230106163726399.png" alt="image-20230106163726399" style="zoom:50%;" />

### 将多边形画到屏幕上的方法：

#### 1.采样

​	**采样是在重复原始信号的频谱**（以此来解释走样）

​	检测**每个可能的像素**（利用像素中心来代表一个像素的位置来进行判断短）（Bounding Box 限制范围）**是不是在三角形内**（利用像素的中心点与三角形的各个顶点构成的向量做叉积来判断），如果在，那就给像素画上颜色

​	**走样：**信号变化太快，采样速度跟不上信号变化的速度导致走样；另外一种说法即，我们用同一种采样方式采样多个函数，但是他们采样的结果是一样的，我们无法区分（如下图所示，用相同的采样方法去采样两个函数，得到的结果是一样的，无法区分）；从可以从频谱角度说明

<img src="./images/image-20230109151917550.png" alt="image-20230109151917550" style="zoom:50%;" />

<img src="./images/image-20230109152031200.png" alt="image-20230109152031200" style="zoom:50%;" />

<img src="./images/image-20230109141800085.png" alt="image-20230109141800085" style="zoom:50%;" />

​	<img src="./images/image-20230109141601422.png" alt="image-20230109141601422" style="zoom:50%;" />

​	**傅里叶变换：**

<img src="./images/image-20230109141417993.png" alt="image-20230109141417993" style="zoom:50%;" />

​	**卷积**：在空间域上做卷积，相当于将空间域转换到频域后相乘

<img src="./images/image-20230109151136325.png" alt="image-20230109151136325" style="zoom:50%;" />

#### 2.反走样

* 先对信号做滤波（去掉一些特定的频率，如模糊，高通滤波（只剩下高频信息）），再进行采样来达到反走样（抗锯齿）的效果
* <img src="./images/image-20230109152229659.png" alt="image-20230109152229659" style="zoom:50%;" />
* MSAA method
  * 增加采样点得到近似的三角形覆盖率，从而更好地上色来减少锯齿
  * 代价是增加了采样点，而导致计算开销变大
  * 还有另外的方法，如 FX（Fast Approximate）AA, T（Temporal）AA
* 超分辨率方法
  * 把小图拉大，但不损失分辨率（DLSS：Deep Learning Super Sampling）

#### 3.三角形的遮挡和可见性处理（Z-buffering）

* 1.画家算法
  * 从远到近，一层一层覆盖，得到最后正确的结果
  * 计算开销较大
  * 不是普适适用的
    * <img src="./images/image-20230110145610458.png" alt="image-20230110145610458" style="zoom:50%;" />
* Z-buffer（深度缓存）算法
  * 对**每个像素**（或对每个采样点）来排深度信息
  * <img src="./images/image-20230110145751482.png" alt="image-20230110145751482" style="zoom:50%;" />
  * 算法（与画的顺序没有关系，复杂度为O（n））：
    * <img src="./images/image-20230110150230914.png" alt="image-20230110150230914" style="zoom:50%;" />
    * 一个例子：
      * <img src="./images/image-20230110150539121.png" alt="image-20230110150539121" style="zoom:50%;" />
  * 处理不了透明物体

## Shading（着色）

 #### 1.Blinn-Phong 着色模型（光线与材质作用）

**一共有三个不同的效果项构成了完整的视觉效果：漫反射、高光、间接光**

<img src="./images/image-20230112140055340.png" alt="image-20230112140055340" style="zoom:50%;" />

* **漫反射项**

  * <img src="./images/image-20230110153656977.png" alt="image-20230110153656977" style="zoom:50%;" />
  * <img src="./images/image-20230110152805181.png" alt="image-20230110152805181" style="zoom:50%;" />

  <img src="./images/image-20230110152850558.png" alt="image-20230110152850558" style="zoom:50%;" />

  <img src="./images/image-20230110153500187.png" alt="image-20230110153500187" style="zoom:50%;" />

  <img src="./images/image-20230110152723467.png" alt="image-20230110152723467" style="zoom:50%;" />

* **高光项**

  * 观察方向与镜面反射方向接近时会看到高光
  * <img src="./images/image-20230112135432165.png" alt="image-20230112135432165" style="zoom:50%;" />
  * 指数P的作用：减少“容忍度”，只有**在小夹角才能看到高光**
    * <img src="./images/image-20230112135825266.png" alt="image-20230112135825266" style="zoom:50%;" />

* **环境光项（间接光照）**

  * 环境光比较复杂，需要做一些近似假设
    * <img src="./images/image-20230112140000638.png" alt="image-20230112140000638" style="zoom:50%;" />

#### 2.着色频率（shading frequencies）

**有三种着色的方式：逐三角形、逐顶点（vertex）、逐像素（Phong shading）**

**这三种着色方式在不同情况下（模型的面数多少），各有优劣（画面质量与计算开销的考量）：**

<img src="./images/image-20230112141216357.png" alt="image-20230112141216357" style="zoom:50%;" />

* **逐三角形着色**：
* **逐顶点着色**：着色时先对三角形的三个顶点做着色，而**三角形内部的点根据顶点的着色值来做平滑差值**
  * 定义**顶点的法线方向**：<img src="./images/image-20230112141517926.png" alt="image-20230112141517926" style="zoom:50%;" />
  * **如何在三角形内部进行平滑差值（基于重心坐标）**：
    * **重心坐标：(利用三角形的三个顶点去描述三角形内部的一个顶点的方式)**
      * <img src="./images/image-20230113211351659.png" alt="image-20230113211351659" style="zoom:50%;" />
    * 求三角形内任何一个点重心坐标的方法：
      * 三角形本身的重心坐标很特殊，它的重心坐标就是（⅓，⅓，⅓）
      * <img src="./images/image-20230113211743732.png" alt="image-20230113211743732" style="zoom:50%;" />
      * 另一种计算方式：<img src="./images/image-20230113215333683.png" alt="image-20230113215333683" style="zoom:50%;" />
      * **三角形内部某一点差值的属性与三角形三个顶点的关系**和**该点重心坐标与三个顶点满足的线性关系相同**，根据这个性质，就可以通过重心坐标来对三角形内部的任意一个点做相关属性（颜色等等）的差值
        * 重心坐标的差值有一个问题：**不能保证投影不变性**
    * 
* **逐像素着色**：
  * <img src="./images/image-20230112140854628.png" alt="image-20230112140854628" style="zoom:50%;" />
  * 定义像素的法线方向：<img src="./images/image-20230112141707359.png" alt="image-20230112141707359" style="zoom:50%;" />

#### 3.渲染管线

* <img src="./images/image-20230112142044725.png" alt="image-20230112142044725" style="zoom:50%;" />
* **Shader（着色器）**：
  * 分为vertex shader 和 fragment shader
  * 每一个顶点或像素都会执行一次
  * ![image-20230112142911902](./images/image-20230112142911902.png)

#### 4.纹理映射（Texture Mapping）

* <img src="./images/image-20230112143633269.png" alt="image-20230112143633269" style="zoom:50%;" />
* <img src="./images/image-20230112144100903.png" alt="image-20230112144100903" style="zoom:50%;" />
* **纹理映射的具体做法：**
  * 三角形内部顶点的uv坐标就根据重心坐标来求得，然后根据uv坐标去相关颜色，把它赋值给bulin-phong模型中的kd即可<img src="./images/image-20230113220753784.png" alt="image-20230113220753784" style="zoom:50%;" />
  * 纹理映射会遇到的问题：
    * 纹理太小时（高分辨率屏幕上应用低分辨率的纹理贴图），会遇到类似锯齿（最终呈现在屏幕上的分辨率很低）的低质量图片，造成这个问题的**原因是当我们在查询像素的uv坐标时，会得到非整数的坐标，这导致很多个屏幕像素对应相同的一个纹理像素**
      * 解决方法：***双线性差值***，即**我们想得到一个更精确（更平滑）非整数uv映射的像素的颜色，我们同时考虑映射后的uv坐标邻近的四个纹理像素，来进行差值得到最终的纹理像素的值**
        * 
        * <img src="./images/image-20230113222420545.png" alt="image-20230113222420545" style="zoom:50%;" />
    * 纹理太大时，会导致严重的走样问题，产生的原因：每个像素点覆盖的纹理像素的范围是不同的，原本的采样方法就不适用了；**利用信号变化频率和采样频率来理解就是，当纹理贴图太大时，我们要把纹理贴图缩放到与像素屏幕一样的大小，这就导致了一个像素覆盖了很多的纹理像素（即一个像素的信号变化频率很大），如果我们的采样方法不变（采样频率小于信号变化频率就会导致走样），就会导致走样**（ps：需要注意的是，远处物体的一个像素会覆盖更多的纹理像素），根据这一理论可以提出如下的解决方法：（**范围查询**）
      *  超采样：即增加采样的点（使采样频率大于信号变化频率来解决走样问题），他的代价是计算开销太大
      * mipmap（图像金字塔）：只能做近似的正方形的范围查询
        * 做了什么操作：**对原始图像进行降低分辨率的操作，每次减少一半（比如，128×128 减少到64×64），一直减少到只剩一个像素，把每次减少分辨率的图像存起来（只增加了原始图三分之一的存储）**
        * 当有了mipmap存储的图后，就可以根据像素在纹理贴图中覆盖的近似正方形范围去查询mipmap中的某层图片来作为该像素的平均纹理像素
          * <img src="./images/image-20230113230302292.png" alt="image-20230113230302292" style="zoom:50%;" />
        * 利用三线性差值来平滑结果（得到连续的表达）
          * <img src="./images/image-20230113230623514.png" alt="image-20230113230623514" style="zoom:50%;" />
        * 这种方法也有一些**缺点**，比如远处的物体会过分模糊，细节缺失，这是因为mipmap**只能做正方形近似**导致的结果<img src="./images/image-20230113231046807.png" alt="image-20230113231046807" style="zoom:50%;" />
          * **解决方法**：
            * 各向异性过滤：对于矩形的覆盖得到了一定的解决，但是并没有完全解决![image-20230113231342623](./images/image-20230113231342623.png)
            * EWA过滤：把不规则的形状长城不同的圆形来拟合这个形状，缺点是开销比较大![image-20230113231215978](./images/image-20230113231215978.png)
  * **纹理的应用**
    * 环境贴图：模拟材质反射环境光照，描述来自不同方向的光照信息
      * 假设：环境光来自于无限远处
      * CubeMap技术，降低纹理贴图的扭曲程度
    * 凹凸贴图：存储高度、法线方向
      * 以更小的开销，获得更细致的视觉效果（仿真复杂的几何细节）
      * <img src="./images/image-20230115152519514.png" alt="image-20230115152519514" style="zoom:50%;" />
      * 计算：**在二维中：**<img src="./images/image-20230115152549402.png" alt="image-20230115152549402" style="zoom:50%;" />
        * 三维可以类比：<img src="./images/image-20230115152617898.png" alt="image-20230115152617898" style="zoom:50%;" />
    * 位移贴图
      * 真正改变几何的位置
      * 需要网格有较高的细致程度

#### 5.阴影（Shadows）

* 利用 **Shadow mapping** 技术生成 Shadow map 在光栅化中做阴影效果
  * 像素能否被**光源**看到、像素能否被**摄像机**看到
  * 1.从光源看向场景，记录每一个能看到的像素的深度；2.从摄像机看向场景，将摄像机看到的点距光源的深度与第一步记录的深度作对比，如果一致，那么该点可见（没有阴影），如果不一致，那么该点就是阴影         <img src="./images/image-20230119141917798.png" alt="image-20230119141917798" style="zoom:50%;" />
  * 只能做硬阴影<img src="./images/image-20230119142910238.png" alt="image-20230119142910238" style="zoom:50%;" />

## 几何

### 几何的表述

* 隐式几何
  * 表示几何上的点满足的关系（函数）
  * 缺点：很难从这个表达式直接看出来几何的形状
  * 优点：很容易判断一个点与几何的位置关系
  * <img src="./images/image-20230116143706608.png" alt="image-20230116143706608" style="zoom:50%;" />
  * CSG：通过基本几何体的运算（交、并、差）来获得其他复杂的几何
  * 距离函数：（融合）<img src="./images/image-20230116144331292.png" alt="image-20230116144331292" style="zoom:50%;" />
* 显式几何
  * 参数映射
    * <img src="./images/image-20230116143323817.png" alt="image-20230116143323817" style="zoom:50%;" />
    * 优缺点与隐式相反
  * 点云表示
    * <img src="./images/image-20230117152359487.png" alt="image-20230117152359487" style="zoom:50%;" />
  * 多边型面
    * <img src="./images/image-20230117152534997.png" alt="image-20230117152534997" style="zoom:50%;" />
* 分形几何
  * 不断重复自己（信号变化频率非常高，容易渲染走样）

### 曲线

* 贝塞尔曲线
  * 用一系列的控制点去控制的曲线
  * 贝塞尔曲线符合仿射变换不变性（对控制点仿射变换后重新画一次）
  * 贝塞尔曲线不符合投影变换不变性
  * **算法（de casdejue）：**                                   <img src="./images/image-20230117153647085.png" alt="image-20230117153647085" style="zoom: 25%;" /><img src="./images/image-20230117153741365.png" alt="image-20230117153741365" style="zoom: 25%;" /><img src="./images/image-20230117154006166.png" alt="image-20230117154006166" style="zoom: 25%;" /><img src="./images/image-20230117154056169.png" alt="image-20230117154056169" style="zoom: 33%;" />
    * **任意阶数的贝塞尔曲线（伯恩斯坦多项式）：**<img src="./images/image-20230117154735191.png" alt="image-20230117154735191" style="zoom:50%;" />
  * 逐段定义的贝塞尔曲线
    * **四个点定义一段贝塞尔曲线，然后把每段曲线连接起来**
    * <img src="./images/image-20230117155900725.png" alt="image-20230117155900725" style="zoom:50%;" />
* 贝塞尔曲面（布料模拟？）

 ### 曲面（几何处理）

<img src="./images/image-20230118112546203.png" alt="image-20230118112546203" style="zoom:50%;" />

* 网格细分

  **引入更多的三角形，并调整其位置**

  * **Loop Subdivision**

    <img src="./images/image-20230118112955964.png" alt="image-20230118112955964" style="zoom:50%;" />

    * 如何更新引入三角形后，各个顶点的位置：
      * 对新的顶点<img src="./images/image-20230118113233692.png" alt="image-20230118113233692" style="zoom:50%;" />
      * 对旧的顶点<img src="./images/image-20230118113419322.png" alt="image-20230118113419322" style="zoom:50%;" />

  * **Catmull-Clark Subdivision** 

    **对于一般的情况，不论是三角形还是四边形都可以用**

    * 一些定义：<img src="./images/image-20230118113837817.png" alt="image-20230118113837817" style="zoom:50%;" />
    * 具体做法：做第一次细分，增加了个数与非四边形面个数一致的这么多奇异点 
    * <img src="./images/image-20230118114452291.png" alt="image-20230118114452291" style="zoom:50%;" />
      * FYI（更新顶点的算法）<img src="./images/image-20230118114412837.png" alt="image-20230118114412837" style="zoom:50%;" />

* 网格简化

  **网格简化的目标是在保持模型大体形状的前提下减少面数，减少面数后，减少渲染开销**（几何的层次结构是一个研究方向）<img src="./images/image-20230118134941433.png" alt="image-20230118134941433" style="zoom:50%;" />

  * 具体做法：
    * 边坍缩：二次误差测量去决策那些边坍缩
    * <img src="./images/image-20230118135558832.png" alt="image-20230118135558832" style="zoom:50%;" />

* 网格规则化

## 光线追踪

**先对光线进行假设：**

* 光沿直线传播
* 光线与光线之间不存在相互作用
* 光线从光源到人眼<img src="./images/image-20230123142241933.png" alt="image-20230123142241933" style="zoom:50%;" />

### Whitted-Style Ray Tracing

**判断光源与人眼射线弹射点的可见关系后，叠加可见弹射点的光线到像素上**

<img src="./images/image-20230123150252397.png" alt="image-20230123150252397" style="zoom:50%;" />

* 数学表达：

  定义一条光线上的点<img src="./images/image-20230123151351839.png" alt="image-20230123151351839" style="zoom:50%;" />

  * 光线与**隐式**表面求交点（**可以利用数值计算去近似**）

    * <img src="./images/image-20230123151426156.png" alt="image-20230123151426156" style="zoom:50%;" />

  * 光线与**显示**表面（三角形）求交点

    * 光线与三角形有一个交点——> 点在三角形内 ；有两个交点在三角形外（**传统算法无法处理大场景，开销太大**）

      * <img src="./images/image-20230124115147913.png" alt="image-20230124115147913" style="zoom:50%;" />
      * MT算法
      * <img src="./images/image-20230124120701620.png" alt="image-20230124120701620" style="zoom:50%;" />

    * **优化算法：Bounding Volumes**

      * 利用一个**简单的“包围盒”**将一个**复杂的物体**包围起来，来**替代**原来的复杂物体做光线的计算

      * **从二维拓展到三维**<img src="./images/image-20230124122018718.png" alt="image-20230124122018718" style="zoom:50%;" />

        <img src="./images/image-20230124122222549.png" alt="image-20230124122222549" style="zoom:50%;" />

        <img src="./images/image-20230124122503850.png" alt="image-20230124122503850" style="zoom:50%;" />

      * 怎么利用包围盒来加速光线与物体的求交点运算

        * 空间划分：
          * KD-Tree（存在的问题：叶子结点可能同时存相同的物体；判断包围盒与空间划分出的立方体的交集在算法上较困难）
            * <img src="./images/image-20230128160235922.png" alt="image-20230128160235922" style="zoom:50%;" />
            * 光线只与叶子节点求交，不与中间结点求交<img src="./images/image-20230128160511183.png" alt="image-20230128160511183" style="zoom:50%;" />
        * 物体划分：
          * BVH：<img src="./images/image-20230128161434177.png" alt="image-20230128161434177" style="zoom: 33%;" /><img src="./images/image-20230128161621263.png" alt="image-20230128161621263" style="zoom: 50%;" /><img src="./images/image-20230128162137938.png" alt="image-20230128162137938" style="zoom:50%;" />

### 辐射度量学

**更为精确（服从物理）的描述光线与光的行为**

#### 前置定义：

* **Radiant Energy and Flux**：<img src="./images/image-20230130163501206.png" alt="image-20230130163501206" style="zoom:50%;" />
* **Radiant intensity**：<img src="./images/image-20230130163330887.png" alt="image-20230130163330887" style="zoom:50%;" />
  * **立体角**：<img src="./images/image-20230130164247169.png" alt="image-20230130164247169" style="zoom:33%;" />
* **Irradiance**：
  * <img src="./images/image-20230202134823554.png" alt="image-20230202134823554" style="zoom:67%;" />
* **Radiance**：
  * <img src="./images/image-20230202135349786.png" alt="image-20230202135349786" style="zoom:50%;" />
* **Irradiance与Radiance的关系**：<img src="./images/image-20230202135847062.png" alt="image-20230202135847062" style="zoom:50%;" />

#### BRDF：

**Bidirectional Reflectance Distribution Function（双向反射分布函数）**：

* **BRDF定义**：BRDF告诉我们**单位面积接收到某一立体角的能量会如何分配到各个不同的出射立体角上去（本质上是一个分布函数，类似权重（入射光分配了多少能量到所考察的出射方向上））**<img src="./images/image-20230203165636736.png" alt="image-20230203165636736" style="zoom:50%;" />

* **反射方程**：任何一个着色点，考虑所有方向的入射光对出射方向上的贡献（积分）<img src="./images/image-20230203170013863.png" alt="image-20230203170013863" style="zoom:50%;" />

  * 反射方程存在的问题：**除了光源外，其他被光源照亮的物体也会反射光线，成为“次”光源，对出射方向做出贡献**（也需要考虑），反射方程就有点**递归**求解的意思了

* **渲染方程**：**基于反射方程**，再考虑物体的**自发光情况**，我们得到**渲染方程**

  * <img src="./images/image-20230203170624731.png" alt="image-20230203170624731" style="zoom:50%;" />
  * <img src="./images/image-20230203171111435.png" alt="image-20230203171111435" style="zoom:50%;" />
  * 通过简单化表示渲染方程来得到渲染方程的解：
    * **得到全局光照方程**：<img src="./images/image-20230203171549352.png" alt="image-20230203171549352" style="zoom:50%;" /><img src="./images/image-20230203171914266.png" alt="image-20230203171914266" style="zoom:50%;" />

* **蒙特卡洛方法**：

  * https://zhuanlan.zhihu.com/p/396653562?utm_campaign=shareopn&utm_medium=social&utm_oi=938846415775129600&utm_psn=1605230717734256640&utm_source=wechat_session
  * 解决什么问题：对**复杂解析式**的函数进行积分
  * 是一种数值方法，无需对解析式进行积分，在积分域内**不断采样**进行计算，再加起来求平均（采样服从的分布函数为P（x）是我们自己选取的）<img src="./images/image-20230204152655760.png" alt="image-20230204152655760" style="zoom:50%;" />![image-20230204154846426](./images/image-20230204154846426.png)

* Path Tracing

  * 解决之前Whitted-Style Ray Tracing 的一些不基于真实物理规则的假设

  * **利用蒙特卡洛方法计算渲染方程积分得到全局光照算法**：

    * **先进行直接光照计算**：<img src="./images/image-20230204160427799.png" alt="image-20230204160427799" style="zoom:50%;" /><img src="./images/image-20230204160526648.png" alt="image-20230204160526648" style="zoom:50%;" /><img src="./images/image-20230204160710818.png" alt="image-20230204160710818" style="zoom:50%;" />

    * **1.再考虑间接光照，得到全局光照**：<img src="./images/image-20230204160854850.png" alt="image-20230204160854850" style="zoom:50%;" /><img src="./images/image-20230204160925810.png" alt="image-20230204160925810" style="zoom:50%;" />

    * **2.考虑到计算爆炸问题，我们只采样1根光线**（N=1）：

      * 得到**路径追踪**算法：<img src="./images/image-20230204161711727.png" alt="image-20230204161711727" style="zoom:50%;" />

      * **解决采样少的噪声问题**：**多算几条路径对一个像素的贡献**<img src="./images/image-20230204161833927.png" alt="image-20230204161833927" style="zoom:50%;" />![image-20230204161922214](./images/image-20230204161922214.png)

    * **3.考虑递归算法的停止条件**：

      * 引入俄罗斯轮盘赌方法：<img src="./images/image-20230204162318903.png" alt="image-20230204162318903" style="zoom:50%;" />
      * **得到路径追踪算法**：<img src="./images/image-20230204162436402.png" alt="image-20230204162436402" style="zoom:50%;" />

    * 4.我们之前的算法是**以着色点为基准来采样**，这样产生的一个问题就是，采样效果很大程度上受到光源形状的影响（光源大效果好，光源小碰运气），为了优化这个问题，我们之后**以光源为基准来采**样，这样的话，就需要重写渲染方程，**把积分变量从以着色点为基准时的立体角换为以光源为基准的光源面积**，我们只需要知道立体角和光源面积的关系式就可以完成方程的重写：<img src="./images/image-20230204163029124.png" alt="image-20230204163029124" style="zoom:50%;" /><img src="./images/image-20230204163218400.png" alt="image-20230204163218400" style="zoom:50%;" />![image-20230204163410331](./images/image-20230204163410331.png)

    * **在经过上述所有优化过后，再次写出路径追踪算法**：<img src="./images/image-20230204163643830.png" alt="image-20230204163643830" style="zoom:50%;" />

    * **5.再考虑光源的可见性问题**：<img src="./images/image-20230204163932929.png" alt="image-20230204163932929" style="zoom:50%;" />

    * **综上所述，得到最终的路径追踪算法**

​				

## 材质：

**Meterial == BRDF** ，材质等价于BRDF，**本质上是描述了某种物体对入射光的响应行为**

### 漫反射

* 漫反射的BRDF视为常数，由于能量守恒，**入射光能量等于反射光能量**，求出**漫反射的BRDF表达式**：（其中**albedo为颜色的调制项**）<img src="./images/image-20230205153351599.png" alt="image-20230205153351599" style="zoom:50%;" />

### 镜面反射

* 根据反射定律，利用不同的方法对入射光、反射光进行计算<img src="./images/image-20230205152904339.png" alt="image-20230205152904339" style="zoom:50%;" />

### 折射

* 折射定律：
  * <img src="./images/image-20230205154448459.png" alt="image-20230205154448459" style="zoom:50%;" />
* 根据折射定律计算折射角的余弦：
  * <img src="./images/image-20230205154625735.png" alt="image-20230205154625735" style="zoom:50%;" />
  * 当根号下小于0时，不存在折射，此时发生全反射：当入射光从光疏介质打到光密介质时会反生

### 菲涅尔项

* 描述**反射率**与**物体法线与观察方向（人眼）夹角**之间的关系：**反射率取决于物体法线与观察方向（人眼）夹角，夹角越大，反射的能量越多**
* ![image-20230205155337734](./images/image-20230205155337734.png)

### 微表面材质

* 假设：
  * 远处：视材质表面是平的，有粗糙度
  * 近处：有凹凸，可以看到几何
* **通过用微表面的法线分布来描述材质的粗糙程度**：
  * <img src="./images/image-20230206123041262.png" alt="image-20230206123041262" style="zoom:50%;" />
  * **微表面假设下的BRDF**：<img src="./images/image-20230206124642943.png" alt="image-20230206124642943" style="zoom:50%;" />![image-20230206125427619](./images/image-20230206125427619.png)
* 各向同性（微表面不存在方向性）与各向异性（微表面存在明显的方向性）材质
  * <img src="./images/image-20230206125642530.png" alt="image-20230206125642530" style="zoom:50%;" />
  * 各向异性材质：不同角度的BRDF不同：<img src="./images/image-20230206125752282.png" alt="image-20230206125752282" style="zoom:50%;" />
* BRDF的性质：
  * 非负性
  * 线性叠加性
    * <img src="./images/image-20230206130139313.png" alt="image-20230206130139313" style="zoom:50%;" />
  * 可逆性：
    * <img src="./images/image-20230206130212149.png" alt="image-20230206130212149" style="zoom:50%;" />
  * 能量守恒
    * <img src="./images/image-20230206130244504.png" alt="image-20230206130244504" style="zoom:50%;" />
  * 各向同性与各向异性
    * 各向同性：<img src="./images/image-20230206130403675.png" alt="image-20230206130403675" style="zoom:50%;" />
* **BRDF的测量**：
  * <img src="./images/image-20230206130547333.png" alt="image-20230206130547333" style="zoom:50%;" />

