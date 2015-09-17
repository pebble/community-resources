---
name: SpaceMerc
creator: [David C. Drake](http://davidcdrake.com)
license: MIT
link: https://github.com/theDrake/spacemerc
appstore: 52d6a8c0333d76e3d000000a
tags:
  - watchapp
  - storage
---
[_SpaceMerc_](http://davidcdrake.com/spacemerc/) is a sci-fi FPS game (first-person shooter) in a simplistic 3D environment. The player is a mercenary defending humanity from hostile aliens in order to earn money which can then be spent on upgrades to weaponry, armor, etc.

Graphics are drawn using [primitive functions](http://developer.getpebble.com/docs/c/Graphics/Drawing_Primitives/) such as `graphics_fill_rect`, `graphics_draw_pixel`, etc., with the exception of the compass needle, which makes use of the [`GPath` functions](http://developer.getpebble.com/docs/c/Graphics/Drawing_Paths/) `gpath_draw_outline` and `gpath_draw_filled`.

Time-sensitive features are handled via [`AppTimer`s](http://developer.getpebble.com/docs/c/Foundation/Timer/), [`TickTimerService`](http://developer.getpebble.com/docs/c/Foundation/Event_Service/TickTimerService/), and the `repeat_interval` argument passed to [`window_single_repeating_click_subscribe`](http://developer.getpebble.com/docs/c/User_Interface/Window/#window_single_repeating_click_subscribe).

Game data are organized into [dynamically-managed](http://developer.getpebble.com/docs/c/Standard_C/Memory/) `struct`s which are saved to and loaded from [persistent storage](http://developer.getpebble.com/docs/c/Foundation/Storage/) via `persist_write_data` and `persist_read_data`.

This app also makes use of [`MenuLayer`s](http://developer.getpebble.com/docs/c/User_Interface/Layers/MenuLayer/), [`TextLayer`s](http://developer.getpebble.com/docs/c/User_Interface/Layers/TextLayer/), [`StatusBarLayer`s](http://developer.getpebble.com/docs/c/User_Interface/Layers/StatusBarLayer/) (Basalt only), an [`InverterLayer`](http://developer.getpebble.com/docs/c/User_Interface/Layers/InverterLayer/) (Aplite only), and various other features of the Pebble SDK.

Screenshots:

![](http://davidcdrake.com/wp-content/uploads/2014/01/SpaceMerc-Fim-Officer.png)
![](http://davidcdrake.com/wp-content/uploads/2014/01/SpaceMerc-Robot.png)
![](http://davidcdrake.com/wp-content/uploads/2014/01/SpaceMerc-Ooze.png)
![](http://davidcdrake.com/wp-content/uploads/2014/01/SpaceMerc-Monstrosity.png)
