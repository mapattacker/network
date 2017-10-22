Prediction
===========

Node Attribute
---------------

Predict node attributes based on centrality properties.

First, parse all the data into a dataframe so that sklearn package can be used.
Centrality metrics are also calculated and parsed.

.. code:: python

  # Your Code Here
  df = pd.DataFrame(index=G.nodes())
  df['dept'] = pd.Series(nx.get_node_attributes(G, 'Department'))
  df['mgmtsalary'] = pd.Series(nx.get_node_attributes(G, 'ManagementSalary'))
  df['deg'] = pd.Series(nx.degree_centrality(G))
  df['btw'] = pd.Series(nx.betweenness_centrality(G))
  df['close'] = pd.Series(nx.closeness_centrality(G))
  df['cluster'] = pd.Series(nx.clustering(G))

  # split train sets
  dftrain = df[df['mgmtsalary'].notnull()]
  X = dftrain[['dept', 'deg', 'btw', 'close', 'cluster']]
  y = dftrain['mgmtsalary']

  # split test sets    
  dftest = df[df['mgmtsalary'].isnull()]
  test = dftest[['dept', 'deg', 'btw', 'close', 'cluster']]

Then, data is split and analysed using logistic regression within a Grid Search. 
An AUC score of 0.94 is obtained.
  
.. code:: python
  
  from sklearn.model_selection import train_test_split
  from sklearn.linear_model import LogisticRegression
  from sklearn.model_selection import GridSearchCV
  from sklearn.preprocessing import MinMaxScaler

  X_train, X_test, y_train, y_test = train_test_split(X, y, random_state=0)

  # Normalisation
  scaler = MinMaxScaler()
  X_train = scaler.fit_transform(X_train)
  X_test = scaler.transform(X_test)
  test = scaler.transform(test)

  clf = LogisticRegression()
  # range of regularisation values
  grid_values = {'C': [100, 110, 120, 122, 125, 140, 150, 200, 250, 300, 320, 350, 400, 420]}
  grid_clf_auc = GridSearchCV(clf, param_grid = grid_values, scoring = 'roc_auc', cv=3)
  grid_clf_auc.fit(X_train, y_train)

  print('Grid best parameter (max. AUC): ', grid_clf_auc.best_params_)
  print('Grid best score (AUC): ', grid_clf_auc.best_score_)

  # Grid best parameter (max. AUC):  {'C': 400}
  # Grid best score (AUC):  0.936997156006

After determining the best C value, with a reasonable AUC score,
will pass this to the final test data which has unknown y-value.

.. code:: python

  from sklearn.linear_model import LogisticRegression
  from sklearn.preprocessing import MinMaxScaler

  def salary_predictions():

      # node attributes to dataframe
      df = pd.DataFrame(index=G.nodes())
      df['dept'] = pd.Series(nx.get_node_attributes(G, 'Department'))
      df['mgmtsalary'] = pd.Series(nx.get_node_attributes(G, 'ManagementSalary'))
      # 4 centrality measures
      df['deg'] = pd.Series(nx.degree_centrality(G))
      df['btw'] = pd.Series(nx.betweenness_centrality(G))
      df['close'] = pd.Series(nx.closeness_centrality(G))
      df['cluster'] = pd.Series(nx.clustering(G))
      
      # split train sets
      dftrain = df[df['mgmtsalary'].notnull()]
      X = dftrain[['dept', 'deg', 'btw', 'close', 'cluster']]
      y = dftrain['mgmtsalary']
      
      # split test sets    
      dftest = df[df['mgmtsalary'].isnull()]
      test = dftest[['dept', 'deg', 'btw', 'close', 'cluster']]
      
      # Normalisation
      scaler = MinMaxScaler()
      X = scaler.fit_transform(X)
      test = scaler.transform(test)
      
      # create model
      clf = LogisticRegression(C=400)
      clf.fit(X, y)
      
      # predict test
      result = clf.predict_proba(test)
      output = pd.Series(result[:,1], index=dftest.index)
      
      return output
    
    
Future Edge Linkage
----------------------

The dataset provides a list of future linkages and ask to provide prediction for others
which have not been given.

First, parse all the data into a dataframe so that sklearn package can be used.
Link metrics are also calculated.

.. code:: python

  fc['prefa'] = [i[2] for i in nx.preferential_attachment(G, fc.index)]
  fc['cneigh'] = fc.index.map(lambda x: len(list(nx.common_neighbors(G, x[0], x[1]))))

  # split train sets
  fctrain = fc[fc['Future Connection'].notnull()]
  X = fctrain[['prefa', 'cneigh']]
  y = fctrain['Future Connection']

  # split test sets    
  fctest = fc[fc['Future Connection'].isnull()]
  test = fctest[['prefa', 'cneigh']]

Then, data is split and analysed using logistic regression within a Grid Search. 
An AUC score of 0.91 is obtained.


.. code:: python

  from sklearn.model_selection import train_test_split
  from sklearn.linear_model import LogisticRegression
  from sklearn.model_selection import GridSearchCV
  from sklearn.preprocessing import MinMaxScaler

  X_train, X_test, y_train, y_test = train_test_split(X, y, random_state=0)

  # Normalisation
  scaler = MinMaxScaler()
  X_train = scaler.fit_transform(X_train)
  X_test = scaler.transform(X_test)
  test = scaler.transform(test)

  clf = LogisticRegression()
  grid_values = {'C': [1, 10, 20, 30, 40, 50, 100, 110, 120, 122, 125, 140, 150]}
  grid_clf_auc = GridSearchCV(clf, param_grid = grid_values, scoring = 'roc_auc', cv=3)
  grid_clf_auc.fit(X_train, y_train)

  print('Grid best parameter (max. AUC): ', grid_clf_auc.best_params_)
  print('Grid best score (AUC): ', grid_clf_auc.best_score_)
  
  # Grid best parameter (max. AUC):  {'C': 10}
  # Grid best score (AUC):  0.905822220111



After determining the best C value, with a reasonable AUC score,
will pass this to the final test data which has unknown y-value.

.. code:: python

  from sklearn.linear_model import LogisticRegression
  from sklearn.preprocessing import MinMaxScaler

  def new_connections_predictions():
      
      # add edge attributes
      fc['prefa'] = [i[2] for i in nx.preferential_attachment(G, fc.index)]
      fc['cneigh'] = fc.index.map(lambda x: len(list(nx.common_neighbors(G, x[0], x[1]))))

      # split train sets
      fctrain = fc[fc['Future Connection'].notnull()]
      X = fctrain[['prefa', 'cneigh']]
      y = fctrain['Future Connection']

      # split test sets    
      fctest = fc[fc['Future Connection'].isnull()]
      test = fctest[['prefa', 'cneigh']]
      
      # Normalisation
      scaler = MinMaxScaler()
      X = scaler.fit_transform(X)
      test = scaler.transform(test)
      
      # build model
      clf = LogisticRegression(C=10)
      clf.fit(X, y)
      
      # predict
      result = clf.predict_proba(test)
      output = pd.Series(result[:,1], index=fctest.index)
      
      return output