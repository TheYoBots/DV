# Surfaces

```py
import numpy as np 
import matplotlib.pyplot as plt 
x = np.outer(np.linspace(-2, 2, 30), np.ones(30))
y = x.copy().T
z = np.cos(x ** 2 + y ** 2)
fig = plt.figure() 
ax = plt.axes(projection='3d') 
ax.plot_surface(x, y, z,cmap='viridis', edgecolor='none')
ax.set_title('Surface plot') 
plt.show()
```

Output:

![image](https://github.com/TheYoBots/DV/assets/73843275/f25d6444-f52e-4ff4-8a97-d09e164fe380)

# Contours

```py
import numpy as np
import matplotlib.pyplot as plt
xlist = np.linspace(-3.0, 3.0,100)
ylist = np.linspace(-3.0, 3.0, 100)
X, Y = np.meshgrid(xlist, ylist)
Z = np.sqrt(X**2 + Y**2)
fig,ax=plt.subplots(1,1)
cp = ax.contourf(X, Y, Z)
fig.colorbar(cp) # Add a colorbar to a plot 
ax.set_title('Filled Contours Plot')
ax.set_xlabel('x (cm)')
ax.set_ylabel('y (cm)')
plt.show()
```
Output:

![image](https://github.com/TheYoBots/DV/assets/73843275/c7c0aaee-b1d1-4c7f-8439-5b3ed5a396e3)

# Hidden Surfaces

```py
import matplotlib.pyplot as plt 
from mpl_toolkits.mplot3d import axes3d 
from matplotlib import pyplot
fig = plt.figure() 
wf = fig.add_subplot(111, projection='3d') 
x, y, z = axes3d.get_test_data(0.1)
wf.plot_wireframe(x,y,z, rstride=2, cstride=2, color='blue')
wf.set_title('Example 1')
pyplot.show()
```
Output:

![image](https://github.com/TheYoBots/DV/assets/73843275/7f27438a-0589-4088-b41f-118f1dd71de8)
