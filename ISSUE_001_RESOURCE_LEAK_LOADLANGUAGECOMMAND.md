<!-- Describe the bug - Please add a clear and concise description of the bug above this line. You can delete this line if you want. It will be hidden in the final bug report -->
OpenRefine can leak a file handle when loading a language file in `LoadLanguageCommand.loadLanguageFile()`. The method opens a `FileInputStream` and wraps it in readers without closing the stream on success or on parse errors.

### To Reproduce
Steps to reproduce the behavior:
1. Start OpenRefine.
2. Trigger the code path that loads a translation file from `main/src/com/google/refine/commands/lang/LoadLanguageCommand.java`.
3. Repeat the request several times or force a parsing error while the file is being read.

### Current Results
The language file stream can remain open after the method returns or after an exception is thrown.

### Expected Behavior
The language file stream should always be closed, even if parsing fails.

### Screenshots
Not provided.

### Versions<!--  (please complete the following information)-->
 - Operating System: Linux
 - Browser Version: N/A for this server-side issue
 - JRE or JDK Version: Not verified
 - OpenRefine: Current workspace version

### Datasets
Not required for reproduction.

### Additional context
This is in `main/src/com/google/refine/commands/lang/LoadLanguageCommand.java` around lines 158-176. A try-with-resources block would prevent the leak.
