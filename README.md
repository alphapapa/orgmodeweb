[OrgModeWeb](https://orgmodeweb.org) is a web app to view, edit and search org files.

The idea is to build a sufficiently usable app for org-mode, giving the same searching and viewing experience as in emacs.

## How It Works?

OrgModeWeb works %100 on web browser, no server side coding, caching, database etc. 

It Uses service-workers to work offline. Can be used as a mobile app (PWA) by adding on Home Screen.

OrgModeWeb creates and stores files on LocalStorage of the browser and uses a newly developed fast javascript parser: OrgParser.

Then it searches on the parsed result using the OrgSearcher which produces same results as in emacs org-mode.

Tested and works on latest versions of modern browsers (Chrome, Firefox, Opera, Edge) and Android versions. Haven't tested older versions.
Haven't tested on Safari but since it supports service-workers, should work fine.

## Currently Supported

- **Agenda View :** view agenda similarly in org-mode
- **Match Search :** match tags and properties as described in [org-mode](https://orgmode.org/manual/Matching-tags-and-properties.html) (no regexp or backward compatibility), some examples:

```bash
    +tag1-tag2
    TODO=DONE|tag3
    SCHEDULED="<today>"
```

- **Keyword Search**
- **Custom TODO keywords :** can set custom TODO keywords and styles in settings
- **Habits :** properly view habits on agenda (no graph)
- **Dropbox Sync :** syncronize org files in your Dropbox. Keeps your account key on LocalStorage, there is no server side!

  - file name in color ![g](https://placehold.it/15/00ff00/000000?text=+) : there are no local changes (lastly synced with server)
  - file name in color ![w](https://placehold.it/15/ffffff/000000?text=+) : there are local changes not synchronized
  - file name in color ![r](https://placehold.it/15/ff0000/000000?text=+) : conflict, both local and server files are changed
  - file name in color ![y](https://placehold.it/15/ffff00/000000?text=+) : currently synchronizing the file

- **Category Filter :** filter by category on Agenda and Search views
- **Text Formatting :** \*bold* /italic/ \_underline_ [[links][...]]
- **Keyboard Shortcuts :** similar to emacs org-mode and org-speed-commands
  - **n, p, f, b, u, down, up :** move cursor on headings
  - **t :** set TODO state on headings
  - **o :** open link (if any) on headings
  - **tab, shift+tab :** cycle visibility of heading(s) on file view, go to heading on Agenda and Search views
  - **M-left, M-right, M-S-left, M-S-right:** decrease/increase level of heading
  - **M-<, M-> :** go-to beginning and end of file
  - **C-enter :** create new file/heading/setting
  - **return :** edit file/heading/setting
  - **C-l :** center current heading on screen
  - **enter :** goto file (on file menu), open link (on heading)
  - **< :** category filter on Agenda and Search views
  - **M-x :** menu
  - **M-s :** settings (on menu page)
- **Custom Agenda Views :** custom agendas similarly in org mode

      as an example: 3-day agenda with projects listing and keyword search
      create a new setting in settings
      set setting name: custom-agenda-b (last letter will be the shortcut key)
      set value as below
      each line corresponds to a search section
      there are 3 types of sections: agenda, tags, search

  ```bash
    --type agenda --agenda-span 3 --header "My Agenda"
    --type tags --filter +prj --header "My Projects"
    --type search --text "#key"
  ```

  ## Limitations

  - LocalStorage limit of browsers are generally 5MB (some are 10MB). Because org files are stored on LocalStorage, it seems to limit the size, but haven't tested it yet.
  - When saving the org file, Org-mode-web tries to keep the file as similar as possible, however minor differences may occur such as number of empty lines, but the information will be same.

  ## Installation

  ```bash
    npm i
  ```

  - to start server

  ```bash
    gulp serve
  ```

  - to start unit tests

  ```bash
    gulp test
  ```
  
  - to create dist package (on /dist folder)

  ```bash
    gulp
  ```