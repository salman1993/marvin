# Extracting entities from images

Marvin can use OpenAI's vision API to process images and convert them into structured data, transforming unstructured information into native types that are appropriate for a variety of programmatic use cases.

The `marvin.beta.extract` function is an enhanced version of `marvin.extract` that accepts images as well as text.


!!! tip "Beta"
    Please note that vision support in Marvin is still in beta, as OpenAI has not finalized the vision API yet. While it works as expected, it is subject to change.

<div class="admonition abstract">
  <p class="admonition-title">What it does</p>
  <p>
    The beta <code>extract</code> function can extract entities from images and text.
  </p>
</div>


<div class="admonition info">
  <p class="admonition-title">How it works</p>
  <p>
    
  This involves a two-step process: first, a caption is generated for the image that is aligned with the structuring goal. Next, the actual extract operation is performed with an LLM.

  </p>
</div>



!!! example "Example: identifying dogs"

    We will extract the breed of each dog in this image:

    ![](https://images.unsplash.com/photo-1548199973-03cce0bbc87b?)

    
    ```python
    import marvin
    
    img = marvin.beta.Image(
        "https://images.unsplash.com/photo-1548199973-03cce0bbc87b?",
    )

    result = marvin.beta.extract(img, target=str, instructions="dog breeds")
    ```

    !!! success "Result"
        ```python
        result == ["Pembroke Welsh Corgi", "Yorkshire Terrier"]
        ```    

## Model parameters
You can pass parameters to the underlying API via the `model_kwargs` and `vision_model_kwargs` arguments of `extract`. These parameters are passed directly to the respective APIs, so you can use any supported parameter.


## Async support
If you are using Marvin in an async environment, you can use `extract_async`:
  
```python
result = await marvin.beta.extract_async(
    "I drove from New York to California.",
    target=str,
    instructions="2-letter state codes",
) 

assert result == ["NY", "CA"]
```