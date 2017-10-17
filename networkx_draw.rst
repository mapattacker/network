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
  nx.draw_networkx(G, pos, with_labels = True, node_size=800, node_color='pink', \
                           alpha=0.7, edge_color='grey', width=1)
  plt.axis('off')
  
  # label edges
  edge_labels = dict([((u,v,), d['distance']) for u,v,d in g.edges(data=True)])
  nx.draw_networkx_edge_labels(G, pos, edge_labels=edge_labels)
  
  
Label Specific Nodes
--------------------

.. code:: python

  nx.draw_networkx_labels(G, pos, labels={'Los Angeles, CA': 'LA', 'New York, NY': 'NYC'}, font_size=18, font_color='w')
  
  
Label Specific Edges
----------------------

.. code:: python

  # plot shortest path
  path = nx.shortest_path(g, source=s,target=t, weight='distance')
  path_edges = zip(path,path[1:])
  nx.draw_networkx_edges(g, pos, edgelist=path_edges, edge_color='r', width=15)
  
  
  # another example
  greater_than_770 = [x for x in G.edges(data=True) if x[2]['weight']>770]
  nx.draw_networkx_edges(G, pos, edgelist=greater_than_770, edge_color='r', alpha=0.4, width=6)


