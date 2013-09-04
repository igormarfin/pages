 
HOW-TO deploy the Pelican Blog
###############################



:date: 2013-09-04 23:37:47
:category: HOW-TO 
:tags:  how-to
:author:	 Igor Marfin 





All steps
----------


Just repeate all steps below:

.. code:: bash

  sudo apt-get install git
  git config credential.helper store
  sudo pip install pelican
  mkdir myweb; cd myweb;
  git clone --recursive https://github.com/getpelican/pelican-themes/ themes/

  #if need, ini repository 
  touch README.md
  git init 
  git pull origin master
  git add README.md
  git commit -m "first commit"
  git push git@github.com:igormarfin/pages master
  #if no, just clone
  git clone https://github.com/igormarfin/pages.git
  cd pages/
  source ~/utils.sh
  cp -r /mnt/WorkingPlace/myweb/themes/ .
  create_config_rst_blog  "Igor Marfin" "Igor Marfin's home page" "http://igormarfin.github.com/pages" "iggy.floyd.de@gmal.comNOTSPAM"
  mkdir -p  ./posts/`date +%Y`/`date +%m`
  add_rst_blog "Igor Marfin" "About me" "no-tags" "About me" "Example of the pelican use" > posts/`date +%Y`/`date +%m`/about_me2.rst
  pelican posts/ -s ./short_local_settings.py
  firefox output/index.html
  deploy_rst_blog  "local_settings.py" "My first post" "igormarfin" "pages"


That's it.





