Role Name
=========

Python Tool Carousel is an ansible role for cloning python tools from github and automagicly configuring them to be commandline executable in their own virtual envoirment. 

The project installs uses an configures Pyenv in attempt to avoid python dependency hell. 

this project is used inside of 
https://github.com/jurjurijur/ansible-playbook-kali2.0

An ansible playbook to set-up your kali workstation.

Requirements 
--------------
ansible 
git 

Role Variables
--------------

# The name of the user you want to own the pyenv and python tool directorys. 
python_tools_user: user 
# The home folder of the user you want pyenv installed 
python_tools_user_homefolder: /home/user


# The global python version you want active after installation (Default is system)
pyenv_global: ["system"]
# what shellfile is used by the user so pyenv can be added to path (default is bashrc)
python_tools_user_shellrcfile: '.bashrc'
# the folder where you want to download your python tools to, en run your python tools from (default /opt)
tool_folder: "/opt"

``` You do not need to specify the defaults if you are okay with them```

# The python tools to isntall in its own virtual envoirment.
python_tools:
  # name of the tool. this will be used to create executable symlinks 
  - name: securityheaders
  # the url to the git repo of the tool
    repo: https://github.com/koenbuyens/securityheaders.git
  # needs to be exact version name that is available with pyenv
    python_version: '2.7.18'
  - name: jwt_tool
    repo: https://github.com/ticarpi/jwt_tool.git
    python_version: '3.11.4'
    # Specify the main file to make executable within its virtualenv. Without one specified by default it will search for {{name}}.py
    main_file: 'jwt_tool.py' 


Dependencies
------------


This ansible role uses ansible-role-pyenv from "static.dev" to convinently install and configure pyenv on the system. https://github.com/staticdev/ansible-role-pyenv


Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

``` main.yml```
  name: install python tools 
  hosts: kali
  become: true
  roles:
    - role: python-tool-carousel
      vars:
        python_tools_user: kali
        python_tools_user_homefolder: /home/kali
        python_tools:
          - name: securityheaders
            repo: https://github.com/koenbuyens/securityheaders.git
            python_version: '2.7.18'
        
        
                                                  

License
-------

BSD

Author Information
------------------

Jurjurijur
