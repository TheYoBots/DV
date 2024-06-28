# pm3d coloring

```py
import numpy as np
import matplotlib.pyplot as pl
from scipy.interpolate import griddata
z=np.loadtxt("data.dat",usecols=[0,1,2],unpack=True)
x=np.arange(0,10.1,0.10)
y=np.arange(0,8.1,0.10)
zi=griddata((z[0],z[1]),z[2],(x[None,:], y[:,None]), method='cubic')
pl.imshow(zi,origin="lower",vmin=0,cmap="hot",aspect="auto",extent=[0,10,0,8])
pl.xlabel("U")
pl.ylabel("V")
pl.title("Zero-Temp gap ")
pl.colorbar()
pl.savefig("outAF.pdf")
```
or
```py
import matplotlib.pyplot as plt
import numpy as np
from matplotlib.colors import LogNorm
dx, dy = 0.015, 0.05
y, x = np.mgrid[slice(-4, 4 + dy, dy), slice(-4, 4 + dx, dx)]
z = (1 - x / 3. + x ** 5 + y ** 5) * np.exp(-x ** 2 - y ** 2)
z = z[:-1, :-1]
z_min, z_max = -np.abs(z).max(), np.abs(z).max()
c = plt.imshow(z, cmap ='Greens', vmin = z_min, vmax = z_max, extent =[x.min(), x.max(), y.min(), y.max()], interpolation ='nearest', origin ='lower')
plt.colorbar(c)
plt.title('matplotlib.pyplot.imshow() function Example', fontweight ="bold")
plt.show()
```
Output:

![image](https://github.com/TheYoBots/DV/assets/73843275/03a974d9-b246-49b2-85ff-fe1af899c8cf)

# 3D mapping
```py
from matplotlib import pyplot as plt, cm, colors
import numpy as np
plt.rcParams["figure.figsize"] = [7.00, 3.50]
plt.rcParams["figure.autolayout"] = True
side = np.linspace(-2, 2, 15)
X, Y = np.meshgrid(side, side)
Z = np.exp(-((X - 1) ** 2 + Y ** 2))
plt.pcolormesh(X, Y, Z, shading='auto')
plt.show()
```
or
```py
from matplotlib import pyplot as plt, cm, colors
import numpy as np
plt.rcParams["figure.figsize"] = [7.00, 3.50]
plt.rcParams["figure.autolayout"] = True
side = np.linspace(-2, 2, 15)
X, Y = np.meshgrid(side, side)
Z = np.exp(-((X - 1) ** 2 + Y ** 2))
plt.pcolormesh(X, Y, Z, shading='auto')
plt.show()
```

Output:

![image](https://github.com/TheYoBots/DV/assets/73843275/b9d999ec-7ca7-44b7-a3ac-269e68330e3d)
