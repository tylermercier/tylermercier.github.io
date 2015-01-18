---
layout: post
title: "Sublime: Tab Size Per Extension"
date: 2015-01-18
categories: blog
---

You can configure sublime to respect 4 space tabs in languages, such as `go` or `python`, while leaving a global default of 2. It will require a little bit of tinkering, however.

On OSX, you will need to add two files to `~/Library/Application Support/Sublime Text 2/Packages/User`

```bash
touch ~/Library/Application Support/Sublime Text 2/Packages/User/Python.sublime-settings

touch ~/Library/Application Support/Sublime Text 2/Packages/User/GoSublime-Go.sublime-settings
```

Then open each file and update your preferences.

```json
{
    "tab_size": 4,
    "translate_tabs_to_spaces": true
}
```

Enjoy no longer fighting with tab sizes.
