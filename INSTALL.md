# Jekyll on Linux

## Prerequisites

### Debian

```
sudo apt-get install ruby-full build-essential
```

### Ubuntu

```
sudo apt-get install ruby-full build-essential zlib1g-dev
```

## Jekyll

```
echo '# Install Ruby Gems to ~/gems' >> ~/.bashrc
echo 'export GEM_HOME="$HOME/gems"' >> ~/.bashrc
echo 'export PATH="$HOME/gems/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

```
gem install jekyll bundler
```

## Run

```
# Install Bundler
gem install bundler.

# Install gems in your Gemfile
bundle install
bundle exec jekyll serve
```