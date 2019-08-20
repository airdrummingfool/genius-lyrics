# genius-lyrics

This is a custom component for Home Assistant to allow fetching song lyrics from [Genius](https://genius.com).

*NOTE:* this is a work in progress -- expect changes.


## Installation

### With HACS
1. Open HACS Settings and add this repository (https://github.com/robert-alfaro/genius-lyrics) as a Custom Repository (use **Integration** as the category).
2. The `Genius Lyrics` page should automatically load (or find it in the HACS Store)
3. Click `Install`

### Manual
Copy the `genius_lyrics` directory from `custom_components` in this repository, and place inside your Home Assistant installation's `custom_components` directory.


## Setup

1. Sign up for a free account at genius.com and authorize access to the [Genius API](http://genius.com/api-clients) to get your `client_access_token`.
2. Install this component
3. Install markdown card mod [lovelace-markdown-mod](https://github.com/thomasloven/lovelace-markdown-mod)
4. Add the following to your `configuration.yaml`

```
genius_lyrics:
  access_token: "your Genius client access token"

sensors:
  - platform: template
    sensors:
      lyrics:
        friendly_name: "Lyrics"
        value_template: ""
```

5. Create markdown card in lovelace.

```
  - type: markdown
    content: >
      ## [[ sensor.lyrics.attributes.artist ]] - [[ sensor.lyrics.attributes.title ]]

      [[ sensor.lyrics.attributes.lyrics ]]
```

6. Create an automation to call service `genius_lyrics.search_lyrics` upon media_player state change, providing "Artist", "Title".

---

## Screenshot

![lyrics-card](/lyrics-card.png)

---

## Example service call JSON

```json
{
 "artist_name":"Protoje",
 "song_title":"Mind of a King",
 "entity_id":"sensor.lyrics"
}
```

---

Thanks to
 - @johnwmillr for `lyricsgenius` python package!
 - @thomasloven for lovelace `markdown-mod`!
