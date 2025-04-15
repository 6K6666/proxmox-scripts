nvidia-gpu-passthrough 

prereqs: nvidia gpu, intel cpu

save it as a .sh file on your proxmox host. chmod +x filename.sh to make it executable. then ./filename.sh to run the script. 
it will automatically grab your gpu display and audio vendor ids
the only thing you will need to do is edit the vm config file where you want the gpu to passed through to

Going back to the Shell window, we need to edit /etc/pve/qemu-server/<vmid>.conf, where <vmid> is the VM ID Number you used during the VM creation (General Tab).
nano /etc/pve/qemu-server/<vmid>.conf
In the editor, let's add these command lines (doesn't matter where you add them, so long as they are on new lines. Proxmox will move things around for you after you save):

machine: q35
cpu: host,hidden=1,flags=+pcid
args: -cpu 'host,+kvm_pv_unhalt,+kvm_pv_eoi,hv_vendor_id=NV43FIX,kvm=off'

credit to this reddit thread for inspiration for this script: https://www.reddit.com/r/homelab/comments/b5xpua/the_ultimate_beginners_guide_to_gpu_passthrough/
