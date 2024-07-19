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

```
python3 libero_100_collect_demonstrations.py --bddl-file /home/bwshen/LIBERO/libero/libero/bddl_files/libero_spatial/pick_up_the_black_bowl_between_the_plate_and_the_ramekin_and_place_it_on_the_plate.bddl
```





@TODO
- 明确```bddl```文件相关 param
    - 分布 var
    - 任务 def
- 修改 3D mouse 的控制模式直接控制 end effector 的位置和状态
- 数据收集,一个hdf5包括多个视角
