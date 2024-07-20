## 遥操作数据集收集指南
### 安装libero, docs:

https://lifelong-robot-learning.github.io/LIBERO/html/getting_started/overview.html

### 安装3D usb鼠标驱动：
不需要使用博客中最后的验证是否demo
https://blog.csdn.net/qq_40081208/article/details/137675822

### 修改```vendor_id```和```product_id```


把
```/home/${USER}/anaconda3/envs/libero/lib/python3.8/site-packages/robosuite/devices/spacemouse.py```
中的 vendor id 和 product id设置成上一个步骤设定的值。使用robosuite的代码，
```
 python3 demo_device_control.py --device=spacemouse
```

测试3D鼠标是否可以和robosuite环境正常交互


### 收集数据
到```scripts```目录下

```
python3 libero_100_collect_demonstrations.py --bddl-file /home/bwshen/LIBERO/libero/libero/bddl_files/libero_spatial/pick_up_the_black_bowl_between_the_plate_and_the_ramekin_and_place_it_on_the_plate.bddl
```


### 增大初始环境分布的variance
BDDLBaseDomain继承自robosuite的SingleArmEnv，然后可以一路继承到robot_env.py文件，可以看到这个参数的有关的描述
```
        initialization_noise (dict or list of dict): Dict containing the initialization noise parameters.
            The expected keys and corresponding value types are specified below:

            :`'magnitude'`: The scale factor of uni-variate random noise applied to each of a robot's given initial
                joint positions. Setting this value to `None` or 0.0 results in no noise being applied.
                If "gaussian" type of noise is applied then this magnitude scales the standard deviation applied,
                If "uniform" type of noise is applied then this magnitude sets the bounds of the sampling range
            :`'type'`: Type of noise to apply. Can either specify "gaussian" or "uniform"

            Should either be single dict if same noise value is to be used for all robots or else it should be a
            list of the same length as "robots" param

            :Note: Specifying "default" will automatically use the default noise settings.
                Specifying None will automatically create the required dict with "magnitude" set to 0.0.
```
所以,

### bddl 文件相关
在 ```(:init)```中，如果注释掉```(On flat_stove_1 main_table_stove_region)```这一行的话，启动mujuco仿真环境会卡一会，还有可能卡成自动重启，并且 Terminal 有输出
```
WARNING: Nan, Inf or huge value in QACC at DOF 15. The simulation is unstable. Time = 49.6800.
```


### @TODO
- 明确```bddl```文件相关 param
    - 分布 var
    - 任务 def
- 修改 3D mouse 的控制模式直接控制 end effector 的位置和状态
- 数据收集,一个hdf5包括多个视角
