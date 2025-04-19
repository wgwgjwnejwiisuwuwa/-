if (answers.length < questions.length) {
        return message.reply('**تم إنهاء العملية بسبب انتهاء الوقت.**');
      }

      await sendOffer(targetChannelID, message.author, answers);
      embed.setDescription('**تم إرسال الملف بنجاح.**');
      await sentMessage.edit({ embeds: [embed] });
      await message.channel.send(imageURL); 
    });

    async function sendOffer(channelID, author, answers) {
      const targetChannel = client.channels.cache.get(channelID);
      if (!targetChannel) return;

      const offerEmbed = new EmbedBuilder()
        .setColor(color)
        .setDescription(`__**
> - المـلفات الـبـرمـجـيـة .

( 1 ) - الـمُـبـرمـج الـعـبـقـري : ${author}.

( 2 ) - المـلف : ${answers[0]}.

( 3 ) - السـعر  : ${answers[1]}.

**__`);

      const actionRow = new ActionRowBuilder().addComponents(
        new ButtonBuilder()
          .setLabel('اطـلب الان - ORdDER NOW')
          .setStyle(ButtonStyle.Link)
          //.setEmoji(':shop:')
          .setURL('https://discord.com/channels/1303398090019045437/1356274075823247590')
      );

      await targetChannel.send({
        content: '@here',
        embeds: [offerEmbed],
        components: [actionRow]
      });

      await targetChannel.send(imageURL); 
    }
  }
};
