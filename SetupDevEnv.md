# Setting Up Rails Development Environment on Mac OS X

This is for my development environment on my Macs. This was done on a 64bit MBP and a 64bit iMac, both running Mac OS X 10.6.4

Based on [The Install (Snow Leopard Edition)](http://blog.therubymug.com/blog/2010/05/20/the-install-osx.html)

**I am not responsible for anything that may result from following the instructions below. Proceed at your own risk.**

## Setup Dotfiles

From

	http://github.com/hashrocket/dotmatrix
	http://github.com/jferris/config_files
	http://github.com/ryanb/dotfiles

## Remove system gems

	sudo rm -r /System/Library/Frameworks/Ruby.framework/Versions/1.8/usr/lib/ruby/gems/1.8
	sudo gem update --system
	sudo gem clean

## Install [Homebrew](http://github.com/mxcl/homebrew)

	ruby -e "$(curl -fsS http://gist.github.com/raw/323731/install_homebrew.rb)"

## Install [Xcode](http://developer.apple.com/technology/xcode.html)

Be sure to have XCode Tools Version 3.2.1 (1613) or later (there were bugs with the dvd release version).

## Install some tools

  brew install wget

## Install Git

	brew install git

## Install MySQL

	brew install mysql

## Edit my.cnf for UTF-8 ([Source](http://darwinweb.net/articles/configuring-mysql-for-utf8-under-homebrew))

	vim /usr/local/var/mysql/my.cnf
	
The file should contain

	[mysqld]
	collation_server=utf8_general_ci
	character_set_server=utf8
	
Then restart MySQL

	launchctl stop com.mysql.mysqld
	launchctl start com.mysql.mysqld

## Install [RVM](http://rvm.beginrescueend.com/rvm/install/)

	bash < <( curl http://rvm.beginrescueend.com/releases/rvm-install-head )

Edit .bashrc / .profile or .bash_profile

	[[ -s "$HOME/.rvm/scripts/rvm" ]] && source "$HOME/.rvm/scripts/rvm"
	
Source your new .bashrc

	source ~/.bashrc

Then check if RVM installed ok:

	type rvm | head -n1

You should get:

	rvm is a function

## Link Homebrew's Readline

	brew link readline

## Install Rubies ([Source](http://blog.plataformatec.com.br/tag/rvm/))

	rvm install 1.8.7 -C --enable-shared,--with-readline-dir=/usr/local
	rvm install ree -C --enable-shared,--with-readline-dir=/usr/local
	rvm install 1.9.2 -C --enable-shared,--with-readline-dir=/usr/local
	
Setup gemsets ([Source](http://www.cantinaconsulting.com/2010/08/25/rocking-out-with-ruby-rails-and-rvm/))

	rvm gemset create rails2
	rvm gemset create rails3
	rvm use 1.8.7@rails2
	gem install rails
	rvm use 1.8.7@rails3
	gem install rails

Switch between Rails 2 and 3

	rvm use 1.8.7@rails2
			OR
	rvm use 1.8.7@rails3

Finally, set default Ruby

	rvm --default 1.8.7@rails2

## Instal some gems

For Github

	gem install github launchy
	
Setup GitHub [Setting user name, email and GitHub token](http://help.github.com/git-email-settings/)
	
	git config --global user.name "Tekkub"
	git config --global user.email "tekkub@gmail.com"
	
For Rails

	gem install rails mysql capistrano capistrano-ext heroku taps

ERROR: 

	Couldn't create database for {"reconnect"=>false, "encoding"=>"utf8", "username"=>"root", "adapter"=>"mysql", "database"=>"test_development", "pool"=>5, "password"=>nil, "socket"=>"/tmp/mysql.sock"}, charset: utf8, collation: utf8_unicode_ci (if you set the charset manually, make sure you have a matching collation)

_If you get any error regarding the mysql gem try this_

	env ARCHFLAGS="-arch x86_64" gem install mysql -- --with-mysql-dir=/usr/local --with-mysql-config=/usr/local/bin/mysql_config

For IRB

	gem install wirble awesome_print hirb utility-belt bond

## Install ImageMagick

	brew install ghostscript

(See [http://github.com/mxcl/homebrew/issues/issue/528](http://github.com/mxcl/homebrew/issues/issue/528) for SL printing problems)

	brew install imagemagick

## DO SOME MORE STUFF HERE

## Generate SSH public key

	ssh-keygen -t rsa

## Copy SSH public key to GitHub

	cat ./ssh/id_rsa.pub | pbcopy

## [TextMate bundles](http://adventuresincoding.com/2010/05/10-textmate-bundlesplugins-to-boost-your-ruby-on-rails-development-productivity/)

[Ruby on Rails](http://github.com/carlosbrando/ruby-on-rails-tmbundle)

	mkdir -p ~/Library/Application\ Support/TextMate/Bundles
	cd ~/Library/Application\ Support/TextMate/Bundles
	git clone git://github.com/carlosbrando/ruby-on-rails-tmbundle.git "Ruby on Rails.tmbundle"
	osascript -e 'tell app "TextMate" to reload bundles'

[AckMate](http://github.com/protocool/AckMate)

	http://github.com/downloads/protocool/AckMate/AckMate.1.1.2.zip
	
[Lua](http://github.com/textmate/lua.tmbundle)

	mkdir -p ~/Library/Application\ Support/TextMate/Bundles
	cd ~/Library/Application\ Support/TextMate/Bundles
	git clone http://github.com/textmate/lua.tmbundle.git
	osascript -e 'tell app "TextMate" to reload bundles'

## Sources

http://matthewhutchinson.net/2010/7/2/rvm-ree-and-postgres-on-osx-snow-leopard

## PHP 5.3

[PHP 5.3 on Snow Leopard](http://seancoates.com/blogs/php-53-on-snow-leopard)