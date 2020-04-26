# Cork Traffic Network
This repository is an open sourced collection of configuration files required to simulate Cork's traffic network using the [SUMO software](https://sumo.dlr.de/docs/).

The files in this repository can be used to create a traffic simulation for Cork, but this simulation is based on a lot of assumptions, which in turn are based on more or less accurate statistics. As people contribute to this repository those assumptions will become better and the simulations more accurate.

The heart of this repository is the network.net.xml file, that represents corks network of streets, traffic lights, routes, etc. This has been converted from openstreetmap, but needs some manual intervention to improve its accuracy.

You are for these reansons strongly encouraged to contribute to this project, either by improving the network file or by providing statistical data and transforming it to the required format. See "How to contribute" for details.

## How to use

First, clone this repository:
```sh
git clone git@github.com:Lobidu/cork-traffic-net.git
```

Next, install the SUMO software according to their [install instructions](https://sumo.dlr.de/docs/Downloads.php) for your system. If you have access to a Linux system, I recommend running sumo on Linux, but make sure your system is powerful enough to support the processing- and memory-heavy simulations. If running on MacOS Catalina, see the Section about "MacOS segmentation fault" at the end of this Readme.

### Simple simulation

Inside the repository, start sumo-gui using the default configuration:

```sh
sumo-gui -c simulation/cork.sumocfg
```
This will load the current default simulation, roughly representing Cork's current traffic network, based on a lot of assumptions and guesses. As people contribute to this repository those assumptions will become better and the simulation ore accurate.

## How to contribute

### Improving the network
The network file has originally been created with sumo's `netconvert` using openstreetmap and some automated guesses as configured in network/generate/netcovert.config. This gave a pretty good base. But to get it right, some manual editing is necessary. Some of it has already been done for the city centre, but there are quite a few areas where a granular local knowledge of the area is necessary to make the model 100% right.

### How to edit network.net.xml
Execute the below command to open the network file in netedit:
```sh
netedit network/network.net.xml
```

## Notes and issues

#### MacOS segmentation fault
If running on MacOS, there is an [open issue](https://github.com/eclipse/sumo/issues/6242) with sumo's dependency "libfox" for MacOS Catalina. In this case you will have to use the Mojave version of libfox. If you get a 'segmentation fault' when starting sumo-gui, follow these steps:

1. Uninstall fox:
   ```sh
    brew uninstall --ignore-dependencies fox
    ```
2. Edit brew Formula of fox:
    ```sh
    brew edit fox
    ```
3. Comment out or delete the following line:
    ```sh
    sha256 "c6697be294c9a0458580564d59f8db32791beb5e67a05a6246e0b969ffc068bc" => :catalina
    ```
4. Install Mojave bottle of fox:
    ```sh
    brew install fox
    ```