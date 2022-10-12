# Automated Reddit to Youtube Bot 

<!-- vscode-markdown-toc -->
* [Description](#description)
* [Example Videos](#example-videos)
* [Usage :](#usage-:)
* [Generate a Video for a Specific Post](#generate-a-video-for-a-specific-post)
* [Generate Only Thumbnails](#generate-only-thumbnails)
* [Enable a Newscaster](#enable-a-newscaster)

<!-- vscode-markdown-toc-config
	numbering=false
	autoSave=true
	/vscode-markdown-toc-config -->
<!-- /vscode-markdown-toc -->

## <a name='description'></a>Description 

Scrape posts from Reddit and automatically generate Youtube Videos and Thumbnails


## <a name='example-videos'></a>Example Videos 

Checkout my Youtube Channel for example videos made by this repo :

[![Watch the video](assets/images/xm5gsv_thumbnail.png)](https://youtu.be/xhE8bFqBAw0)


I have also been working on integrating art generated by artificial intelligence into these automated videos :

[![Watch the video](assets/images/the_man_on_my_patio.png)](https://youtu.be/nCjYH3ETXNo)


## <a name='usage-:'></a>Usage :

Copy config file, and populate it with Reddit PRAW and AWS Polly auth tokens  :

```
cp config-example.py config.py
```

Look into your youtube channel in chrome and then use this plugin to export the cookie :

[Export cookie JSON file for Puppeteer](https://chrome.google.com/webstore/detail/%E3%82%AF%E3%83%83%E3%82%AD%E3%83%BCjson%E3%83%95%E3%82%A1%E3%82%A4%E3%83%AB%E5%87%BA%E5%8A%9B-for-puppet/nmckokihipjgplolmcmjakknndddifde)

Save the cookie in this repo with filename `cookies.json`

Download video backgrounds using youtube-dl :

```
cd assets/backgrounds
yt-dlp -f 22 --output "%(uploader)s_%(id)s.%(ext)s" https://www.youtube.com/playlist?list=PLGmxyVGSCDKvmLInHxJ9VdiwEb82Lxd2E
```

Make sure you have Docker installed and then run the following 

```
docker-compose up
```

or alternatively you can run via :

```
pip install -r requirements.txt
python app.py
```

## <a name='generate-a-video-for-a-specific-post'></a>Generate a Video for a Specific Post 

or if you want to generate a video for a specific reddit post you can specify it via the `--url` param :

```
python app.py --url https://www.reddit.com/r/AskReddit/comments/hvsxty/which_legendary_reddit_post_comment_can_you_still/
```

or you can do multiple url's by seperating with a comma, ie :

```
python app.py --url https://www.reddit.com/r/post1,https://www.reddit.com/r/post2,https://www.reddit.com/r/post3
```

## <a name='generate-only-thumbnails'></a>Generate Only Thumbnails

if you want to generate only thumbnails you can specify `--thumbnail-only` mode, this will skip video compilation process :

```
python app.py --thumbnail-only
```

## <a name='enable-a-newscaster'></a>Enable a Newscaster

If you want to enable a Newscaster, edit settings.py and set :

```
enable_newscaster = False
```

![](assets/newscaster.png)

If the newcaster video has a green screen you can remove it with the following settings, 
use an eye dropper to get the RGB colour of the greenscreen and set it to have it removed :

```
newscaster_remove_greenscreen = True
newscaster_greenscreen_color = [1, 255, 17] # Enter the Green Screen RGB Colour 
newscaster_greenscreen_remove_threshold = 100
```