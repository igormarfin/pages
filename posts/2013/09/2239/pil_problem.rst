 
Install python PIL ( Python image Library )
############################################



:date: 2013-09-06 22:41:19
:category: HOW-TO 
:tags:  how-to
:author:	 Igor Marfin 





It helped me to fix a problem with PIL
---------------------------------------

I've taken ideas from `http://obroll.com/install-python-pil-python-image-library-on-ubuntu-11-10-oneiric/`_\ .
First, uninstall current PIL:

.. code:: bash

   sudo pip uninstall PIL

Then install jpeglib, freetypes


.. code:: bash

   sudo apt-get install libjpeg8 libjpeg62-dev libfreetype6 libfreetype6-dev

We should fix path libraries needed by PIL as :


.. code:: bash

  sudo ln -s /usr/lib/i386-linux-gnu/libjpeg.so /usr/lib
  sudo ln -s /usr/lib/i386-linux-gnu/libfreetype.so /usr/lib
  sudo ln -s /usr/lib/i386-linux-gnu/libz.so /usr/lib


Now we are ready installing PIL by :

.. code:: bash

   sudo pip install -U PIL


.. _`http://obroll.com/install-python-pil-python-image-library-on-ubuntu-11-10-oneiric/`: http://obroll.com/install-python-pil-python-image-library-on-ubuntu-11-10-oneiric/




