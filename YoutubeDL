#Intitialize YouTube downloader
ydl = youtube_dl.YoutubeDL({'outtmpl': '%(id)s%(ext)s'})

# works when /ytdl <link> is given
@bot.message_handler(commands=['ytdl'])
def down(msg):
    args = msg.text.split()[1]
    try:
        with ydl:
            result = ydl.extract_info(
                args,
                download=False  # We just want to extract the info
            )

        if 'entries' in result:
            # Can be a playlist or a list of videos
            video = result['entries'][0]
        else:
            # Just a video
            video = result
        
        for i in video['formats']:
            link = '<a href=\"' + i['url'] + '\">' + 'link' + '</a>'
            if i.get('format_note'):
                bot.reply_to(msg, 'Quality-' + i['format_note'] + ': ' + link, parse_mode='HTML')
            else:
                bot.reply_to(msg, link, parse_mode='HTML', disable_notification=True)
    except:
        bot.reply_to(msg, 'This can\'t be downloaded by me')
