---
layout: post
title: Programming environment
summary: How to I set up my programming environment.
tags: [git, cygwin]
css:
- /css/pygments.css
- /css/gist.css
---


## Cygwin

with:
* mintty ("link":http://code.google.com/p/mintty/)
* git ("link":http://git-scm.com/)
* git-completion
* gitk
* openssh
* wget
* sqlite3
* rsync
* mc
* lighttpd

cygrunsrv --install php5 --path /usr/local/php-5.3.1/php-cgi.exe -a '-b 127.0.0.1:9000'

add to ~/.bashrc

```bash
source /etc/bash_completion.d/git

export PS1='
\[\033[32m\]\u@\h \[\033[33m\w$(__git_ps1)\033[0m\]
$ '
export DISPLAY=127.0.0.1:0.0

alias ui='cd /c/Code/yoga/web'
alias web='cd /c/Code/github/lauriro.github.com'

alias ssh-add='if ! kill -0 "$SSH_AGENT_PID" 2>/dev/null; then ssh-agent >~/ssh-agent-pid; fi; source ~/ssh-agent-pid; ssh-add'

alias ssh-sandy='ssh -oproxycommand="ssh -p 11822 lauri@195.50.194.58 nc %h %p" '

alias runphp='/usr/local/php-5.3.1/php-cgi.exe -b 127.0.0.1:9000 &'
alias runwww='kill `cat /var/run/lighttpd.pid` 2>/dev/null; /usr/sbin/lighttpd -f /etc/lighttpd/lighttpd.conf'

alias diffmerge='/c/Box/soft/DiffMerge/DiffMerge.exe'
alias runx='XWin.exe -screen 0 -multiwindow -clipboard -xkblayout ee > /dev/null 2>&1 &'

```

prepare git

```bash
#!/bin/sh
git config --global user.name 'Lauri Rooden' 
git config --global user.email <me>@<email>
```

<script src="http://gist.github.com/285926.js"></script>

h2. Notepad++ ("link":http://notepad-plus.sourceforge.net/)

with:
* "Context Menu Component":http://notepad-plus.sourceforge.net/commun/misc/NppShell.zip copy to your notepad++ directory and run reg.bat
* "Plugins":http://sourceforge.net/apps/mediawiki/notepad-plus/index.php?title=Plugin_Central
** Explorer plugin (Light Explorer removed)
** LanguageHelp
** Function List


p(highlight_header). run_editor.sh ( "download":/notes/run_editor.sh )

```bash
#!/bin/sh
/c/soft/npp/notepad++.exe -multiInst -notabbar -nosession -noPlugin "`cygpath -w "${1}"`"
```

## DiffMerge ("link":http://www.sourcegear.com/diffmerge/)


## Lighttpd ("link":http://www.lighttpd.net/)

```bash
fastcgi.server = ( ".php" =>( "localhost" =>("host" => "127.0.0.1","port" => 9000, "docroot" => "C:\web", "allow-x-send-file" => "enable" )))

$HTTP["url"] =~ "^/(images)/" {
	proxy.server  = ( "" => ( 
		("host" => "192.168.24.84", "port" => 8080 )
	) )
}
```

## nginx ("link":http://nginx.net/)

as a webserver

## php ("link":http://php.net/)

On FreeBSD:

```bash
pkg_add -r pkg-config
pkg_add -r libiconv
pkg_add -r libxml2

wget http://php-fpm.anight.org/downloads/head/php-5.2.8-fpm-0.5.10.diff.gz

wget http://ee2.php.net/get/php-5.2.8.tar.bz2/from/ee.php.net/mirror

bzip2 -cd php-5.2.8.tar.bz2  | tar xf -
gzip -cd php-5.2.8-fpm-0.5.10.diff.gz | patch -d php-5.2.8 -p1

cd php-5.2.8

./configure --enable-fastcgi --enable-fpm --with-pgsql
./configure --enable-memory-limit --with-layout=GNU --with-config-file-scan-dir=/usr/local/etc/php --disable-all --enable-libxml --with-libxml-dir=/usr/local --enable-spl --with-regex=php --disable-cli --enable-fastcgi --enable-fpm --with-pgsql

make all install
```

"DropboxPath":http://wiki.getdropbox.com/DropboxAddons/DropboxPath
C:\soft\DropboxPath>DropboxPath.exe "C:\dropbox"
