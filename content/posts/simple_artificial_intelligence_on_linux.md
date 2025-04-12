---
date: '2024-11-19T15:44:20-04:00'
draft: false
title: 'Simple Artificial Intelligence on Linux'
cover:
    image: img/ai_ollama.webp
    alt: "Llama 3.2 running in ollama"
    caption: "Asking llama3.2 for a comparison between Xubuntu and Linux Mint XFCE"
---

### Initial look at artificial intelligence

We might be a bit late to the game, but I’ve started looking at what we need at the Computer Recycling Project to run artificial intelligence models locally (on the machine, versus on the server) under Linux. [The Ollama project](https://ollama.com/download) makes it very easy to install a number of artificial intelligence models under Linux.

Once ollama is installed you can download a model by typing:

```shell
ollama pull <model name>
```

So if you wanted to pull Llama 3.2 you would type:

```shell
ollama pull llama3.2
```

This command simply downloads the model. To run the AI with the model type:

```shell
ollama run <model>
```

Again for llama3.2 the command would be:

```shell
ollama run llama3.2
```

This of course assumes you’ve downloaded the model first. A list of models ollama can work with can be found on the github ollama web page at: (https://github.com/ollama/ollama) Some models have different strengths. For example: codellama is suppose to be better at writing code than the regular llama 3.2 model.

### My brief experience

I’ve only spent a couple of days with Llama 3.2 and I’ve already noticed some issues. Llama isn’t bad, but you cannot trust that it’s correct on things. For example, I have a XEON E5-2690 V2 CPU that llama 3.2 thought was an 8 core 16 thread CPU, when in fact it’s a 10 core 20 thread CPU. I corrected llama on some mistakes it make, but I found that when making some comparisons llama will sometimes revert back to the old information it had about something. More infuriatingly it might state the new information, but further down suggest something that’s bound to old information it has.

I also asked llama 3.2 to write a bit of GML (GameMaker Language) and it was able to write a bit of code. Asking for bits of small code seems mostly okay. I was very surprised when I asked llama 3.2 about the differences between the Brother ScanNCut SDX125e cutting machine, Cricut cutting machines, and Silhouette cutting machines, it gave me a pretty good list of advantages and disadvantages of each.

The last thing I experienced has to do with the speed of running llama 3.2. Having an Nvidia GPU really seems to help – a lot. The Intel Core i7-4790 with 16GB of RAM and a 4GB Nvidia Quadro P1000 runs models much faster than an i7-7700K with 16GB of RAM and an AMD RX580 8GB graphics card – at least in my testing. Having an Nvidia GPU really helps. 

