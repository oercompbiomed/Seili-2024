---
title: Investigating the protein-protein network
layout: single
permalink: /training/stringapp/
sidebar:
  nav: "training-stringapp"
---
## Origin of material

Most more these exercises has been adopted from [the StringApp exercises](https://jensenlab.org/training/stringapp/) made by Nadezhda T Doncheva and Lars J Jensen.

## Learning objectives

In these exercises, we will use the [stringApp](http://apps.cytoscape.org/apps/stringApp) for [Cytoscape](http://cytoscape.org/) to retrieve molecular networks from the [STRING](https://string-db.org/) database. The exercises will teach you how to:

* retrieve networks for proteins of interest
* retrieve networks for a disease
* layout and visually style the resulting networks
* import external data and map them onto a network
* perform enrichment analyses and visualize the results
* merge and compare networks
* select proteins by attributes
* identify functional modules through network clustering

## Prerequisites

To follow the exercises, please make sure that you have the latest version of Cytoscape installed. Then start Cytoscape and update the current apps if necessary by checking the **App Updates** icon in the right-most corner of the manubar. 

The exercises require you to have certain Cytoscape apps installed. Go to the [Cytoscape App Store](https://apps.cytoscape.org/) in your web browser and search for [stringApp](http://apps.cytoscape.org/apps/stringApp), select the app and press the **Install** button to install it. Similarly, make sure you have the [yFiles Layout Algorithms](https://apps.cytoscape.org/apps/yfileslayoutalgorithms) and [clusterMaker2](https://apps.cytoscape.org/apps/clustermaker2) apps installed before switching back to Cytoscape.

If you are not already familiar with the STRING database, we highly recommend that you go through the short [STRING exercises](https://jensenlab.org/training/string/) to learn about the underlying data before working with it in these exercises.

## Exercise 1: Basics


In this exercise, we will perform some simple queries to retrieve molecular networks based on a protein, a small-molecule compound, a disease, and a topic in PubMed.

### 1.1 Protein queries

Go to the menu **File → Import → Network from Public Databases**. In the import dialog, choose **STRING: protein query** as **Data Source** and type your favorite protein into the **Enter protein names or identifiers** field (e.g. one or more of the potential biomarkers GLO1, HGD, PSMB6 and PRX1 for 2,3,7,8-Tetrachlorodibenzodioxi, see [paper](https://www.sciencedirect.com/science/article/abs/pii/S1570963916300310)). You can select the appropriate organism by typing the name (e.g. Homo sapiens). The **Maximum number of interactors** determines how many interaction partners of your protein(s) of interest will be added to the network. By default, if you enter only one protein name, the resulting network will contain 10 additional interactors. If you enter more than one protein name, the network will contain only the interactions among these proteins, unless you explicitly ask for additional proteins.

Unless the name(s) you entered give unambiguous matches, a disambiguation dialog will be shown next. It lists all the matches that the stringApp finds for each ambiguous query term and selects the first one for each. Select the right one(s) you meant and continue by pressing the **Import** button.


_<u>Questions:</u>_  
_How many nodes are in the resulting network?_  
_How does this compare to the maximum number of interactors you specified?_  
_What types of information do the **Node** and **Edge Table** provide?_  

### 1.2 Compound queries

Go to the menu **File → Import → Network from Public Databases**. In the import dialog, choose **STITCH: protein/compound query** as **Data Source** and type your favorite compound into the **Enter protein or compound names or identifiers** field (e.g. dioxin). You can select the organism and number of additional interactors just like for the protein query above, and the disambiguation dialog also works the same way.

_<u>Question:</u>_  
_How is this network different from the protein-only network with respect to node types and the information provided in the **Node Table**?_

### 1.3 Disease queries

Go to the menu **File → Import → Network from Public Databases**. In the import dialog, choose **STRING: disease query** as **Data Source** and type a disease of interest into the **Enter disease term** field (e.g. liver disease). The stringApp will retrieve a STRING network for the top-N proteins (by default 100) associated with the disease.

The next dialog shows all the matches that the stringApp finds for your disease query and selects the first one. Make sure to select the intended disease before pressing the **Import** button to continue.

_<u>Question:</u>_  
_Which additional attribute column do you get in the **Node Table** for a disease query compared to a protein query? Hint: check the last column._

### 1.4 PubMed queries

Go to the menu **File → Import → Network from Public Databases**. In the import dialog, choose **STRING: PubMed query** as **Data Source** and type query representing a topic of interest into the **PubMed Query** field (e.g. dioxin poisoning). You can use any query that would work on the PubMed website, but it should obviously a topic with related genes or proteins. The stringApp will query PubMed for the abstracts, find the top-N proteins (by default 100) associated with these abstracts, and retrieve a STRING network for them.

_<u>Question:</u>_  
_Which attribute column do you get in the **Node Table** for a PubMed query compared to a disease query? Hint: check the last columns._

### 1.5 Using the Cytoscape Search bar

The types of queries described above can alternatively be performed through the Cytoscape Search bar (located at the top of the **Network** panel in the **Control Panel**). Click on the drop-down menu with an icon for the different resources. Select one of the four possible STRING queries and directly enter your query in the text field. To change settings such as organism, click the ☰ button next to the text field. Finally, click the 🔍 button to retrieve a STRING network for your query.

## Exercise 2: Continuing Your Main Investigation

In this exercise, we will work with the obtained tables for the significant transcription factors. Find them [here](TODO) in case you want to start with the original data.

### 2.1 Protein network retrieval

Close the current session in Cytoscape from the menu **File → Close**. 
TODO: Take on of the files and open it. You can choose how many of the most significant regulators you want to include (e.g. all with a p-value below 0.05).

Go to the menu **File → Import → Network from Public Databases**. In the import dialog, choose **STRING: protein query** as the **Data Source** and paste the list of gene names of the regulators in the table (column `factor`) into the **Enter protein names or identifiers** field. Make sure that the option **maximum additional interactors** is set to **0** before pressing the **Import** button. 

Next, the disambiguation dialog might show all query terms that cannot be matched to a unique STRING protein, with the first matching STRING protein for each query term automatically selected. This default is fine for this exercise; click the **Import** button to continue. Check that **View → Always Show Graphics Details** for a detailed view of the network.

_<u>Questions:</u>_  
_How many nodes and edges are there in the resulting network?_  
_Do most of the proteins form a connected network? Why?_

Cytoscape provides several layout options under the **Layout** menu. Try the **Degree Sorted Circle Layout** and the **yFiles Organic Layout**. Check also one of the Cytoscape force-directed layouts, **Prefuse Force Directed Layout** or **Edge-weighted Spring Embedded Layout** with the attribute ‘score’ as edge weight (this is the combined STRING interaction score).

_<u>Question:</u>_  
_Do any of the suggested layouts help you to recognize patterns in the network? In which way?_

### 2.2 Discrete color mapping

Cytoscape allows you to map attributes of the nodes and edges to visual properties such as node color and edge width. Here, we will map drug target family data from the [Pharos](https://pharos.nih.gov/idg/targets) database to the node color. This data is contained in the node attribute called **target family**.

Select **Style** from the side menu in the left panel (it is between **Network** and **Filter**). Click the **◀** button to the right of the property you want to change, in this case **Fill Color**, and change **Column** from name to **(T) family**, which is the node column containing the data that you want to use. The **Mapping Type** should remain set to **Discrete Mapping**. This action will remove the rainbow coloring of the nodes and present you with a list of all the different values of the attribute that exist in the network, in this case several protein target families.

To color the proteins in a given target family, first click the field to the **right** of an attribute value, i.e. **GPCR** or **Ion channel**, then click the ⋯ button and choose a color from the color selection dialog. You can also set the default color for all nodes that do not have a target family annotation from Pharos by clicking on the **grey square** in the first column of the **Fill Color** row. Alternatively and preferably, select all categories and press the right mouse button to color all of them via **Mapping Value Generators**.

_<u>Question:</u>_  
_How many of the proteins in the network are enzymes?_

As expected, there are many transcription factors in the network. We can avoid counting them manually by creating a selection filter in the **Filter** tab (located underneath **Style**). Click the **ᐩ** button and choose **Column filter** from the drop-down menu. Then, find and select the attribute **(T) Node: family**. Write **transcription factor** in the text field to select all nodes with this annotation.

_<u>Question:</u>_  
_How many transcription factors are in the network?_

### 2.3 Data import

Network nodes and edges can have additional information associated with them that we can load into Cytoscape and use for visualization. We will import the data from the original file with gene names. Before doing that, add a new column `lpval` to the data file that contains the logarithmic values of `pval` (base 10).

To import the node attributes file into Cytoscape, go to **File → Import → Table from File** and navigate to the directory that contains the table file. In the resulting dialog entitled Import Columns From Table, use the drop-down menu next to **Where to Import Table Data** to choose the option **To a Network Collection**. Next, change the **Key Column for Network** from **shared name** to **query term** and click **OK**.

<details>
<summary><em>Detailed explanation: Understanding Cytoscape's data import</em></summary>

<p>The preview in the bottom of the import dialog will show how the file is interpreted given the current settings and will update automatically when you change them. To change the default interpretation of a column, click the arrow in its column heading. For example, you can decide whether the column is imported or not by changing the <strong>Meaning</strong> of the column (hover over each symbol with the mouse to see what they mean). This column-specific dialog will also allow you to change the column name and type.</p>

<p>Another important part is that you need to map unique identifiers between the entries in the data and the nodes in the network. The key point of this is to identify which nodes in the network are equivalent to which entries in the table. This enables mapping of data values into visual properties like Fill Color and Shape. This kind of mapping is typically done by comparing the unique identifier for each node (Key Column for Network) with the unique identifier for each data row in the table (marked with key symbol).</p>

<p>The <strong>Key Column for Network</strong> can be changed using a drop-down menu and allows you to set the node attribute column that is to be used as key to map to. In this case it is <strong>query term</strong> because this attribute contains the gene names you entered when retrieving the network. You can also change the Key by pressing the key button for the column that is to be used as key for mapping values in the dataset.</p>

<p>If there is a match between the value of a Key in the dataset and the value the Key Column for Network field in the network, all attribute–value pairs associated with the element in the dataset are assigned to the matching node in the network. You will find the imported columns at the end of the Node Table.</p>
</details>

### 2.4 Continuous color mapping

Now, we want to color the nodes according to the logarithmic p-values from the Lisa analysis. From the left panel side menu, select **Style** (it is underneath **Network**). Then click on the **◀** button to the right of the property you want to change, for example **Border Paint** (here you need to set to default value of **Border Width** to e.g. 10). Next, set **Column** to the node column containing the data that you want to use (lpval). Since this is a numeric value, we will use the **Continuous Mapping** as the **Mapping Type**, and set a color gradient for how abundant each protein is. The default Cytoscape color gradient already gives a nice visualization of the significance.

_<u>Questions:</u>_  
_Are the most significant nodes grouped together?_  
_Do you see any issues with the color gradient when using the original `pval` values?_

To change the colors, double click on the color gradient in order to bring up the **Continuous Mapping Editor** window and edit the colors for the continuous mapping. In the mapping editor dialog, the color that will be used for the minimum value is on the left, and the maximum is on the right. Double click on the triangles on the top and sides of the gradient to change the colors. The triangles on the top represent the values at which the data will be clipped; anything above the right triangle will be set to the max value. This is useful if you have a small number of values that are significantly higher than the median. As you move the triangles and change the color, the display in the network pane will automatically update -- this is all easier to do than to explain! If at any point it does not seem to work as expected, it is easiest to just delete the mapping and start again.

_<u>Question:</u>_  
_Can you improve the color mapping such that it is easier to see which nodes have a p-value below 0.001?_

### 2.5 Save session

To keep all the networks, data, and visualizations you created, you can save them as a Cytoscape session and open them at a later time point. Go to **File → Save**, choose where to save the file, give it a proper name and click the **Save** button.

## Exercise 3: Retrieving a subgroup of relevant interactors

In this exercise, we will focus on clustering, a common network analysis task, as well as functional enrichment within the Cytoscape stringApp environment.

### 3.1 Network clustering

Starting from the network in Exercise 2, we will use the MCL algorithm to identify clusters of tightly connected proteins within the network. To do that, press the **Cluster network (MCL)** button in the **STRING Results panel** on the right side of the network view. Keep the default **granularity parameter (inflation value)** set to **4** and click **OK** to start the clustering. The clusterMaker app will now run the algorithm and automatically create a network showing the clusters.

_<u>Question:</u>_  
_How many clusters have at least 10 nodes?_

<details>
<summary><em>Alternative instructions for clustering</em></summary>

<p>Go to the menu <b>Apps → clusterMaker → ClusterMaker Cluster Network → MCL Cluster</b>>. Set the <b>Granularity parameter (inflation value)</b> to 4 and choose the <b>stringdb::score</b> attribute (i.e. the overall STRING confidence score) as <b>Array Sources</b>, select the option <b>Create new clustered network</b>, and click OK to start the clustering. The app will now run the algorithm and automatically create a network showing the clusters.</p>
</details>

### 3.2 Subnetworks and physical interactions

We will work with the largest cluster in the network (it should be in the upper left corner). Select the nodes of this cluster by holding down the modifier key (Shift on Windows, Ctrl or Command on Mac) and then left-clicking and dragging to select multiple nodes. The nodes will turn yellow if they are selected properly. Then, create a new network by clicking on the **New Network from Selection** button and choosing the option **From Selected Nodes, All Edges** or via the menu item **File → New Network → From Selected Nodes, All Edges**.

_<u>Question:</u>_    
_How many nodes and edges are there in this cluster?_

The cluster is very dense and almost fully connected, i.e. it has edges representing functional associations between almost all pairs of nodes. Change the network type to physical interactions by navigating to the **Edges tab** in the **STRING Results panel** and clicking the **Change network type** button. Leave the confidence cutoff at the default value, change the network type from **full STRING network** to **physical subnetwork** using the drop-down menu, and click **OK**. To better see the new set of edges, apply a layout of your choosing, e.g. the **yFiles Organic Layout**.

_<u>Question:</u>_   
_How many edges does the resulting network contain and why are there now fewer edges?_

### 3.3 Functional enrichment

Next, we will retrieve functional enrichment for the proteins in our network of the largest cluster. After making sure that no nodes are selected in the network, go to the menu **Apps → STRING Enrichment → Retrieve functional enrichment** or use the **Functional Enrichment** button in the **Nodes tab** of the **STRING Panel** on the right side. Then, select the original, not clustered network ‘String Network’ as **Background** (instead of ‘genome’) and click **OK**. A new **STRING Enrichment tab** will appear in the **Table Panel** on the bottom. It contains a table of enriched terms and corresponding information for each enrichment category. You can see which proteins are annotated with a given term by selecting the term in the **STRING Enrichment panel** and you can see the terms annotating a given node by selecting it. You should find many of the expected terms, such as _DNA binding_.

_<u>Question:</u>_   
_How many statistically significant terms are in the table? Which is the most significant term for each of the categories GO Biological Process, GO Molecular Function, and KEGG Pathways? Hint: Look at the FDR (false discovery rate) value column and use the **Filter** button to select individual categories._

<!-- To explore only specific types of terms, e.g. GO terms, and to remove redundant terms from the table, click on the filter icon in the **Table panel** (leftmost icon). Select the three types of GO terms, enable the option to **Remove redundant terms** and set **Redundancy cutoff** to 0.2. In this way, you will see only the statistically significant GO terms that do not represent largely the same set of proteins within the network. You can see which proteins are annotated with a given term by selecting the term in the **STRING Enrichment** panel.
-->

Next, we will visualize the top-5 enriched terms in the network using split charts, click the colorful chart icon to show the terms as the charts on the network. You can manually change the layout of the network to improve the visualization. First apply the **yFiles Organic Layout** and then scale the network to reduce the overlap of the charts using the **Layout Tools (Layout → Layout Tools**).

To save the list of enriched terms and associated p-values as a text file, go to **Apps → STRING Enrichment → Export enrichment results**.

You can investigate the other cluster to learn more about e.g. their biological functions.

<!--### 3.4 Enriched publications

To retrieve a list of publications that are enriched for the proteins in the network, go to the menu **Apps → STRING Enrichment → Retrieve enriched publications** or press the **Enriched Publications** button. A new tab called **STRING Publications** will appear in the **Table Panel** on the bottom. It contains a table of enriched publications and associated information such as how many of the network proteins were mentioned in each publication.

_What is the title of the most recent publication?_-->

## Exercise 4 (optional): Predicting Protein Structures

In this exercise, we are going to focus on a small subset of proteins to investigate their structure with [AlphaFold 3](https://alphafoldserver.com).

### 4.1 Extracting Subnetwork

We take the first cluster and filter for the proteins with the lowest p-values. Open the **Filter** tab and click the **ᐩ** button and choose **Column filter** from the drop-down menu. Then, find and select the attribute **(pval**. Click on the **Show** button below to show only the filtered proteins. Then take an upper threshold of 0.0001 to keep only the very significant regulators. 

Save a picture of the network (**File → Export → Export to Image ...**)

_<u>Question:</u>_   
_Which are the most connected proteins (only physical interactions)?_  

### 4.2 Predicting Protein Dimers

Take two examples for interacting proteins from the given network. You can also take a pair or supposedly non-interacting proteins. Then open [AlphaFold 3](https://alphafoldserver.com) in a browser.

Find the protein sequences in Uniprot. For that, search the gene name in [UniProt](https://www.uniprot.org/uniprot), and select the protein from the right species. Go to **Sequence & Isoforms** to see the sequence. Then find the small button **Copy sequence** in the box containing the protein sequence.

In the AlphaFold interface, select protein as molecule type before pasting the protein sequence. Then click on **Add entity** to add another protein sequence. Save the results and try to understand what they mean.

_<u>Questions:</u>_   
_Why don't we predict the structures of single proteins? (Check the Uniprot entry again)_  
_Note what you not about the respective positions of the proteins._



## Supporting lectures

The theoretical background for these exercises is covered in these short online lectures:

[![STRING](training_string.png)](https://youtu.be/o208DwyFbNk)
[![Cytoscape](training_cytoscape.png)](https://youtu.be/Ohf9IPUJ82w)
[![stringApp](training_stringapp.png)](https://youtu.be/MXmzXxNqmnI)
[![stringApp tutorial](training_stringapp_tutorial.png)](https://youtu.be/kRQyPDMF_8k)
[![DISEASES](training_diseases.png)](https://youtu.be/xkYixhO2CJQ)
[![Enrichment analysis](training_enrichment_analysis.png)](https://youtu.be/2NC1QOXmc5o)
[![stringApp enrichment analysis](training_stringapp_enrichment_analysis.png)](https://youtu.be/AUEyZw-iJHg)

## Supporting literature

Doncheva NT, Morris JH, Gorodkin J and Jensen LJ (2019). Cytoscape stringApp: Network analysis and visualization of proteomics data. *Journal of Proteome Research*, **18**:623-632.  
[Abstract](https://www.ncbi.nlm.nih.gov/pubmed/30450911) [Full text](https://doi.org/10.1021/acs.jproteome.8b00702) [Preprint](https://doi.org/10.1101/358283)

[![CC BY 4.0](https://i.creativecommons.org/l/by/4.0/88x31.png)](https://creativecommons.org/licenses/by/4.0/)
