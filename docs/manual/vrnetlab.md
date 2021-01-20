Containerlab focuses on containers, but there are way more routing products which are only shipped in a virtual machine packaging. Leaving containerlab users without ability to create topologies with both containerized and VM-based routing systems would have been a shame.

Keeping this requirement in mind from the very beginning, we added a kind [`bridge`](../lab-examples/ext-bridge.md), that allows to, ehm, bridge your containerized topology with other resources available via a bridged network. For example a VM based router.

<div class="mxgraph" style="max-width:100%;border:1px solid transparent;margin:0 auto; display:block;" data-mxgraph="{&quot;page&quot;:0,&quot;zoom&quot;:1.5,&quot;highlight&quot;:&quot;#0000ff&quot;,&quot;nav&quot;:true,&quot;check-visible-state&quot;:true,&quot;resize&quot;:true,&quot;url&quot;:&quot;https://raw.githubusercontent.com/srl-wim/container-lab/diagrams/vrnetlab.drawio&quot;}"></div>

<script type="text/javascript" src="https://cdn.jsdelivr.net/gh/hellt/drawio-js@main/embed2.js" async></script>

Although this approach has many pros, it doesn't allow users to define the VM based nodes in the same topology file. But not anymore, with [`vrnetlab`](https://github.com/plajjan/vrnetlab) integration containerlab became capable of launching topologies with VM-based routers.

## Vrnetlab
Vrnetlab essentially allows to package a regular VM inside a container and makes it runnable and accessible as if it was a container image all way long.

To make this work, vrnetlab provides a set of scripts that will build the container image taking a user provided qcow file as an input.

<div class="mxgraph" style="max-width:100%;border:1px solid transparent;margin:0 auto; display:block;" data-mxgraph="{&quot;page&quot;:1,&quot;zoom&quot;:1.5,&quot;highlight&quot;:&quot;#0000ff&quot;,&quot;nav&quot;:true,&quot;check-visible-state&quot;:true,&quot;resize&quot;:true,&quot;url&quot;:&quot;https://raw.githubusercontent.com/srl-wim/container-lab/diagrams/vrnetlab.drawio&quot;}"></div>

!!!info
    Although multiple vendors are supported in vrnetlab, to make these images work with container-based networking, we needed to fork the project and provide the necessary improvements.  
    Thus, the VM based products will appear in the supported list gradually.

### Supported VM products


#### Nokia SR OS
Nokia's virtualized SR OS, aka VSR/VSim has been added to containerlab supported kinds under the [vr-sros](kinds/vr-sros.md) kind. A [demo lab](../lab-examples/vr-sros.md) explains the way this kind can be used.

To build a container image with SR OS inside users should follow [the instructions](https://github.com/hellt/vrnetlab/tree/master/sros#building-the-docker-image) provided and using the code of the forked version of a vrnetlab project.

### Limitations
* LACP and BPDU packets can not be delivered to/from VM's running inside the containers when launched with containerlab.