---
layout: post
title: Searching my Spotify playlists with fzf
published: false
categories: [command line]
---

Spotify, for all it's _great_ features, does not have the functionality to
search personal playlists for songs. Before I continue my rant, here is what I
had in mind when I had started throwing things in the kitchen sink.

![](/images/search_demo.gif)

Most of my Spotify playlists are a bunch of albums strung together one after the
other. I rarely have mix-tape type playlists, which I only create with the
intention of playing at social gatherings (eventually..)

This was not really a problem in the days of yore when Spotify was just a
cool-to-have piece of social capital. But I now have various playlists and have
lost track of the different albums in each playlist. Besides, searching for
songs/albums in personal playlists is not specific to the described scenario.

So I decided to code this [monstrosity](https://github.com/junkmechanic/spotifz)
as I was tired of twiddling my thumbs waiting for them to introduce this in
the actual app.

# spotifz

At the core of all of this is [fzf](https://github.com/junegunn/fzf), which has
become quite a ubiquitous search tool on the command line.  It expects a list of
items which the user can search for and select from. Then, it returns the
selected item(s). That's the gist. It is used here in a similar fashion as one
would use _rofi_ (or _dmenu_). Also, here it is expected as a binary and called
by forking a shell (yep!).

The rest is just dealing with the Spotify API and some caching of _personal
data_.

The interface is quite basic and so there is no point going through all of it's
functionality. Instead, it might be worth putting down a word or two about the
paradigm followed to build the interface, which would set us up to discuss the
main search function seen in the demo above.

## Interface

The interface is made up of *screens*. Here is a display of two screens:
_'Home'_ and _'Devices'_.

![](/images/screens.gif)

Each screen can be thought of as a separate call to fzf with the options for
that screen passed as the list of items. Once an option is selected by the
user, the subsequent call to fzf is made with the options on the selected
screen.
