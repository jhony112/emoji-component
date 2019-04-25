# emoji-component
Simple web component for rendering (svg, png, jpg) emojis

-<h2>Installation </h2>

npm install --save emoji-component


-<h2>Configuration</h2>
<p>emojis</p>
This component requires you to structure your emojis in a array , for example

Sample emoji list

[
  {
    "id":"555",
    "tag": "::happy::",
    "keywords": [
      "Happy",
      "Ecstatic",
      "Joyful",
      "Great",
      "Elated"
    ],
    "source": "1.svg",
    "category": "Good Mood"
  },
  {
    "id":"315",
    "tag": "::sad::",
    "keywords": [
      "Sad",
      "Sorrowful",
      "Disappointed"
    ],
    "source": "2.svg",
    "category": "Bad Mood"
  }
  ]
<p>recently_used</p>
Same as emojis

<p>onEmojiClicked</p>
This method returns the selected emoji object
i.e
 {
    "id":"315",
    "tag": "::sad::",
    "keywords": [
      "Sad",
      "Sorrowful",
      "Disappointed"
    ],
    "source": "2.svg",
    "category": "Bad Mood"
  }

<p>background</p>
Sets the background of the component


-<h2>Usage</h2>

<template>
  <div>
    <Emoji :emojis='emoji_list' :recently_used='recently_used' @onEmojiClicked="getSelected" background=grey />
  </div>
</template>

<script>
import Emoji from 'emoji-component'
 export default {
        name: 'app',
        components: {
            Emoji
        },

        data: function () {
            return {
                emoji_list:[
  {
    "id":"555",
    "tag": "::happy::",
    "keywords": [
      "Happy",
      "Ecstatic",
      "Joyful",
      "Great",
      "Elated"
    ],
    "source": "1.svg",
    "category": "Good Mood"
  },
  ] ,
                recently_used: []
            };
        },
        methods: {
            getSelected: function (emoji) {
            //callback on emoji clicked 
                console.log(emoji)
            }
        }
    }
</script>
