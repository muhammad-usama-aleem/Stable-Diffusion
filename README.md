# Stable-Diffusion

## Notes from "Practical Deep learning for coders: Stable Diffusion"


1. ### Classifier-Free Guidance:
    _Classifier-Free Guidance_ is a method to increase the adherence of the output to the conditioning signal we used (the text).

    Roughly speaking, the larger the guidance the more the model tries to represent the text prompt. However, large values tend to produce less diversity. The default is `7.5`, which represents a good compromise between variety and fidelity. This [blog post](https://benanne.github.io/2022/05/26/guidance.html) goes into deeper details on how it works.
    
    We can generate multiple images for the same prompt by simply passing a list of prompts instead of a string.

2. ### Negative prompts:
    _Negative prompting_ refers to the use of another prompt (instead of a completely unconditioned generation), and scaling the difference between generations of that prompt and the conditioned generation.

3. ### Image to Image:
    Even though Stable Diffusion was trained to generate images, and optionally drive the generation using text conditioning, we can use the raw image diffusion process for other tasks.

    For example, instead of starting from pure noise, we can start from an image an add a certain amount of noise to it. We are replacing the initial steps of the denoising and pretending our image is what the algorithm came up with. Then we continue the diffusion process from that state as usual.
    
    This usually preserves the composition although details may change a lot. It's great for sketches!


### Fine-tuning:
1. Textual Inversion
      Textual inversion is a process where you can quickly "teach" a new word to the text model and train its embeddings close to some visual representation. This is achieved by adding a new token to the vocabulary, freezing the weights of all the models (except the text encoder), and train with a few representative images.


2. Dreambooth:
      [Dreambooth](https://dreambooth.github.io) is a kind of fine-tuning that attempts to introduce new subjects by providing just a few images of the new subject. The goal is similar to that of [Textual Inversion](#Textual-Inversion), but the process is different. Instead of creating a new token as Textual Inversion does, we select an existing token in the vocabulary (usually a rarely used one), and fine-tune the model for a few hundred steps to bring that token close to the images we provide. This is a regular fine-tuning process in which all modules are unfrozen.

