---
title: "Emacs For Windows 10 : Install All The Icons."
slug: emacs-for-windows-10-install-all-the-icons
date_published: 2021-01-09T21:12:55.000Z
date_updated: 2021-09-12T01:54:12.000Z
tags: Emacs, icons, all-the-icons-install-fonts
---

In emacs, if you ever run into the need to have access to all the icons and fonts, may it be for doom-emacs icons bar, or centaur-emacs icons and font or Spacemacs icons, 
you will have to run this command inside of Emacs (M-x meaning Alt+x which is to access the Emac's mini-buffer)

1. You install the package all-the-icons from [Melpa](https://melpa.org/#/getting-started)
2. You do the command all-the-icons-install-fonts from the minibuffer
3. you install the files generated.

    M-x package-install all-the-icons 
    
    M-x all-the-icons-install-fonts

![](/content/images/2021/01/image-7.png)
BUT THEN it is important to go to the folder where you installed the fonts and install manually all the files that appeared after this command.

![](/content/images/2021/01/image-20.png)
Now, make sure to click and install every one of them. After which the icons should show nicely on your Emacs.

enjoy :D !
