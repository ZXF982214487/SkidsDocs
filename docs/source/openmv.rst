openmv摄像头测距
------------------
模块介绍
^^^^^^^^^^^^^^^^^^^^^
OpenMV摄像头是一款小巧，低功耗，低成本的电路板，它帮助你很轻松的完成机器视觉（machine vision）应用。
你可以通过高级语言Python脚本（准确的说是 MicroPython ），而不是C/C++。Python的高级数据结构使你很容易在机器视觉算法中处理复杂的输出。
但是，你仍然可以完全控制OpenMV，包括IO引脚。你可以很容易的使用外部终端触发拍摄或者或者执行算法，也可以把算法的结果用来控制IO引脚。



编程学习
^^^^^^^^^^^^^^^^^^^^^
读取openmv画面信息，计算出目标物体与摄像头距离，代码如下：
 ::

	import sensor, image, time
	
	blue_threshold   = (0, 77, 0, -27, -128, 0)#设置目标颜色的LAB色彩空间参数
	
	sensor.reset() # 初始化摄像头
	sensor.set_pixformat(sensor.RGB565) 
	sensor.set_framesize(sensor.QQVGA) 
	sensor.skip_frames(10) 
	sensor.set_auto_whitebal(False) 
	clock = time.clock() 

	K=5000#设置参数

	while(True):
		clock.tick() # Track elapsed milliseconds between snapshots().
		img = sensor.snapshot() # Take a picture and return the image.

		blobs = img.find_blobs([yellow_threshold])
		if len(blobs) == 1:
			# Draw a rect around the blob.
			b = blobs[0]
			img.draw_rectangle(b[0:4]) # rect
			img.draw_cross(b[5], b[6]) # cx, cy
			Lm = (b[2]+b[3])/2#像素点大小
			length = K/Lm
			print(length)#输出距离






