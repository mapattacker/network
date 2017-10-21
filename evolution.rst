Evolution
==========

The degree of a node in an undirected graph is the number of neighbors it has.

The **degree distribution** of a graph is the probability distribution of the degrees over the entire network.

.. code:: python

  degrees = G.degree()
  degree_values = sorted(set(degrees.values()))
  histogram = [list(degrees.values()).count(i)/float(nx.number_of_nodes( G)) \
              for i in degree_values]

  import matplotlib.pyplot as plt

  plt.bar(degree_values,histogram)
  plt.xlabel('Degree')
  plt.ylabel('Fraction of Nodes')
  plt.show()


.. figure:: images/degreed.png
    :width: 400px
    :align: center
    :height: 100px
    :alt: alternate text
    :figclass: align-center

    From University of Michigan, Python for Data Science Coursera Specialization


Preferential Attachment Model
-----------------------------
The degree distribution of a graph is the probability distribution of the degrees over the entire network.

 • Many real networks have degree distributions that look like power laws (𝑃𝑘 =C𝑘^-a).
 • Models of network generation allow us to identify mechanisms that give rise to observed patterns in real data.
 • The Preferential Attachment Model produces networks with a power law degree distribution.

 .. figure:: images/degreed2.png
     :width: 600px
     :align: center
     :height: 100px
     :alt: alternate text
     :figclass: align-center

     From University of Michigan, Python for Data Science Coursera Specialization

``nx.barabasi_albert_graph(n, m)`` returns a network with n nodes.
Each new node attaches to m existing nodes according to the Preferential Attachment model.


.. code:: python

  G = nx.barabasi_albert_graph(1000000,1)
  degrees = G.degree()
  degree_values = sorted(set(degrees.values()))
  histogram = [list(degrees.values().count(i))/float(nx.number_of_node s(G)) \
                for i in degree_values]

  import matplotlib.pyplot as plt

  plt.plot(degree_values,histogram, 'o')
  plt.xlabel('Degree')
  plt.ylabel('Fraction of Nodes')
  plt.xscale('log')
  plt.yscale('log')
  plt.show()

Small World Model
------------------
Social networks tend to have high clustering coefficient and small average path length.

 • Start with a ring of 𝑛 nodes, where each node is connected to its 𝑘 nearest neighbors.
 • Fix a parameter 𝑝 ∈ [0,1]
 • Consider each edge 𝑢, 𝑣 . With probability 𝑝, select a node 𝑤 at random and rewire the edge (𝑢, 𝑣) so it becomes (𝑢, 𝑤).

.. code:: python

  G = nx.watts_strogatz_graph(1000,6,0.04)
  degrees = G.degree()
  degree_values = sorted(set(degrees.values()))
  histogram = [list(degrees.values()).count(i)/float(nx.number_of_node s(G)) \
                for i in degree_values]

  import matplotlib.pyplot as plt

  plt.bar(degree_values,histogram)
  plt.xlabel('Degree')
  plt.ylabel('Fraction of Nodes')
  plt.show()


Variants of the small world model in NetworkX:

• Small world networks can be disconnected, which is sometime undesirable.

``nx.connected_watts_strogatz_graph(n, k, p, t)`` runs watts_strogatz_graph(n, k, p) up to t times, 
until it returns a connected small world network.

• ``nx.newman_watts_strogatz_graph(n, k, p)`` runs a model similar to the small world model, 
but rather than rewiring edges, new edges are added with probability 𝑝.



