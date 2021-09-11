# Molecule Test
A simple project to test how to use Molecule to test a playbook.
The default *scenario* use Docker to run a container that will be the target of the Ansible playbook.
I expect that as I use this project to learn and test Molecule, I will create additional scenarios for things like *Vagrant* or *AWS* etc.

## Requirements
You need to have Docker installed
You need to have Python 3.6+ installed

This project uses the Molecule v3.x test frame work and it will need to be installed.
My recommendation would be to create a Python 3 virtual environment in a .venv and activate it.
Once the python virtual environment is activated, you would install Ansible, molecule and any other needed python modules.
A `requirements.txt` file that lists the required modules to be `pip` installed is provided.

```shell
$ python3 -m venv .venv
$ source .venv/bin/activate
$ pip install --upgrade pip
$ pip install -r requirements.txt
```

## Run molecule on the local host

The Molecule tool is designed to help with testing Ansible roles, but as in this case works for testing playbooks as well.

The normal workflow for me is:
1. Run `$ molecule create` to create a molecule testing environment using the *default* scenario.
2. Edit the `playbook.yml` and related files.
3. Run `$ molecule converge` to test that the current playbook.yml *works* without errors when running the Ansible tasks.
4. Fix any errors or add new features to the `playbook.yml` and any related files and return to the `converge` task.
5. Edit the `test_playbook.yml` and related files
6. Run `$ molecule verify` to verify that the Ansible tasks run by the converge process actually worked as expected.
7. Fix any errors in the `playbook.yml` and related files and return to step 3 the *converge* task.
8. Fix any errors in the `test_playbook.yml` and related files and return to step 6 the *verify* task.
9. Return to step 2 the *Edit the playbook.yml* step and add features.
10. Run `$ molecule destroy` to bring down the molecule testing environment

Once you have the features that you want in the playbook working as expected, you can run a full `test` task.
`$ molecule test` use the default scenario and run all molecule tasks using the `playbook.yml` file.
