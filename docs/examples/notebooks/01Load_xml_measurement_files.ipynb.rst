
1. Load your first measurement files
====================================

This notebook is located in
https://github.com/bdestombe/python-dts-calibration/tree/master/examples/notebooks

.. code:: ipython3

    import os
    import glob
    
    from dtscalibration import read_xml_dir

The data files are located in ``./python-dts-calibration/tests/data``

.. code:: ipython3

    try:
        # this file is excecuted as script
        wd = os.path.dirname(os.path.realpath(__file__))
        
    except:
        # Excecuted from console. pwd = ./docs
        wd = os.getcwd()
    
    filepath = os.path.join(wd, '..', '..', 'tests', 'data', 'double_ended2')
    print(filepath)


.. parsed-literal::

    /Users/bfdestombe/Projects/dts-calibration/python-dts-calibration/examples/notebooks/../../tests/data/double_ended2


.. code:: ipython3

    timezone_netcdf = 'UTC',
    timezone_ultima_xml = 'Europe/Amsterdam'
    file_ext = '*.xml'

.. code:: ipython3

    # Just to show which files are in the folder
    filepathlist = sorted(glob.glob(os.path.join(filepath, file_ext)))
    filenamelist = [os.path.basename(path) for path in filepathlist]
    
    for fn in filenamelist:
        print(fn)


.. parsed-literal::

    channel 1_20180328014052498.xml
    channel 1_20180328014057119.xml
    channel 1_20180328014101652.xml
    channel 1_20180328014106243.xml
    channel 1_20180328014110917.xml
    channel 1_20180328014115480.xml


.. code:: ipython3

    ds = read_xml_dir(filepath,
                      timezone_netcdf=timezone_netcdf,
                      timezone_ultima_xml=timezone_ultima_xml,
                      file_ext=file_ext)


.. parsed-literal::

    6 files were found, each representing a single timestep
    6 recorded vars were found: LAF, ST, AST, REV-ST, REV-AST, TMP
    Recorded at 1693 points along the cable
    Dask: Setting up handle for delayed readout. 1 out of 6
    Dask: Setting up handle for delayed readout. 6 out of 6
    Directly reading time and extra info from xml files. 1 out of 6
    Directly reading time and extra info from xml files. 6 out of 6


.. code:: ipython3

    print(ds)


.. parsed-literal::

    <xarray.DataStore>
    Dimensions:                (time: 6, x: 1693)
    Coordinates:
      * x                      (x) float32 -80.5043 -80.3772 ... 134.421 134.548
        filename               (time) <U31 'channel 1_20180328014052498.xml' ... 'channel 1_20180328014115480.xml'
        timeFWstart            (time) datetime64[ns] 2018-03-27T22:40:52.097000 ... 2018-03-27T22:41:15.061000
        timeFWend              (time) datetime64[ns] 2018-03-27T22:40:54.097000 ... 2018-03-27T22:41:17.061000
        timeFW                 (time) datetime64[ns] 2018-03-27T22:40:53.097000 ... 2018-03-27T22:41:16.061000
        timeBWstart            (time) datetime64[ns] 2018-03-27T22:40:54.097000 ... 2018-03-27T22:41:17.061000
        timeBWend              (time) datetime64[ns] 2018-03-27T22:40:56.097000 ... 2018-03-27T22:41:19.061000
        timeBW                 (time) datetime64[ns] 2018-03-27T22:40:55.097000 ... 2018-03-27T22:41:18.061000
        timestart              (time) datetime64[ns] 2018-03-27T22:40:52.097000 ... 2018-03-27T22:41:15.061000
        timeend                (time) datetime64[ns] 2018-03-27T22:40:56.097000 ... 2018-03-27T22:41:19.061000
      * time                   (time) datetime64[ns] 2018-03-27T22:40:54.097000 ... 2018-03-27T22:41:17.061000
    Data variables:
        ST                     (x, time) float32 dask.array<shape=(1693, 6), chunksize=(1693, 1)>
        AST                    (x, time) float32 dask.array<shape=(1693, 6), chunksize=(1693, 1)>
        REV-ST                 (x, time) float32 dask.array<shape=(1693, 6), chunksize=(1693, 1)>
        REV-AST                (x, time) float32 dask.array<shape=(1693, 6), chunksize=(1693, 1)>
        TMP                    (x, time) float32 dask.array<shape=(1693, 6), chunksize=(1693, 1)>
        acquisitionTime        (time) float64 2.098 2.075 2.076 2.133 2.085 2.062
        referenceTemperature   (time) float64 21.05 21.05 21.05 21.05 21.05 21.06
        probe1Temperature      (time) float64 4.361 4.36 4.359 4.36 4.36 4.361
        probe2Temperature      (time) float64 18.58 18.58 18.58 18.58 18.58 18.57
        referenceProbeVoltage  (time) float64 0.1217 0.1217 0.1217 ... 0.1217 0.1217
        probe1Voltage          (time) float64 0.114 0.114 0.114 0.114 0.114 0.114
        probe2Voltage          (time) float64 0.121 0.121 0.121 0.121 0.121 0.121
        userAcquisitionTimeFW  (time) float64 2.0 2.0 2.0 2.0 2.0 2.0
        userAcquisitionTimeBW  (time) float64 2.0 2.0 2.0 2.0 2.0 2.0
    Attributes:
        uid:                                                                     ...
        nameWell:                                                                ...
        nameWellbore:                                                            ...
        name:                                                                    ...
        indexType:                                                               ...
        startIndex:uom:                                                          ...
        startIndex:#text:                                                        ...
        endIndex:uom:                                                            ...
        endIndex:#text:                                                          ...
        stepIncrement:uom:                                                       ...
        stepIncrement:#text:                                                     ...
        startDateTimeIndex:                                                      ...
        endDateTimeIndex:                                                        ...
        direction:                                                               ...
        indexCurve:                                                              ...
        logCurveInfo_0:uid:                                                      ...
        logCurveInfo_0:mnemonic:                                                 ...
        logCurveInfo_0:classWitsml:                                              ...
        logCurveInfo_0:unit:                                                     ...
        logCurveInfo_0:curveDescription:                                         ...
        logCurveInfo_0:typeLogData:                                              ...
        logCurveInfo_1:uid:                                                      ...
        logCurveInfo_1:mnemonic:                                                 ...
        logCurveInfo_1:classWitsml:                                              ...
        logCurveInfo_1:curveDescription:                                         ...
        logCurveInfo_1:typeLogData:                                              ...
        logCurveInfo_2:uid:                                                      ...
        logCurveInfo_2:mnemonic:                                                 ...
        logCurveInfo_2:classWitsml:                                              ...
        logCurveInfo_2:curveDescription:                                         ...
        logCurveInfo_2:typeLogData:                                              ...
        logCurveInfo_3:uid:                                                      ...
        logCurveInfo_3:mnemonic:                                                 ...
        logCurveInfo_3:classWitsml:                                              ...
        logCurveInfo_3:curveDescription:                                         ...
        logCurveInfo_3:typeLogData:                                              ...
        logCurveInfo_4:uid:                                                      ...
        logCurveInfo_4:mnemonic:                                                 ...
        logCurveInfo_4:classWitsml:                                              ...
        logCurveInfo_4:curveDescription:                                         ...
        logCurveInfo_4:typeLogData:                                              ...
        logCurveInfo_5:uid:                                                      ...
        logCurveInfo_5:mnemonic:                                                 ...
        logCurveInfo_5:classWitsml:                                              ...
        logCurveInfo_5:unit:                                                     ...
        logCurveInfo_5:curveDescription:                                         ...
        logCurveInfo_5:typeLogData:                                              ...
        logData:mnemonicList:                                                    ...
        logData:unitList:                                                        ...
        customData:acquisitionTime:                                              ...
        customData:referenceTemperature:uom:                                     ...
        customData:referenceTemperature:#text:                                   ...
        customData:probe1Temperature:uom:                                        ...
        customData:probe1Temperature:#text:                                      ...
        customData:probe2Temperature:uom:                                        ...
        customData:probe2Temperature:#text:                                      ...
        customData:forwardMeasurementChannel:                                    ...
        customData:forwardSignalAverages:                                        ...
        customData:referenceProbeVoltage:                                        ...
        customData:probe1Voltage:                                                ...
        customData:probe2Voltage:                                                ...
        customData:fibreStatusOk:                                                ...
        customData:fibreBreakLocation:                                           ...
        customData:isDoubleEnded:                                                ...
        customData:reverseMeasurementChannel:                                    ...
        customData:reverseSignalAverages:                                        ...
        customData:measurementStatus:                                            ...
        customData:SystemSettings:softwareVersion:                               ...
        customData:SystemSettings:DAQSettings:Card:                              ...
        customData:SystemSettings:DAQSettings:MinimumRecordLength:               ...
        customData:SystemSettings:DAQSettings:MaximumRecordLength:               ...
        customData:SystemSettings:DAQSettings:PreTriggerSamples:                 ...
        customData:SystemSettings:DAQSettings:TriggerInDirection:                ...
        customData:SystemSettings:DAQSettings:TriggerMode:                       ...
        customData:SystemSettings:DAQSettings:TriggerRateDividerFactor:          ...
        customData:SystemSettings:DAQSettings:ReferenceClockDirection:           ...
        customData:SystemSettings:DAQSettings:ClockSource:                       ...
        customData:SystemSettings:HardwareSettings:UltimaSerialNumber:           ...
        customData:SystemSettings:HardwareSettings:DigitalLine_0:Name:           ...
        customData:SystemSettings:HardwareSettings:DigitalLine_0:DataArray:      ...
        customData:SystemSettings:HardwareSettings:DigitalLine_1:Name:           ...
        customData:SystemSettings:HardwareSettings:DigitalLine_1:DataArray:      ...
        customData:SystemSettings:HardwareSettings:DigitalLine_2:Name:           ...
        customData:SystemSettings:HardwareSettings:DigitalLine_2:DataArray:      ...
        customData:SystemSettings:HardwareSettings:DigitalLine_3:Name:           ...
        customData:SystemSettings:HardwareSettings:DigitalLine_3:DataArray:      ...
        customData:SystemSettings:HardwareSettings:NumberOfChannels:             ...
        customData:SystemSettings:LaserSettings:LaserIsControlled:               ...
        customData:SystemSettings:LaserSettings:LaserWarmupTime:                 ...
        customData:SystemSettings:LaserSettings:LaserCoolDownTime:               ...
        customData:SystemSettings:LaserSettings:DigitalLine_0:Name:              ...
        customData:SystemSettings:LaserSettings:DigitalLine_0:DataArray:         ...
        customData:SystemSettings:LaserSettings:DigitalLine_1:Name:              ...
        customData:SystemSettings:LaserSettings:DigitalLine_1:DataArray:         ...
        customData:SystemSettings:LaserSettings:DigitalLine_2:Name:              ...
        customData:SystemSettings:LaserSettings:DigitalLine_2:DataArray:         ...
        customData:SystemSettings:LaserSettings:MinimumPulseWidth:               ...
        customData:SystemSettings:LaserSettings:MaximumPulseWidth:               ...
        customData:SystemSettings:LaserSettings:MinimumLaserPower:               ...
        customData:SystemSettings:LaserSettings:MaximumLaserPower:               ...
        customData:SystemSettings:LaserSettings:PulseWidth:                      ...
        customData:SystemSettings:LaserSettings:LaserPower:                      ...
        customData:SystemSettings:SamplingIntervalSettings_0:SamplingInterval:   ...
        customData:SystemSettings:SamplingIntervalSettings_0:IsPermitted:        ...
        customData:SystemSettings:SamplingIntervalSettings_0:PreTriggerShift:    ...
        customData:SystemSettings:SamplingIntervalSettings_0:SignalOffsetRange:Si...
        customData:SystemSettings:SamplingIntervalSettings_0:SignalOffsetRange:Si...
        customData:SystemSettings:SamplingIntervalSettings_1:SamplingInterval:   ...
        customData:SystemSettings:SamplingIntervalSettings_1:IsPermitted:        ...
        customData:SystemSettings:SamplingIntervalSettings_1:PreTriggerShift:    ...
        customData:SystemSettings:SamplingIntervalSettings_1:SignalOffsetRange:Si...
        customData:SystemSettings:SamplingIntervalSettings_1:SignalOffsetRange:Si...
        customData:SystemSettings:SamplingIntervalSettings_2:SamplingInterval:   ...
        customData:SystemSettings:SamplingIntervalSettings_2:IsPermitted:        ...
        customData:SystemSettings:SamplingIntervalSettings_2:PreTriggerShift:    ...
        customData:SystemSettings:SamplingIntervalSettings_2:SignalOffsetRange:Si...
        customData:SystemSettings:SamplingIntervalSettings_2:SignalOffsetRange:Si...
        customData:SystemSettings:SamplingIntervalSettings_3:SamplingInterval:   ...
        customData:SystemSettings:SamplingIntervalSettings_3:IsPermitted:        ...
        customData:SystemSettings:SamplingIntervalSettings_3:PreTriggerShift:    ...
        customData:SystemSettings:SamplingIntervalSettings_3:SignalOffsetRange:Si...
        customData:SystemSettings:SamplingIntervalSettings_3:SignalOffsetRange:Si...
        customData:SystemSettings:SamplingIntervalSettings_4:SamplingInterval:   ...
        customData:SystemSettings:SamplingIntervalSettings_4:IsPermitted:        ...
        customData:SystemSettings:SamplingIntervalSettings_4:PreTriggerShift:    ...
        customData:SystemSettings:SamplingIntervalSettings_4:SignalOffsetRange:Si...
        customData:SystemSettings:SamplingIntervalSettings_4:SignalOffsetRange:Si...
        customData:SystemSettings:SamplingIntervalSettings_5:SamplingInterval:   ...
        customData:SystemSettings:SamplingIntervalSettings_5:IsPermitted:        ...
        customData:SystemSettings:SamplingIntervalSettings_5:PreTriggerShift:    ...
        customData:SystemSettings:SamplingIntervalSettings_5:SignalOffsetRange:Si...
        customData:SystemSettings:SamplingIntervalSettings_5:SignalOffsetRange:Si...
        customData:SystemSettings:SamplingIntervalSettings_6:SamplingInterval:   ...
        customData:SystemSettings:SamplingIntervalSettings_6:IsPermitted:        ...
        customData:SystemSettings:SamplingIntervalSettings_6:PreTriggerShift:    ...
        customData:SystemSettings:SamplingIntervalSettings_6:SignalOffsetRange:Si...
        customData:SystemSettings:SamplingIntervalSettings_6:SignalOffsetRange:Si...
        customData:SystemSettings:VoltageSweepSettings:DigitalLine:Name:         ...
        customData:SystemSettings:VoltageSweepSettings:DigitalLine:DataArray:    ...
        customData:SystemSettings:VoltageSweepSettings:Amplitude:                ...
        customData:SystemSettings:VoltageSweepSettings:MinimumVoltage:           ...
        customData:SystemSettings:VoltageSweepSettings:MaximumVoltage:           ...
        customData:SystemSettings:ProgramControlSettings:SkipLaserOnCheck:       ...
        customData:SystemSettings:ProgramControlSettings:AllowRemoteControl:     ...
        customData:SystemSettings:ProgramControlSettings:DisableReboot:          ...
        customData:SystemSettings:ChannelSettings_0:ChannelNumber:               ...
        customData:SystemSettings:ChannelSettings_0:InternalFibreLength:         ...
        customData:SystemSettings:ChannelSettings_1:ChannelNumber:               ...
        customData:SystemSettings:ChannelSettings_1:InternalFibreLength:         ...
        customData:SystemSettings:ChannelSettings_2:ChannelNumber:               ...
        customData:SystemSettings:ChannelSettings_2:InternalFibreLength:         ...
        customData:SystemSettings:ChannelSettings_3:ChannelNumber:               ...
        customData:SystemSettings:ChannelSettings_3:InternalFibreLength:         ...
        customData:SystemSettings:TemperatureReferenceSettings:InternalReferenceS...
        customData:SystemSettings:TemperatureReferenceSettings:InternalReferenceS...
        customData:SystemSettings:TemperatureReferenceSettings:SamplingRate:     ...
        customData:SystemSettings:TemperatureReferenceSettings:UseReferenceResist...
        customData:SystemSettings:TemperatureReferenceSettings:ReferenceResistor:...
        customData:SystemSettings:TemperatureReferenceSettings:MaximumVoltage:   ...
        customData:SystemSettings:TemperatureReferenceSettings:TemperatureProbeSe...
        customData:SystemSettings:TemperatureReferenceSettings:TemperatureProbeSe...
        customData:SystemSettings:TemperatureReferenceSettings:TemperatureProbeSe...
        customData:SystemSettings:TemperatureReferenceSettings:TemperatureProbeSe...
        customData:SystemSettings:TemperatureReferenceSettings:TemperatureProbeSe...
        customData:SystemSettings:TemperatureReferenceSettings:TemperatureProbeSe...
        customData:SystemSettings:TemperatureReferenceSettings:TemperatureProbeSe...
        customData:SystemSettings:TemperatureReferenceSettings:TemperatureProbeSe...
        customData:SystemSettings:TemperatureReferenceSettings:TemperatureProbeSe...
        customData:SystemSettings:TemperatureReferenceSettings:TemperatureProbeSe...
        customData:SystemSettings:TemperatureReferenceSettings:TemperatureProbeSe...
        customData:SystemSettings:TemperatureReferenceSettings:TemperatureProbeSe...
        customData:SystemSettings:TemperatureReferenceSettings:TemperatureProbeSe...
        customData:SystemSettings:TemperatureReferenceSettings:TemperatureProbeSe...
        customData:SystemSettings:TemperatureReferenceSettings:TemperatureProbeSe...
        customData:SystemSettings:TemperatureReferenceSettings:TemperatureProbeSe...
        customData:SystemSettings:TemperatureReferenceSettings:TemperatureProbeSe...
        customData:SystemSettings:TemperatureReferenceSettings:TemperatureProbeSe...
        customData:SystemSettings:TemperatureReferenceSettings:TemperatureProbeSe...
        customData:SystemSettings:TemperatureReferenceSettings:TemperatureProbeSe...
        customData:SystemSettings:TemperatureReferenceSettings:TemperatureProbeSe...
        customData:SystemSettings:TemperatureReferenceSettings:TemperatureProbeSe...
        customData:SystemSettings:TemperatureReferenceSettings:TemperatureProbeSe...
        customData:SystemSettings:TemperatureReferenceSettings:TemperatureProbeSe...
        customData:SystemSettings:TemperatureReferenceSettings:TemperatureProbeSe...
        customData:SystemSettings:TemperatureReferenceSettings:TemperatureProbeSe...
        customData:SystemSettings:TemperatureReferenceSettings:TemperatureProbeSe...
        customData:SystemSettings:RawProcessingSettings:DAQSamplingFrequency:    ...
        customData:SystemSettings:RawProcessingSettings:EffectiveStokesRI:       ...
        customData:SystemSettings:RawProcessingSettings:EffectiveAntiStokesRI:   ...
        customData:SystemSettings:RawProcessingSettings:CorrectForZigZag:        ...
        customData:SystemSettings:RawProcessingSettings:LaserOnLength:           ...
        customData:SystemSettings:MeasurementSettings:InternalAveragingTime:     ...
        customData:SystemSettings:MeasurementSettings:InternalDifferentialLoss:  ...
        customData:SystemSettings:MeasurementSettings:TemperatureScalingFactor:  ...
        customData:SystemSettings:MeasurementSettings:MaximumMeasurementLength:  ...
        customData:SystemSettings:MeasurementSettings:SaveSignalData:            ...
        customData:SystemSettings:OvershootCorrectionSettings:CorrectForOvershoot...
        customData:SystemSettings:OvershootCorrectionSettings:Rotation:          ...
        customData:SystemSettings:OvershootCorrectionSettings:MultiplicationFacto...
        customData:SystemSettings:CurveCalibrationSettings:StartTemperature:     ...
        customData:SystemSettings:CurveCalibrationSettings:m:                    ...
        customData:SystemSettings:CurveCalibrationSettings:c:                    ...
        customData:SystemSettings:OperatingLimitsSettings:MinimumInputPower:     ...
        customData:SystemSettings:OperatingLimitsSettings:MaximumInputPower:     ...
        customData:SystemSettings:OperatingLimitsSettings:PowerHysteresis:       ...
        customData:SystemSettings:OperatingLimitsSettings:MinimumInternalTemperat...
        customData:SystemSettings:OperatingLimitsSettings:MaximumInternalTemperat...
        customData:SystemSettings:OperatingLimitsSettings:TemperatureHysteresis: ...
        customData:SystemSettings:SAHSettings:DeviceType:                        ...
        customData:SystemSettings:SAHSettings:SAHCOMPort:                        ...
        customData:SystemSettings:SAHSettings:DeviceYCOMPort:                    ...
        customData:SystemSettings:SAHSettings:MaximumPumpCurrent:                ...
        customData:SystemSettings:SAHSettings:DefaultTargetVoltage:              ...
        customData:SystemSettings:SAHSettings:WarmUpTime:                        ...
        customData:SystemSettings:SAHSettings:CoolDownTime:                      ...
        customData:SystemSettings:SAHSettings:TimingSettings:MaintainSettings:Tim...
        customData:SystemSettings:SAHSettings:TimingSettings:MaintainSettings:Num...
        customData:SystemSettings:SAHSettings:TimingSettings:MaintainSettings:Ste...
        customData:SystemSettings:SAHSettings:TimingSettings:MaintainSettings:Sta...
        customData:SystemSettings:SAHSettings:TimingSettings:FastSettings:TimeBet...
        customData:SystemSettings:SAHSettings:TimingSettings:FastSettings:NumberO...
        customData:SystemSettings:SAHSettings:TimingSettings:FastSettings:StepSiz...
        customData:SystemSettings:SAHSettings:TimingSettings:FastSettings:StateTr...
        customData:SystemSettings:SAHSettings:TimingSettings:SuperFastSettings:Ti...
        customData:SystemSettings:SAHSettings:TimingSettings:SuperFastSettings:Nu...
        customData:SystemSettings:SAHSettings:TimingSettings:SuperFastSettings:St...
        customData:SystemSettings:SAHSettings:TimingSettings:SuperFastSettings:St...
        customData:SystemSettings:RangeSettings:MeasurementRange:                ...
        customData:SystemSettings:RangeSettings:LaserFrequency:                  ...
        customData:SystemSettings:RangeSettings:TargetVoltage:                   ...
        customData:SystemSettings:PowerTimingSettings:OpticsOnWait:              ...
        customData:SystemSettings:PowerTimingSettings:DAQPowerOnWait:            ...
        customData:SystemSettings:PowerTimingSettings:DAQUSBOnWait:              ...
        customData:SystemSettings:PowerTimingSettings:OpticsOffWait:             ...
        customData:SystemSettings:PowerTimingSettings:DAQPowerOffWait:           ...
        customData:SystemSettings:PowerTimingSettings:DAQUSBOffWait:             ...
        customData:UserConfiguration:softwareVersion:                            ...
        customData:UserConfiguration:MainMeasurementConfiguration:ConfigurationNa...
        customData:UserConfiguration:MainMeasurementConfiguration:ConfigurationCo...
        customData:UserConfiguration:MainMeasurementConfiguration:MeasurementMeth...
        customData:UserConfiguration:MainMeasurementConfiguration:NumberOfMeasure...
        customData:UserConfiguration:MainMeasurementConfiguration:MeasurementInte...
        customData:UserConfiguration:MainMeasurementConfiguration:AutoRestart:   ...
        customData:UserConfiguration:MainMeasurementConfiguration:TemperatureUnit...
        customData:UserConfiguration:MainMeasurementConfiguration:DistanceUnits: ...
        customData:UserConfiguration:MainMeasurementConfiguration:MeasurementSyst...
        customData:UserConfiguration:MainMeasurementConfiguration:LaserFrequency:...
        customData:UserConfiguration:ChannelConfiguration_0:ChannelNumber:       ...
        customData:UserConfiguration:ChannelConfiguration_0:ChannelName:         ...
        customData:UserConfiguration:ChannelConfiguration_0:ChannelIsActive:     ...
        customData:UserConfiguration:ChannelConfiguration_0:SaveChannelData:     ...
        customData:UserConfiguration:ChannelConfiguration_0:AcquisitionConfigurat...
        customData:UserConfiguration:ChannelConfiguration_0:AcquisitionConfigurat...
        customData:UserConfiguration:ChannelConfiguration_0:AcquisitionConfigurat...
        customData:UserConfiguration:ChannelConfiguration_0:TemperatureCalibratio...
        customData:UserConfiguration:ChannelConfiguration_0:TemperatureCalibratio...
        customData:UserConfiguration:ChannelConfiguration_0:TemperatureCalibratio...
        customData:UserConfiguration:ChannelConfiguration_0:TemperatureCalibratio...
        customData:UserConfiguration:ChannelConfiguration_0:TemperatureCalibratio...
        customData:UserConfiguration:ChannelConfiguration_0:TemperatureCalibratio...
        customData:UserConfiguration:ChannelConfiguration_0:TemperatureCalibratio...
        customData:UserConfiguration:ChannelConfiguration_0:TemperatureCalibratio...
        customData:UserConfiguration:ChannelConfiguration_0:TemperatureCalibratio...
        customData:UserConfiguration:ChannelConfiguration_0:TemperatureCalibratio...
        customData:UserConfiguration:ChannelConfiguration_0:TemperatureCalibratio...
        customData:UserConfiguration:ChannelConfiguration_0:TemperatureCalibratio...
        customData:UserConfiguration:ChannelConfiguration_0:TemperatureCalibratio...
        customData:UserConfiguration:ChannelConfiguration_0:TemperatureCalibratio...
        customData:UserConfiguration:ChannelConfiguration_0:TemperatureCalibratio...
        customData:UserConfiguration:ChannelConfiguration_0:FibreCheckConfigurati...
        customData:UserConfiguration:ChannelConfiguration_0:FibreCorrectionConfig...
        customData:UserConfiguration:ChannelConfiguration_0:FibreCorrectionConfig...
        customData:UserConfiguration:ChannelConfiguration_1:ChannelNumber:       ...
        customData:UserConfiguration:ChannelConfiguration_1:ChannelName:         ...
        customData:UserConfiguration:ChannelConfiguration_1:ChannelIsActive:     ...
        customData:UserConfiguration:ChannelConfiguration_1:SaveChannelData:     ...
        customData:UserConfiguration:ChannelConfiguration_1:AcquisitionConfigurat...
        customData:UserConfiguration:ChannelConfiguration_1:AcquisitionConfigurat...
        customData:UserConfiguration:ChannelConfiguration_1:AcquisitionConfigurat...
        customData:UserConfiguration:ChannelConfiguration_1:TemperatureCalibratio...
        customData:UserConfiguration:ChannelConfiguration_1:TemperatureCalibratio...
        customData:UserConfiguration:ChannelConfiguration_1:TemperatureCalibratio...
        customData:UserConfiguration:ChannelConfiguration_1:TemperatureCalibratio...
        customData:UserConfiguration:ChannelConfiguration_1:TemperatureCalibratio...
        customData:UserConfiguration:ChannelConfiguration_1:TemperatureCalibratio...
        customData:UserConfiguration:ChannelConfiguration_1:TemperatureCalibratio...
        customData:UserConfiguration:ChannelConfiguration_1:TemperatureCalibratio...
        customData:UserConfiguration:ChannelConfiguration_1:TemperatureCalibratio...
        customData:UserConfiguration:ChannelConfiguration_1:TemperatureCalibratio...
        customData:UserConfiguration:ChannelConfiguration_1:TemperatureCalibratio...
        customData:UserConfiguration:ChannelConfiguration_1:TemperatureCalibratio...
        customData:UserConfiguration:ChannelConfiguration_1:TemperatureCalibratio...
        customData:UserConfiguration:ChannelConfiguration_1:TemperatureCalibratio...
        customData:UserConfiguration:ChannelConfiguration_1:TemperatureCalibratio...
        customData:UserConfiguration:ChannelConfiguration_1:FibreCheckConfigurati...
        customData:UserConfiguration:ChannelConfiguration_1:FibreCorrectionConfig...
        customData:UserConfiguration:ChannelConfiguration_1:FibreCorrectionConfig...
        customData:UserConfiguration:ChannelConfiguration_2:ChannelNumber:       ...
        customData:UserConfiguration:ChannelConfiguration_2:ChannelName:         ...
        customData:UserConfiguration:ChannelConfiguration_2:ChannelIsActive:     ...
        customData:UserConfiguration:ChannelConfiguration_2:SaveChannelData:     ...
        customData:UserConfiguration:ChannelConfiguration_2:AcquisitionConfigurat...
        customData:UserConfiguration:ChannelConfiguration_2:AcquisitionConfigurat...
        customData:UserConfiguration:ChannelConfiguration_2:AcquisitionConfigurat...
        customData:UserConfiguration:ChannelConfiguration_2:TemperatureCalibratio...
        customData:UserConfiguration:ChannelConfiguration_2:TemperatureCalibratio...
        customData:UserConfiguration:ChannelConfiguration_2:TemperatureCalibratio...
        customData:UserConfiguration:ChannelConfiguration_2:TemperatureCalibratio...
        customData:UserConfiguration:ChannelConfiguration_2:TemperatureCalibratio...
        customData:UserConfiguration:ChannelConfiguration_2:TemperatureCalibratio...
        customData:UserConfiguration:ChannelConfiguration_2:TemperatureCalibratio...
        customData:UserConfiguration:ChannelConfiguration_2:TemperatureCalibratio...
        customData:UserConfiguration:ChannelConfiguration_2:TemperatureCalibratio...
        customData:UserConfiguration:ChannelConfiguration_2:TemperatureCalibratio...
        customData:UserConfiguration:ChannelConfiguration_2:TemperatureCalibratio...
        customData:UserConfiguration:ChannelConfiguration_2:TemperatureCalibratio...
        customData:UserConfiguration:ChannelConfiguration_2:TemperatureCalibratio...
        customData:UserConfiguration:ChannelConfiguration_2:TemperatureCalibratio...
        customData:UserConfiguration:ChannelConfiguration_2:TemperatureCalibratio...
        customData:UserConfiguration:ChannelConfiguration_2:FibreCheckConfigurati...
        customData:UserConfiguration:ChannelConfiguration_2:FibreCorrectionConfig...
        customData:UserConfiguration:ChannelConfiguration_2:FibreCorrectionConfig...
        customData:UserConfiguration:ChannelConfiguration_3:ChannelNumber:       ...
        customData:UserConfiguration:ChannelConfiguration_3:ChannelName:         ...
        customData:UserConfiguration:ChannelConfiguration_3:ChannelIsActive:     ...
        customData:UserConfiguration:ChannelConfiguration_3:SaveChannelData:     ...
        customData:UserConfiguration:ChannelConfiguration_3:AcquisitionConfigurat...
        customData:UserConfiguration:ChannelConfiguration_3:AcquisitionConfigurat...
        customData:UserConfiguration:ChannelConfiguration_3:AcquisitionConfigurat...
        customData:UserConfiguration:ChannelConfiguration_3:TemperatureCalibratio...
        customData:UserConfiguration:ChannelConfiguration_3:TemperatureCalibratio...
        customData:UserConfiguration:ChannelConfiguration_3:TemperatureCalibratio...
        customData:UserConfiguration:ChannelConfiguration_3:TemperatureCalibratio...
        customData:UserConfiguration:ChannelConfiguration_3:TemperatureCalibratio...
        customData:UserConfiguration:ChannelConfiguration_3:TemperatureCalibratio...
        customData:UserConfiguration:ChannelConfiguration_3:TemperatureCalibratio...
        customData:UserConfiguration:ChannelConfiguration_3:TemperatureCalibratio...
        customData:UserConfiguration:ChannelConfiguration_3:TemperatureCalibratio...
        customData:UserConfiguration:ChannelConfiguration_3:TemperatureCalibratio...
        customData:UserConfiguration:ChannelConfiguration_3:TemperatureCalibratio...
        customData:UserConfiguration:ChannelConfiguration_3:TemperatureCalibratio...
        customData:UserConfiguration:ChannelConfiguration_3:TemperatureCalibratio...
        customData:UserConfiguration:ChannelConfiguration_3:TemperatureCalibratio...
        customData:UserConfiguration:ChannelConfiguration_3:TemperatureCalibratio...
        customData:UserConfiguration:ChannelConfiguration_3:FibreCheckConfigurati...
        customData:UserConfiguration:ChannelConfiguration_3:FibreCorrectionConfig...
        customData:UserConfiguration:ChannelConfiguration_3:FibreCorrectionConfig...
        _sections:                                                               ...

