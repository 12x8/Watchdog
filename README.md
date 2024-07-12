# 👁️ Watchdog
Script qui permet de savoir quand sa parle de toi sans te mentionner

```js
import { Client, Message, TextChannel } from 'discord.js-selfbot-v13';
const config = require('./config.json');
const token = config.token;
import * as colors from 'colors';
import 'colors';

const client = new Client({
    ws: { properties: { $browser: "Discord iOS" } },
});

client.on('ready', () => {
    console.log('Le selfbot est connecté ✔'.green);
});

client.on('messageCreate', async (message: Message) => {
    const mentions = message.mentions.users.map(user => user.id);
    const ditPasMonBlaze = ['tu', 'met', 'tes pseudo'];
    
    if (mentions.includes(client.user!.id) || ditPasMonBlaze.some(word => message.content.toLowerCase().includes(word))) {
        const tropFan = message.author.displayName || message.author.tag;
        const serveur = message.guild ? message.guild.name : 'DM';
        const salon = message.channel instanceof TextChannel ? message.channel.name : 'Salon inconnu';
        
        console.log(`\n\nMessage de :`.white + ` ${tropFan} | ${message.author.tag}`.red + `\nServeur :`.white + ` ${serveur}`.green + `\nSalon du message :`.white + ` ${salon}`.blue + `\nContenu du message :`.white + ` ${message.content}`.yellow);
    }
});

client.login(token);
```
