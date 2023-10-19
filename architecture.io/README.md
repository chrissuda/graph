# Architecture_diagrams

This repository contains system diagrams in graphviz dot format. For more about graphviz see https://graphviz.org/

There are two files to illustrate the site facing flow and the non-site facing call flows. Please edit site_facing.gv or non_site_facing.gv files to update the call graphs.

Visualizing the graph
---------------------
The files in graphviz format can be visualized using the graphviz clients suggested on the site. We have leverage couple of open source libraries to be able to visualize the graphs in a web browser. The following libraries have been used for the same.

* https://github.com/mountainstorm/jquery.graphviz.svg
* https://github.com/hpcc-systems/hpcc-js-wasm#graphviz

Key constructs

Graphviz supports the following shapes https://graphviz.org/doc/info/shapes.html. We plan to use the following for shapes

`circle` for a node
`cylinder` for a data store
`Msquare` for async queues

```
OMS_Prod [shape="Msquare"]
```

From a edge perspective regular solid lines represent sync call. For a flows move from sync to async, use `dashed` line to illustrate the same.

```
OMS_Prod -> OMS_Cons[style="dashed"];
```

For illustrating logical clusters we plan to leverage subgraphs to group nodes into a cluster. For example, for UI, we are grouping pages into a logical cluster as shown below

```
  subgraph cluster_android {
    style=filled;
    color=lightgrey;
    node [style=filled,color=white];
    and_Home [label="Home"]
    and_Search [label="Search"]
    and_Item [label="Item"]
    and_Cart [label="Cart"]
    and_Acc [label="My Acc"]
    label = "Droid App";
  }
```
Custom Attributes
-----------------
We plan to add additional documentation to the nodes via custom attributes that have a prefix of `wm_`. 

`wm_feature`
Its a comma-separated list to indicate if the node has changes related to a feature. The below nodes indicate that IRO has changes for marketplace and ads, while rollups has changes for marketplace only.

```
  IRO [wm_feature="marketplace,ads"]
  Rollups [ wm_feature="marketplace"]
```

Running visualization locally
-----------------------------
Once you have made changes to the gv files, you can start a web server with the current directory as the home directory and access sf.html or nsf.html pages

Easy way to launch a web server on mac on port 8000, run the following python command from the directory of this repo.
`python -m SimpleHTTPServer 8000` or python3 - 'python -m http.server 8000'
This will start a webserbver on port 8000 and you can access the following urls to look at site_facing and non_site_facing call graphs.

* http://localhost:8000/sf.html
* http://localhost:8000/nsf.html

Sharing link to visualization
------------------------------
The following repo has been enabled for git pages. The following git pages links can be shared to visualize the graphs once they have been checked in and merged to master.

* https://gecgithub01.walmart.com/pages/r0choud/architecture.io/sf.html
* https://gecgithub01.walmart.com/pages/r0choud/architecture.io/nfs.html  -> Not ready 


Contributing
------------
* Fork the repository and make changes to the following files
  * `site_facing.gv` for site facing flows
  * `non_site_facing.gv` for non site facing flows
* If there are new flows that fall outside of the two, create a new file for the directed graph.
* Create a PR for merging the changes back


