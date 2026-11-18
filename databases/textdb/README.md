# textdb: this tutorial database in the plain text store format (ots maxlite)

`test_db` is `../filesystemdb/test_db` converted to the `textdb://` format of the otsdaq maxlite configuration store
(`otsdaq_convert_config_db`, 44 table versions and 6 group keys, numbers kept, verified), then changed in three ways so it
runs on ots maxlite (no ROOT, no Logbook):

- `DataProcessorTable` v2: the Visualizer consumer `DB1Consumer1` uses `RawDataVisualizerConsumer` instead of the ROOT plugin
  `DemoDQMHistosConsumer`; this is Configuration group `defaultConfig` key 2.
- `XDAQApplicationTable` v4: `LogbookSupervisor` Status Off; this is Context group `testContext` key 4.
- `GroupAliasesTable` v5: `defaultSystemAlias` points at `defaultConfig` key 2 (Backbone `TableEditWizBackbone` key 5).

Use it as `ARTDAQ_DATABASE_URI=textdb://<path>/databases/textdb/test_db`. ots maxlite cannot read the artdaq-database format
and has no converter, so the maxlite installer takes this copy.

The active groups in `Data/ServiceData/ActiveTableGroups.cfg` are Context 4, Backbone 5, Configuration 2 and Iterate 3.
They fit `textdb` only: `../filesystemdb/test_db` is the unchanged one of branch `iterator` (Context 3, Backbone 4,
Configuration 1), so for ots lite or full use branch `iterator`.

As in branch `iterator`, the Iterate group has no plans: the tutorial creates one. Checked on ots maxlite: a plan `ScanPort`
(`fsm PhysicsRuns0`, `configure defaultSystemAlias`, `label Main`, `run 10`, `repeat Main 1`, `halt`) made with
`ai_scripts/iteration_plan.py` played and wrote two run files. The Iterator window of the browser was not tried.
Note: `Data/TableInfo/IterationPlanTableInfo.xml` here is an old definition (its commands end at `RUN`, so saving a plan
with `HALT` fails until `UpdateOTS.sh --tables` has refreshed it, which the installer does).
