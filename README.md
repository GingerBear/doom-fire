# doom-fire

Few days ago I was browsing HN and found an article about how fire is implemented in DOOM http://fabiensanglard.net/doom_fire_psx/. It's very simple and the result is surprisingly good. I cannot stop but trying to implemented in JavaScript right away. I managed to get it working and added some extra controls. Since I found the original article still need a bit digestion to understand. I want to talk about how it is implemented in my own (hopefully even simpler) words.

## The Basic

To make fire in a pixel grid, the basic idea is that, we traverse each pixel and update each pixel above them to be “cooler”. And we do it over and over again. This way, if we set all bottom line of pixels to “hottest”. we can see just sit and let it grow up. Like this:

[FIG 1]

If make it bigger and we put color on it, it looks like this.

[FIG 2]

## The Trick

But that doesn't really look like fire, it's too "linear". The trick to make it look fire is adding some randomness to how the fire "grow" up.

First, instead of always make the above pixel "cooler", we only do it by 50% chance. It looks like this:

[FIG 3]

It looks better. Next, instead of go straight up, we can add a shift to left or right randomly.

In code, when we traverse each pixel, find the pixel above, then either, update that pixel, or update the one on its left, or update the one on its right. The result looks like this.

[FIG 4]

We can render it on canvas instead of using HTML to improve the performance.

[FIG 5]

## Control fire

### wind

In the original article, the author left an exercise for readers to simulate wind. If you get the idea how the fire is generated, it's pretty straight forward to know wind can be simulated. All we need to do adjust the shift of left or right when update the above pixel. If we shift more to the left, it will cause the pixel leaning toward left, which makes it look like there is a wind blow from right to left. And the same goes to the other way.

### Fade the fire

Fading the fire can be simulated by gradually updating the bottom section of the pixel to be "cooler". It will not only "fade" the bottom section but also "fade" all the pixels above, because they are propagated.

### fire intensity

Fire intensity basically means how long does it take for a pixel to get "cool down" as it propagates up. Currently, we set it to be 50% chance to cool down. So if we want the fire to be more "intense", we just need to make let less possible to cool down.

You can try to control the fire here:

[Final result]

You can find the source code at https://github.com/GingerBear/doom-fire
