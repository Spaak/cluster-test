# Cluster Test

[![DOI](https://zenodo.org/badge/777739144.svg)](https://zenodo.org/doi/10.5281/zenodo.10877824)

Cluster-based permutation testing in arbitrary dimensions, in a simple Matlab script.

Note: requires Matlab imaging processing toolbox (`bwconncomp` function, specifically). This is available on most Matlab installations.

Main file (usable by itself) is `cluster_test.m`, with an optional helper `cluster_test_helper.m`. Docs are in those files.

From `cluster_test.m`:
```
% CLUSTER_TEST performs a cluster-corrected test that datobs is higher/lower
% than the distribution as expected under the null hypothesis. The 'null'
% distribution should be pre-computed (manually or using CLUSTER_TEST_HELPER)
% and entered as an argument into this function.
%
% datobs - observed data MxNx...xZ
% datrnd - null distribution, MxNx...xZxPerm
% tail - whether to test datobs < null (tail==-1), datobs > null (tail==1)
% or datobs <> null (tail==0, default).
% alpha - critical level (default 0.05)
% clusteralpha - nonparametric threshold for cluster candidates (default
% 0.05)
% clusterstat - how to combine statistics in cluster candidates (can be
% 'sum' (default) or 'size')
%
% Returns:
% h - MxNx...xZ logical matrix indicating where significant clusters were
% found (though note that formally speaking the test concerns the data as a
% whole, so the interpretation of the location of clusters within h should
% be done with caution).
% p - MxNx...xZ matrix of p-values associated with clusters.
% clusterinfo - struct with extra cluster info, e.g. indices
%
% Written by Eelke Spaak, Oxford University, June 2015.
```

From `cluster_test_helper.m`:
```
% CLUSTER_TEST_HELPER is a helper function for doing cluster-corrected
% permutation tests in arbitrary dimensions. The randomizations are
% generated under the assumption that input dat was computed using a paired
% statistic T for which T(a,b) = -T(b,a) holds, where a and b are the data
% under the two paired conditions. (E.g. raw difference would work.)
%
% dat - an NxMx...xZxObs data matrix. The trailing dimension must correspond
% to the unit of observation (e.g., subjects or trials).
%
% nperm - the number of permutations to generate
%
% diffstat - how to compute the 'difference statistic'. Can be 'diff'
% (default) or 't' (compute one-sample t-score).
%
% Returns:
% datobs - NxMx...xZ statistic for observed data, averaged across observations
% datrnd - NxMx...xZxPerm statistic under the null hypothesis
%
% Written by Eelke Spaak, Oxford University, June 2015.
```
