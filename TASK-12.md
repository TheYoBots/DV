# Annotation
```py
import numpy as np
import matplotlib. pyplot as plt
x = np.arange(0, 10, 0.005)
y = np.exp(-x / 3.) * np.sin(3 * np.pi * x)
fig, ax = plt.subplots()
ax.plot(x, y)
ax.set_xlim(0, 10)
ax.set_ylim(-1, 1)
xdata, ydata = 5, 0
xdisplay, ydisplay = ax.transData.transform((xdata, ydata))
bbox = dict(boxstyle ="round", fc ="0.8")
arrowprops = dict(arrowstyle = "->", connectionstyle = "angle")
offset = 72
ax.annotate('data = (%.1f, %.1f)'%(xdata, ydata), (xdata, ydata), xytext =(-2 * offset, offset), textcoords ='offset points', bbox = bbox, arrowprops = arrowprops)
disp = ax.annotate('display = (%.1f, %.1f)'%(xdisplay, ydisplay), (xdisplay, ydisplay), xytext =(0.5 * offset, -offset), xycoords ='figure pixels', textcoords ='offset points', bbox = bbox, arrowprops = arrowprops)
plt.show()
```
and
```py
import matplotlib.pyplot as plt
import numpy as np
fig, geeeks = plt.subplots()
t = np.arange(0.0, 5.0, 0.001)
s = np.cos(3 * np.pi * t)
line = geeeks.plot(t, s, lw = 2)
geeeks.annotate('Local Max', xy =(3.3, 1),
				xytext =(3, 1.8),
				arrowprops = dict(facecolor ='green', shrink = 0.05))
geeeks.set_ylim(-2, 2)
plt.show()
```

Output:

![image](https://github.com/TheYoBots/DV/assets/73843275/18bc17d3-637e-4e9d-9523-21f8305ac76f)
