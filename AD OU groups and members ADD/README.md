# Program objectives
This script adds AD groups and their members based on information provided in a text file. The group names in AD are generated by combining a prefix with the folder name.

## Program phases

### Variables

Set the needed variables:
- $ouPath -> path to the OU where the AD groups will be created.
- $groupPrefix -> prefix used to generate group names based on folder names.
- $results -> array to store results and messages during group creation and user addition.
- $filePath -> path to the text file containing folder names and user-group associations.
- $outputFile -> path to the text file where results and messages will be saved.

### Functions

- Test-ADGroupExists -> checks if an AD group exists based on its SAM account name.
- Get-ADGroupMembers -> retrieves the members of an AD group.
- Add-UsersToADGroup -> adds users to an AD group.

### Execution

- It reads each line from the text file specified in $filePath.
- If a line matches the pattern indicating a folder under analysis, it extracts the folder name.
- It generates a group name and SAM account name based on the folder name by combining the prefix and folder name.
- It checks if the group already exists in AD:
    - If not, creates the group and logs the action.
    - If the group exists, logs its existence along with its distinguished name.
- If a line matches the pattern indicating a user associated with a group, it extracts the username.
- It checks if the group exists:
    - If the group exists, checks if the user is already a member.
        - If the user is a member, logs a message indicating the user is already a member of the group.
        - If the user is not a member, adds the user to the group and logs the action.
    - If the group does not exist, logs a message indicating the group does not exist, and the user cannot be added.

### Output
The script generates a text file containing information about group creation, existing groups, user addition, and any associated messages.