# EvolNET

The project presents a possible approach to visualizing the evolution of social networks. The action flow contains of the following:
* Creating a networkx graph from the dataset including a _year_ label for each edge
* Performing community detection based on the graph structure using the Greedy Modularity Communities algorithm (alternatively the Girvan-Newman or any other community detection algorithm may be used here). Community membership determines further coloring of each node
* For each year _Y_:
    * extracting a subgraph _S_ containing the edges labeled with _year <= Y_
    * obtaining 32-dim embeddings for all nodes of _S_ using the [node2vec](https://arxiv.org/abs/1607.00653?context=cs) algorithm
    * dimensionality reduction from 32 to 2 dimensions based on [UMAP](https://arxiv.org/abs/1802.03426) in order to obtain x and y coordinates for each node from _S_
    * visualizing all nodes of S using the obtained coordinates and precomputed community-related coloring

The visualisation is based on the [bloomberg/bqplot](https://github.com/bloomberg/bqplot) project.

### Set up
##### Package requirements
All required packages are listed in _req.txt_ file. You can create an identical conda environment by executing:

```conda create -n your_env_name --file req.txt```
##### Enabling Jupyter extensions
In order to enable the required notebook extensions, run:

```jupyter nbextension enable --py widgetsnbextension```

### Dataset
I use a [DBLP](https://dblp.uni-trier.de/) Computer Science citation dataset. If you want to use the same dataset, please download _DBLP-citation-Jan8.tar.bz2_ from [here]( https://aminer.org/lab-datasets/citation/). Extract it and place the _DBLP-citation-Jan8.txt_ file in the main folder.
Next, open the _parser.ipynb_ notebook and run all the cells. It will produce _dblp_nodes.csv_ and _dblp_edges.csv_ files representing the graph structure of the dataset. The attached notebook persists only articles written by top 100 publishing authors and having no less than 10 citations. You can adjust these parameters in the notebook.

In order to use any other dataset, you should create your own parser and adjust the main scrip accordingly. 


#### TODO
[-] dynamicly adjust node2vec embedding size according to the graph size

