# TestTileMap

![Deko](issue.gif)

## TileMap Layers

- behind character
  - Back - floor
  - WaterBack - top half of water tiles
  - ItemBack - top half of tree, obelisk etc
- in front of character
  - WaterFore - lower half of water tiles
  - Fore - walls and doors and stairs
  - ItemFore - lower half of tree, obelisk etc
  - Light - light and line of sight

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
the first tile will chose a randomStartTime and pass it to the second in the pair? but where and when?

## what i have considered

- using one sprite and animation for both tiles
  - i need two because they are on different layers and different positions
    - the character passes in front of bottom and behind top
    - the bottom of the oblisk is between front and back water etc but top is above both on its own itemFore layer

## what i have tried

- i have a split brush that i use to pain two tiles at once called a SplitBrush
  - it paints each half to a differnt layer
    - so i should just be able to set the top half to start at the sane RandomStartTime as the bottom right???
    - add a sync option but does not seem to work cuz these functions are only called when building the cache? so not work

- from SplitBrush.Paint i should be able to GetTileAnimationData from one and set to other? no cannot convert tilemap to itilemap!?
- !!!!!!!!set both to same random value here instead of in other file??? no cannot get tile animation data
- so do it inside GetTileAnimationData? no
- connect them in paint and use Connection data in GetTileAnimationData??? no idk

a. i want some tiles to sync with all others of same type (working) (waterBack & waterFore animated tiled)
b. i want some tiles to not sync with all others of same type (working) (torches & banners)
c. i want some tiles to sync with all others of same type and with top half but since all start at 0 this works by default (working) (water brush places back and fore tiles in sync)
d. i want some tiles to not sync with all others of same type but sync in pairs with other specific tiles (not working) (oblisk brush)

## TODO

- test random sync torch
- random sync oblisks?
