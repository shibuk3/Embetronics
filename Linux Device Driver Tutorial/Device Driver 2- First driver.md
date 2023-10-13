```
#include<linux/kernel.h>
#include<linux/init.h>
#include<linux/module.h>
 
/*
** Module Init function
*/
static int __init hello_world_init(void)
{
    printk(KERN_INFO "Welcome to EmbeTronicX\n");
    printk(KERN_INFO "This is the Simple Module\n");
    printk(KERN_INFO "Kernel Module Inserted Successfully...\n");
    return 0;
}

/*
** Module Exit function
*/
static void __exit hello_world_exit(void)
{
    printk(KERN_INFO "Kernel Module Removed Successfully...\n");
}
 
module_init(hello_world_init);
module_exit(hello_world_exit);
 
MODULE_LICENSE("GPL");
MODULE_AUTHOR("EmbeTronicX <embetronicx@gmail.com>");
MODULE_DESCRIPTION("A simple hello world driver");
MODULE_VERSION("2:1.0");
```
## Compiling our driver
Once we have the C code, it is time to compile it and create the module file hello_world_module.ko. creating a Makefile for your module is straightforward.
```
obj-m += hello_world.o
 
ifdef ARCH
  #You can update your Beaglebone path here.
  KDIR = /home/embetronicx/BBG/tmp/lib/modules/5.10.65/build
else
  KDIR = /lib/modules/$(shell uname -r)/build
endif
 
all:
  make -C $(KDIR)  M=$(shell pwd) modules
 
clean:
  make -C $(KDIR)  M=$(shell pwd) clean
```

In Terminal you need to enter sudo make. Now we got hello_world_module .ko


### Loading

To load a Kernel Module, use the insmod command with root privileges.

For example, our module file name is hello_world_module.ko
```
sudo insmod hello_world_module.ko
```


lsmod used to see the modules were inserted. In the below image, I’ve shown the prints in the init function. Use dmesg to see the kernel prints.



So, when I load the module, it executes the init function.

### Listing the Modules
In order to see the list of currently loaded modules, use the lsmod command. In the above image, you can see that I have used lsmod command.

Unloading
To un-load, a Kernel module, use the rmmod command with root privileges.

In our case,
```
sudo rmmod hello_world_module.ko or sudo rmmod hello_world_module
```


So, when I unload the module, it executes the exit function.


### Getting Module Details
In order to get information about a Module (author, supported options), we may use the modinfo command.

For example
```
modinfo hello_world_module.ko
```
