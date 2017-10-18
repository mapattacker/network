Visualization
==============

Layouts
--------

.. code:: python

  ['circular_layout',
   'random_layout',
   'shell_layout',
   'spring_layout',
   'spectral_layout',
   'fruchterman_reingold_layout']
   
   
Basic Chart
-------------

.. code:: python

  import networkx as nx
  import matplotlib.pyplot as plt
  import seaborn as sns
  %matplotlib inline
  
  
  plt.figure(figsize=(5, 5))
  
  G = nx.read_gpickle('major_us_cities')
  
  # chose the layout
  pos = nx.random_layout(G)
  
  # draw network
  # nx.draw() also can, but has no axes
  nx.draw_networkx(G, pos, with_labels = True, node_size=800, node_color='pink', \
                           alpha=0.7, edge_color='grey', width=1)
  
  # off axes
  plt.axis('off')
  
  # label edges
  edge_labels = dict([((u,v,), d['distance']) for u,v,d in g.edges(data=True)])
  nx.draw_networkx_edge_labels(G, pos, edge_labels=edge_labels)
  

Varying Node Color, Size, Edge Widths
----------------------------------------


.. code:: python
  
  # using degree for each node
  node_color = [G.degree(v) for v in G] 
  # using node attribute, population * by a small constant so it won't be too large
  node_size = [0.0005*nx.get_node_attributes(G, 'population')[v] for v in G]
  # using weight * by small constant
  edge_width = [0.0015*G[u][v]['weight'] for u,v in G.edges()]


  
Label Specific Nodes
--------------------

.. code:: python

  nx.draw_networkx_labels(G, pos, labels={'Los Angeles, CA': 'LA', 'New York, NY': 'NYC'}, \
                          font_size=18, font_color='w')
  
  
Specific Edges Widths
----------------------

.. code:: python

  # plot shortest path
  path = nx.shortest_path(g, source=s,target=t, weight='distance')
  path_edges = zip(path,path[1:])
  nx.draw_networkx_edges(g, pos, edgelist=path_edges, edge_color='r', width=15)
  
  
  # Weights > 770
  greater_than_770 = [x for x in G.edges(data=True) if x[2]['weight']>770]
  nx.draw_networkx_edges(G, pos, edgelist=greater_than_770, edge_color='r', alpha=0.4, width=6)


Position Node Coordinates
--------------------------

If the coordinates of nodes are embedded in the node attributes,
we can plot them to position at those coordinates in the graph.

.. code:: python
  
  # Draw the graph using custom node positions
  plt.figure(figsize=(10,7))
  
  # view the data
  G.nodes(data=True)
  #   [('El Paso, TX', {'location': (-106, 31), 'population': 674433}),
  #  ('Long Beach, CA', {'location': (-118, 33), 'population': 469428}),
  #  ('Dallas, TX', {'location': (-96, 32), 'population': 1257676}),
  #  ('Oakland, CA', {'location': (-122, 37), 'population': 406253}),
  
  pos = nx.get_node_attributes(G, 'location')
  nx.draw_networkx(G, pos)



