# telescope-bookmarks.nvim
A Neovim Telescope extension to open your browser bookmarks right from the editor!

![telescope-bookmarks.nvim](https://user-images.githubusercontent.com/67177269/115862442-c89d7280-a451-11eb-94c5-501095f88ed7.png)

<details>
<summary><em>Screenshot configuration</em></summary>

```lua
require('telescope').extensions.bookmarks.bookmarks(
  require('telescope.themes').get_dropdown {
    width = 0.8,
    results_height = 0.8,
    previewer = false,
  }
)
```

</details>


Supported browsers on the respective OS:

<table>
  <thead>
    <tr>
       <th rowspan=2>Browser</th>
       <th colspan=3>Operating System</th>
    </tr>
    <tr>
      <td align=center>MacOS</td>
      <td align=center>Linux</td>
      <td align=center>Windows</td>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Google Chrome</td>
      <td align=center>☑️</td>
      <td align=center>☑️</td>
      <td align=center>☑️</td>
    </tr>
    <tr>
      <td>Brave</td>
      <td align=center>☑️</td>
      <td align=center>☑️</td>
      <td align=center>☑️</td>
    </tr>
    <tr>
      <td>Safari <a href="https://github.com/dhruvmanila/telescope-bookmarks.nvim#Safari"><sup>[1]</sup></a></td>
      <td align=center>☑️</td>
      <td align=center>-</td>
      <td align=center>-</td>
    </tr>
    <tr>
      <td>Firefox <a href="https://github.com/dhruvmanila/telescope-bookmarks.nvim#Firefox"><sup>[2]</sup></a></td>
      <td align=center>☑️</td>
      <td align=center>☑️</td>
      <td align=center>☑️</td>
    </tr>
  </tbody>
</table>

_Please take a look at the [**Caveats**](https://github.com/dhruvmanila/telescope-bookmarks.nvim#Caveats) section if you're planning to use this plugin with **Safari** and **Firefox** browser_

## Requirements

* [telescope.nvim](https://github.com/nvim-telescope/telescope.nvim)

## Installation

Using [packer.nvim](https://github.com/wbthomason/packer.nvim)

```lua
use 'dhruvmanila/telescope-bookmarks.nvim'
```

Using [vim-plug](https://github.com/junegunn/vim-plug)

```vim
Plug 'dhruvmanila/telescope-bookmarks.nvim'
```

## Telescope Config

Loading the extension:

```lua
require('telescope').load_extension('bookmarks')
```

Extension options:

```lua
require('telescope').setup {
  extensions =
    bookmarks = {
      -- Available: 'brave', 'google_chrome', 'safari'
      selected_browser = 'brave',
      url_open_command = 'open',
    },
  }
}
```

## Available Commands

```vim
Telescope bookmarks

" Using lua function
lua require('telescope').extensions.bookmarks.bookmarks(opts)
```

When you press `<CR>` on a selected bookmark, it will open the URL using the `url_open_command` option in your default browser.

## Caveats

### Safari

The application which is used to run neovim should be allowed full disk access as the bookmarks file (`~/Library/Safari/Bookmarks.plist`) is in a restricted directory. This can be done in ***System Preferences > Security & Privacy > Full Disk Access*** and then click on the checkbox next to your preferred application. Please take a look at the below image for more details:

<details>
  <summary><i>Allow full disk access to the application running neovim (iTerm2)</i></summary>

<img width="668" alt="Full disk access settings" src="https://user-images.githubusercontent.com/67177269/115988185-16db7e80-a5d6-11eb-9667-f37bb288bfa8.png">

</details>

### Firefox

Firefox uses the Mozilla's "mozLz4" format to compress e.g., bookmarks backups (.jsonlz4). This file format is in fact just plain LZ4 data with a custom header: magic number (8 bytes) and uncompressed file size (4 bytes, little endian).

There's a `decompress_file_content` function which will decompress the given file content which is in the above format, but that requires the [LZ4 compression library](https://github.com/lz4/lz4) which needs to be downloaded by the user.

## References

* [Browsing Chrome bookmarks with fzf](https://junegunn.kr/2015/04/browsing-chrome-bookmarks-with-fzf/)
* [Code: plist parser](https://codea.io/talk/discussion/1269/code-plist-parser)
* [Firefox bookmarks file format](https://hg.mozilla.org/mozilla-central/file/tip/toolkit/components/lz4/lz4.js)
