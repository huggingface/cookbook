# Open-Source AI Cookbook

This repo contains community-driven practical examples of building AI applications and solving various tasks with AI 
using open-source tools and models. 

## Contributing to the cookbook

Everyone is welcome to contribute, and we value everybody's contribution! There are several ways you can contribute to 
the [Open-Source AI Cookbook](https://huggingface.co/learn/cookbook/index):

* Submit an idea for a desired example/guide via [GitHub Issues](https://github.com/huggingface/cookbook/issues).
* Contribute a new notebook with a practical example.
* Improve existing examples by fixing issues/typos. 

Before contributing, check currently [open issues](https://github.com/huggingface/cookbook/issues) and
[pull requests](https://github.com/huggingface/cookbook/pulls) to avoid working on something that someone else is
already working on.

After you contribute, feel free to ask for a request to join to [this organization](https://huggingface.co/huggingcooks) to claim the badge. 🏅

### What makes a good Cookbook notebook?

We believe that the Cookbook will be the most beneficial for everyone in the community if the Jupyter notebooks have the 
following qualities: 

* *Practical*: Your notebook should provide an illustration of an end-to-end project or a specific aspect of AI development. Aim for real-world applications, but try to avoid overcomplicating. Clearly explain the objectives, challenges and steps involved.
* *Build with open-source tools and models*: Utilize open source libraries, datasets, and pre-trained models available under permissive licenses. Include links to all resources used within the notebook.
* *Clearly written*: Ensure your writing is clear, concise, and free from grammatical errors. Maintain a friendly and approachable tone throughout the notebook. Explain the steps you take to solve a problem, challenges, alternative approaches.
* *Executes without errors*: Test your notebook to avoid runtime errors. 
* *Adds to existing "recipes"*: Before submitting, review existing notebooks to confirm that the subject hasn't been covered yet. We welcome diverse use cases, modalities, techniques, and approaches! 

### Creating a pull request

To contribute a new example/guide, open a pull request, and tag @merveenoyan and @stevhliu.

Here are some tips:

* Make sure that your notebook's file name is in lowercase.
* Don't forget to add your notebook to the `_toctree.yml` and to `index.md`.
* Right after the notebook's first header, add yourself as an author like this: `_Authored by: [Aymeric Roucher](https://huggingface.co/m-ric)_`. You can link to your Hugging Face profile, or to your GitHub profile.
* Remove non-informative code cell outputs (e.g. from `pip install`). Make sure the notebook doesn't contain any empty code cells.
* If using any images in the markdown, upload them to the [huggingface/cookbook-images](https://huggingface.co/datasets/huggingface/cookbook-images) dataset. Then use the link to the image in your markdown, e.g.:
```![RAG diagram](https://huggingface.co/datasets/huggingface/cookbook-images/resolve/main/rag-diagram.png)```

Once your pull request is merged, the notebook will show up in the [Open-Source AI Cookbook](https://hf.co/learn/cookbook).

### Translating the Cookbook into your language

We'd love to have the Cookbook to be available in many more languages! Please follow the steps below if you'd like to 
help translate the notebooks into your language 🙏.

If some of the notebooks have already been translated into your language, add new translated notebooks 
under `notebooks/your_language`. Don't forget to add the new translated notebook to `notebooks/your_language/_toctree.yml`,
and to `notebooks/your_language/index.md`.

If the notebooks have not yet been translated to your language, create a directory under `notebooks` with your `LANG-ID` 
(e.g. see `en` for English, `zh-CN` for Chinese). The `LANG-ID` should be ISO 639-1 (two lower case letters) language 
code -- see [here](https://www.loc.gov/standards/iso639-2/php/code_list.php) for reference. Alternatively, 
`{two lowercase letters}-{two uppercase letters}` format is also supported, e.g. `zh-CN`.

Create the `notebooks/LANG-ID/_toctree.yml`, and `notebooks/LANG-ID/index.md`, and add the translated notebook.

Finally, add your language code (the exact same `LANG-ID`) to the `build_documentation.yml` and `build_pr_documentation.yml` 
files in the `.github/workflows` folder.
