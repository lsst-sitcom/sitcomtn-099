:tocdepth: 1

.. sectnum::

.. Metadata such as the title, authors, and description are set in metadata.yaml

.. TODO: Delete the note below before merging new content to the main branch.

.. note::

   **This technote is a work-in-progress.**


Abstract
========

.. _LVV-C248 : https://jira.lsstcorp.org/secure/Tests.jspa#/testCycle/LVV-C248 
.. _LVV-T1782: https://jira.lsstcorp.org/secure/Tests.jspa#/testPlayer/testExecution/LVV-E2601

This tech note reports the investigations on the M2 Cell :abbr:`RBM (Rigid Body Motion)` faults occurring at the TMA. During the execution of the Test Cycle `LVV-C248`_ many faults have been encountered under different :abbr:`RBM (Rigid Body Motion)` trajectories. This report summarizes the preliminary empirical findings collected during multiple testing sessions carried out in the following dates:

- Day1: 16 Nov 2023
 
  **4 faults**, tangent force error on A2, A3, A5, A6, surrogate handling LUT & TMA at Zenith


- Day2: 22 Nov 2023, 

  **2 faults**, tangent force limit on A3, A5, surrogate handling LUT & TMA at Horizon


- Day3: 23 Nov 2023,
  
  **No faults**, :abbr:`RBM (Rigid Body Motion)` along X and Y axes for +/- 50 micron, surrogate optical LUT & TMA at Zenith.


- Day4: 27 Nov 2023, 
  
  **No faults**, :abbr:`RBM (Rigid Body Motion)` along X and Y axes up to +/- 160 micron and along Z up +/- 1 mm, surrogate optical LUT & TMA at Zenith.


- Day5: 28 Nov 2023, 
  
  **No faults**, :abbr:`RBM (Rigid Body Motion)` along X and Y axes up to +/- 700 micron at steps of 50 micron, surrogate optical LUT & TMA at Zenith.


The previous execution of this test case (`LVV-T1782`_) was carried out at Level3 without encountering any fault during the :abbr:`RBM (Rigid Body Motion)` sequence until the limit switch position was hit. The nature of the failures encountered during the exection of this test at the TMA is still under investigation and this tech note provides an analysis of the tangent links' behaviours in terms of forces and related force errors for each of the testing windows listed above.


Failure context
================

.. _fault_ticket_OBS300 : https://jira.lsstcorp.org/browse/OBS-300

The most severe fault event (`fault_ticket_OBS300`_) was encountered on 16 Nov 2023 as shown in :ref:`Figure 1 <fig1>` and :ref:`Figure 2 <fig2>`.



.. image:: /_static/tangent_force_4fault.png
   :target: ../_images/tangent_force_4fault.png
   :alt: LSST Logo
.. _fig1:

   :ref:`Figure 1 <fig1>`. Screenshot from the Chronograph showing the jump of the A2, A3, A5, A6 tangent link force errors during the major fault. 




.. image:: /_static/Values_to_recover_from_the_second_fault.png
   :target: ../_images/Values_to_recover_from_the_second_fault.png
   :alt: LSST Logo
.. _fig2:

   :ref:`Figure 2 <fig2>`. Screenshot from M2 GUI showing the fault alarm triggered by the A2, A3, A5, A6 tangent link force errors. The fault occurred during a :abbr:`RBM (Rigid Body Motion)` homing procedure 266 micron away from the zero home position.


The recovery from the tangent force error fault Te-Wei Tsai had to enlarge the hard-coded values of the tangent force error threshold from 1000 N (original Harris value) to 2000 N (at the time of writing set threshold). 





Data Analysis Preliminary Results
=========================================

.. _tangent_force_error_math : https://confluence.lsstcorp.org/pages/viewpage.action?spaceKey=LTS&title=Tangent+Load+Cell+Fault+Detection


The most severe fault event (`tangent_force_error_math`_) was encountered on 



Add content here.
See the `reStructuredText Style Guide <https://developer.lsst.io/restructuredtext/style.html>`__ to learn how to create sections, links, images, tables, equations, and more.

.. Make in-text citations with: :cite:`bibkey`.
.. Uncomment to use citations
.. .. rubric:: References
.. 
.. .. bibliography:: local.bib lsstbib/books.bib lsstbib/lsst.bib lsstbib/lsst-dm.bib lsstbib/refs.bib lsstbib/refs_ads.bib
..    :style: lsst_aa
