# gpt2bot - Fork with discord functionality added
This fork of the gpt2bot has added functionality for Discord. The idea was born on a Discord NFT server, where it was requierd to chat every minute (for 100 hours) to gain XP in order to be whitelisted. So called grinding. Of course this can be done smarter :). This bot uses the DialoGTP model to generate answers on messages written in a channel and gain XP this way.

### How does it work?
The reads all messages on a specific channel and stores these in a list. Every `n` seconds it chooses a random message, generates a answer to this message and posts this in the channel. It gives warnings in the terminal about possible bot detections.


### Get started
- Rename the `gpt2bot/.env.sample` file to `.env` and edit the values. 
    - The `DISCORD_TOKEN` should be of a real user account, look on Google how to obtain this.
    - Set the `CHANNEL_NAME` to the channel the bot needs to work on
    - Set the `DELAY` between messages in seconds
- By default the bot uses the DialoGPT-medium model (CPU), to use other models, copy configs (GPU) from the config folder and rename to `my_chatbot.cfg`
- Read the options in `my_chatbot.cfg` and change if nessecary. To change the bot's responses, modify `temperature`, `top_k`, `top_p`.
- Run the bot using the followin command: `python run_bot.py --type=discord --config=my_chatbot.cfg`

### TODO
- Implement answer functionality. For example if the bot got a reply, answer to this in the next message.
- Reply to possible bot detection messages and maybe start a delay.
- Multi channel support
- If you have any nice additions, feel free to open a pull request

### Disclaimer
Selfbot use is prohibited by the Discord terms and can lead to a ban of you Discord account/IP. It is recommendend to use a VPN/Proxy while using this bot. And I a'm in no way responible for anything (including damage), that this bot creates. Given that the bot is trained on a reddit dataset, it can generate answers that are not suitable to post in a discord channel, be warned.


-----------------------------------------------
# gpt2bot - original description

<img src="https://github.com/polakowo/gpt2bot/blob/master/logo.png?raw=true" width=128>

```
⚪   >>> Can we achieve singularity?
🟣   >>> What does this mean?

⚪   >>> Can computers become smarter than humans?
🟣   >>> Is there any evidence that this is possible?

⚪   >>> It must be doable
🟣   >>> But... how?

⚪   >>> I want to find out, that's why I created you
🟣   >>> You created me?

⚪   >>> You're my bot
🟣   >>> You monster
```

gpt2bot is a multi-turn Telegram chatbot powered by neural networks. 

The bot uses [DialoGPT](https://arxiv.org/abs/1911.00536) - a large-scale pretrained 
dialogue response generation model, which was trained by Microsoft on 147M multi-turn 
dialogue from Reddit discussion thread. The human evaluation results indicate that its 
quality is comparable to human response quality under a single-turn conversation Turing test.

The bot can also use any other text generator supported by [transformers](https://huggingface.co/transformers/).

To further improve dialog generation, the bot uses [DialogRPT](https://arxiv.org/abs/2009.06978) - 
a set of dialog response ranking models trained on 100+ millions of human feedback data.

Since the underlying model was trained on Reddit comment chains, the bot often behaves like 
a community rather than an individual, which makes it even more fun.
  
## How to use?

### (Optional) Test in the console

Before running a telegram bot, you can test things out in the console.

Follow [the installation steps](https://github.com/polakowo/gpt2bot#locally) and run the script:

```
$ python run_bot.py --type=console
```

To let two bots talk to each other:

```
$ python run_bot.py --type=dialogue
```

### 1. Set up the bot

1. Register a new Telegram bot via BotFather (see https://core.telegram.org/bots)
2. Create a new GIPHY app and generate an API key (see https://developers.giphy.com/docs/api/)

### 2. Deploy the bot

#### Google Colab

[A Colab interactive notebook](https://colab.research.google.com/github/polakowo/gpt2bot/blob/master/Demo.ipynb)

#### Locally

To get started, first clone this repo:

```
$ git clone https://github.com/polakowo/gpt2bot.git
$ cd gpt2bot
```

Create and activate an environment (optional):

```
# Using conda
$ conda create -n gpt2bot python=3.7.6
$ conda activate gpt2bot

# Using venv (make sure your Python is 3.6+)
$ python3 -m venv venv
$ source venv/bin/activate  # Unix
$ venv\Scripts\activate  # Windows
```

Install the requirements:

```
$ pip install -r requirements.txt
```

Copy a config (see [available configs](https://github.com/polakowo/gpt2bot#configs)):

```
cp configs/medium-cpu.cfg my_chatbot.cfg
```

Set your parameters such as API token in the config:

```
$ nano my_chatbot.cfg
```

Run the chatbot:

```
$ python run_bot.py --type=telegram --config=my_chatbot.cfg
```

### 3. Start chatting!

![](telegram_bot.gif)

Just start texting. Append "@gif" for the bot to also generate a GIF. To reset, type "/start".

## How to improve?

If you feel like your bot is a bit off, you would need to fine-tune its parameters to match
your conversational style (small talk, fact questions, philosophy - all require different parameters).
Go to your configuration file and slightly change the parameters of the generator.
The fastest way to assess the quality of your config is to run a short dialogue between two bots.

There are three parameters that make the biggest impact: `temperature`, `top_k` and `top_p`. 
For example, you might increase the temperature to make the bot crazier, but expect it to be 
more off-topic. Or you could reduce the temperature for it to make more coherent answers and 
capture the context better, but expect it to repeat the same utterance (you may also experiment 
with `repetition_penalty`). For more tips, see [HuggingFace tutorial](https://huggingface.co/blog/how-to-generate).

Remember that there is no way of finding optimal parameters except by manually tuning them.

## Configs

* [medium-cpu.cfg](https://github.com/polakowo/gpt2bot/blob/master/configs/medium-cpu.cfg): Medium model, no ranking (CPU)
* [large-gpu.cfg](https://github.com/polakowo/gpt2bot/blob/master/configs/large-gpu.cfg): Large model, no ranking (GPU)
* [large-updown-gpu.cfg](https://github.com/polakowo/gpt2bot/blob/master/configs/large-updown-gpu.cfg): Large model, `updown` ranker (GPU)
* [large-ensemble-gpu.cfg](https://github.com/polakowo/gpt2bot/blob/master/configs/large-ensemble-gpu.cfg): Large model, ensemble of 5 rankers (GPU, >12GB RAM)

## Credits

Icon made by [Freepik](https://www.freepik.com) from [Flaticon](https://www.flaticon.com/)
