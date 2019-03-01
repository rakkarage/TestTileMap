# TestTileMap

![issue](issue.gif)

based on the tileMap extras from
<https://github.com/Unity-Technologies/2d-extras>

i made an AnimatedTile.cs class and related classes

i can set an animated tile to:

- sync=true: all instances will start on same animation frame
  - needed for water tiles because they line up with each other
  - works by ???
    - `tileData.sprite = AnimatedSprites[RandomStartTime ? Random.Range(0, AnimatedSprites.Length) : 0];`
    - overriding GetTileData and setting a random sprite from the animation
- sync=false: all instances will start on random animation frame
  - needed for wall torches and banners so they not all same
  - works by ???
    - `tileAnimationData.animationStartTime = RandomStartTime ? Random.value : 0;`
    - override GetTileAnimationData and setting start time to random time

but now i need to make a way to sync two different tiles animations? in pairs?
the top and bottom halves? for the top an bottom of these animated oblisks
they work fine if sync=true but i wanna get sync=false working with these too

what i have considerd:

- using one sprite and animation for both tiles
  - i need two because they are on different layers and different positions - the character passes in front of bottom and behind top

what i have tried:

- add a sync object property
  - get the animation frame from that object and set it in this one overriding the random start time
  - but these functions are only called when building the cache? so not work

known issues:

- gaps between tiles
  - can be fixed with settings, irrelevant to this issue

how can i sync pairs of animated tiles with same randomStartTime? if possible?
do you know what i mean?
thanks
