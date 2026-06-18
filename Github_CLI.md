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

|COMMANDS|   usage |
|----------|----------|
gh issue create|        Create a new issue
gh issue  list |         List issues in a repository
gh issue   status|        Show status of relevant issues
gh issue   close|         Close issue
gh issue   comment|    Add a comment to an issue
gh issue   delete |        Delete issue
gh issue   develop |      Manage linked branches for an issue
gh issue   edit |        Edit issues
gh issue  lock |          Lock issue conversation
gh issue   pin |          Pin an issue
gh issue   reopen |        Reopen issue
gh issue   transfer |     Transfer issue to another repository
gh issue   unlock |       Unlock issue conversation
gh issue   unpin |      Unpin an issue
gh issue   view |         View an issue
-----------------------------------------------------

**pr**            Manage pull requests
|COMMANDS|   usage |
|----------|----------|
gh pr create|        Create a pull request
gh pr   list|         List pull requests in a repository
gh pr   status|        Show status of relevant pull requests
gh pr   checkout|    Check out a pull request in git
gh pr   checks|     Show CI status for a single pull request
gh pr   close|        Close a pull request
gh pr   comment|      Add a comment to a pull request
gh pr   diff|         View changes in a pull request
gh pr   edit|          Edit a pull request
gh pr   lock|         Lock pull request conversation
gh pr   merge|         Merge a pull request
gh pr   ready|         Mark a pull request as ready for review
gh pr   reopen|       Reopen a pull request
gh pr   revert|        Revert a pull request
gh pr   review|       Add a review to a pull request
gh pr   unlock|        Unlock pull request conversation
gh pr   update-branch| Update a pull request branch
gh pr   view|          View a pull request
---------------------------------------------


  **skill**         Install and manage agent skills (preview)

  |COMMANDS|   usage |
|----------|----------|
gh skill install|      Install agent skills from a GitHub repository (preview)
gh skill  preview|     Preview a skill from a GitHub repository (preview)
gh skill  publish|       Validate and publish skills to a GitHub repository (preview)
gh skill  search|        Search for skills across GitHub (preview)
gh skill  update|        Update installed skills to their latest versions (preview)
-----------------------------------------------------  

**additional commands**
|COMMANDS|   usage |
|----------|----------|
  project:   |    Work with GitHub Projects.
  release:    |   Manage releases
  agent-task:  |  Work with agent tasks (preview)
  alias:        | Create command shortcuts
  api:          | Make an authenticated GitHub API request
  attestation:  | Work with artifact attestations
  completion:   | Generate shell completion scripts
  config:       | Manage configuration for gh
  copilot:      | Run the GitHub Copilot CLI (preview)
  extension:    | Manage gh extensions
  gpg-key:      | Manage GPG keys
  label:        | Manage labels
  licenses:     | View third-party license information
  preview:      | Execute previews for gh features
  ruleset:      | View info about repo rulesets
  search:       | Search for repositories, issues, and pull requests
  secret:       | Manage GitHub secrets
  ssh-key:      | Manage SSH keys
  status:       | Print information about relevant issues, pull requests, and notifications across repositories
  variable:     | Manage GitHub Actions variables

--------------------------------------------
