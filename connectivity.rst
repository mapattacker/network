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
    :width: 400px
    :align: center
    :height: 100px
    :alt: alternate text
    :figclass: align-center

    From University of Michigan, Python for Data Science Coursera Specialization