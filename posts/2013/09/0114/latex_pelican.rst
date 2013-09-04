 
Latex formulas in Pelican?
###########################



:date: 2013-09-05 01:18:39
:category: HOW-TO 
:tags:  Latex, Mathjax, formula, mathmode
:author:	 Igor Marfin 





How to setup Mathjax properly
------------------------------

I've taken a solution from the  Hans Frangohr's blog_

..  _blog : http://www.southampton.ac.uk/~fangohr/blog/setting-up-pelican-how-to-make-equations-work.html


To be able to use equations in the static Pelican Blog generator, the key is to include a code snippet like

.. code:: html

  <!-- Using MathJax, with the delimiters $ -->
  <!-- Conflict with pygments for the .mo and .mi -->
  <script type="text/x-mathjax-config">
  MathJax.Hub.Config({
  "HTML-CSS": {
  styles: {
  ".MathJax .mo, .MathJax .mi": {color: "black ! important"}}
  },
  tex2jax: {inlineMath: [['$','$'], ['\\\\(','\\\\)']],processEscapes: true}
  });
  </script>

  <script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS_HTML"></script>
  </head>


in the template/base.html theme file (just before the <body> section.). I put it to my default theme template:

.. code :: bash

   nano -w themes/tuxlite_tbs/templates/base.html # fix head in base.html



That's it.


