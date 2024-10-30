https://arcade.makecode.com/S85541-20415-75011-49010
# Sylus-princess
class SpriteKind:
    coins = SpriteKind.create()
    grassy = SpriteKind.create()

def on_on_overlap(sprite, otherSprite):#Set the coins to be destroyed when the player touches it, gaining 5 point and generating a confetti effect animation.
    sprites.destroy(otherSprite, effects.confetti, 100)
    info.change_score_by(5)
sprites.on_overlap(SpriteKind.player, SpriteKind.coins, on_on_overlap)

def on_countdown_end():#Set the game to end at the end of the countdown
    game.over(True, effects.bubbles)
info.on_countdown_end(on_countdown_end)

def on_on_overlap2(sprite2, otherSprite2):#Set the player to lose 1 life point when the player sprite touches an enemy sprite. The enemy is destroyed and an animation of the ash effect is generated.
    info.change_life_by(-1)
    guard.destroy(effects.ashes, 500)
sprites.on_overlap(SpriteKind.player, SpriteKind.enemy, on_on_overlap2)

def on_life_zero():#Set the game to end when the life value reaches zero
    game.over(False, effects.splatter)
info.on_life_zero(on_life_zero)

def on_on_overlap3(sprite3, otherSprite3):#Set the food to be destroyed when the player touches it, gaining 1 point and generating a fountain effect animation.
    sprites.destroy(otherSprite3, effects.fountain, 100)
    info.change_score_by(1)
sprites.on_overlap(SpriteKind.player, SpriteKind.food, on_on_overlap3)

guard: Sprite = None
diamonds: Sprite = None
coins2: Sprite = None
scene.set_background_color(3)#Background colour settings
game.splash("Sylus princess")#Setting up the display of game names
mySprite = sprites.create(img("""
        . . . . . . 5 5 5 5 . . . . . . 
            . . . . . 5 1 1 1 1 5 . . . . . 
            . . . . f 1 5 5 5 5 1 f . . . . 
            . . . f 1 1 1 1 1 1 1 1 f . . . 
            . . . f 1 1 f f f f 1 1 f . . . 
            . . . f 1 f f d d f f 1 f . . . 
            . . f 1 f d f d d f d f 1 f . . 
            . . f 1 f d 2 d d 2 d f 1 f . . 
            . . f 1 1 f d d d d f 1 1 f . . 
            . f 1 1 f 3 f f f f 3 f 1 1 f . 
            . . f f d 3 5 3 3 5 3 d f f . . 
            . . f d d f 3 5 5 3 f d d f . . 
            . . . f f 3 3 3 3 3 3 f f . . . 
            . . . f 3 3 5 3 3 5 3 3 f . . . 
            . . . f f f f f f f f f f . . . 
            . . . . . f f . . f f . . . . .
    """),
    SpriteKind.player)#Setting up the image of the player
scene.camera_follow_sprite(mySprite)#Setting the camera to follow the player
game.show_long_text("Help the princess retrieve the diamonds taken by the dragon.",
    DialogLayout.BOTTOM)#A brief introduction to the content of the game
game.show_long_text(" And avoid the guards in the bunker!", DialogLayout.BOTTOM)#A brief introduction to the content of the game
controller.move_sprite(mySprite, 90, 90)#Setting the player's movement speed
mySprite.set_position(24, 5)#Setting the player's initial birth point
tiles.set_tilemap(tilemap("""
    Map
"""))#Game Map
info.start_countdown(30)#Set the game time to 30 seconds countdown
for index in range(5):#Set the number of coins generated to 5
    coins2 = sprites.create(img("""
            . . . b b . . . 
                    . . b 5 5 b . . 
                    . b 5 1 d 5 b . 
                    . b 5 1 5 5 b . 
                    . c 5 1 5 5 c . 
                    . c 5 5 1 5 c . 
                    . . f 5 5 f . . 
                    . . . f f . . .
        """),#Setting up the image of the coins
        SpriteKind.coins)#Set the type of coins to coins
    tiles.place_on_random_tile(coins2, sprites.dungeon.dark_ground_center)#Set coin to randomly generate on the map
for index2 in range(15):#Set the number of diamonds generated to 15
    diamonds = sprites.create(img("""
            . . . . . . . . . . . . . . . . 
                    . f . . . . . . . . . . . . . . 
                    f 5 f . . . . . . . . . . . . . 
                    . f . . . . . . . . . . . . . . 
                    . . . . f f f f f f f f . . . . 
                    . . . f 1 1 f 1 1 f 1 1 f . . . 
                    . . f 1 9 9 f 1 9 f 1 9 9 f . . 
                    . f 1 9 9 f 1 9 9 9 f 9 9 9 f . 
                    . f 1 9 9 f 1 9 9 9 f 9 9 9 f . 
                    . . f 9 9 9 f 1 9 f 9 9 9 f . . 
                    . . . f 9 9 f 1 9 f 9 9 f . . . 
                    . . . . f 9 9 f 1 9 9 f . . . . 
                    . . . . . f 9 f 1 9 f . . . . . 
                    . . . . . . f 9 1 f . . . f . . 
                    . . . . . . . f f . . . f 5 f . 
                    . . . . . . . . . . . . . f . .
        """),#Setting up the image of the diamond
        SpriteKind.food)#Set the type of diamond to food
    tiles.place_on_random_tile(diamonds, sprites.dungeon.dark_ground_center)#Set diamonds to randomly generate on the map
for index3 in range(7):#Set the number of guards generated to 7
    guard = sprites.create(img("""
            ..............................
                    ..............................
                    ..............................
                    ..............................
                    ..............................
                    ..............................
                    ..............................
                    ..............................
                    ........f...........f.........
                    .......fe...........ef........
                    .......fef..fffff..fef........
                    .......feeff22222ffeef........
                    .......fef222222222fef........
                    ........f22222222222f.........
                    .......f2222222222222f........
                    .......f22ff2222ff222f........
                    ...f..f222332222332222f..f....
                    ..fff.f222222222222222f.fff...
                    .ffffff222222222222222ffffff..
                    fff...f22222fffff22222f...fff.
                    f.....f22222222f222222f.....f.
                    .......f2222222222222f........
                    ........ff222222222ff.........
                    ..........fffffffff...........
                    ..............................
                    ..............................
                    ..............................
                    ..............................
                    ..............................
                    ..............................
        """),#Setting up the image of the guards
        SpriteKind.enemy)#Set the type of guard to enemy
    tiles.place_on_random_tile(guard, sprites.dungeon.dark_ground_center)#Setting up guards to appear randomly on the map
    guard.set_velocity(randint(20, 30), 0)#Set guards to move only in parallel
    guard.set_bounce_on_wall(True)#Allow guards to rebound after hitting a wall
info.set_life(1)

def on_forever():#background music
    music.play(music.string_playable("E G G A G E C - ", 120),
        music.PlaybackMode.UNTIL_DONE)
    music.play(music.string_playable("C D E E D C D - ", 120),
        music.PlaybackMode.UNTIL_DONE)
forever(on_forever)
