Markdown Monster offers a few simple AI based text completion features:

* Text Summarization
* Language Translation
* Grammar Checking

![](https://github.com/RickStrahl/ImageDrop/blob/master/MarkdownMonster/AiCompletionFeatures.gif?raw=true)

## Requirements and Configuration
In order to use the AI features in Markdown Monster you will to have one of the following:

* OpenAI Account
* Azure OpenAI Account
* Local Ollama Installation

For more information on configuration please see:

* [OpenAI Provider Configuration](VFPS://Topic/_6Y41CLPFE)

## AI Context Menu
All completion features are available on the Editor's context menu via the **AI** submenu:

![](/images/AiCompletion_ContextMenu.png)

The menu is context sensitive based on selection status but most options are available at all times. Note also that you can set various relevant configuration values like languages for translation, number of paragraphs used for summaries, and a quick selection of one of the configured OpenAi Providers.

> Note that the [OpenAI Configuration Window](VFPS://Topic/_6Y41CLPFE) configures both the Completion functions as well as the Image Generator. Click on **OpenAI Connection Setup...** to configure one or more providers for each AI.

## Text Summarization
Text summarization allows you to summarize either the active selection from the editor or the entire document. Click on the **Summarize Selection** or **Summarize Document** options in the context menu.  Progress and Errors are displayed on the Main Window taskbar.

A summary result is displayed in the AI Result window that shows the summary text generated and has options to paste the text into the document or to the clipboard.

![](/images/AiCompletion_TextSummary.png)

If there is no selection the text is pasted at the current location. If a selection was used Paste at Cursor will paste the text after the selected text.

## Text Translation
A number of translation features are available that allow you to:

* Translate the active Editor Selection
* Translate the document
* Generic Translation

Both selection and document translation pre-fill the text to translate and automatically translate the text when the dialog is invoked, while generic translation provides an empty source text field and you have to manually click the **Translate again** button the translate the text.

![AiCompletion Translation](/images/AiCompletion_Translation.png)

You can run multiple translations and switch languages if you choose to do so. You can also change the language prior to starting the language translation on the Context menu. The last languages are always remembered for subsequent translations.

Clicking on **Paste at Cursor** pastes the translated text after the current text selection.

## Grammar Checking
You can check grammar and style suggestions using the **Check Grammar of Selection**. This feature works by showing Grammar suggestions in a Diff Window that shows original and fixed text side by side along with an editable block of the fixed text below:

![AiCompletion CheckGrammar](/images/AiCompletion_CheckGrammar.png)

You can make changes to the text below which updates the *Checked* display on the right.

You can click the **Accept** button to apply the changes against the active selection of the original text in the editor.

> #### @icon-warning Keep Selections small
> This feature tends to be somewhat slow to process especially on larger blocks of text so we suggest you keep this to one or several paragraphs at a time. It's also easier to work with smaller checks rather than the entire document both in terms of performance as well as being able to see the changes.

## Setting Providers and Operational Settings
Providers are configured via the [Provider Configuration Window](VFPS://Topic/_6Y41CLPFE) which lets you set up multiple providers that you can easily switch between. You can use the set up dialog to create and select the active provider. 

In addition the context menu, and all of the result screens also contain drop down lists that allow you to change the provider. Any provider change you make is sticky and is remembered for the next operation. 

However any permanent changes that persist across MM sessions, require an explict **Save Settings** click on the configuration window.

Operational settings like the languages for translation, and the number of paragraphs for summarization are configurable in the context menu, and these settings are updated in real time, but like the provider settings an explicit **Save Settings** is required to persist the changes across MM sessions.

## Providers, Performance and Accuracy
Please keep in mind that the result for all of these operations are AI generated which means the following:

* Results may not be repeatable
* Results can be inaccurate 
* Different providers and Models provide very different results
* Different providers have different performance
* Large documents/selections may fail due to token size used
* Local models tend to be much slower than online models even on high end hardware


AI results are interpreted and processed dynamically and as such tend to be non-repeatable. Running the same input data most likely will produce different results. Sometimes the result variation is minor, sometimes it is not. It's not predictable.

AI is not perfect and it's possible for AI to get a completion result completely wrong. This is especially true for local SLM models which tend to be less sophisticated. 

It's possible to run local AIs using Ollama which is a local AI model engine that supports many different kinds of AI models. While it's possible and relatively easy to set up, we've found local models lacking both in performance and reliability of results compared to the online LLM OpenAI models. 

Model Recommendations:

Prefer online Models:

* OpenAI
* Azure OpenAI

The online models tend to be faster than local models and especially `gpt-4o-mini` provides consistently reliable results for all operations.

If you use Ollama and Offline Models:

* Use Ollama3 or Mistral

These two seem to work best, but even so they are slow to process and still produce some bad results including ignoring system prompt instructions on occasion.

Keep an eye on new local models that are likely going to improve - specifically Phi3.5+ which seems to be improving rapidly.