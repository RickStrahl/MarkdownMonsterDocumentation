Markdown Monster has support for AI Image Generation via OpenAI or Azure OpenAI using **Dall-E-3** by using the **OpenAI Image Addin** from the toolbar.

You can provide a description of an image to create, and the OpenAI API generated an image. You can take that image and embed it into your document, copy it to clipboard, or open it in an image viewer, editor or a Web Browser. 

The addin keeps track of recently generated images for later review and you can easily re-run, or tweak the prompt and re-run the image generation, using either the original prompt or the AI revised prompt.

Here's what Image Generator Addin UI looks like:

![](/images/OpenAiImageGeneration.jpg)

Images are saved on disk, so you can go back and review previously generated images and pull up both the saved image, the original entered prompt as well as the AI revised prompt. This allows easy reuse of the saved images, as well as using the saved prompts to create similar new generated images.

### First Time Startup: The OpenAI Configuration Form
When you first start the Image Generator it pops up the OpenAI API Configuration form, as you'll need to provide an API key to get started. Choose the AI Provider from **OpenAI** or **Azure OpenAI**, and then fill in the API key and for Azure the API Key and deployment Web Site Url.

The form has quick links for signup, API keys and pricing:

![OpenAI Configuration Form](/images/OpenAiConfiguration.png)

> #### @icon-info-circle OpenAI or Azure OpenAI API  Key Required
> In order to use the image generation feature in Markdown Monster, you need to have an API Key from OpenAI or Azure OpenAI. You can [sign up for an account](https://platform.openai.com/signup) or log in and grab your API key from the [Api Keys page](https://platform.openai.com/api-keys). When you first sign up you get some free credits, and after that [pricing](https://openai.com/pricing) is reasonable for a good amount of image generations.

Once you have the key entered, you can provide a few optional defaults for image generation and you're on your way generating images.

### The Image Generation Form
The image generation form contains 4 areas:

* The prompt
* Generation options
* Generated Image Display (or preview of previous images)
* And a list of previously generated images

The process to create images is simple:

* Enter a prompt description for the image to generate
* Optionally change generation options
* Press the Go button (`ctrl-enter`) 

The generator takes a while to generate the image (typically 15-20 seconds or so) and when done displays the image in the preview display area.

Once the image has been generated you can:

* Embed the image into the Markdown Document at the cursor
* Save the image to a new file
* Copy the image to the Clipboard
* Open the image in your configured Image Editor
* Open the image in Explorer
* Open the image in your Web Browser
* Delete the image

> **Note**: Each image generation incurs a small charge at the OpenAI provider (ie. OpenAI or Azure) using your account you used for registration.

### The Saved Image Strip
Once an image has been created it's added to the list of saved images which is shown on the bottom of the form as an image strip. You can scroll through the list and click on any image to display it and the prompt in the previewer. You can re-generate a new image from the prompt by pressing the **Go** button.

The previewer also has a context menu with all the actions described above available on the saved images.

> #### @icon-info-circle No Two generated Images are the Same
> Be aware that no two Image Generation requests will produce the same or even very similar results! So don't be surprised if you 're-run' a previously saved prompt and get a totally different result.  
>
> If you get an image result that works for you, you can use the **Revised Prompt** to get additional images generated that more closely match the original.

> #### @icon-info-circle Be Descriptive!
> AI generated images tend to be very random and its important to be as specific as you can be in your image prompt description to produce results that match your expectations. Even with that you may still have to try many iterations to produce an acceptable result - rarely do you end up with a perfect image on the first try. Typically you run a prompt and figure out ways to refine the query to make it more specific. 

### Re-running Prompts
Once an image has been created you can re-run the prompt to create additional images. When you re-run prompts **a new prompt with all associated settings is created** and saved in the Recent Images list. IOW, you can re-run an existing prompt, and it will automatically make a copy, so the original prompt is never lost unless you explicitly delete it.

> You can also modify an existing prompt and run it, without modifying an existing prompt. The prompt input is always a copy, so you can make any changes you like and then run the prompt again without affecting the original image or prompt that you started from.

Because image generation is always random and can produce variable results it's very common to run a single prompt or slight variations thereof many times before getting a good image result and it's quick and easy to do so by just pressing the **Go** button again to produce a new prompt and image.

> #### @icon-info-circle Take Advantage of the Revised Prompt for Re-Rendering
>Image generation returns both an image and a *revised prompt* which indicates how the AI interpreted your initial prompt.  
> This revised prompt probably is much more specific than your entered prompt and if you want to produce similar variations, using the revised prompt often produces more closely related images.