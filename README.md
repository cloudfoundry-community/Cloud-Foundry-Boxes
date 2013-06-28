# Vagrant boxes for Cloud Foundry

If you are developing Cloud Foundry and want some useful Vagrant boxes to get you started, then you need look no further than the following Dropbox:

* [Cloud Foundry Boxes](https://www.dropbox.com/sh/c71td6p4ffrt4uh/1oyn4vmVbD)

Currently only virtualbox boxes are being shared.

## Usage

### dea_ng

The [dea_ng](https://github.com/cloudfoundry/dea_ng) project l there is a Vagrant box at `~/boxes/ci_with_warden_prereqs.box`.

Options:

1. Download the latest `warden-ubuntu-*.box` box from the Dropbox page above and save as `~/boxes/ci_with_warden_prereqs.box`
2. Add the entire Dropbox to your own Dropbox and run the `rake` task. See `Shared Dropbox` section below.

Then launch the vagrant box from within the project folder:

```
$ vagrant up
```

### cf-vagrant-installer

The [cf-vagrant-installer](https://github.com/Altoros/cf-vagrant-installer) project will not look for a local Vagrant box, as `dea_ng` above does. You need to edit the existing `Vagrantfile` with the following changes:

``` ruby
config.vm.box = "cf-install"
config.vm.provider :virtualbox do |v, override|
  override.vm.box_url = "~/boxes/cf-install-virtualbox.box"
  v.customize ["modifyvm", :id, "--memory", "2048"]
end
```

Then launch the vagrant box from within the project folder:

```
$ vagrant up
```


## Shared Dropbox

You can either download the specific box that you need into `~/boxes`, or you can Share the Dropbox with yourself and have the boxes constantly updated as they change.

To add symlinks into `~/boxes` you simply run the default rake task within the Dropbox:

```
$ cd ~/Dropbox/Cloud\ Foundry\ Boxes
$ rake
```

This will create symlinks within `~/boxes` to the Vagrant boxes within your Dropbox:

```
$ ls -al ~/boxes  
... cf-install-virtualbox.box -> /Users/drnic/Dropbox/Cloud Foundry Boxes/Rakefile/cf-install-virtualbox.box
... ci_with_warden_prereqs.box -> /Users/drnic/Dropbox/Cloud Foundry Boxes/Rakefile/ci_with_warden_prereqs.box
```

