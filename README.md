# GData

This is a fork of the official Gdata gem:

* http://code.google.com/p/gdata

So far, the only change is to allow support for Ruby 1.9.x by removing the `jcode` requirement in `lib/gdata.rb`.

To install this in a Bundler-enabled project, add the following line to your Gemfile:

    gem 'gdata', :git => 'git://github.com/pjmorse/gdata.git'

Note that much of the Install directions below don't apply to this fork.

## DESCRIPTION:

Ruby wrapper for working with Google Data APIs

## SYNOPSIS:

    yt = GData::Client::YouTube.new
    yt.source = 'my_cool_application'
    yt.clientlogin('username', 'password')
    yt.client_id = 'CLIENT_ID'
    yt.developer_key = 'DEVELOPER_KEY'
    feed = yt.get('http://gdata.youtube.com/feeds/api/users/default/uploads').to_xml
  
    # creating, updating, and deleting a playlist
  
    entry = <<-EOF
    <entry xmlns="http://www.w3.org/2005/Atom"
        xmlns:yt="http://gdata.youtube.com/schemas/2007">
      <title type="text">Ruby Utility Unit Test</title>
      <summary>This is a test playlist.</summary>
    </entry>
    EOF
  
    response = yt.post('http://gdata.youtube.com/feeds/api/users/default/playlists', entry).to_xml
  
    edit_uri = response.elements["link[@rel='edit']"].attributes['href']
  
    response.elements["summary"].text = "Updated description"
  
    response = yt.put(edit_uri, response.to_s).to_xml
  
    yt.delete(edit_uri).to_xml
  
    # uploading a video
  
    test_movie = '/path/to/a/movie.mov'
    mime_type = 'video/quicktime'
    feed = 'http://uploads.gdata.youtube.com/feeds/api/users/default/uploads'

    entry = <<EOF
    <entry xmlns="http://www.w3.org/2005/Atom"
      xmlns:media="http://search.yahoo.com/mrss/"
      xmlns:yt="http://gdata.youtube.com/schemas/2007">
      <media:group>
        <media:title type="plain">Test Movie</media:title>
        <media:description type="plain">
          This is a test with the Ruby library
        </media:description>
        <media:category
          scheme="http://gdata.youtube.com/schemas/2007/categories.cat">People
        </media:category>
        <media:keywords>test,lame</media:keywords>
      </media:group>
    </entry>
    EOF
   
    response = @yt.post_file(feed, test_movie, mime_type, entry).to_xml

## REQUIREMENTS:

* A sunny disposition

Tested against Ruby 1.9.3 patch level 194

## INSTALL:

    -sudo gem install gdata- // see note above about Bundler

To generate documentation:

    rake doc
  
To run unit tests:
  
    cp test/test_config.yml.example test/test_config.yml
    # edit test/test_config.yml
    rake test

## LICENSE:

Copyright (C) 2008 Google Inc.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

      http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.