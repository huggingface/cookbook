
# Interactive Development In HF Spaces
_Authored by: [Moritz Laurer](https://huggingface.co/MoritzLaurer)_


Services like Google Colab or Kaggle Notebooks have made it dramatically easier for people to access compute in easy-to-use Jupyter notebooks in the browser. Unfortunately, these services also have several limitations: 
- GPUs are unstable, and a training job can be canceled right before it finishes.
- The choice of GPUs is limited to just a few single GPUs.
- There is no native support for connecting to the cloud GPU via your preferred local IDE like VS Code. 

HF JupyterLab Spaces overcome these limitations. With a HF JupyterLab Space, you can:
- Do all of your development work in JupyterLab in your browser.
- Dynamically switch between CPUs and a wide range of GPUs that never stop unless you want them to.
- Connect to cloud compute resources with your preferred local IDE like VS Code via SSH for full remote development. 

This recipe guides you through the setup of your own JupyterLab Space.


## Interactive Development in HF JupyterLab Spaces

### Creating your JupyterLab Space
To create your own HF JupyterLab Space, navigate to the [Space creation page](https://huggingface.co/new-space?template=SpacesExamples%2Fjupyterlab) and click on `Docker` > `JupyterLab`. A HF JupyterLab Space is essentially a Docker container with a pre-configured copy of JupyterLab that runs on Hugging Face's cloud infrastructure. Here is some advice on configuring your JupyterLab Space: 

- **Choosing the correct owner**: If you are using the JupyterLab Space as part of your work for an Enterprise Hub Organization, select the organization's name under the `Owner` dropdown (e.g. the dummy "enterprise-explorers" in the image below). Any compute costs will then be billed on the account of this Enterprise Organization. 
- **Access control**: If you want only selected members of your team to access the JupyterLab Space, you can click on `Everyone` right next to `Access Control` and limit access to the JupyterLab Space to a predefined Resource Group. Resource Groups are an Enterprise Hub feature that enables you to limit access to selected repositories (models, datasets, Spaces) to a smaller group of team members. See the [docs](https://huggingface.co/docs/hub/en/security-resource-groups) on how to create your first Resource Group.

<div style="flex justify-center">
    <img src="https://huggingface.co/datasets/huggingface/cookbook-images/resolve/main/enterprise-jupyterlab-creation-1.png" width="450">  
</div>

- **Choosing your hardware**: You can choose from a wide range of hardware from free CPUs to A100 GPUs. When setting up the Space, we recommend you choose the free basic CPU. You can switch to better paid hardware once you need it (see available hardware and prices [here](https://huggingface.co/pricing)). 
- **Persistent storage**: It is important to attach persistent storage to the Space, so that all the files you create (code, models, data) are also saved when the Space is paused or reset. You can always increase the disk space in the settings later when necessary. All persistent data is stored in the `/data` directory ([docs](https://huggingface.co/docs/hub/en/spaces-storage)).
- **Set your password**: Once the Space is created, it will require a password for logging into JupyterLab. This password is defined with the `JUPYTER_TOKEN` Space secret. If you do not define a password here, the default password is "huggingface". We recommend setting a strong password.
- **Dev Mode**: Dev Mode is a feature for Enterprise Hub subscribers that enables you to SSH into any HF Space. Activate this to connect your local VS Code for remote development on the Space's cloud hardware (this can also be switched on/off later). See the preview docs [here](https://huggingface.co/dev-mode-explorers). 
- **Private Spaces**: As an additional layer of security, we recommend setting the Space to private, so that only members of your Enterprise Organization (and of specific Resource Groups) can see it.

<div style="flex justify-center">
    <img src="https://huggingface.co/datasets/huggingface/cookbook-images/resolve/main/enterprise-jupyterlab-creation-2.png" width="450">
</div>

Once you have configured the JupyterLab Space, you can click on `Create Space`. The Space will be built and after a few seconds you will see the JupyterLab login screen. You can now login with the password you defined before. 

<div style="flex justify-center">
    <img src="https://huggingface.co/datasets/huggingface/cookbook-images/resolve/main/enterprise-jupyterlab-login.png">
</div>


### Using your JupyterLab Space

You can now work in your own JupyterLab Space in the browser! You can create your own directory structure with .ipynb notebooks or any other files and datasets in the File Browser on the left. If you have activated persistent storage, all files are permanently stored in the default `/data` directory of the Space. 

<div style="flex justify-center">
    <img src="https://huggingface.co/datasets/huggingface/cookbook-images/resolve/main/enterprise-jupyterlab-first-notebook.png">
</div>


### Dynamically switching between CPUs and GPUs

Similar to services like Google Colab, you can change the hardware the Space is running on-the-fly. We recommend doing initial setup work on the upgraded or free CPU, for example data cleaning, setting up Endpoints, or testing APIs. Once your code is set up, you can simply click on `Settings` at the top right of the Space and change to a wide selection of hardware that might be required for more compute intensive inference or training jobs. When you change hardware, the Space will restart itself and all environment variables will be lost (like with Google Colab) and you will have a new clean environment on the new hardware after some seconds. Your stored and saved files (code, data etc.) will of course also be available on the new hardware. The image below shows the available hardware at the time of writing (June 2024) and this will be updated in the future. 

In the bottom left of the image, you can also see the `Sleep time settings` where you can define how long you want the hardware to run in case of inactivity. This is a major advantage over Google Colab. If you want to save money, you can make the Space sleep after 15 minutes of inactivity, but if you need the hardware to be available for a 48 hour training run or longer, you can just prevent the Space from falling asleep and let it run for as long as you want. You can also manually `Pause` the Space and you will no longer be charged for the Space Hardware. 

<div style="flex justify-center">
    <img src="https://huggingface.co/datasets/huggingface/cookbook-images/resolve/main/enterprise-jupyterlab-hardware-options.png">
</div>

If you scroll down in the settings, you will see additional options, like expanding storage, resetting the Space, etc. In case you have not set a password during Space creation, you can also create a secret called `JUPYTER_TOKEN` here later, which will replace the default "huggingface" password.

> [!TIP]
> When you actively work with the Space over several days or weeks, files can accumulate in the storage cache. When you get a warning that the persistent storage is full and you think that the storage quota should not be reached yet, it might be helpful to factory reset the Space to empty the cache. 


### Customizing your JupyterLab Space

Remember that your JupyterLab Space is just a pre-configured Docker container, so if you are familiar with Docker, you can also customize it to your needs. For example, you can go to the `Files` section of your Space and add new requirements to the `requirements.txt` file or you can change from the default container image to another image in the `Dockerfile`, e.g. if you need a specific CUDA and PyTorch version preinstalled. 

<div style="flex justify-center">
    <img src="https://huggingface.co/datasets/huggingface/cookbook-images/resolve/main/enterprise-jupyterlab-files.png">
</div>




## Dev Mode: Develop on HF Spaces from your local VS Code

What if you don't like working in JupyterLab in the browser? Enter `Dev Mode`. `Dev Mode` enables you to SSH into any Space's hardware from a local IDE like VS Code. [HF Pro/Enterprise](https://huggingface.co/pricing) subscribers can activate `Dev Mode` for any Space in the Space's settings. 

Once `Dev Mode` is activated, you will see a pop-up at the bottom left of your JupyterLab Space's window. To SSH into your local VS Code, you first need to install the [VS Code Remote - SSH extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-ssh) locally and add your SSH key to your [HF Profile](https://huggingface.co/settings/keys). Clicking on `Connect with VS Code` should then open your local VS Code window and establish the remote connection to your Space. A similar process should be possible with any IDE that supports remote development with SSH. 

<div style="flex justify-center">
    <img src="https://huggingface.co/datasets/huggingface/cookbook-images/resolve/main/enterprise-jupyterlab-devmode-popup.png" width="450">
</div>


When connecting to your Space with SSH, your default directory will be an empty `/app` directory. You then need to change to the `/data` directory, where all your persistent files (code, data, models etc.) are stored. The `/data` directory is the only directory with guaranteed file persistance across sessions. You can find the files of your Docker container in the `HOME/user/app` directory, in case you want to modify the underlying Docker container. 

> [!TIP]
> Persisted files in the `/data` directory are currently not automatically backed up. We therefore recommend making backups of your most important files on a regular basis to avoid accidental data loss. 


## Now write some code!

That's it, you can now run a JupyterLab Space in your browser, switch between one or multiple powerful GPUs on-the-fly, and connect to the hardware from your local IDE. 

This entire recipe was written in a JupyterLab Space on a free CPU and we invite you to follow all other recipes of the Enterprise Hub Cookbook in your own JupyterLab Space. 
