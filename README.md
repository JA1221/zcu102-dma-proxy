# zcu102-dma-proxy
 yocto recipe

## Linux DMA From User Space
[Xilinx Wiki Link](https://xilinx-wiki.atlassian.net/wiki/spaces/A/pages/18842418/Linux+DMA+From+User+Space)
![](https://i.imgur.com/A99NEo4.png)

### Vivado Design
![](https://i.imgur.com/ekO7SbQ.png)

---


1. create kernel module  
   ```
   petalinux-create -t modules -n dma-proxy --enable
   ```
2. create test app  
   ```
   petalinux-create -t apps --name dma-proxy-test --enable
   ```
3. Move the files to
   * \<project path>/project-spec/meta-user/recipes-modules/
   * \<project path>/project-spec/meta-user/recipes-apps/
4. Modify the `.dtsi` file
   * \<project path>/project-spec/meta-user/recipes-bsp/device-tree/files/system-user.dtsi  
   ```
    /include/ "system-conf.dtsi"
    / {
        dma_proxy {
            compatible ="xlnx,dma_proxy";
            dmas = <&axi_dma_0 0
                    &axi_dma_0 1>;
            dma-names = "dma_proxy_tx", "dma_proxy_rx";
        };
    };
   ```