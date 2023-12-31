<!--Copyright 2023 The HuggingFace Team. All rights reserved.

Licensed under the Apache License, Version 2.0 (the "License"); you may not use this file except in compliance with
the License. You may obtain a copy of the License at

http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on
an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the
specific language governing permissions and limitations under the License.
-->

# Conditional image generation

[[open-in-colab]]

Conditional image generation allows you to generate images from a text prompt. The text is converted into embeddings which are used to condition the model to generate an image from noise.

The [`DiffusionPipeline`] is the easiest way to use a pre-trained diffusion system for inference.

Start by creating an instance of [`DiffusionPipeline`] and specify which pipeline [checkpoint](https://huggingface.co/models?library=diffusers&sort=downloads) you would like to download.

In this guide, you'll use [`DiffusionPipeline`] for text-to-image generation with [`runwayml/stable-diffusion-v1-5`](https://huggingface.co/runwayml/stable-diffusion-v1-5):

```python
>>> from diffusers import DiffusionPipeline

>>> generator = DiffusionPipeline.from_pretrained("runwayml/stable-diffusion-v1-5", use_safetensors=True)
```

The [`DiffusionPipeline`] downloads and caches all modeling, tokenization, and scheduling components. 
Because the model consists of roughly 1.4 billion parameters, we strongly recommend running it on a GPU.
You can move the generator object to a GPU, just like you would in PyTorch:

```python
>>> generator.to("cuda")
```

Now you can use the `generator` on your text prompt:

```python
>>> image = generator("An image of a squirrel in Picasso style").images[0]
```

The output is by default wrapped into a [`PIL.Image`](https://pillow.readthedocs.io/en/stable/reference/Image.html?highlight=image#the-image-class) object.

You can save the image by calling:

```python
>>> image.save("image_of_squirrel_painting.png")
```

Try out the Spaces below, and feel free to play around with the guidance scale parameter to see how it affects the image quality!

<iframe
	src="https://stabilityai-stable-diffusion.hf.space"
	frameborder="0"
	width="850"
	height="500"
></iframe>