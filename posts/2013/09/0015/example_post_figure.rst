 
How to publish a post with plots
#################################



:date: 2013-09-07 00:17:15
:category: HOW-TO 
:tags:  how-to
:author:	 Igor Marfin 





An Example of the posting a report on "Validation BTag HLT 2011 in RelVal53X" 
------------------------------------------------------------------------------


This is quite easy:

.. code:: bash

  relpath=yes; prepare_rst2pdf_template 2 "500:700" static/plots53x2011HLT/ png 8 "HLT BTAG 2011 MENU RelVal53x" > 06.09.13_marfin_2011legacyMenu.In53x.rst
  cd /mnt/WorkingPlace/myblog/pages/
  cp -r /mnt/WorkingPlace/presentation/06.09.13_TSG_meeting/static/plots53x2011HLT  posts/
  cp -r /mnt/WorkingPlace/presentation/06.09.13_TSG_meeting/06.09.13_marfin_2011legacyMenu.In53x.rst  .
  # fix header
  nano -w 06.09.13_marfin_2011legacyMenu.In53x.rst 
  # fix  add to STATIC_PATHS=["images","plots53x2011HLT"]
  nano -w local_settings.py
  nano -w short_local_settings.py
  _post=./posts/`date +%Y`/`date +%m`/`date +%H%M`
  mkdir -p  $_post
  cp 06.09.13_marfin_2011legacyMenu.In53x.rst $_post
  Changeword "image:: static" "image:: http://igormarfin.github.io/pages/static"  $_post/06.09.13_marfin_2011legacyMenu.In53x.rst $_post/06.09.13_marfin_2011legacyMenu.In53x.rst
  deploy_rst_blog  "local_settings.py" "Control plots of 2011 HLT RelVal53x study" "igormarfin" "pages"


I'll add a functionality to perform the steps above in the automatic way.





