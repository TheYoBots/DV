# Graph data visualization
```py
import networkx as nx
import matplotlib.pyplot as plt

class GraphVisualization:
	def __init__(self):
		self.visual = []

	def addEdge(self, a, b):
		temp = [a, b]
		self.visual.append(temp)

	def visualize(self):
		G = nx.Graph()
		G.add_edges_from(self.visual)
		nx.draw_networkx(G)
		plt.show()

G = GraphVisualization()
G.addEdge(0, 2)
G.addEdge(1, 2)
G.addEdge(1, 3)
G.addEdge(5, 3)
G.addEdge(3, 4)
G.addEdge(1, 0)
G.visualize()
```

Output:

![image](https://github.com/TheYoBots/DV/assets/73843275/74ffebfb-52ae-46f5-a5a0-7e4eca9acacc)
