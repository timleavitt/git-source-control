# git-source-control
 Server-side source control extension for Git on InterSystems' platforms

## Prerequisites/Dependencies

* IRIS instance with license key
* Git 2.31.0+
* OpenSSH 7.6+
* InterSystems package manager (https://openexchange.intersystems.com/package/ObjectScript-Package-Manager)

## Installation and Setup

1. Load this repository into IRIS from the community package registry. 
    ```
    zpm "install git-source-control"
    ```
2. Configure settings by running the following method and answering the prompts:
   ```
   d ##class(SourceControl.Git.API).Configure()
   ```
3. If using VSCode: Set up `isfs` server-side editing. First, save your current workspace in which you have the code open. Then, open the `.code-workspace` file generated by VS Code and add the following to the list of folders: 
    ```
    {
        "name": "<whatever you want the folder to show up as in the project explorer view>",
        "uri": "isfs://<instance_name>:<namespace_name>/"
    }
    ```

## Basic Use

### Studio
Add a file for tracking by right-clicking on it in the workspace/project view and choosing Git &gt; Add.
This same menu also has options to remove (stop tracking the file), discard changes (revert to the index), or commit changes.

You can browse file history and commit changes through a user interface launched from the top level Git > "Launch Git UI" menu item. There is also a page for configuring settings.

### VSCode
The same right click menus as in Studio live under "Server Source Control..." when right-clicking in a file (in the editor) or on a file when exploring an isfs folder. The top level "source control" menu is accessible through the command palette or the source control icon in the top right of the editor.

## Notes

### Security
If you want to interact with remotes from VSCode/Studio directly (e.g., to push/pull), you must use ssh (rather than https), create a public/private key pair to identify the instance (not yourself), configure the private key file for use in Settings, and configure the public key as a deploy key in the remote(s).

## During Development

:warning: Whenever any code in this project is updated outside the server (e.g. after every `git pull`), you _have_ to run `zpm "load <absolute path to git-source-control>"`. Otherwise, the changes won't be reflected on the server. However, if you load git-source-control via the InterSystems package manager and run `git pull` via the extension itself with the default pull event handler configured, it'll just work.
