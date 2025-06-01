## Goal
- Simplified pulls of multiple github repos at once.
    - This would save me so much time at work doing this manually.

## Acceptance Criteria
For a given folder like so with different github repo clones:
```
    - MainFolder
        - Repo 1
        - Repo 2
        - Repo 3
        - GithubMassPull
```
## Functionality
1. Commands
    1. ```./GitBatchTool pull``` command will pull updates from all repos *except* from "GitBatchTool"
    2. ```./GitBatchTool checkout main``` command will switch branches for all repos that do not have uncomitted changes *except* from "GitBatchTool"
2. If conflicts arise, the problematic repo is skipped over and output is provided saying as such.
    - Results are also saved in datetimestamped files, for tracability
3. If a username/password or token is required, it will prompt the user to do so at each interval.

### References:
1. Bulk check all subdirectories
    1. https://stackoverflow.com/questions/3497123/run-git-pull-over-all-subdirectories
    2. Notes from reference:
        ```PowerShell
        find ..\ -type d -depth 1 -exec git --git-dir={}/.git --work-tree=$PWD/{} pull origin master \;
        ```
        - The ```..\``` will make it go into the parent directory of the gitBatchTool.
        - ```-type d``` to find directories - not files
        - ``` -depth 1``` for max depth of 1 within the sub-directories 
        - ```-exec {} \;``` will run the command in the bracket (I think, need to confirm) for every find.
        - ```git --git-dir={}/.git --work-tree=$PWD/{} pull``` will pull the individual directories
2. Saving Output:
    1. https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/out-file?view=powershell-7.5
    2. Notes from reference:
        - ```Out-File``` Seems to be the approach I need for piping the results to a file.
        - ```function``` appears to allow someone to build functions in powershell. Should take advantage of. Will make it easier to build this as a powershell program. This particular example also shows how to handle it for the entire scope.
            - https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/out-file?view=powershell-7.5#example-5-set-file-output-width-for-entire-scope
