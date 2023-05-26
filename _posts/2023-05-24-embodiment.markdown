---
layout: post
title: "Embodiment - Part 1"
date: 2023-05-25 00:00:00 -0000
categories: Embodiment D-ID TorToiSe ai-voice-cloning StableDiffusion SadTalker
---

# Embodiment - Part 1

## A D-ID-like on your local machine 

I was delighted to discover an Internet creating an embodiment of an AI - a "talking head" video where the text, speaker's voice and a video of the speaker actually talking were the result of AI synthesis.
Do check it out - click in to navigate to the full tweet for the video:

<blockquote class="twitter-tweet"><p lang="ja" dir="ltr">1　WebUIでAI画像を生成<br>2　ChatGPTで文章を生成（合成音声AIについての説明）<br>3　COEIROINKでの合成音声AI(25/100epoch)を作成し、文章を音声出力<br>4　D-IDで1,3を読み込ませてAIによる自動口パク・動画化<br>コエイロインクが学習途中データだからまだまだガビってるけど面白い。 <a href="https://t.co/yVB8A9pTLD">pic.twitter.com/yVB8A9pTLD</a></p>&mdash; 852話 (@8co28) <a href="https://twitter.com/8co28/status/1625838748486496257?ref_src=twsrc%5Etfw">February 15, 2023</a></blockquote> 

In English, this was the author's workflow:
1. Generate AI image with WebUI
2. Generate text with ChatGPT (An explanation about sythetic voice AI)
3. Create a voice AI with COEIROINK and synthesize voice from text
4. Use D-ID for lipsync and speaking animation

I have a capable graphics card, so I wondered if I could achieve something similar, running locally, for free.
I succeeded:

> The duration of our passions is no more dependant upon us than the duration of our life.

<video
  src="{{site.url}}/assets/YYYP_Karin-HermitageMikuReads-Maxim5.mp4"
  width="512"
  height="512"
  preload='none'
  controls>
Your browser does not support the video element
</video>

My workflow:

1. Generate AI image with local [AUTOMATIC1111 WebUI](https://github.com/AUTOMATIC1111/stable-diffusion-webui)
2. I don't have an LLVM running locally (yet), I just made do with ["Maxims"](https://www.gutenberg.org/files/9105/9105-h/9105-h.htm) - a collection of 500 or so aphorisms left to us by Francois Duc De La Rochefoucauld.
They have a winning combination of being brief and being enjoyable to read and reflect on.
3. Create a voice AI with [TorToiSe](https://git.ecker.tech/mrq/tortoise-tts).
In order to lean into spoken word synthesis, I did not build my training data from any living person's recordings, but took advantage of [SynthV Karin](https://www.ah-soft.com/synth-v/karin/)
4. Used [SadTalker](https://github.com/OpenTalker/SadTalker) for lipsync and speaking animation

My hope here is to share the details on setting up this stack locally and my learnings in my future posts, so please stay tuned for Part 2, which will be on local setup and iterative development.
