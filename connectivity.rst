Network Connectivity
====================


Clustering
----------------
Clustering coefficients measures the degree to which nodes in a network tend to cluster or form triangles.

Local Clustering Coefficient
*****************************
Find the clustering of a particular node.

# pairs of A's friends who are friends with each other / # all possible pairs of A's friends

.. code:: python

  # G is a graph, A is a node
  nx.clustering(G, 'A') 

Global Clustering Coefficient
*****************************

**Average clustering** of entire network by averaging all local clustering coefficient values of all nodes.

.. code:: python

  nx.average_clustering(G)
  
  
**Transitivity** is the ratio of number of triangles and number of “open triads”. 
Puts larger weight on high degree nodes.

.. code:: python

  nx.transitivity(G)
  
  
.. figure:: images/clustering.png
    :width: 600px
    :align: center
    :height: 100px
    :alt: alternate text
    :figclass: align-center

    From University of Michigan, Python for Data Science Coursera Specialization
    
    
Distance
---------

Shortest Path
**************
Shortest distance from a start node to the end node.

.. code:: python

  nx.shortest_path(G,'A', 'H')
  # ['A', 'B', 'C', 'E', 'H']
  
  nx.shortest_path_length(G,'A', 'H')
  # 4
  
  
Breadth First Search
*********************


.. code:: python

  T = nx.bfs_tree(G, 'A') 
  T.edges()
  # [('A', 'K'), ('A', 'B'), ('B', 'C'), ('C', 'E'), ('C', 'F'), ('E', 'I'), ('E', 'H'), ('E', 'D'), ('F', 'G'), ('I', 'J')]
  
  nx.shortest_path_length(G,'A')
  # {'A': 0, 'B': 1, 'C': 2, 'D': 4, 'E': 3, 'F': 3, 'G': 4, 'H': 4, 'I': 4, 'J': 5, 'K': 1}
  
.. figure:: images/breadthfirst.png
    :width: 200px
    :align: center
    :height: 100px
    :alt: alternate text
    :figclass: align-center

    From University of Michigan, Python for Data Science Coursera Specialization
  