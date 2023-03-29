---  
share: true  
tag: public  
---  
# [Embeded vimeo video download](https://www.reddit.com/r/youtubedl/comments/fzv58p/getting_some_embedded_vimeo_videos_from_a_webpage/)  
  
  
  
vimeo got some protection that lets users embed videos and only let them load from their domain, this makes youtube-dl unable to use its vimeo extractor.  
  
open the browser's dev tools, load up the video, might need to start it (can pause immediately), then in the network tab, then you can filter for an url that contains `.json?base64_init=1`, copy it and after replacing the text i just quoted with `.mpd`, you should be able to just run `youtube-dl -o file.mp4 "URL"`  
  
  
my example:  
  
https://player.vimeo.com/video/325083382  
  
got it to work using:   
youtube-dl -o file.mp4 "https://19vod-adaptive.akamaized.net/exp=1667859480~acl=%2F882dcecd-9166-40e7-83e6-32ef01598d12%2F%2A~hmac=6bd567b2668acff6119cd8dc4f3d14da6898cc11203847b2a2c398de4c42cc7d/882dcecd-9166-40e7-83e6-32ef01598d12/sep/video/e9d397db,d1215277,d6f1836a,7a3f3560/master.mpd"