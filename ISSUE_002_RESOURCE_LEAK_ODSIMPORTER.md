<!-- Describe the bug - Please add a clear and concise description of the bug above this line. You can delete this line if you want. It will be hidden in the final bug report -->
OpenRefine can leak a file handle while preparing ODS import metadata. `OdsImporter.createParserUIInitializationData()` opens a `FileInputStream` inside a loop and does not close it explicitly.

### To Reproduce
Steps to reproduce the behavior:
1. Start OpenRefine.
2. Load an ODS file so the ODS importer path runs.
3. Repeat with multiple ODS files or trigger an exception during document loading.

### Current Results
The file input stream may remain open for each file processed in the loop.

### Expected Behavior
Each opened stream should be closed reliably, even when loading or parsing fails.

### Screenshots
Not provided.

### Versions<!--  (please complete the following information)-->
 - Operating System: Linux
 - Browser Version: N/A for this server-side issue
 - JRE or JDK Version: Not verified
 - OpenRefine: Current workspace version

### Datasets
An ODS file is required to trigger the importer path.

### Additional context
This is in `main/src/com/google/refine/importers/OdsImporter.java` around lines 79-95. A try-with-resources block around the `FileInputStream` would fix the leak.
