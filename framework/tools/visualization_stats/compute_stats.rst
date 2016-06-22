.. _framework-tools-visualization-stats-stats:

==================
Compute statistics
==================


.. _framework-tools-visualization-stats-stats-correlation:

Correlation for numeric columns
===============================

This tool computes the matrix of correlation coefficients (Pearson's correlation, Kendall's rank correlation, Spearman's rank correlation) between numeric columns.

All invalid, blank and comment lines are skipped when performing computations. The number of skipped lines is displayed in the resulting history item.

.. _framework-tools-visualization-stats-stats-wilcox:

Compute Wilcoxon test with R
============================

This tool compute a Wilcoxon test with R's ``wilcox.test`` function.
