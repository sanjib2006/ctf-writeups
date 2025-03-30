# CTF Writeup - Chronos CTF (IIT Mandi)

## Challenge: Back In Time - 5 

### Category: OSINT

### Writeup Author: iamgreedy

### Challenge Description
> The traitor just checked into a fancy hotel and posted a picture on Instagram—but no location tag! Your mission: analyze their posts, spot unique details, and track down the exact hotel they’re staying at. The clues are there... if you know where to look! 🌍🔍
Flag Format: saic{hotel_name}
Example: If you find out the picture was taken at Hotel Prestige, the flag would be: saic{hotel_prestige}
Happy hunting, detective! 🕵️‍♂️

### Solution
From the github profile of `Pavitr Prabhakar` found out his username `SpideyPavitr`. Checked this username name on instagram and got the following image:

<img src="image.webp">

On google image search found out that this image was taken near the `Selamat Datang Monument`.

Explored the location on google earth and street view and found out that the hotel is `Grand Hyatt Jakarta`.

### Final Flag
```
saic{grand_hyatt_jakarta}
```

