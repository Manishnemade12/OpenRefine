<!-- Describe the bug - Please add a clear and concise description of the bug above this line. You can delete this line if you want. It will be hidden in the final bug report -->
`ImportingUtilitiesTests.testImportCompressedFiles()` opens a new `InputStreamReader` and `FileInputStream` for each suffix in the loop, but only closes the last reader after the loop finishes.

### To Reproduce
Steps to reproduce the behavior:
1. Run the server test suite, or run `ImportingUtilitiesTests.testImportCompressedFiles()` directly.
2. Observe the loop that processes the compressed sample files.
3. Trigger an exception during parsing or inspect file handles while the test is running.

### Current Results
Multiple readers are created in the loop, and earlier ones are not closed if the loop continues or an exception is thrown.

### Expected Behavior
Each opened reader and input stream should be closed after each iteration.

### Screenshots
Not provided.

### Versions<!--  (please complete the following information)-->
 - Operating System: Linux
 - Browser Version: N/A for this test issue
 - JRE or JDK Version: Not verified
 - OpenRefine: Current workspace version

### Datasets
The `persons` sample files used by the test are sufficient.

### Additional context
This is in `main/tests/server/src/com/google/refine/importing/ImportingUtilitiesTests.java` around lines 500-532. Using try-with-resources inside the loop would close each reader correctly.
