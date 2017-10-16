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

  nx.shortest_path(G, 'A', 'H')
  # ['A', 'B', 'C', 'E', 'H']
  
  nx.shortest_path_length(G, 'A', 'H')
  # 4
  
  
Breadth First Search
*********************
Find the distance from one node to all other nodes.

One method is the Breadth First Search, which is a systematic and efficient procedure for computing distances 
from a node to all other nodes in a large network by “discovering” nodes in layers.

.. code:: python

  T = nx.bfs_tree(G, 'A') 
  T.edges()
  # [('A', 'K'), ('A', 'B'), ('B', 'C'), ('C', 'E'), ('C', 'F'), ('E', 'I'), ('E', 'H'), ('E', 'D'), ('F', 'G'), ('I', 'J')]
  
  nx.shortest_path_length(G, 'A')
  # {'A': 0, 'B': 1, 'C': 2, 'D': 4, 'E': 3, 'F': 3, 'G': 4, 'H': 4, 'I': 4, 'J': 5, 'K': 1}
  
.. .. figure:: images/breadthfirst.png
..     :width: 400px
..     :align: center
..     :height: 100px
..     :alt: alternate text
..     :figclass: align-center
.. 
..     From University of Michigan, Python for Data Science Coursera Specialization
  
  
Distance Measures
*****************

**Average Distance** between every pair of nodes.

.. code:: python

  nx.average_shortest_path_length(G)
  # 2.52727272727

**Diameter** maximum distance between any pair of nodes.

.. code:: python

  nx.diameter(G)
  # 5

**Eccentricity** of a node n is the largest distance between n and all other nodes.

.. code:: python

  nx.eccentricity(G)
  # {'A': 5, 'B': 4, 'C': 3, 'D': 4, 'E': 3, 'F': 3, 'G': 4, 'H': 4, 'I': 4, 'J': 5, 'K': 5}  


**Radius** of a graph is the minimum eccentricity.

.. code:: python

  nx.radius(G)
  # 3
  

**Periphery** of a graph is the set of nodes that have eccentricity equal to the diameter.

.. code:: python

  nx.periphery(G)
  # ['A', 'K', 'J']


**Center** of a graph is the set of nodes that have eccentricity equal to the radius.

.. code:: python

  nx.center(G)
  # ['C', 'E', 'F']
  
  
