# MVP Transformation / MVP変換

## 中文理解

MVP 是 Model、View、Projection 三个变换的组合。  
它描述了一个 3D 顶点从物体自身坐标，经过世界坐标、相机坐标，最后被投影到屏幕上的过程。

## English Explanation

MVP stands for Model, View, and Projection transformations.  
It describes how a vertex is transformed from an object's local space to world space, then to camera space, and finally projected onto the screen.

## 日本語説明

MVPは、Model、View、Projectionの三つの変換を指します。  
3Dモデルの頂点をローカル座標からワールド座標、カメラ座標へ変換し、最終的に画面上に投影するために使われます。

---

# Key Concepts / 重要概念

## 1. Model Matrix / Model行列

### 中文理解

Model 矩阵负责物体自身的移动、旋转和缩放。  
它把模型从自己的局部坐标系变换到世界坐标系。

### English Explanation

The Model matrix represents the object's translation, rotation, and scaling.  
It transforms the object from local space to world space.

### 日本語説明

Model行列は、物体自身の移動、回転、拡大縮小を表します。  
モデルをローカル座標からワールド座標へ変換します。

---

## 2. View Matrix / View行列

### 中文理解

View 矩阵表示从相机视角观察世界。  
它通常可以理解为把整个世界移动和旋转到相机前方。

### English Explanation

The View matrix represents the world from the camera's point of view.  
It can be understood as transforming the world into the camera's coordinate system.

### 日本語説明

View行列は、カメラから見た世界を表すための行列です。  
ワールド座標をカメラ座標系へ変換します。

---

## 3. Projection Matrix / Projection行列

### 中文理解

Projection 矩阵负责把 3D 空间投影到 2D 屏幕上。  
透视投影会产生近大远小的效果。

### English Explanation

The Projection matrix projects 3D space onto a 2D screen.  
Perspective projection makes closer objects appear larger and farther objects appear smaller.

### 日本語説明

Projection行列は、3D空間を2D画面に投影するための行列です。  
透視投影では、近くの物体は大きく、遠くの物体は小さく見えます。

---

## 重点

#### 1. 座標空間のチェイン：

ローカル座標 → ワールド座標 → カメラ座標 → クリップ座標 → スクリーン座標

#### 2. 核心函数

get_model_matrix(float rotation_angle)   比如绕Z轴旋转

cosθ  -sinθ  0  0
sinθ   cosθ  0  0
0      0     1  0
0      0     0  1

#### 3. View Matrix

图形学里经常不是“我移动相机”，而是“我把世界变换到相机坐标系下”。也就是说，相机动到右边，等价于世界往左边动。

#### 4. Projection Matrix

Projection Matrix 把相机看到的 3D 空间压到后续可以显示在 2D 屏幕上的坐标范围里。



# 理解

## Q1. 为什么矩阵乘法的顺序很重要？

### 中文理解

矩阵乘法没有交换律，不同顺序变换会导致最后得到的结果不同

### English Explanation

Matrix multiplication is not commutative, so changing the order of transformations can produce different results.  

### 日本語説明

行列の掛け算には交換法則がないため、変換の順番を変えると最終的な結果も変わります。

---

## Q2. 为什么 View 变换可以理解为“移动整个世界”？

### 中文理解

View 变换的目的是把世界坐标转换到相机坐标系中。
从计算角度来看，我们通常把相机看作坐标系的原点，因此需要对整个世界做相机移动的反向变换。 
比如相机向右移动，可以理解为世界相对于相机向左移动。

### English Explanation

The purpose of the View transformation is to convert world coordinates into the camera coordinate system. 
From a mathematical point of view, the camera is treated as the origin of the view space, so the world is transformed by the inverse of the camera transformation. 
For example, if the camera moves to the right, the world can be understood as moving to the left relative to the camera.

### 日本語説明

View変換の目的は、ワールド座標をカメラ座標系へ変換することです。 
計算上は、カメラを視点座標系の原点として扱うため、カメラの移動とは逆方向にワールド全体を変換すると考えることができます。 
例えば、カメラが右に移動した場合、相対的には世界全体が左に移動したように扱われます。

---

## Q3. 透视投影为什么会产生近大远小？

### 中文理解

透视投影中，物体的屏幕坐标会受到深度值的影响。 
当物体离相机越远时，z 值越大，类似 x / z、y / z 的结果就越小，所以它在屏幕上看起来也越小。 
这就是近处物体看起来大，远处物体看起来小的原因。

### English Explanation

In perspective projection, the screen position of a point is affected by its depth. 
When an object is farther from the camera, its z value becomes larger, so values like x / z and y / z become smaller. 
As a result, distant objects appear smaller on the screen, while closer objects appear larger.

### 日本語説明

透視投影では、点のスクリーン上の位置は深度の影響を受けます。 
物体がカメラから遠くなるほど z の値が大きくなり、x / z や y / z のような値は小さくなります。 
その結果、近くの物体は大きく、遠くの物体は小さく見えます。

---

## Q4. Unity 中的 Transform 和 Camera 分别对应 MVP 的哪一部分？

### 中文理解

Unity 中物体自身的 Transform 主要对应 Model Matrix，因为它决定了物体在世界中的位置、旋转和缩放。 
Camera 的 Transform 对应 View Matrix，因为它决定了从哪个位置和方向观察世界。 
Camera 的 FOV、Near Clip、Far Clip、Aspect Ratio 等设置对应 Projection Matrix，因为它们决定了 3D 空间如何被投影到屏幕上。

### English Explanation

In Unity, an object's Transform mainly corresponds to the Model matrix, because it defines the object's position, rotation, and scale in the world. 
The Camera's Transform corresponds to the View matrix, because it defines the position and direction from which the world is viewed. 
Camera settings such as FOV, Near Clip, Far Clip, and Aspect Ratio correspond to the Projection matrix, because they define how 3D space is projected onto the screen.



### 日本語説明

Unityでは、オブジェクト自身のTransformは主にModel行列に対応します。これは、物体のワールド空間における位置、回転、拡大縮小を決めるためです。 
CameraのTransformはView行列に対応します。これは、どの位置と方向から世界を見るかを決めるためです。 
また、CameraのFOV、Near Clip、Far Clip、Aspect Ratioなどの設定はProjection行列に対応し、3D空間をどのように画面へ投影するかを決めます。



**Object Transform → Model**
**Camera Transform → View**
**Camera Settings → Projection**