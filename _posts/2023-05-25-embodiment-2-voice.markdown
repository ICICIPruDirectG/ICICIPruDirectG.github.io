---
layout: post
title: "Embodiment - Part 2"
date: 2023-05-26 00:00:00 -0000
categories: Embodiment D-ID TorToiSe ai-voice-cloning StableDiffusion SadTalker
---

# Embodiment - Part 2

## Speaking voice synthesis AI

Since my initial go at this, [TorToiSe-TTS](https://git.ecker.tech/mrq/tortoise-tts) had become [AI Voice Cloning](https://git.ecker.tech/mrq/ai-voice-cloning).
I have been able to install it locally and use it to train and fine-tune a speaking voice AI, which I will now present to you:

<table border="0">
 <tr>
    <td><b style="font-size:30px">TorToiSe-TTS</b></td>
    <td><b style="font-size:30px">AI Voice Cloning</b></td>
 </tr>
 <tr>
   <td>
   <video
    src="{{site.url}}/assets/YYYP_Karin-HermitageMiku-Maxim378.mp4"
    width="512"
    height="512"
    preload='none'
    controls>
  Your browser does not support the video element
  </video>
   <div>We give advice, but we cannot give the wisdom to profit by it.</div>
  </td>
  <td>
  <video
    src="{{site.url}}/assets/Karin1245-CourtMiku-Maxim9-1216.mp4"
    width="512"
    height="512"
    preload='none'
    controls>
  Your browser does not support the video element
  </video>
  <div>The passions possess a certain injustice and self interest which makes it dangerous to follow them,
and in reality we should distrust them even when they appear most trustworthy.</div>
  </td>
 </tr>
</table>

### Installation
 
I am running Windows 11, Powershell, pyenv w/3.10.5.
What this means for AI Voice Cleanup is that I had to comment out all the venv commands and let it rely on pyenv managed python:

in `setup-cuda.bat` - a script you should run after cloning the repo
```
:: python -m venv venv
:: call .\venv\Scripts\activate.bat
```

in `start.bat` - a script you should run to start the WebUI
```
::call .\venv\Scripts\activate.bat
```

and in `train.bat` - a script that will be invoked when you are fine-tuning
```
:: call .\venv\Scripts\activate.bat
```

Let me know if you run into any setup issues - I will put it here in this post.

### Spoken Voice AI

#### Samples

In order to train the voice model, you need a small number of short, clear and representative samples of the voice.
Because I wanted to amplify the synthetic part of voice synthesis, I have chosen to use 4 10~13 second clips from a vocal track in a song produced with the [SynthV Karin](https://www.ah-soft.com/karin/) vociebank.

> I want to take a moment to appreciate the song's producer: ゆよゆっぺ (Yuyoyuppe) - he is one of my favorites,
because for his technicality, musicality and the debt of gratitude I owe him for his collabs with 花たん (Hanatan), who in her own right is a talented vocalist with immense range.
If you are into such things, please join me in supporting them with your attention and money.

The song - ["Datte"](https://www.youtube.com/watch?v=0MKomCQ_KSA) which I have acquired through digital download already includes the vocal track separately, so it was easy to open it with [Audacity](https://www.audacityteam.org/) and choose which segments I felt matched the aesthetic I wanted to imitate.
TorToiSe-TTS gives this guidance for samples:

1. Good sources are YouTube interviews (you can use youtube-dl to fetch the audio), audiobooks or podcasts.
2. Cut your clips into ~10 second segments.
You want at least 3 clips.
More is better, but I only experimented with up to 5 in my testing.
3. Save the clips as a WAV file with floating point format and a 22,050 sample rate.
4. Avoid clips with background music, noise or reverb.
These clips were removed from the training dataset.
Tortoise is unlikely to do well with them.
5. Avoid speeches. These generally have distortion caused by the amplification system.
6. Avoid clips from phone calls.
7. Avoid clips that have excessive stuttering, stammering or words like "uh" or "like" in them.
8. Try to find clips that are spoken in such a way as you wish your output to sound like.
For example, if you want to hear your target voice read an audiobook, try to find clips of them reading a book.
9. The text being spoken in the clips does not matter, but diverse text does seem to perform better.

TorToiSe-TTS is also open about it's limitations:

1. It is primarily good at reading books and speaking poetry.
Other forms of speech do not work well.
2. It was trained on a dataset which does not have the voices of public figures.
While it will attempt to mimic these voices if they are provided as references, it does not do so in such a way that most humans would be fooled.

For my use case - creating comfy spoken word synthesis and internationalization, this would do just fine.

> The interesting part here is that I have trained an English voice model from Japanese samples. 
It's possible because in my layman's understanding, this technology relies on matching the sounds of speech to known sub-word particles, or tokens, and then composing new words out of them.

> This technology adds a fun new dimension to the usual subs vs dubs meta, doesn't it?
I want you to share my excitement here - listen:
I wager it would go big because it would open new markets for Hollywood -
it allows the (filthy illiterate uncultured) original audio disrespecteres to have a much better experience with foreign media.
And then it's inevitable that these models, trained on the voices of the stars, would be shared with the whole world by our [pirate friends](https://www.youtube.com/watch?v=zeIjmvZZ_SQ).
Can't wait for an explosion of creativity that would follow!

#### Training

Now that we have the samples, we need to create our first voice.

1. Open up AI Voice Cloning WebUI in your browser
2. Navigate to the Utilities tab -> Import/Analyze
3. Drop your samples in and give your new voice a name before clicking "Import Voice"
4. When it finishes, navigate to the Ganerate tab and click "Refresh Voice List" - your new voice should now appear in the "Voice" dropdown

That's it - you are now ready to generate.
If you need some text, I suggest ["Maxims"](https://www.gutenberg.org/files/9105/9105-h/9105-h.htm) - a collection of 500 or so aphorisms left to us by Francois Duc De La Rochefoucauld.
They have a winning combination of being brief and being enjoyable to read and reflect on.

Start experimenting with the configs and note everything down, especially the seeds for the generations that you liked.
Here is the [AI Voice Cloning reference](https://git.ecker.tech/mrq/ai-voice-cloning/wiki/Generate) for the configs used for generation

Now that we have our first voice, we need to refine it.
Here is the [AI Voice Cloning reference](https://git.ecker.tech/mrq/ai-voice-cloning/wiki/Training) for training steps and configs.
As of the time of writing, it's a bit disorganized, so I encourage you to read it beginning to end to make sure you can understand the whole process.
The order of tabs in the "Training" UI matches the order in which you will need to proceed:

1. "Prepare Dataset" - taking your vocie samples, splitting and transcribing them
2. "Generate Configuration" - entering the training parameters
3. "Run Training" - train and monitor metrics

When training finishes, the last iteration of fine-tuned model will be used for generation.
You can verify this by looking at the logs in your terminal - there will be a new line like
```
Loading autoregressive model: ./training/Karin 1245/finetune/models//51_gpt.pth
```

##### Prepare Dataset

1. Open up AI Voice Cloning WebUI in your browser
2. Navigate to the Training Tab -> Prepare Dataset
3. In the "Dataset Source", select your voice.
This isn't the model you created, but the samples you have used to compute the voice latents earlier.
Behind the scenes, they have been copied to the `ai-voice-cloning/voices` folder.
If they have not been, create one yourself and copy the samples there by hand.
4. In the "Language" input, enter the 2-letter ISO language code that matches your samples
5. Click "Transcribe and Process"
6. When finished, manually verify the accuracy of the transcription.
In `ai-voice-cloning/training` folder, locate the subfolder named after your voice.
In that folder, open the `audio` subfolder as well as `train.txt` and `validation.txt` files.
Those txt files should contain audio file to text mapping like
```
audio/YYYP Karin 1_00001.wav|貴方の言う正常が知りたくて
audio/YYYP Karin 1_00002.wav|メイクを取って取り繕って
audio/YYYP Karin 1_00003.wav|脊髄で返す言葉はだって
```
Listen to the referenced audio files and correct any transcription mistakes

##### Generate Configuration

AI-Voice-Cloning [recommends a config](https://git.ecker.tech/mrq/ai-voice-cloning/wiki/Training#generate-configuration) like this:

```
Text LR Weight: governs how much to train the text portion (phonemes) of the model.

    For English, leave this at 0.01, as you don't really need to re-teach it English.
    For non-English, set this to 1, as you'll need to effectively "teach" the model a new language.

Mel LR Weight: governs how much to train the mel spectrogram portion (speech) of the model.

    For most finetune applications (for voices), leave this at 1.0, as you're effectively re-teaching the model how to sound.

...

The following settings are robust enough that I can suggest them, for small or large datasets.

    Epochs: 50 (increase/decrease as needed, according to how big your dataset is)
    Learning Rate: 0.0001
    Learning Rate Scheme: MultiStepLR
    Learning Rate Schedule: [2, 4, 9, 18, 25, 33, 50, 59]

However, if you want accuracy, I suggest an LR of 1e-5 (0.00001), as longer training at low LRs definitely make the best models.
```

Click `Validate Training Configuration`, have it succeed, and then click `Save Training Configuration`.
You are now ready for the final step.

##### Run Training

AI-Voice-Cloning [explains](https://git.ecker.tech/mrq/ai-voice-cloning/wiki/Training#brief-explanation) the charts:

```
To the right are two graphs to give a raw and rough idea on how well the model is trained.

The first graph will show an aggregate of loss values, and if requested, validation loss rates. These values quantify how much the output from the model deviates from the input sources. There's no one-size-fits-all value on when it's "good enough", as some models work fine with a high enough value, while some other models definitely benefit from really, low values. However, achieving a low loss isn't easy, as it's mostly predicated on an adequate learning rate.

The second graph isn't as important, but it models where the learning rate is at the last reported moment.

Typically, a "good model" has the text-loss a higher than the mel-loss, and the total-loss a little bit above the mel-loss. If your mel-loss is above the text-loss, don't expect decent output. I believe I haven't had anything decent come out of a model with this behavior.
```

Enjoy your new and improved voice AI!

### Conclusion

Take a moment to appreciate that you are now an artist:

Through a focus of your will you have made a number of aesthetic choices that transformed source audio into something of your own.
This is the same as a photographer choosing the right subject to make the right shot with the right gear and the right setup in order to capture their feelings.
