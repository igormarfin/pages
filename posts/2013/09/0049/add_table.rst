 
HOW TO add the table to a post
###############################



:date: 2013-09-07 00:51:56
:category: HOW-TO 
:tags:  how-to
:author:	 Igor Marfin 





An Example of use "utils.sh" API: function "Make_Table()"
----------------------------------------------------------


You can get a nice table, just call the fucntion ``Make_Table()``

.. code:: bash
   
   Make_Table  "Test of the table" test.tbl ascii > test.rst; rst2pdf test.rst


where the file ``test.tbl`` contains ::

   Algo Name ;  Eff. ; Err 
   BtagIP1 ; 0.89; +- 0.10 
   BtagIP2 ; 0.45; +- 0.11 
   BtagIP3 ; 0.64; +- 0.14 


The table is presented like 


                Test of the table


+-----------+---------+-----------+
|Algo Name  |   Eff.  |    Err    |
+-----------+---------+-----------+
| BtagIP1   |   0.89  |  +- 0.10  |
+-----------+---------+-----------+
| BtagIP2   |   0.45  |  +- 0.11  |
+-----------+---------+-----------+
| BtagIP3   |   0.64  |  +- 0.14  |
+-----------+---------+-----------+



Below there is the code of ``Make_Table`` extracted from ``utils.sh`` with a help a command:

.. code:: bash

   ExtractFunctionBody ~/utils.sh  Make_Table | awk '{print "   " $0}'



The code is 

.. code:: c

   Make_Table()
   {
   #Make_Table_begin_
   local help='
   #$1 header of table
   #
   #$2 file containing table in groff(tbl) format:
   #
   #    aa ;    bb ;    cc
   #    dd ;    vv ;    etc
   #
   #
   #
   #$3 -- type: ps or ascii
   '
   
   if [ $# -lt 3 ]; then print_help "$0" "$help"; return 1; fi
   
   
   #Define format! --> Maximal number of fields!
   
   #Initial max of NF:
   maxNF=`cat $2 | sed -n "1p" | awk -F';' "{print NF}"`;
   nl=`cat $2| wc -l`;
   

   for (( i=1; i<=$nl;i++ ))
   do
   
   curLine=`cat $2 | sed -ne "${i}p"`;
   
   
   curNF=`echo $curLine |  awk -F';' '{print NF}'`;
   cmpr=`echo "$maxNF > $curNF" | bc`;
   
   if [ $cmpr -eq 0 ] ; then maxNF=$curNF; fi 
   
   done
      
   echo '.TS
   allbox tab(;);' > tmp.file;
   for (( i=1; i<=$maxNF;i++ ))
   do
   echo -n "c" >> tmp.file;
   done
   echo  '.' >> tmp.file;
   cat $2 >> tmp.file;
   echo '.TE' >> tmp.file;

   
   
        echo "          $1      ";
   
   # tbl table.tbl | troff -Tascii | grotty 2>|/dev/null  | sed -e '/^$/d'
   if [  "$3" = 'ascii' ];
   then
   tbl tmp.file | troff -Tascii |  grotty 2>|/dev/null  | sed -e '/^$/d';
   fi;
   
   if [  "$3" = 'ps' ];
   then
   tbl tmp.file | troff -Tps |  grops 2>|/dev/null > $2.ps;
   fi;
   rm tmp.file;
   return 0;
   #Make_Table_end_
   }

