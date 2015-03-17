# ranger-vagrant
This is a Vagrant setup for Apache Ranger 

#Requirements:
----------

- [VirtualBox](https://www.virtualbox.org/wiki/Downloads). Grab the VirtualBox Extension Pack as well.
- [Vagrant](http://www.vagrantup.com/downloads.html). 
- [Ansible](http://docs.ansible.com/intro_installation.html). Because i am not a good [cook](https://www.chef.io/chef/)!!


 
Getting Started:
----
Checkout this repo :
```
$ git clone git@github.com:gautamborad/ranger-vagrant.git
```

Edit the config file to your liking :
```
$ vi config
```

Bootup vagrant :
```
$ vagrant up
```

Available options:

|Property|Desc|
 ----------------- | ------------------
|box_url | The base box to use. Provide a local url, if you already have the box downloaded. (file://path/to/file.box) |
| rpm_install  | `true/false` Do rpm install of ranger-admin? |
| rpm_install_params | Properties used when rpm_install is `true` |
| |**hdp_repo**: Link to the HDP repo to use. |
| |**db_flavor**: `mysql`. DB flavor to use |
| build_ranger|`true/false` Checkout and build ranger? |
| build_params|Params used when `build_ranger` is `true` |
| | **ranger_src_dir** : Dir where the code is checked out. |
| | **ranger_repo**: `https://github.com/apache/incubator-ranger.git`. Ranger Repo to clone |
| | **ranger_branch**: `master`. Branch to clone |
| | **apply_patches**: `true/false` Apply patches before building? If `yes` all patches (`*.patch` files in the `data/patches/` will be applied before building |



