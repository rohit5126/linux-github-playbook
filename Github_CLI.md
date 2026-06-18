# GITHUB CLI COMMANDS

**REPO** #Manage repositories 

|COMMANDS|   usage |
|----------|----------|
|gh repo create | Create a new repository|
gh repo list | List repositories owned by user
gh repo archive |      Archive a repository
gh repo autolink  |    Manage autolink references
gh repo clone |      Clone a repository locally
gh repo delete |      Delete a repository
gh repo deploy-key |    Manage deploy keys in a repository
gh repo  edit   |       Edit repository settings
gh repo fork |          Create a fork of a repository
gh repo  gitignore  |   List and view available repository gitignore templates
gh repo  license |      Explore repository licenses
gh repo rename |   Rename a repository
gh repo set-default |  Configure default repository for this directory
gh repo sync |         Sync a repository
gh repo unarchive   | Unarchive a repository
gh repo view |      View a repository
----------------------------------------

**auth** #authentication gh using github

|COMMANDS|   usage |
|----------|----------|
gh auth login |         Log in to a GitHub account
gh auth logout |        Log out of a GitHub account
gh auth refresh |     Refresh stored authentication credentials
gh auth setup-git |     Setup git with GitHub CLI
gh auth status |     Display active account and authentication state on each known GitHub host
gh auth switch |     Switch active GitHub account
gh auth token |        Print the authentication token gh uses for a hostname and account
-----------------------------------------------------

**browse**      #Open repositories, issues, pull requests, and more in the browser
```
EXAMPLES
  # Open the home page of the current repository
  $ gh browse
  
  # Open the script directory of the current repository
  $ gh browse script/
  
  # Open issue or pull request 217
  $ gh browse 217
  
  # Open commit page
  $ gh browse 77507cd94ccafcf568f8560cfecde965fcfa63
  
  # Open repository settings
  $ gh browse --settings
  
  # Open main.go at line 312
  $ gh browse main.go:312
  
  # Open blame view for main.go at line 312
  $ gh browse main.go:312 --blame
  
  # Open main.go with the repository at head of bug-fix branch
  $ gh browse main.go --branch bug-fix
  
  # Open main.go with the repository at commit 775007cd
  $ gh browse main.go --commit=77507cd94ccafcf568f8560cfecde965fcfa63

```
---------------------------------------------------------

**gist**          # Manage gists

|COMMANDS|   usage |
|----------|----------|
gh gist clone |        Clone a gist locally
gh gist create |       Create a new gist
gh gist   delete |      Delete a gist
gh gist   edit |        Edit one of your gists
gh gist   list |        List your gists
gh gist rename |       Rename a file in a gist
gh gist  view |          View a gist
--------------------------------------------------

**issue**       #Manage issues


  org:           Manage organizations
  pr:            Manage pull requests
  project:       Work with GitHub Projects.
  release:       Manage releases
  repo:          Manage repositories
  skill:         Install and manage agent skills (preview)

