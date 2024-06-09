
# Interactive Development In HF Spaces

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

<div style="text-align: center;">
    <img src="https://cdn-lfs-us-1.huggingface.co/repos/13/3d/133d8ca2460bf82ba2bdbe928d91a6c780364a6d0cf9005087db081cca492c02/4b119b0ae20e55127488b1f0317413b36491936696b354bd8d1012ea28a1e06f?response-content-disposition=inline%3B+filename*%3DUTF-8%27%27enterprise-jupyterlab-creation-1.png%3B+filename%3D%22enterprise-jupyterlab-creation-1.png%22%3B&response-content-type=image%2Fpng&Expires=1717861243&Policy=eyJTdGF0ZW1lbnQiOlt7IkNvbmRpdGlvbiI6eyJEYXRlTGVzc1RoYW4iOnsiQVdTOkVwb2NoVGltZSI6MTcxNzg2MTI0M319LCJSZXNvdXJjZSI6Imh0dHBzOi8vY2RuLWxmcy11cy0xLmh1Z2dpbmdmYWNlLmNvL3JlcG9zLzEzLzNkLzEzM2Q4Y2EyNDYwYmY4MmJhMmJkYmU5MjhkOTFhNmM3ODAzNjRhNmQwY2Y5MDA1MDg3ZGIwODFjY2E0OTJjMDIvNGIxMTliMGFlMjBlNTUxMjc0ODhiMWYwMzE3NDEzYjM2NDkxOTM2Njk2YjM1NGJkOGQxMDEyZWEyOGExZTA2Zj9yZXNwb25zZS1jb250ZW50LWRpc3Bvc2l0aW9uPSomcmVzcG9uc2UtY29udGVudC10eXBlPSoifV19&Signature=G3L195ww4hShsdRVo6hXSQ9kXvfJ0S73l4ifLsRoSCmPHVp7GUbDbtFiWakrJVuDVjXYEWGb7zbGDxoVLdIhEE04OmNLPFo6bxjAiktN-Gb5qPUJUq4NkZAtvrI2kMep0bSwbx4Ua8nvXQDfRXJ8K7J0FXXczRAYw2VQS9avEqTdD7l1Vgp7vIM6NXhuU4fClKkQf2XNdIxAFLEsrwT8O0KrEBE46Lemj6J6gixqLz5VL6la5QZf3gJEwhd7CZSkYAFUGs8w1BtliuVvqIc0YktD1tK338WIlYTQ6KgBgnRYcZaZa3pjmv0M-BzFXGth-60Y68TsQQAML024kuL-4w__&Key-Pair-Id=KCD77M1F0VK2B" width="450">  
</div>

- **Choosing your hardware**: You can choose from a wide range of hardware from free CPUs to A100 GPUs. When setting up the Space, we recommend you choose the free basic CPU. You can switch to better paid hardware once you need it (see available hardware and prices [here](https://huggingface.co/pricing)). 
- **Persistent storage**: It is important to attach persistent storage to the Space, so that all the files you create (code, models, data) are also saved when the Space is paused or reset. You can always increase the disk space in the settings later when necessary. All persistent data is stored in the `/data` directory ([docs](https://huggingface.co/docs/hub/en/spaces-storage)).
- **Set your password**: Once the Space is created, it will require a password for logging into JupyterLab. This password is defined with the `JUPYTER_TOKEN` Space secret. If you do not define a password here, the default password is "huggingface". We recommend setting a strong password.
- **Dev Mode**: Dev Mode is a feature for Enterprise Hub subscribers that enables you to SSH into any HF Space. Activate this to connect your local VS Code for remote development on the Space's cloud hardware (this can also be switched on/off later). See the preview docs [here](https://huggingface.co/dev-mode-explorers). 
- **Private Spaces**: As an additional layer of security, we recommend setting the Space to private, so that only members of your Enterprise Organization (and of specific Resource Groups) can see it.

<div style="text-align: center;">
    <img src="https://cdn-lfs-us-1.huggingface.co/repos/13/3d/133d8ca2460bf82ba2bdbe928d91a6c780364a6d0cf9005087db081cca492c02/1e42e3e8dfe4dd4d305067ba92f14d5ccdc437ccec0eece581258ea465959527?response-content-disposition=inline%3B+filename*%3DUTF-8%27%27enterprise-jupyterlab-creation-2.png%3B+filename%3D%22enterprise-jupyterlab-creation-2.png%22%3B&response-content-type=image%2Fpng&Expires=1717861295&Policy=eyJTdGF0ZW1lbnQiOlt7IkNvbmRpdGlvbiI6eyJEYXRlTGVzc1RoYW4iOnsiQVdTOkVwb2NoVGltZSI6MTcxNzg2MTI5NX19LCJSZXNvdXJjZSI6Imh0dHBzOi8vY2RuLWxmcy11cy0xLmh1Z2dpbmdmYWNlLmNvL3JlcG9zLzEzLzNkLzEzM2Q4Y2EyNDYwYmY4MmJhMmJkYmU5MjhkOTFhNmM3ODAzNjRhNmQwY2Y5MDA1MDg3ZGIwODFjY2E0OTJjMDIvMWU0MmUzZThkZmU0ZGQ0ZDMwNTA2N2JhOTJmMTRkNWNjZGM0MzdjY2VjMGVlY2U1ODEyNThlYTQ2NTk1OTUyNz9yZXNwb25zZS1jb250ZW50LWRpc3Bvc2l0aW9uPSomcmVzcG9uc2UtY29udGVudC10eXBlPSoifV19&Signature=ZzRr23ruwyHpUopApGTt6Rab7gndileIqyK6VeX29A7LrJgrxhFfvc7KDcDQfDioegJXStjnjjhATlbwX4DLX-jF5Z-bPsybsHtgoaGjSY3f9hNrg9SrzpeKaesZctiFzHfCNIIABRVJqX4b%7EPFDM0sZCNVSXK4iA2p1p2SYvTWh4%7EDoL6Sd4urtRur9ZTvRV1s%7EX6kyhWgUphiF1HwixS6weKkLD4iIS8ZmNo6fnOEdMDLNRuWkBE9t0ksVZ3k2zxIeGbkgSE4-9xQz18JssjaVr5KlXXcemV2hrzP-GzSK2fiHoiwja%7EDZqfpiDE5bl%7EuGal-LABAjjtOtiyppQQ__&Key-Pair-Id=KCD77M1F0VK2B" width="450">
</div>

Once you have configured the JupyterLab Space, you can click on `Create Space`. The Space will be built and after a few seconds you will see the JupyterLab login screen. You can now login with the password you defined before. 

<div style="text-align: center;">
    <img src="https://cdn-lfs-us-1.huggingface.co/repos/13/3d/133d8ca2460bf82ba2bdbe928d91a6c780364a6d0cf9005087db081cca492c02/063fa68890553c1a1cd44555f3a835222a35d50936e2f6a5d77a7b03bf3ea0bf?response-content-disposition=inline%3B+filename*%3DUTF-8%27%27enterprise-jupyterlab-login.png%3B+filename%3D%22enterprise-jupyterlab-login.png%22%3B&response-content-type=image%2Fpng&Expires=1717861340&Policy=eyJTdGF0ZW1lbnQiOlt7IkNvbmRpdGlvbiI6eyJEYXRlTGVzc1RoYW4iOnsiQVdTOkVwb2NoVGltZSI6MTcxNzg2MTM0MH19LCJSZXNvdXJjZSI6Imh0dHBzOi8vY2RuLWxmcy11cy0xLmh1Z2dpbmdmYWNlLmNvL3JlcG9zLzEzLzNkLzEzM2Q4Y2EyNDYwYmY4MmJhMmJkYmU5MjhkOTFhNmM3ODAzNjRhNmQwY2Y5MDA1MDg3ZGIwODFjY2E0OTJjMDIvMDYzZmE2ODg5MDU1M2MxYTFjZDQ0NTU1ZjNhODM1MjIyYTM1ZDUwOTM2ZTJmNmE1ZDc3YTdiMDNiZjNlYTBiZj9yZXNwb25zZS1jb250ZW50LWRpc3Bvc2l0aW9uPSomcmVzcG9uc2UtY29udGVudC10eXBlPSoifV19&Signature=D9z64AMRDQ13S6z5Dm-NwCTPCqf04131WA8ccrhUAb4ervq7hSK%7EBdb7AAf8CCy2%7ErrS4WvghzT1otb9DO6gDPKAPY4ZmXBkcgowyrJepz59GVsLswquC%7EzhERc6KH8wJUEWnJGubeEUC13zgloOBRoau28SavFywF12t8dKbX5bwAKr0Cc6IPktHdeL7hkiDZND40Ep2h1EnXyNtEiSqssvvfEb7py1tDsfdfxILe537-Ufr3u6k3%7Eop7CQO3cbsf7DIuxS64BprhOE5L82P4tfnBF0EVxSqEei%7E7g2j5J-DrH%7EgXKlR6bNa0FiOewgA5JRzPvxXox39v3Cd3Eerw__&Key-Pair-Id=KCD77M1F0VK2B">
</div>


### Using your JupyterLab Space

You can now work in your own JupyterLab Space in the browser! You can create your own directory structure with .ipynb notebooks or any other files and datasets in the File Browser on the left. If you have activated persistent storage, all files are permanently stored in the default `/data` directory of the Space. 

<div style="text-align: center;">
    <img src="https://cdn-lfs-us-1.huggingface.co/repos/13/3d/133d8ca2460bf82ba2bdbe928d91a6c780364a6d0cf9005087db081cca492c02/f21f543fbd3c22cdc6d160bee065060836b0cc505a6724fdbf6b0bc6e280d6cd?response-content-disposition=inline%3B+filename*%3DUTF-8%27%27enterprise-jupyterlab-first-notebook.png%3B+filename%3D%22enterprise-jupyterlab-first-notebook.png%22%3B&response-content-type=image%2Fpng&Expires=1717861438&Policy=eyJTdGF0ZW1lbnQiOlt7IkNvbmRpdGlvbiI6eyJEYXRlTGVzc1RoYW4iOnsiQVdTOkVwb2NoVGltZSI6MTcxNzg2MTQzOH19LCJSZXNvdXJjZSI6Imh0dHBzOi8vY2RuLWxmcy11cy0xLmh1Z2dpbmdmYWNlLmNvL3JlcG9zLzEzLzNkLzEzM2Q4Y2EyNDYwYmY4MmJhMmJkYmU5MjhkOTFhNmM3ODAzNjRhNmQwY2Y5MDA1MDg3ZGIwODFjY2E0OTJjMDIvZjIxZjU0M2ZiZDNjMjJjZGM2ZDE2MGJlZTA2NTA2MDgzNmIwY2M1MDVhNjcyNGZkYmY2YjBiYzZlMjgwZDZjZD9yZXNwb25zZS1jb250ZW50LWRpc3Bvc2l0aW9uPSomcmVzcG9uc2UtY29udGVudC10eXBlPSoifV19&Signature=FiU6p-3BSvjMHNAwfnmof9J6lh7X37N7Fk9JHdBXT3mjDT3C7N4hLmY6jTCER56FnJBF74NpHiP10YG4ybvuvL%7EjDzZ9RPKXOv-gRCcwYBb7v8uJPJjLU7YP1YdTXF-ir4mr0C4K40IgOpLjdlXUKTr01cupUtRMox-xesX3Z3D5AfAViNTd1tXLE-9KaeupBHZyfeNGS-M2vunfR%7EWKdVVAyLxSaET5VNxLzLKj8EHzGnwBq6Ckd0cLpHNg39shnu0UCwg7Xvwzhx2aOxWsYSfVc-T9%7Ev-iXy1hiBg08%7EQ4mD-jLzNz1LhEnH83RMOeh4MMjARl4mL7%7ESJn1cnreQ__&Key-Pair-Id=KCD77M1F0VK2B">
</div>


### Dynamically switching between CPUs and GPUs

Similar to services like Google Colab, you can change the hardware the Space is running on-the-fly. We recommend doing initial setup work on the upgraded or free CPU, for example data cleaning, setting up Endpoints, or testing APIs. Once your code is set up, you can simply click on `Settings` at the top right of the Space and change to a wide selection of hardware that might be required for more compute intensive inference or training jobs. When you change hardware, the Space will restart itself and all environment variables will be lost (like with Google Colab) and you will have a new clean environment on the new hardware after some seconds. Your stored and saved files (code, data etc.) will of course also be available on the new hardware. The image below shows the available hardware at the time of writing (June 2024) and this will be updated in the future. 

In the bottom left of the image, you can also see the `Sleep time settings` where you can define how long you want the hardware to run in case of inactivity. This is a major advantage over Google Colab. If you want to save money, you can make the Space sleep after 15 minutes of inactivity, but if you need the hardware to be available for a 48 hour training run or longer, you can just prevent the Space from falling asleep and let it run for as long as you want. You can also manually `Pause` the Space and you will no longer be charged for the Space Hardware. 

<div style="text-align: center;">
    <img src="https://cdn-lfs-us-1.huggingface.co/repos/13/3d/133d8ca2460bf82ba2bdbe928d91a6c780364a6d0cf9005087db081cca492c02/ce651a2be35a88878755f41531c877b50ba194fce0971397010e2271904bbf39?response-content-disposition=inline%3B+filename*%3DUTF-8%27%27enterprise-jupyterlab-hardware-options.png%3B+filename%3D%22enterprise-jupyterlab-hardware-options.png%22%3B&response-content-type=image%2Fpng&Expires=1717920105&Policy=eyJTdGF0ZW1lbnQiOlt7IkNvbmRpdGlvbiI6eyJEYXRlTGVzc1RoYW4iOnsiQVdTOkVwb2NoVGltZSI6MTcxNzkyMDEwNX19LCJSZXNvdXJjZSI6Imh0dHBzOi8vY2RuLWxmcy11cy0xLmh1Z2dpbmdmYWNlLmNvL3JlcG9zLzEzLzNkLzEzM2Q4Y2EyNDYwYmY4MmJhMmJkYmU5MjhkOTFhNmM3ODAzNjRhNmQwY2Y5MDA1MDg3ZGIwODFjY2E0OTJjMDIvY2U2NTFhMmJlMzVhODg4Nzg3NTVmNDE1MzFjODc3YjUwYmExOTRmY2UwOTcxMzk3MDEwZTIyNzE5MDRiYmYzOT9yZXNwb25zZS1jb250ZW50LWRpc3Bvc2l0aW9uPSomcmVzcG9uc2UtY29udGVudC10eXBlPSoifV19&Signature=Ye2vpEAbFaQuVTru4iLEQncnF4VzON9mAEmkJqjyJQy9J0S4kA%7EtO3O3LwWFVHOT2esYGDjG1re0lwYLG3mft1lxieoJbm5vuwIPNELMSa-Vb3e7bA6ZuOcisklEoTwpRi0aQcKa6NlWoF3rNDFLwmLdZVQNHvFKCee6%7E0wiRol-znACCk-7uIoJ7dclyRmVmUgdsgskVfSVIXDYVZH%7EQyA5yH4AhNIwQhb5gNjhVZq0OG%7EbmCGkdszhLVD5ljw4E6Lage5kr1ID8owZFNI62jKbNHvIJS-MM0WtN3iu0zCt9mv28Py0A-UKDrBmbSvJQuCwvcRAlhjiLUPyApct2g__&Key-Pair-Id=KCD77M1F0VK2B">
</div>

If you scroll down in the settings, you will see additional options, like expanding storage, resetting the Space, etc. In case you have not set a password during Space creation, you can also create a secret called `JUPYTER_TOKEN` here later, which will replace the default "huggingface" password.

> [!TIP]
> When you actively work with the Space over several days or weeks, files can accumulate in the storage cache. When you get a warning that the persistent storage is full and you think that the storage quota should not be reached yet, it might be helpful to factory reset the Space to empty the cache. 


### Customizing your JupyterLab Space

Remember that your JupyterLab Space is just a pre-configured Docker container, so if you are familiar with Docker, you can also customize it to your needs. For example, you can go to the `Files` section of your Space and add new requirements to the `requirements.txt` file or you can change from the default container image to another image in the `Dockerfile`, e.g. if you need a specific CUDA and PyTorch version preinstalled. 

<div style="text-align: center;">
    <img src="https://cdn-lfs-us-1.huggingface.co/repos/13/3d/133d8ca2460bf82ba2bdbe928d91a6c780364a6d0cf9005087db081cca492c02/815b9d20b9c241eb0463b758785e105747b119cef3376bf2d8ba88b2f8a6aaf7?response-content-disposition=inline%3B+filename*%3DUTF-8%27%27enterprise-jupyterlab-files.png%3B+filename%3D%22enterprise-jupyterlab-files.png%22%3B&response-content-type=image%2Fpng&Expires=1717862111&Policy=eyJTdGF0ZW1lbnQiOlt7IkNvbmRpdGlvbiI6eyJEYXRlTGVzc1RoYW4iOnsiQVdTOkVwb2NoVGltZSI6MTcxNzg2MjExMX19LCJSZXNvdXJjZSI6Imh0dHBzOi8vY2RuLWxmcy11cy0xLmh1Z2dpbmdmYWNlLmNvL3JlcG9zLzEzLzNkLzEzM2Q4Y2EyNDYwYmY4MmJhMmJkYmU5MjhkOTFhNmM3ODAzNjRhNmQwY2Y5MDA1MDg3ZGIwODFjY2E0OTJjMDIvODE1YjlkMjBiOWMyNDFlYjA0NjNiNzU4Nzg1ZTEwNTc0N2IxMTljZWYzMzc2YmYyZDhiYTg4YjJmOGE2YWFmNz9yZXNwb25zZS1jb250ZW50LWRpc3Bvc2l0aW9uPSomcmVzcG9uc2UtY29udGVudC10eXBlPSoifV19&Signature=RPiojDTwLVObSt1SWrZ9b5qLQW147kRygV8UeuH1le9I77OFI0HLK9F3yka5a4DaQG23HUIn24KbOT6ArM%7EcIuk79ZpONLdZXO9yaMC0MQcoZdj2I8tmpzJITZ115tWjfjIi53Mg-M50E4GUF8uo9eSAWjsNn2SV9OJRnML-tw9kOA%7Ettjn7aSKvcekmpacA23TSo1MI5vsuhQFbrtiDG0G92OqMfCTIVRfaM%7E2oKWHOb3ShjEwQJ3yiJytlkUAGyziNM6amHF4ZoacYQmfih6YcQceDoIm-5hkoLBEatgehua9Hx3kfdiE4wWQn42mPINCoJjpvswXd4XOVrSNp3w__&Key-Pair-Id=KCD77M1F0VK2B">
</div>




## Dev Mode: Develop on HF Spaces from your local VS Code

What if you don't like working in JupyterLab in the browser? Enter `Dev Mode`. `Dev Mode` enables you to SSH into any Space's hardware from a local IDE like VS Code. [HF Pro/Enterprise](https://huggingface.co/pricing) subscribers can activate `Dev Mode` for any Space in the Space's settings. 

Once `Dev Mode` is activated, you will see a pop-up at the bottom left of your JupyterLab Space's window. To SSH into your local VS Code, you first need to install the [VS Code Remote - SSH extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-ssh) locally and add your SSH key to your [HF Profile](https://huggingface.co/settings/keys). Clicking on `Connect with VS Code` should then open your local VS Code window and establish the remote connection to your Space. A similar process should be possible with any IDE that supports remote development with SSH. 

<div style="text-align: center;">
    <img src="https://cdn-lfs-us-1.huggingface.co/repos/13/3d/133d8ca2460bf82ba2bdbe928d91a6c780364a6d0cf9005087db081cca492c02/f462b2fa4e25380194c0cf062f1e68d50290d6b1737b357449622491fe756474?response-content-disposition=inline%3B+filename*%3DUTF-8%27%27enterprise-jupyterlab-devmode-popup.png%3B+filename%3D%22enterprise-jupyterlab-devmode-popup.png%22%3B&response-content-type=image%2Fpng&Expires=1717923752&Policy=eyJTdGF0ZW1lbnQiOlt7IkNvbmRpdGlvbiI6eyJEYXRlTGVzc1RoYW4iOnsiQVdTOkVwb2NoVGltZSI6MTcxNzkyMzc1Mn19LCJSZXNvdXJjZSI6Imh0dHBzOi8vY2RuLWxmcy11cy0xLmh1Z2dpbmdmYWNlLmNvL3JlcG9zLzEzLzNkLzEzM2Q4Y2EyNDYwYmY4MmJhMmJkYmU5MjhkOTFhNmM3ODAzNjRhNmQwY2Y5MDA1MDg3ZGIwODFjY2E0OTJjMDIvZjQ2MmIyZmE0ZTI1MzgwMTk0YzBjZjA2MmYxZTY4ZDUwMjkwZDZiMTczN2IzNTc0NDk2MjI0OTFmZTc1NjQ3ND9yZXNwb25zZS1jb250ZW50LWRpc3Bvc2l0aW9uPSomcmVzcG9uc2UtY29udGVudC10eXBlPSoifV19&Signature=eAC0IDJcfic%7EUilq-aHshD5ygR7NYWsTa%7ELBhSu%7EPxfL2BL-0dTL1mgJ5QdQfSEldkszgPb0KaKBJaE-071G9aWHRWJXKLN0eodo%7EsfTchKLIZwBgT-KWwRyRouEqCrc-qquGkTWR3VWc5YwKwsoe2Eg1J2Ft-P-brR%7EguRouQo%7EONPqhvLrGwtHkv-hD-qJ8TIBHq%7EkrUuw65AH8oV9dYLJ8rug4gbNu0z9oAv7XbLku5RUlWLi1EhHyrNTq9-RYpXURu%7E0wZx-ip9E7S8yQcYHIh5%7EJdJ-l32KszUAzkmfAEcUIjk4yDQtzna2MW7Db4BbeDbttYBYQ2kT-swQmQ__&Key-Pair-Id=KCD77M1F0VK2B" width="450">
</div>


When connecting to your Space with SSH, your default directory will be an empty `/app` directory. You then need to change to the `/data` directory, where all your persistent files (code, data, models etc.) are stored. The `/data` directory is the only directory with guaranteed file persistance across sessions. You can find the files of your Docker container in the `HOME/user/app` directory, in case you want to modify the underlying Docker container. 

> [!TIP]
> Persisted files in the `/data` directory are currently not automatically backed up. We therefore recommend making backups of your most important files on a regular basis to avoid accidental data loss. 


## Now write some code!

That's it, you can now run a JupyterLab Space in your browser, switch between one or multiple powerful GPUs on-the-fly, and connect to the hardware from your local IDE. 

This entire recipe was written in a JupyterLab Space on a free CPU and we invite you to follow all other recipes of the Enterprise Hub Cookbook in your own JupyterLab Space. 
