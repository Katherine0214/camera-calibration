# camera-calibration
>本算法包用于实现单目、双目相机标定。



🛠️ 一、单目标定
---
### 步骤： 

- #### 计算内参初始值：```init_intrinsic_param.m```

   先求出单应矩阵H，然后利用旋转向量相互正交的约束关系从H中分离出内参矩阵；


- #### 计算外参：```extrinsic_computation.m``` 
    
    先求出外参初始值（用solvePnP），再优化外参；

- #### 优化所有参数：```go_calib_optim.m``` 

    通过最小化重投影误差优化所有参数（内参、畸变参数（畸变初始值全为0）、外参）。



👾 二、双目标定     ```calib_stereo.m```
---

### 步骤： 

- #### 根据单目标定的内参，求出两个相机到世界坐标系的外参：```extrinsic_computation.m```


- #### 对于每张图片，计算出左右相机之间的R,T，并取平均值作为初始值：```compose_motion.m``` 
    

- #### 重新优化所有参数： 

  通过之前计算的内外参，将三维点投影到右相机二维图像上；用到上面的R,T初始值将右相机点转换到左相机点；令投影点与图像上检测到的点的误差最小。

    


🎲 三、极线矫正     ```rectify_stereo_pair.m```
---

- #### 根据左右相机之间的R,T，计算出左右相机分别各自旋转、平移的矩阵。


📖 四、其他资料 
--- 

(1) 参数介绍：```parameters.html```


(2) 函数介绍：```functions.html``` 
    

(3) 标定步骤：```example.html``` 



