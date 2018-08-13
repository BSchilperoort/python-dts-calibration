
2. Define calibration sections
==============================

.. code:: ipython3

    import os
    import glob
    
    from dtscalibration import read_xml_dir


.. parsed-literal::

    /Users/bfdestombe/PycharmProjects/dts-calibration/python-dts-calibration/.tox/docs/lib/python3.6/importlib/_bootstrap.py:219: RuntimeWarning: numpy.dtype size changed, may indicate binary incompatibility. Expected 96, got 88
      return f(*args, **kwds)


.. code:: ipython3

    try:
        wd = os.path.dirname(os.path.realpath(__file__))
    except:
        wd = os.getcwd()
    
    filepath = os.path.join(wd, '..', '..', 'tests', 'data', 'double_ended')
    timezone_netcdf = 'UTC',
    timezone_ultima_xml = 'Europe/Amsterdam'
    file_ext = '*.xml'
    
    ds = read_xml_dir(filepath,
                      timezone_netcdf=timezone_netcdf,
                      timezone_ultima_xml=timezone_ultima_xml,
                      file_ext=file_ext)


.. parsed-literal::

    3 files were found, each representing a single timestep
    6 recorded vars were found: LAF, ST, AST, REV-ST, REV-AST, TMP
    Recorded at 2330 points along the cable
    processing file 1 out of 3


A calibration is needed to estimate temperature from Stokes and
anti-Stokes measurements. There are three unknowns for a single ended
calibration procedure :math:`\gamma`, :math:`C`, and :math:`\alpha`. The
parameters :math:`\gamma` and :math:`\alpha` remain constant over time,
while :math:`C` may vary.

At least two calibration sections of different temperatures are needed
to perform a decent calibration procedure.

+------------+------------------------------+----------------+--------------------+
| Name       | Name reference temperature   | Number of      | Location of        |
| section    | time series                  | sections       | sections (m)       |
+============+==============================+================+====================+
| Cold bath  | probe1Temperature            | 2              | 7.5-17.0;          |
|            |                              |                | 70.0-80.0          |
+------------+------------------------------+----------------+--------------------+
| Warm bath  | probe2Temperature            | 2              | 24.0-34.0;         |
|            |                              |                | 85.0-95.0          |
+------------+------------------------------+----------------+--------------------+

Each section requires a reference temperature time series, such as the
temperature measured by an external temperature sensor. They should
already be part of the DataStore object.

Sections are defined in a dictionary with its keywords of the names of
the reference temperature time series. Its values are lists of slice
objects, where each slice object is a section.

Note that slice is part of the standard Python library and no import is
required.

.. code:: ipython3

    sections = {
        'probe1Temperature': [slice(7.5, 17.), slice(70., 80.)],  # cold bath
        'probe2Temperature': [slice(24., 34.), slice(85., 95.)],  # warm bath
        }
    ds.sections = sections

.. code:: ipython3

    ds.sections




.. parsed-literal::

    {'probe1Temperature': [slice(7.5, 17.0, None), slice(70.0, 80.0, None)],
     'probe2Temperature': [slice(24.0, 34.0, None), slice(85.0, 95.0, None)]}



NetCDF files do not support reading/writing python dictionaries.
Internally the sections dictionary is stored in ``ds._sections`` as a
string encoded with yaml, which can be saved to a netCDF file. Each time
the sections dictionary is requested, yaml decodes the string and
evaluates it to the Python dictionary.