 
A sparse checkout in GIT
#########################



:date: 2013-09-05 11:43:47
:category: HOW-TO 
:tags:  how-to
:author:	 Igor Marfin 





Is there any way to clone a git repository's sub-directory only?
-----------------------------------------------------------------


Let's imagine that we have in a git repo which is  the root,  two a sub-dir



.. code:: bash


  elemoine/blog/content/cv/ 



Is there anyway to do checkout in one place only the sud-dir like so


.. code:: bash

    svn co svn+ssh://admin@domain.com/home/admin/repos/elemoine/blog/content/cv/ cv

The is called a sparse checkout, and that feature was added in git 1.7.0 (Feb. 2012). 
This idea was brought by 'Chronial' at stackoverflow.com_
The steps to do a sparse clone are as follows:


.. code:: bash

  git init my_cv
  cd my_cv
  git remote add -f origin https://github.com/elemoine/blog.git


This creates an empty repository with your remote. Then do:


.. code:: bash

   git config core.sparsecheckout true


Now you need to define which files/folders you want to actually check out. This is done by listing them in .git/info/sparse-checkout, eg:


.. code:: bash

  echo content/cv >> .git/info/sparse-checkout


Last but not least, update your empty repo with the state from the remote:


.. code:: bash


   git pull origin master




.. _stackoverflow.com: http://stackoverflow.com/questions/600079/is-there-any-way-to-clone-a-git-repositorys-sub-directory-only




