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
 
  **4 faults**, tangent force error on A2, A3, A5, A6, surrogate handling LUT & TMA at Zenith.


- Day2: 22 Nov 2023, 

  **2 faults**, tangent force limit on A3, A5, surrogate handling LUT & TMA at Horizon.


- Day3: 23 Nov 2023,
  
  **No faults**, :abbr:`RBM (Rigid Body Motion)` steps along X and Y axes for +/- 50 micron, surrogate optical LUT & TMA at Zenith.


- Day4: 27 Nov 2023, 
  
  **No faults**, :abbr:`RBM (Rigid Body Motion)` steps of variable amplitude up to +/- 160 micron along X and Y axes and along Z up +/- 1 mm, surrogate optical LUT & TMA at Zenith.


- Day5: 28 Nov 2023, 
  
  **No faults**, :abbr:`RBM (Rigid Body Motion)` along X and Y axes up to +/- 700 micron at steps of 50 micron, (no homing command) surrogate optical LUT & TMA at Zenith.


The previous execution of this test case (`LVV-T1782`_) was carried out at Level3 without encountering any fault during the :abbr:`RBM (Rigid Body Motion)` sequence until the limit switch position was hit. The nature of the failures encountered during the execution of the test at the TMA is still under investigation and this tech note provides an analysis of the tangent links' behaviors in terms of forces and related force errors for each of the testing windows listed above.


Failure context
================

.. _fault_ticket_OBS300 : https://jira.lsstcorp.org/browse/OBS-300

The most severe fault event (on Day1, `fault_ticket_OBS300`_) was encountered on 16 Nov 2023 as shown in :ref:`Figure 1 <fig1>` and :ref:`Figure 2 <fig2>`.



.. image:: /_static/tangent_force_4fault.png
   :target: ../_images/tangent_force_4fault.png
   :alt: LSST Logo
.. _fig1:

   :ref:`Figure 1 <fig1>`. Screenshot from the Chronograph showing the >1000 N jump of the A2, A3, A5, A6 tangent link force errors during the major fault. TMA at Zenith.
 


.. image:: /_static/Values_to_recover_from_the_second_fault.png
   :target: ../_images/Values_to_recover_from_the_second_fault.png
   :alt: LSST Logo
.. _fig2:

   :ref:`Figure 2 <fig2>`. Screenshot from M2 GUI showing the fault alarm (in red) triggered by the A2, A3, A5, A6 tangent link force errors. The fault occurred during a :abbr:`RBM (Rigid Body Motion)` homing procedure, 266 microns away from the zero home position. TMA at Zenith.


Given the TMA configuration (pointing at Zenith) and the simultaneous fault of 4 tangent links, the recovery from the tangent force error fault has required Te-Wei Tsai to enlarge the hard-coded LabView values of the tangent force error threshold from 1000 N (original Harris value) to 2000 N (current threshold). The second series of fault events (Day 2) occurred instead with the TMA pointing at the horizon and the alarm triggered was related to the maximum closed-loop force error from the A3 and A5 tangent links as reported in :ref:`Figure 3 <fig3>`. The recovery from this fault was achieved by enabling the open-loop max force limits and bringing back the two tangent links by manually commanding x100 steps sequence with the M2 GUI until their force limit lowered below the threshold of max force limit in closed-loop. An odd behavior encountered during the fault on Day 2, was a non-linear response to a commanded :abbr:`RBM (Rigid Body Motion)` step: we observed a jump of about 90 microns as a response to a 10-20 micron commanded step (`fault_ticket_OBS300`_).



.. image:: /_static/RBM_force_limit_errors.jpg
   :target: ../_images/RBM_force_limit_errors.jpg
   :alt: LSST Logo
.. _fig3:

   :ref:`Figure 3 <fig3>`. Screenshot from M2 GUI showing the fault alarm triggered by the A3, A5 tangent link closed-loop max force limit errors. The fault occurred during a :abbr:`RBM (Rigid Body Motion)` following commanded steps of 20 microns and 10 microns respectively at 177 microns and 87 microns away from the zero home position. TMA at the horizon.



Data Analysis Preliminary Results
=========================================

.. _tangent_force_error_math : https://confluence.lsstcorp.org/pages/viewpage.action?spaceKey=LTS&title=Tangent+Load+Cell+Fault+Detection


The most severe fault event (`tangent_force_error_math`_) was encountered during an homing position following a :abbr:`RBM (Rigid Body Motion)` sequence along the Y axis. From the data inspection, we could infer that the reason for the fault is the amplitude of the :abbr:`RBM (Rigid Body Motion)` step.




.. image:: /_static/movement_and_ferror_y.png
   :target: ../_images/movement_and_ferror_y.png
   :alt: LSST Logo
.. _fig4:

   :ref:`Figure 4 <fig4>`. RBM commands sequence along the Y axis (left y axis) and corresponding tangent link force errors (right y axis).



.. image:: /_static/movement_and_ferror_x.png
   :target: ../_images/movement_and_ferror_x.png
   :alt: LSST Logo
.. _fig5:

   :ref:`Figure 5 <fig5>`. RBM commands sequence along the X axis (left x axis) and corresponding tangent link force errors (right x axis).





See the `reStructuredText Style Guide <https://developer.lsst.io/restructuredtext/style.html>`__ to learn how to create sections, links, images, tables, equations, and more.

.. Make in-text citations with: :cite:`bibkey`.
.. Uncomment to use citations
.. .. rubric:: References
.. 
.. .. bibliography:: local.bib lsstbib/books.bib lsstbib/lsst.bib lsstbib/lsst-dm.bib lsstbib/refs.bib lsstbib/refs_ads.bib
..    :style: lsst_aa
