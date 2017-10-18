Influence Measures and Network Centralization
===============================================

Centrality and other measures identify the most important nodes in a network.


Degree Centrality
-------------------
Assumption: Important nodes have many connections.

**Undirected networks**: Use degree.

𝐶𝑣 = d𝑣/(𝑁 - 1)
where 𝑁 is total number of nodes. Minus 1 to remove node in question
𝑑 is the degree of node 𝑣.

.. code:: python

  degCent = nx.degree_centrality(G)
  # gives a dictionary. key = node, value = centrality ratio
  degCent[34]
  .. 0.515 # 17/33

**Directed networks**: use in-degree or out-degree


.. code:: python

  # in-degree centrality
  indegCent = nx.in_degree_centrality(G) 
  indegCent[‘A’]
  
  # out-degree centrality
  indegCent = nx.out_degree_centrality(G) 
  indegCent[‘A’]
  

Closeness Centrality
---------------------
Assumption: important nodes are close to other nodes. 
It is calculated by (total number of nodes that node N can reach) - sum(shortest path of node N).

.. figure:: images/closeness_centrality.png
    :width: 400px
    :align: center
    :height: 100px
    :alt: alternate text
    :figclass: align-center

    From University of Michigan, Python for Data Science Coursera Specialization
    
    
.. code:: python

  closeCent =nx.closeness_centrality(G) 
  closeCent[32]
  .. 0.541
  
  # Manual calculation
  sum(nx.shortest_path_length(G,32).values()) 
  .. 61
  (len(G.nodes())-1)/61.
  .. 0.541
  
  
Normalisation (multiply a constant i.e., total # nodes in graph) is required for directed graphs, 
as node in question may only reach a few nodes in the entire graph.

.. code:: python

  nx.closeness_centrality(G, normalized= True)
  closeCent[‘L’]
  .. 0.071
  
  
  
Betweenness Centrality
----------------------
Assumption: important nodes connect other nodes.



Basic Page Rank
---------------

Scaled Page Rank
----------------


Hubs & Authorities
-------------------
