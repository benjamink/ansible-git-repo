# ansible-git-repo

Demonstration Ansible repo for solving an issue between [kitchen-ansible](https://github.com/neillturner/kitchen-ansible) & [git-repo](https://code.google.com/p/git-repo/).

## Setting up repo

[git-repo](https://code.google.com/p/git-repo/) is a tool developed by Google for managing multiple disparate repositories as a single project.  This tool proves to be very useful for tying together all the roles and test repositories into a single project directory for developing Ansible code.

### Prerequisite Tools

    $ brew install gpg repo

### Initializing Project

Create a file named `default.xml` in the current project directory, commit it & push it into the repository.  The file should contain the following at a minimum:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<manifest>

  <remote name="github" fetch="https://github.com/benjamink/"/>

  <default revision="master" remote="github" sync-j="4"/>

  <!-- Custom Ansible Roles -->
  <project name="ansible-helloworld" path="roles/helloworld" groups="roles"/>

  <!-- Additional project definitions... -->

</manifest>
```

Initialize the current project with `repo`:

    $ repo init -q -u https://github.com/benjamink/ansible-git-repo.git

### Pull in Projects

Once the current repository has been initialized for `git-repo` it's necessary to pull in the various projects listed in the manifest file:

    $ repo sync
