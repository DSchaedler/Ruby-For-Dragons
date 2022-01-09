---
title: DragonRuby API Documentation
layout: default
resource: true
categories: [Docs]
---

{% include header.html %}

# GTK
`notify!` - Creates a toast notification. Takes arguments `string`.  
## Network
`http_get` - Creates `GET` request. Takes arguments `url`, `extra_headers = {}`.  
`http_post` - Creates `POST` request. Takes arguments `url`, `form_fields = {}`, `extra_headers = {}`.  
`start_server!` - Launches the embedded HTTP server. Takes arguments `port: [Integer]`, and `enable_in_prod: [Boolean]`

[Back to Top](/Ruby_for_Dragons/DragonRuby-API-Documentation)

# Inputs
`http_requests` - Array of HTTP `GET` and `POST` requests received. Array Items are instances of a `request` class with the following attributes:
* Attributes
  * `.address`
  * `.body`
  * `.headers` - A hash of HTTP headers for this request
    * `Connection`
    * `Content-Type`
    * `User-Agent`
    * `Content-Length`
    * `Host`
  * `.id`
  * `.method` - `GET` or `POST`
  * `.raw_body`
  * `.uri`- Subdirectory of Top Level Domain

* Methods
  * `.respond`
  * `.reject`

## Controller

[Back to Top](/Ruby_for_Dragons/DragonRuby-API-Documentation)

## Keyboard

### Character Keys
`exclamation_point` - \!  
`zero` - 0  
`one` - 1  
`two` - 2  
`three` - 3  
`four` - 4  
`five` - 5  
`six` - 6  
`seven` - 7  
`eight` - 8  
`nine` - 9  
`enter` - ⏎  
`tab` - ↹  
`open_round_brace` - \(  
`close_round_brace` - \)  
`open_curly_brace` - \{  
`close_curly_brace` - \}  
`open_square_brace` - \[  
`close_square_brace` - \]  
`colon` - :  
`semicolon` - ;  
`equal_sign` - =  
`hyphen` - -  
`space` - ⎵  
`dollar_sign` - $  
`double_quotation_mark` - "  
`single_quotation_mark` - '  
`backtick` - \`  
`tilde` - ~  
`period` - \.  
`comma` - ,  
`pipe` - |  
`underscore` - \_  
`a` - a  
`b` - b  
`c` - c  
`d` - d  
`e` - e  
`f` - f  
`g` - g  
`h` - h  
`i` - i  
`j` - j  
`k` - k  
`l` - l  
`m` - m  
`n` - n  
`o` - o  
`p` - p  
`q` - q  
`r` - r  
`s` - s  
`t` - t  
`u` - u  
`v` - v  
`w` - w  
`x` - x  
`y` - y  
`z` - z  
`plus` - \+  
`at` - @  
`forward_slash` - \/  
`back_slash` - \\  
`asterisk` - \*  
`less_than` - <  
`greater_than` - >  
`carat` - ^  
`ampersand` - &  
`superscript_two` - ²  
`circumflex` - ˆ  
`question_mark` - ?  
`section_sign` - §  
`ordinal_indicator` - º  

### Control Keys
`alt` - Alt / ⌥ Option   
`meta` - ⊞ Win / ⌘  
`control` - Ctrl  
`shift` - Shift  
`backspace` - Backspace  
`delete` - Del  
`escape` - Esc  
`left` - ←  
`right` - →  
`up` - ↑  
`down` - ↓  
`pageup` - Page Up  
`pagedown` - Page Down  

### Special Keys
`left_right` - Returns `-1` for `left`, `1` for `right`, or `0` for neither.  
`up_down` - Returns `-1` for `down`, `1` for `up`, or `0` for neither.  
`ctrl_KEY` - Dynamic method, eg `args.inputs.keyboard.ctrl_a`.  
`directional_vector` - Returns a normal vector `[x, y]`, or `nil`. Possible values for `x` and `y` are `0`, `1`, `-1`, `0.707`, `-0.707`. `0,707` is used when a diagonal direction is input.  
`truthy_keys` - Returns a collection of Symbols that represent all keys that are in the pressed or held state.     
`char` - **Not Defined**   

[Back to Top](/Ruby_for_Dragons/DragonRuby-API-Documentation)

## Mouse

### Mouse Buttons
`args.inputs.mouse.bits`  
`args.inputs.mouse.button_left`  
`args.inputs.mouse.button_middle`  
`args.inputs.mouse.button_right`  
`args.inputs.mouse.click`  
`args.inputs.mouse.click.inside_circle? [circle_center_x, circle_center_y], radius`  
`args.inputs.mouse.click.inside_rect? [x, y, width, height]`  
`args.inputs.mouse.down`  
`args.inputs.mouse.down.inside_circle? [circle_center_x, circle_center_y] radius`  
`args.inputs.mouse.down.inside_rect? [x, y, width, height]`  
`args.inputs.mouse.previous_click`  
`args.inputs.mouse.previous_click.inside_circle? [circle_center_x, circle_center_y], radius`  
`args.inputs.mouse.previous_click.inside_rect? [x, y, width, height]`  
`args.inputs.mouse.up`  
`args.inputs.mouse.up.inside_circle? [circle_center_x, circle_center_y], radius`  
`args.inputs.mouse.up.inside_rect? [x, y, width, height]`  
`args.inputs.mouse.wheel`  
`args.inputs.mouse.wheel.x`  
`args.inputs.mouse.wheel.y`  

### Mouse Location

`args.inputs.mouse.inside_circle? [circle_center_x, circle_center_y], radius`  
`args.inputs.mouse.inside_rect? [x, y, width, height]`  
`args.inputs.mouse.moved`  
`args.inputs.mouse.x`  
`args.inputs.mouse.y`  

[Back to Top](/Ruby_for_Dragons/DragonRuby-API-Documentation)

# Outputs
## Borders
`args.outputs.borders << [x, y, width, height]`

## Labels
`args.outputs.labels << [x, y, "string"]`

## Lines
`args.outputs.lines << [x, y, x2, y2]`

## Primitives
`args.outputs.primitives <<[x, y, width, height].solid!`

## Solids
`args.outputs.solids << [x, y, width, height]`

## Sounds
`args.outputs.sounds << 'path/sound.ogg'`

## Sprites
`args.outputs.sprites << [x, y, width, height, 'path/sprite.png']`

[Back to Top](/Ruby_for_Dragons/DragonRuby-API-Documentation)

{% include footer.html %}
