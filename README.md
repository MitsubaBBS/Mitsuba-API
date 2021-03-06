Mitsuba API
===========

## Welcome ##

Welcome to Mitsuba's poorly documented read-only JSON API guide!

JSON representations of threads are exposed at the following URLs:

http(s)://example.com/`board`/res/`threadnumber`.json

*This guide was last updated July 06, 2013.*

### Posts Object ####

| **attribute**   | **value**      | **description**      | **possible values**                        | **example value**     |
|:----------------|:---------------|:---------------------|:-------------------------------------------|:----------------------|
| `no`            | `integer`      | Post number          | 1-9999999999999                            | `9001`                |
| `resto`         | `integer`      | Reply to             | 0 (is thread), 1-9999999999999             | `0`                   |
| `sticky`        | `integer`      | Stickied thread?     | 0 (no), 1 (yes)                            | `1`                   |
| `closed`        | `integer`      | Closed thread?       | 0 (no), 1 (yes)                            | `0`                   |
| `now`           | `string`       | Date and time        | MM\/DD\/YY(Day)HH:MM (:SS on some boards)  | `08\/08\/12(Wed)01:11`|
| `time`          | `integer`      | UNIX timestamp       | UNIX timestamp                             | `1344570123`          |
| `name`          | `string`       | Name                 | text                                       | `moot`                |
| `trip`          | `string`       | Tripcode             | text (format: !tripcode!!securetripcode)   | `!Ep8pui8Vw2`         |
| `id`            | `string`       | ID                   | text (8 characters), Mod, Admin, Developer | `Admin`               |
| `capcode`       | `string`       | Capcode              | none, mod, admin, admin_highlight, developer | `admin`             |
| `country`       | `string`       | Country code         | text (2 characters, ISO 3166-1 alpha-2), XX (unknown) | `XX`       |
| `country_name`  | `string`       | Country name         | text                                       | `Unknown`             |
| `email`         | `string`       | Email                | text                                       | `moot@4chan.org`      |
| `sub`           | `string`       | Subject              | text                                       | `This is a subject`   |
| `com`           | `string`       | Comment              | text (includes escaped HTML)               | `This is a comment`   |
| `files`         | `array`        | Files info           | array (described lower)                    |                       |
| `filedeleted`   | `integer`      | File deleted?        | 0 (no), 1 (yes)                            | `0`                   |
| `spoiler`       | `integer`      | Spoiler image?       | 0 (no), 1 (yes)                            | `0`                   |
| `custom_spoiler`| `integer`      | Custom spoilers?     | 1-99                                       | `3`                   |

### Files array ###

| **attribute**   | **value**      | **description**      | **possible values**                        | **example value**     |
|:----------------|:---------------|:---------------------|:-------------------------------------------|:----------------------|
| `tim`           | `integer`      | Renamed filename     | UNIX timestamp + microseconds              | `1344402680740`       |
| `filename`      | `string`       | Original filename    | text                                       | `OPisa`               |
| `ext`           | `string`       | File extension       | .jpg, .png, .gif, .pdf, .swf               | `.jpg`                |
| `fsize`         | `integer`      | File size            | 1-8388608                                  | `2500`                |
| `md5`           | `string`       | File MD5             | text (24 character, packed base64 MD5 hash)| `NOetrLVnES3jUn1x5ZPVAg==` |
| `w`             | `integer`      | Image width          | 1-10000                                    | `500`                 |
| `h`             | `integer`      | Image height         | 1-10000                                    | `500`                 |
| `tn_w`          | `integer`      | Thumbnail width      | 1-250                                      | `250`                 |
| `tn_h`          | `integer`      | Thumbnail height     | 1-250                                      | `250`                 |


**Note the following attributes are optional:**  
`sticky` `closed` (only displays on OPs when true)  
`id` (only displays when board has DISPLAY_ID set)  
`name` (only displays if name is present, which is always unless there is a blank name and tripcode)  
`trip` (only displays if tripcode is present)  
`email` (only displays if email is present)  
`sub` (only displays if subject is present)  
`com` (only displays if comment is present)  
`capcode` (only displays when using a capcode)  
`country` `country_name` (only displays when board uses country flags)  
`filename` (only displays when image uploaded)  
`ext` (only displays when image uploaded)  
`fsize` (only displays when image uploaded)  
`md5` (only displays when image uploaded)  
`w` (only displays when image uploaded)  
`h` (only displays when image uploaded)  
`tn_w` (only displays when image uploaded)  
`tn_h` (only displays when image uploaded)  
`filedeleted` (only displays when image uploaded)  
`spoiler` (only displays when image uploaded)  
`custom_spoiler` (only display on OPs, only displays when board has custom spoiler images)  
`omitted_posts` (only displays on OPs on index pages)  
`omitted_images` (only displays on OPs on index pages)  
`replies` (only displays on OPs)  
`images` (only displays on OPs)  
`bumplimit` (only displays on OPs when true)  
`imagelimit` (only displays on OPs when true)  

**Note about custom spoilers:**  
`custom_spoiler` describes the number of custom spoilers that exist for the specified board. If the number is `4`, it means that you can choose anywhere from 1 to 4. 
For our imageboard pages, the custom spoiler images changes every time a new post is made. If you are writing a browser add-on with auto-update 
functionality, you should first check the HTML to see if a custom spoiler has been posted, and use the same number, so when new spoiler posts come in, they match the pre-existing ones. 
If there are no custom spoilers already in a thread, you can just random whatever you'd like, since there is no need to match pre-existing ones.

### Where are the files? ###

Boards: http(s)://boards.4chan.org/`board`/  
Indexes: http(s)://boards.4chan.org/`board`/`[1-10]` (# of pages varies per board, directory root is page 0)  

Threads: http(s)://boards.4chan.org/`board`/res/`resto`  
Replies: http(s)://boards.4chan.org/`board`/res/`resto`#p`no`  

Images: http(s)://images.4chan.org/`board`/src/`tim`.`ext`  
Thumbnails: http(s)://thumbs.4chan.org/`board`/thumb/`tim`s.jpg  

Spoiler image: http(s)://static.4chan.org/image/spoiler.png  
Custom spoilers: http(s)://static.4chan.org/image/spoiler-`board``custom_spoiler`.png  

Closed thread icon: http(s)://static.4chan.org/image/closed.gif  
Sticky thread icon: http(s)://static.4chan.org/image/sticky.gif  
Admin capcode icon: http(s)://static.4chan.org/image/adminicon.gif  
Mod capcode icon: http(s)://static.4chan.org/image/modicon.gif  
Developer capcode icon: http(s)://static.4chan.org/image/developericon.gif  
File deleted (for OPs): http(s)://static.4chan.org/image/filedeleted.gif  
File deleted (for replies): http(s)://static.4chan.org/image/filedeleted-res.gif  

Country flags: http(s)://static.4chan.org/image/country/`country`.gif  
/pol/ country flags: http(s)://static.4chan.org/image/country/troll/`country`.gif  

### Examples ###

To view a pretty-printed version of our thread, index, and catalog JSON, use [JSONLint](http://jsonlint.com).
