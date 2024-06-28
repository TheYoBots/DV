# Annotation
```py
import matplotlib.pyplot as plt
import numpy as np


fig, geeeks = plt.subplots()

t = np.arange(0.0, 5.0, 0.001)
s = np.cos(3 * np.pi * t)
line = geeeks.plot(t, s, lw = 2)

# Annotation
geeeks.annotate('Local Max', xy =(3.3, 1),
				xytext =(3, 1.8),
				arrowprops = dict(facecolor ='green',
								shrink = 0.05),)

geeeks.set_ylim(-2, 2)

# Plot the Annotation in the graph
plt.show()
```

Output:

![image](https://github.com/TheYoBots/DV/assets/73843275/18bc17d3-637e-4e9d-9523-21f8305ac76f)
