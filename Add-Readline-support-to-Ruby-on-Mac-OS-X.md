#### NOTE: guard-zeus causes issues when typing into the Pry session. 
##### See: https://github.com/guard/guard-zeus/issues/18 for a workaround

# Adding Readline support to Pry

If you are on Mac OS X and have problems with either Guard not reacting to file changes or Pry behaving strangely, then you probably suffer under a Ruby build that uses `libedit` instead of `readline`.

If you are not using Mac OS X or are using JRuby, then you're fine.

## Option 1: Build Ruby With GNU Readline Using RVM

You can use [RVM](https://rvm.io/) to build your Ruby with GNU readline support. First install the readline package with RVM:

```Bash
$ rvm pkg install readline --verify-downloads 1
```

Then configure RVM to use the readline package by adding

```Bash
ruby_configure_flags=--with-readline-dir="$rvm_path/usr"
```

to `~/.rvm/user/db`. Finally you need to reinstall your Ruby of choice:

```Bash
$ rvm reinstall 2.3.1
```

## Option 2: Build Ruby With GNU Readline Using RVM and Homebrew

You can also install the latest Readline with [Homebrew](http://mxcl.github.com/homebrew/). First install Readline:

```Bash
$ brew install readline
$ brew link readline
```

Then configure RVM to use the Homebrew readline by adding

```Bash
ruby_configure_flags=--with-readline-dir=/usr/local/opt/readline
```

to `~/.rvm/user/db`. Finally you need to reinstall your Ruby of choice:

```Bash
$ rvm reinstall 1.9.3
```

## Option 3: Build Ruby With GNU Readline Using rbenv, ruby_build and Homebrew

As a rbenv user, you can install readline and ruby_build with Homebrew:

```bash
$ brew install readline ruby-build
```

now set the configure options when compile Ruby:

```
$ RUBY_CONFIGURE_OPTS=--with-readline-dir=`brew --prefix readline` rbenv install 2.3.1
```

## Option 4: Using a pure Ruby readline implementation

The easiest way to get a working readline implementation is to install [rb-readline](https://github.com/luislavena/rb-readline), a pure Ruby readline implementation. You can install it by simply adding

```Ruby
group :development do
  gem 'rb-readline'
end
```

to your `Gemfile` and install it with `bundle exec`.