# kPAR
Realtime Top-k Personalized PageRank over Large Graphs on GPUs PVLDB2020

### NOTE: please click Releases and download kPAR.zip to get the code with dblp dataset.

Please cite our papers if you choose to use our code.

```
@article{DBLP:journals/pvldb/ShiYJXY19,
  author    = {Jieming Shi and
               Renchi Yang and
               Tianyuan Jin and
               Xiaokui Xiao and
               Yin Yang},
  title     = {Realtime Top-k Personalized PageRank over Large Graphs on GPUs},
  journal   = {PVLDB},
  volume    = {13},
  number    = {1},
  pages     = {15--28},
  year      = {2019}
}
```


### Environment:

	Ubuntu 16.04.12
	gcc 5.4.0
	Cuda 10.0.130
	Tesla P100 16GB or K80 11GB: driver version 410.79

### Directory (use dblp as an example):
	kPAR
		src -- source codes
		data
			dblp
				graph.txt -- edge list of the graph
				attribute.txt -- number of nodes and edges
				queries.txt -- randomly generated queries
				dblp.PRoverDegRank -- nodes ranked by PR/Deg
				result -- result directory of top-k output


### Build:
cd src/
make clean
make

### Run (use dblp as an example):
	build index:
		./kpar indexing --dataset dblp --epsilon 0.5
	run query:
		./kpar query --gpu_idx 0 --dataset dblp --query_size 50 --epsilon 0.5 --k 100

### Switch of GPUs (e.g., from K80 to P100):
	1. in src/Makefile, comment out CFLAGS += -gencode arch=compute_35,code=sm_35 and uncomment #CFLAGS += -gencode arch=compute_60,code=sm_60 
	2. in src/util/config.h comment out const size_t TOTAL_THREADS_GPU = 2048 * 13 and uncomment //const size_t TOTAL_THREADS_GPU = 2048 * 56
