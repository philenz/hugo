## Image Builder Notes
![alt text](https://docs.microsoft.com/en-nz/azure/virtual-machines/media/image-builder-overview/image-builder-flow.png "High level overview")

### [Introduction](https://www.infoworld.com/article/3603129/working-with-azure-image-builder.html)
* Uses [managed identities](https://github.com/danielsollondon/azvmimagebuilder/blob/master/aibPermissions.md) to access resources, and you need to set up the appropriate permissions across resource groups, using an identity tag in your templates.
* You create the identity in the Azure CLI or in PowerShell and then add the appropriate permissions for creating, managing, and distributing images.
* Under the hood, the service is based around a JSON image template, deployed and managed in the Azure CLI. This defines the VM image and its capabilities, which are stored as an artifact in an Azure Resource Group.
* Once the template is in place, Image Builder will download the source files for the image (either as a VM image or an installer ISO), along with any scripts needed to build your image.
* Images are built as they’re needed before they’re stored in your image gallery, ready for use.
* Images should be stored in a [Shared Image Gallery](https://docs.microsoft.com/en-us/azure/virtual-machines/shared-image-galleries), which can be replicated globally, as well as offering redundant storage.
* Applications can be configured using ARM templates to build on these images, and high availability and targeted regional distribution should minimize the time needed to deploy an image.

### QuickStarts

#### [0_Creating_a_Custom_Linux_Managed_Image](https://github.com/danielsollondon/azvmimagebuilder/tree/master/quickquickstarts/0_Creating_a_Custom_Linux_Managed_Image)
```bash
cd 0_Creating_a_Custom_Linux_Managed_Image
# az login
./register.sh
./createResourceGroup.sh
./setPermissions.sh
./createImage.sh
# if any issues...
#./troubleshoot.sh
./createVM.sh
./cleanup.sh
```
#### [0_Creating_a_Custom_Windows_Managed_Image](https://github.com/danielsollondon/azvmimagebuilder/tree/master/quickquickstarts/0_Creating_a_Custom_Windows_Managed_Image)
```powershell
cd 0_Creating_a_Custom_Windows_Managed_Image
# Connect-AzAccount
.\prepareTemplate.ps1
.\submitTemplate.ps1
.\buildImage.ps1
.\status.ps1
.\createVM.ps1
```
#### [1_Creating_a_Custom_Win_Shared_Image_Gallery_Image](https://github.com/danielsollondon/azvmimagebuilder/tree/master/quickquickstarts/1_Creating_a_Custom_Win_Shared_Image_Gallery_Image)
```powershell
cd 1_Creating_a_Custom_Win_Shared_Image_Gallery_Image
.\createGallery.ps1
```
### VistaControlPlane
#### Use Managed Image
```powershell
cd VistaControlPlane
# prereqs...
.\register.ps1
.\setPermissions.ps1
.\createVNet.ps1
.\createImageGallery.ps1
.\createStorageAccount.ps1
# run image builder...
.\submitTemplate.ps1
.\buildImage.ps1
.\status.ps1
# create test vm from image...
.\createVMfromImage.ps1
# remove test vm/disk/nsg/pip/nic
.\cleanup.ps1
# modify an image...
.\modifyImage.ps1
```
#### Use Storage Account
#### Update using Shared Image Gallery
### Links

* [Preview: Azure Image Builder overview](https://docs.microsoft.com/en-nz/azure/virtual-machines/image-builder-overview)
  * [Preview: Create a Windows VM with Azure Image Builder](https://docs.microsoft.com/en-nz/azure/virtual-machines/windows/image-builder)
  * [Preview: Create an Azure Image Builder template](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/image-builder-json)
  * [Preview: Create a Windows image and distribute it to a Shared Image Gallery](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/image-builder-gallery)
* [Azure VM Image Builder Samples Repo](https://github.com/azure/azvmimagebuilder)...
  * * ...or [the original version](https://github.com/danielsollondon/azvmimagebuilder) which has useful readmes on the quickstarts missing from the new one!
* [Image Builder Template Reference](https://docs.microsoft.com/en-nz/azure/virtual-machines/linux/image-builder-json)
* [Azure Image Builder Service networking options](https://docs.microsoft.com/en-nz/azure/virtual-machines/linux/image-builder-networking)
* [Troubleshoot Azure Image Builder Service](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/image-builder-troubleshoot)
* [Configure Azure Image Builder Service permissions using Azure CLI](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/image-builder-permissions-cli)
* [Getting the Latest Image Version ResourceID from Shared Image Gallery](https://github.com/danielsollondon/azvmimagebuilder/tree/master/solutions/8_Getting_Latest_SIG_Version_ResID)
* [GitHub Action to Build Custom Virtual Machine Images](https://github.com/marketplace/actions/build-azure-virtual-machine-image)
* [Azure Image Builder Service DevOps Task](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/image-builder-devops-task)
