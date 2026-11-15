# textdb: this tutorial database in the plain text store format

`test_db` is `../filesystemdb/test_db` converted to the `textdb://` format of the otsdaq maxlite configuration store
(`otsdaq_convert_config_db`, every table version and group key with its number kept, 35 versions, 7 group keys).
Use it as `ARTDAQ_DATABASE_URI=textdb://<path>/databases/textdb/test_db`. ots maxlite cannot read the artdaq-database
format and has no converter, so the maxlite installer takes this copy.

Contents are those of `first_demo_waveform` (first_demo without ROOT: the Visualizer consumer is
`RawDataVisualizerConsumer`). The active groups in `Data/ServiceData/ActiveTableGroups.cfg` are Context 6, Backbone 4
and Configuration 2, in both formats.
