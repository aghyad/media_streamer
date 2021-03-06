# Media Streamer

A simple music server using Sinatra. Yarr.

Requirements
------------

#### Ruby Version
Ruby 2.1.5 or higher (although, anything from 1.9.3 on should work but I won't guarantee it)

#### Gems
* activesupport
* eventmachine
* multi_json
* sinatra
* sinatra-contrib
* taglib-ruby
* thin

#### Libraries
* [TagLib](http://taglib.github.io/)

Installation
------------

    $ git clone git@github.com:seaneshbaugh/media_streamer.git media_streamer
    $ cd media_streamer
    $ bundle install

Usage
-----

```ruby
rackup
```

This application defaults to development mode (like all Sinatra applications). To run in production mode do the following:

```ruby
RAKE_ENV=production rackup
```

To run on a different port:

```ruby
rackup -p 9999
```

Example settings.yml
--------------------

Because the settings I use are guaranteed to be different from the settings you will use I've excluded my settings.yml file from source control. Below are some sample settings:

    development:
      music_directory: "/Users/me/Music/"
      allowed_file_types:
        - "mp3"
        - "m4a"
        - "ogg"
      default_encoding: "utf-8"
      file_blacklist:
        - "Automatically Add to iTunes"
        - "Automatically Add to iTunes.localized"
        - "Mobile Applications"
        - "Album Artwork"

    production:
      music_directory: "J:/Music/"
      allowed_file_types:
        - "mp3"
        - "m4a"
        - "ogg"
      default_encoding: "utf-8"
      file_blacklist:
        - "Automatically Add to iTunes"
        - "Automatically Add to iTunes.localized"
        - "Mobile Applications"
        - "Album Artwork"
      protection:
        except: :json_csrf

You will obviously want to set the `music_directory` to wherever your music lives.

For a complete list of Sinatra's available settings go [here](http://www.sinatrarb.com/intro#Available%20Settings).

Currently the only settings specific to this application are `music_directory`, `allowed_file_types`, and `file_blacklist`. All three are required.

HTML5 Audio and Browser Support
-------------------------------

This application will attempt to use the [HTML5 audio element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/audio) to play songs in the page. If the browser does not support the audio element then it will fall back to the default behavior of letting the browser decide what to do (which is typically playing the file in the browser). Right now this means browsers that don't support playing the format of your files will not work properly. Check this [comprehensive list of browser support for media types](https://developer.mozilla.org/en-US/docs/HTML/Supported_media_formats#Browser_compatibility) to see if your browser can play a desired format. As of now Chrome or Safari is your best bet for media format support. Since most everyone has their songs encoded in mp3 this effectively rules out Firefox on non-Windows platforms.

Notes
-----

* Use this at your own risk.
* You'll probably need to set up port forwarding for your router.
* It is highly recommended you keep the robots.txt file in place.
