.. _routines.array-creation:

Array creation routines
=======================

.. seealso:: :ref:`Array creation <arrays.creation>`

.. currentmodule:: mxnet.np

Ones and zeros
--------------
.. autosummary::
   :toctree: generated/

   ones
   ones_like
   zeros
   zeros_like

.. code::

   full
   full_like
   identity
   empty
   empty_like
   eye

From existing data
------------------
.. autosummary::
   :toctree: generated/

   array
   copy

.. code::

   asarray
   asanyarray
   ascontiguousarray
   asmatrix
   frombuffer
   fromfile
   fromfunction
   fromiter
   fromstring
   loadtxt

.. _routines.array-creation.rec:

Creating record arrays (:mod:`np.rec`)
-----------------------------------------

.. note:: :mod:`np.rec` is the preferred alias for
   :mod:`np.core.records`.

.. autosummary::
   :toctree: generated/

.. code::

   core.records.array
   core.records.fromarrays
   core.records.fromrecords
   core.records.fromstring
   core.records.fromfile

.. _routines.array-creation.char:

Creating character arrays (:mod:`np.char`)
---------------------------------------------

.. note:: :mod:`np.char` is the preferred alias for
   :mod:`np.core.defchararray`.

.. autosummary::
   :toctree: generated/

.. code::

   core.defchararray.array
   core.defchararray.asarray

Numerical ranges
----------------
.. autosummary::
   :toctree: generated/

   arange

.. code::

   linspace
   logspace
   geomspace
   meshgrid
   mgrid
   ogrid

Building matrices
-----------------
.. autosummary::
   :toctree: generated/

.. code::

   diag
   diagflat
   tri
   tril
   triu
   vander

The Matrix class
----------------
.. autosummary::
   :toctree: generated/

::

   mat
   bmat
