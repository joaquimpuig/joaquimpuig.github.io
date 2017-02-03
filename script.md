Importing the datafiles
-----------------------

To reproduce the analysis from the paper, you should download the files
from the website of Implementation Science
<https://implementationscience.biomedcentral.com/articles/10.1186/s13012-016-0522-3>.

The titles of the supplementary material may be confusing, but you
should download the file '13012\_2016\_522\_MOESM3\_ESM.graphml' which
is a format in the [GraphML language](http://graphml.graphdrawing.org/).
This is a very convenient format which supports vertex attributes. For
the sake of confientiality, the provided file only includes two boolean
attributes which are the vaccination status and whether the node was
vaccinated or not.

To analyse the network using the 'statnet' suite, it is necessary to use
the 'igraph' (to read 'graphml' files), 'intergraph' (to convert between
one and the other). We first load the network using the convenient
'igraph' facilities:

    library('igraph')

    ## 
    ## Attaching package: 'igraph'

    ## The following objects are masked from 'package:stats':
    ## 
    ##     decompose, spectrum

    ## The following object is masked from 'package:base':
    ## 
    ##     union

    net.igraph<-read_graph('13012_2016_522_MOESM3_ESM.graphml',format='graphml')

Next we want to convert the network in the 'igraph' format to the
'network' format (used by the 'statnet' suite). This is done with the
'integraph' package:

    library('intergraph')
    net<-asNetwork(net.igraph)

The network is now in the right format to use with 'statnet', and we
have kept vertex attributes:

    library('statnet')

    ## Loading required package: tergm

    ## Loading required package: statnet.common

    ## Loading required package: ergm

    ## Loading required package: network

    ## network: Classes for Relational Data
    ## Version 1.13.0 created on 2015-08-31.
    ## copyright (c) 2005, Carter T. Butts, University of California-Irvine
    ##                     Mark S. Handcock, University of California -- Los Angeles
    ##                     David R. Hunter, Penn State University
    ##                     Martina Morris, University of Washington
    ##                     Skye Bender-deMoll, University of Washington
    ##  For citation information, type citation("network").
    ##  Type help("network-package") to get started.

    ## 
    ## Attaching package: 'network'

    ## The following objects are masked from 'package:igraph':
    ## 
    ##     add.edges, add.vertices, %c%, delete.edges, delete.vertices,
    ##     get.edge.attribute, get.edges, get.vertex.attribute,
    ##     is.bipartite, is.directed, list.edge.attributes,
    ##     list.vertex.attributes, %s%, set.edge.attribute,
    ##     set.vertex.attribute

    ## 
    ## ergm: version 3.6.0, created on 2016-03-24
    ## Copyright (c) 2016, Mark S. Handcock, University of California -- Los Angeles
    ##                     David R. Hunter, Penn State University
    ##                     Carter T. Butts, University of California -- Irvine
    ##                     Steven M. Goodreau, University of Washington
    ##                     Pavel N. Krivitsky, University of Wollongong
    ##                     Martina Morris, University of Washington
    ##                     with contributions from
    ##                     Li Wang
    ##                     Kirk Li, University of Washington
    ##                     Skye Bender-deMoll, University of Washington
    ## Based on "statnet" project software (statnet.org).
    ## For license and citation information see statnet.org/attribution
    ## or type citation("ergm").

    ## NOTE: If you use custom ERGM terms based on 'ergm.userterms'
    ## version prior to 3.1, you will need to perform a one-time update
    ## of the package boilerplate files (the files that you did not write
    ## or modify) from 'ergm.userterms' 3.1 or later. See
    ## help('eut-upgrade') for instructions.

    ## Loading required package: networkDynamic

    ## 
    ## networkDynamic: version 0.9.0, created on 2016-01-12
    ## Copyright (c) 2016, Carter T. Butts, University of California -- Irvine
    ##                     Ayn Leslie-Cook, University of Washington
    ##                     Pavel N. Krivitsky, University of Wollongong
    ##                     Skye Bender-deMoll, University of Washington
    ##                     with contributions from
    ##                     Zack Almquist, University of California -- Irvine
    ##                     David R. Hunter, Penn State University
    ##                     Li Wang
    ##                     Kirk Li, University of Washington
    ##                     Steven M. Goodreau, University of Washington
    ##                     Jeffrey Horner
    ##                     Martina Morris, University of Washington
    ## Based on "statnet" project software (statnet.org).
    ## For license and citation information see statnet.org/attribution
    ## or type citation("networkDynamic").

    ## 
    ## tergm: version 3.4.0, created on 2016-03-28
    ## Copyright (c) 2016, Pavel N. Krivitsky, University of Wollongong
    ##                     Mark S. Handcock, University of California -- Los Angeles
    ##                     with contributions from
    ##                     David R. Hunter, Penn State University
    ##                     Steven M. Goodreau, University of Washington
    ##                     Martina Morris, University of Washington
    ##                     Nicole Bohme Carnegie, New York University
    ##                     Carter T. Butts, University of California -- Irvine
    ##                     Ayn Leslie-Cook, University of Washington
    ##                     Skye Bender-deMoll
    ##                     Li Wang
    ##                     Kirk Li, University of Washington
    ## Based on "statnet" project software (statnet.org).
    ## For license and citation information see statnet.org/attribution
    ## or type citation("tergm").

    ## Loading required package: ergm.count

    ## 
    ## ergm.count: version 3.2.2, created on 2016-03-29
    ## Copyright (c) 2016, Pavel N. Krivitsky, University of Wollongong
    ##                     with contributions from
    ##                     Mark S. Handcock, University of California -- Los Angeles
    ##                     David R. Hunter, Penn State University
    ## Based on "statnet" project software (statnet.org).
    ## For license and citation information see statnet.org/attribution
    ## or type citation("ergm.count").

    ## NOTE: The form of the term 'CMP' has been changed in version 3.2
    ## of 'ergm.count'. See the news or help('CMP') for more information.

    ## Loading required package: sna

    ## sna: Tools for Social Network Analysis
    ## Version 2.4 created on 2016-07-23.
    ## copyright (c) 2005, Carter T. Butts, University of California-Irvine
    ##  For citation information, type citation("sna").
    ##  Type help(package="sna") to get started.

    ## 
    ## Attaching package: 'sna'

    ## The following objects are masked from 'package:igraph':
    ## 
    ##     betweenness, bonpow, closeness, components, degree,
    ##     dyad.census, evcent, hierarchy, is.connected, neighborhood,
    ##     triad.census

    ## 
    ## statnet: version 2016.4, created on 2016-03-23
    ## Copyright (c) 2016, Mark S. Handcock, University of California -- Los Angeles
    ##                     David R. Hunter, Penn State University
    ##                     Carter T. Butts, University of California -- Irvine
    ##                     Steven M. Goodreau, University of Washington
    ##                     Pavel N. Krivitsky, University of Wollongong
    ##                     Skye Bender-deMoll
    ##                     Martina Morris, University of Washington
    ## Based on "statnet" project software (statnet.org).
    ## For license and citation information see statnet.org/attribution
    ## or type citation("statnet").

    ## unable to reach CRAN

    list.vertex.attributes(net)

    ## [1] "id"           "interview"    "na"           "vaccinated"  
    ## [5] "vertex.names"

which we can check computing the mixing matrix of HCWs by vaccination
status:

    mixingmatrix(net,'vaccinated')

    ##        To
    ## From    FALSE TRUE Total
    ##   FALSE   165  117   282
    ##   TRUE    104   80   184
    ##   Total   269  197   466

or perfom an ERGM analysis like in the paper:

    model1<-ergm(net~edges+nodematch('vaccinated')+mutual+nodeifactor('vaccinated'))

    ## Starting maximum likelihood estimation via MCMLE:
    ## Iteration 1 of at most 20: 
    ## The log-likelihood improved by 0.2811 
    ## Step length converged once. Increasing MCMC sample size.
    ## Iteration 2 of at most 20: 
    ## The log-likelihood improved by 0.4629 
    ## Step length converged twice. Stopping.
    ## Evaluating log-likelihood at the estimate. Using 20 bridges: 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 .
    ## 
    ## This model was fit using MCMC.  To examine model diagnostics and check for degeneracy, use the mcmc.diagnostics() function.

    summary(model1)

    ## 
    ## ==========================
    ## Summary of model fit
    ## ==========================
    ## 
    ## Formula:   net ~ edges + nodematch("vaccinated") + mutual + nodeifactor("vaccinated")
    ## 
    ## Iterations:  2 out of 20 
    ## 
    ## Monte Carlo MLE Results:
    ##                             Estimate Std. Error MCMC % p-value    
    ## edges                       -5.91650    0.08977      0  <1e-04 ***
    ## nodematch.vaccinated         0.02654    0.08905      0  0.7657    
    ## mutual                       4.71401    0.18687      0  <1e-04 ***
    ## nodeifactor.vaccinated.TRUE  0.29572    0.10245      0  0.0039 ** 
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ##      Null Deviance: 160727  on 115940  degrees of freedom
    ##  Residual Deviance:   5690  on 115936  degrees of freedom
    ##  
    ## AIC: 5698    BIC: 5736    (Smaller is better.)

We end with a plot of the network with nodes colored according to the
vaccination status (black: vaccinated, red: unvaccinated).

    gplot(net, vertex.col = 1+as.integer(as.logical(net %v% "interview")))

![](script_files/figure-markdown_strict/unnamed-chunk-6-1.png)
