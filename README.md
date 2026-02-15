# Immersed-on-Fedora-43-latency-Issue-
# This is based on the nvidia gpus
This is about changing video encoding/decoding process from cpu to gpu!

This issue happens due to not installing the drivers or system/immersed issues
You can verify this by ```vainfo``` and if you see a message like ```vaInitialize failed with error code -1 (unknown libva error)```

first you need to install the nvidia graphics va-api drivers if they are not installed already:

# Enable RPM Fusion
```sudo dnf install https://mirrors.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm https://mirrors.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm```

# Install the translation layer
```sudo dnf install libva-nvidia-driver```

# Swap to the "Freeworld" Drivers
```sudo dnf swap mesa-va-drivers mesa-va-drivers-freeworld```

```sudo dnf swap mesa-vdpau-drivers mesa-vdpau-drivers-freeworld```

# Force the Environment Variables
```export LIBVA_DRIVER_NAME=nvidia```

```export __GLX_VENDOR_LIBRARY_NAME=nvidia```

```vainfo```

# Make it perminant
add export ```LIBVA_DRIVER_NAME=nvidia``` and ```export __GLX_VENDOR_LIBRARY_NAME=nvidia``` to the end of ```.bashrc``` file so it will force exported everytime you login. 

# Verification
after running immersed and connecting the headset you can run ```nvidia-smi dmon -s u``` and check the ```enc``` column, if it was more than 15% it is doing the job right.

Hope you enjoied. 
