# Graphics Math Notes / グラフィックス数学ノート

## 1. Vector / ベクトル

### 中文理解
向量可以表示位置、方向、速度、法线、颜色等信息。在图形学中，很多计算本质上都是对向量进行操作。

### English Explanation
A vector can represent position, direction, velocity, normal, or color in computer graphics. Many graphics calculations are based on vector operations.

### 日本語説明
ベクトルは、位置、方向、速度、法線、色などを表すために使われます。  
コンピュータグラフィックスでは、多くの計算がベクトルを基礎として行われます。

---

## 2. Dot Product / 内積

### 中文理解
点乘可以用来判断两个方向有多接近。结果越大，说明两个方向越接近；结果为 0，说明两个方向垂直；结果为负，说明方向相反。

在图形学中，点乘经常用于光照计算。例如表面法线和光线方向越接近，表面通常越亮。

### English Explanation
The dot product is used to measure how similar two directions are.  
A larger positive value means the two vectors point in a similar direction. A value of zero means they are perpendicular, and a negative value means they point in opposite directions.

In computer graphics, the dot product is commonly used in lighting calculations. For example, when the surface normal and the light direction are closer, the surface usually appears brighter.

### 日本語説明
内積は、二つの方向がどれくらい近いかを調べるために使われます。  
値が大きいほど二つのベクトルは近い方向を向いており、0の場合は直交し、負の場合は反対方向を向いています。

グラフィックスでは、内積はライティング計算によく使われます。例えば、表面の法線方向と光の方向が近いほど、その面は明るく見えます。

---

## 3. Cross Product / 外積

### 中文理解
叉乘可以从两个向量生成一个新的垂直向量。在图形学中，它常用于计算三角形表面的法线。

例如，一个三角形有三个点，可以用两条边做叉乘，得到这个三角形面的朝向。

### English Explanation
The cross product generates a new vector that is perpendicular to two input vectors.  
In computer graphics, it is often used to calculate surface normals.

For example, given two edge vectors of a triangle, their cross product gives the normal direction of that triangle surface.

### 日本語説明
外積は、二つのベクトルに対して垂直な新しいベクトルを求めるために使われます。  
グラフィックスでは、三角形の表面法線を計算する際によく使われます。

例えば、三角形の二つの辺ベクトルの外積を取ることで、その面がどちらを向いているかを表す法線を求めることができます。

---

## 4. Matrix / 行列

### 中文理解
矩阵可以表示各种变换，例如平移、旋转、缩放和投影。图形学中通常把顶点位置和矩阵相乘，从而把物体从一个坐标空间变换到另一个坐标空间。

### English Explanation
A matrix can represent transformations such as translation, rotation, scaling, and projection.  
In computer graphics, vertex positions are multiplied by matrices to transform them from one coordinate space to another.

### 日本語説明
行列は、平行移動、回転、拡大縮小、投影などの変換を表すために使われます。  
グラフィックスでは、頂点座標に行列を掛けることで、ある座標空間から別の座標空間へ変換します。

---

## 5. Homogeneous Coordinates / 同次座標

### 中文理解
齐次坐标是在普通坐标后面增加一个 w 分量。  
在 3D 图形学中，普通坐标是 `(x, y, z)`，齐次坐标是 `(x, y, z, w)`。

这样做的好处是，可以把平移、旋转、缩放和投影都统一成矩阵乘法来处理。

### English Explanation
Homogeneous coordinates add an extra component, `w`, to a normal coordinate.  
In 3D graphics, a position `(x, y, z)` is represented as `(x, y, z, w)`.

This makes it possible to handle translation, rotation, scaling, and projection uniformly using matrix multiplication.

### 日本語説明
同次座標は、通常の座標に `w` 成分を追加した表現です。  
3Dグラフィックスでは、通常の座標 `(x, y, z)` を `(x, y, z, w)` として扱います。

これにより、平行移動、回転、拡大縮小、投影などをすべて行列計算として統一的に扱うことができます。

---

## 6. MVP Transformation / MVP変換

### 中文理解
MVP 指 Model、View、Projection 三个变换。

Model 矩阵把物体从自身的局部坐标变换到世界坐标。  
View 矩阵把世界坐标变换到相机视角下的坐标。  
Projection 矩阵把 3D 空间投影到 2D 画面上。

### English Explanation
MVP refers to Model, View, and Projection transformations.

The Model matrix transforms an object from local space to world space.  
The View matrix transforms world space into the camera’s view space.  
The Projection matrix projects 3D space onto a 2D screen.

### 日本語説明
MVPは、Model、View、Projectionの三つの変換を指します。

Model行列は、物体をローカル座標からワールド座標へ変換します。  
View行列は、ワールド座標をカメラから見た座標系へ変換します。  
Projection行列は、3D空間を2D画面に投影するために使われます。



## 理解

#### Q1. Model, View, Projection 分别是什么？

Model行列は、モデル自身のローカル座標をワールド座標へ変換する行列です。  
View行列は、ワールド座標をカメラから見た座標系へ変換する行列です。  
Projection行列は、3D空間上の座標を2D画面に投影するための行列です。

#### Q2. 为什么 3D 图形学要用矩阵？

3Dグラフィックスでは、モデルの移動、回転、拡大縮小、投影などの変換を数式として扱う必要があります。  
行列を使うことで、これらの変換を統一的に計算でき、頂点座標を効率よく別の座標空間へ変換できます。

#### Q3. 为什么需要齐次坐标？

同次座標は、通常の3D座標 `(x, y, z)` に `w` 成分を加えた表現です。  
これにより、平行移動、回転、拡大縮小、投影などの変換をすべて行列計算として統一的に扱うことができます。

#### Q4. Unity 的 Camera 和 GAMES101 的 View / Projection 有什么关系？

UnityのCameraは、GAMES101で学ぶView変換とProjection変換に対応しています。  
Cameraの位置や回転はView行列に関係し、視野角、Near Clip、Far Clip、アスペクト比などの設定はProjection行列に関係します。  
つまり、UnityのCameraは、3D空間をカメラから見た座標系へ変換し、それを最終的に画面上に投影する役割を持っています。