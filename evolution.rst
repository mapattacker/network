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
    :width: 600px
    :align: center
    :height: 100px
    :alt: alternate text
    :figclass: align-center

    From University of Michigan, Python for Data Science Coursera Specialization
  
Preferential Attachment
------------------------
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

