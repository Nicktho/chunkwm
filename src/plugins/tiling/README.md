#### chunkwm-tiling configuration index

* [config variables](#config-variables)
  * [global tiling mode](#set-global-tiling-mode)
  * [specific desktop tiling mode](#set-tiling-mode-for-a-specific-desktop)
  * [default desktop bsp layout](#set-default-bsp-layout-for-a-specific-desktop)
  * [global offset and window gap](#set-global-desktop-offset-and-window-gap)
  * [specific desktop offset and window gap](#set-desktop-offset-and-window-gap-for-a-specific-desktop)
  * [global offset and window gap incremental step](#set-desktop-offset-and-window-gap-incremental-step)
  * [set spawn position of bsp-windows](#spawned-windows-are-tiled-to-the-left)
  * [set optimal ratio used by bsp_split_mode optimal](#set-optimal-ratio-used-by-bsp_split_mode-optimal)
  * [configure how regions are split](#configure-how-regions-are-split)
  * [configure ratio used when regions are split](#configure-ratio-used-when-regions-are-split)
  * [set wrap behaviour for window focus command](#set-wrap-behaviour-for-window-focus-command)
  * [set state of mouse follows focus](#set-state-of-mouse-follows-focus)
  * [float the next window attempted tiled](#the-next-window-attempted-tiled-will-be-made-floating-instead)
  * [center window on monitor when floated](#center-a-window-on-monitor-when-toggled-floating-by-the-user)
  * [constrain window to region size](#constrain-window-to-bsp-region-size)
  * [signal dock to make windows topmost when floated](#signal-dock-to-make-windows-topmost-when-floated)
* [window commands](#window-commands)
  * [focus window](#focus-window)
  * [swap window](#swap-window)
  * [warp window](#warp-window)
  * [warp floating window](#warp-floating-window)
  * [send window to desktop](#send-window-to-desktop)
  * [send window to monitor](#send-window-to-monitor)
  * [increase region size](#increase-region-size)
  * [decrease region size](#decrease-region-size)
  * [set bsp-insertion point](#set-bsp-insertion-point)
  * [toggle various window options](#toggle-various-window-options)
* [desktop commands](#desktop-commands)
  * [desktop layout](#desktop-layout)
  * [rotate desktop](#rotate-desktop)
  * [mirror desktop](#mirror-desktop)
  * [equalize desktop](#equalize-size-of-all-windows-on-desktop)
  * [adjust desktop padding](#adjust-desktop-padding)
  * [adjust desktop gap](#adjust-desktop-window-gap)
  * [toggle desktop offset and gap](#toggle-desktop-offset-and-window-gap)
  * [serialize desktop to file](#serialize-desktop-bsp-tree-to-file)
  * [deserialize desktop from file](#deserialize-desktop-bsp-tree-from-file)
* [monitor commands](#monitor-commands)
  * [focus monitor](#focus-monitor)
* [window rules](#window-rules)

---

#### config variables

##### set global tiling mode

    chunkc config global_desktop_mode <option>
    <option>: bsp | monocle | float

##### set tiling mode for a specific desktop

    chunkc config <index>_desktop_mode monocle
    <index>: mission-control index

##### set default bsp-layout for a specific desktop

    chunkc config <index>_desktop_tree <file>
    <index>: mission-control index
    <file>: /path/to/file (e.g: ~/.chunkwm_layouts/dev_1)

##### set global desktop offset and window gap

    chunkc config global_desktop_offset_top     20
    chunkc config global_desktop_offset_bottom  20
    chunkc config global_desktop_offset_left    20
    chunkc config global_desktop_offset_right   20
    chunkc config global_desktop_offset_gap     15

##### set desktop offset and window gap for a specific desktop

    chunkc config 1_desktop_offset_top          190
    chunkc config 1_desktop_offset_bottom       190
    chunkc config 1_desktop_offset_left         190
    chunkc config 1_desktop_offset_right        190
    chunkc config 1_desktop_offset_gap          15

##### set desktop offset and window gap incremental step

    chunkc config desktop_padding_step_size     10.0
    chunkc config desktop_gap_step_size         5.0

##### spawned windows are tiled to the left

    chunkc config bsp_spawn_left <option>
    <option>: 1 | 0
    desc: new windows are tiled as the left-child

##### set optimal ratio used by bsp_split_mode optimal

    chunkc config bsp_optimal_ratio             1.618
    desc: determines if the new split should be horizontal or vertical

##### configure how regions are split

    chunkc config bsp_split_mode                <option>
    <option>: vertical | horizontal | optimal

##### configure ratio used when regions are split

    chunkc config bsp_split_ratio               <option>
    <option>: 0 < value < 1

##### set wrap behaviour for window focus command

    chunkc config window_focus_cycle            <option>
    <option>: none | monitor | all

##### set state of mouse follows focus

    chunkc config mouse_follows_focus           <option>
    <option>: 1 | 0

##### the next window attempted tiled will be made floating instead

    chunkc config window_float_next             <option>
    <option>: 1 | 0

##### center a window on monitor when toggled floating by the user

    chunkc config window_float_center           <option>
    <option>: 1 | 0

##### constrain window to bsp region size

    chunkc config window_region_locked          <option>
    <option>: 1 | 0

##### signal dock to make windows topmost when floated
    chunkc config window_float_topmost          <option>
    <option>: 1 | 0
    desc: requires chwm-sa (https://github.com/koekeishiya/chwm-sa)

---

#### window commands

##### focus window

    chunkc window --focus <option>
    <option>: north | east | south | west
    short flag: -f

##### swap window

    chunkc window --swap <option>
    <option>: north | east | south | west
    short flag: -s
    desc: swap two windows in-place

##### warp window

    chunkc window --warp <option>
    <option>: north | east | south | west
    short flag: -w
    desc: move window in direction and modifies layout

##### warp floating window

    chunkc window --warp-floating <option>
    <option>: fullscreen | left | right | top-left
              top-right  | bottom-left  | bottom-right
    short flag: -W
    desc: move and resize a floating window to specific region of monitor

##### send window to desktop

    chunkc window --send-to-desktop <option>
    <option>: prev | next | index
    short flag: -d

##### send window to monitor

    chunkc window --send-to-monitor <option>
    <option>: prev | next | index
    short flag: -m

##### increase region size

    chunkc window --use-temporary-ratio <ratio> --adjust-window-edge <option>
    <ratio>: 0 < value < 1
    <option>: north | east | south | west
    short flags: -r, -e

##### decrease region size

    chunkc window --use-temporary-ratio <ratio> --adjust-window-edge <option>
    <ratio>: -1 < value < 0
    <option>: north | east | south | west
    short flags: -r, -e

##### set bsp-insertion point

    chunkc window --use-insertion-point <option>
    <option>: focus | north | east | south | west
    short flag: -i

##### toggle various window options

    chunkc window --toggle <option>
    <option>: native-fullscreen | fullscreen | parent | split | float
    short flag: -t

---

#### desktop commands

##### desktop layout

    chunkc desktop --layout <option>
    <option>: bsp | monocle | float
    short flag: -l

##### rotate desktop

    chunkc desktop --rotate <option>
    <option>: 90 | 180 | 270
    short flag: -r

##### mirror desktop

    chunkc desktop --mirror <option>
    <option>: vertical | horizontal
    short flag: -m

##### equalize size of all windows on desktop

    chunkc desktop --equalize
    short flag: -e

##### adjust desktop padding

    chunkc desktop --padding <option>
    <option>: inc | dec
    short flag: -p

##### adjust desktop window gap

    chunkc desktop --gap <option>
    <option>: inc | dec
    short flag: -g

##### toggle desktop offset and window gap

    chunkc desktop --toggle offset
    short flag: -t

##### serialize desktop bsp-tree to file

    chunkc desktop --serialize <file
    <file>: /path/to/file
    short flag: -s

##### deserialize desktop bsp-tree from file

    chunkc desktop --deserialize <file
    <file>: /path/to/file
    short flag: -d

---

#### monitor commands

##### focus monitor

    chunkc monitor -f <option>
    <option>: prev | next | index

#### window rules

| filter   | short flag | type      | description                        |
|----------|:----------:|:---------:|:----------------------------------:|
| --owner  | -o         | POSIX ERE | application name matches pattern   |
| --name   | -n         | POSIX ERE | window name matches pattern        |
| --except | -e         | POSIX ERE | window name does not match pattern |

| properties | short flag | value | description                            |
|------------|:----------:|:-----:|:--------------------------------------:|
| --state    | -s         | float | automatically float window             |
| --state    | -s         | tile  | force-tile window regardless of AXRole |

sample rules:

    chunkc rule --owner "System Preferences" --state tile
    chunkc rule --owner Finder --name Copy --state float
