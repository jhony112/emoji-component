# emoji-component
Simple web component for rendering (svg, png, jpg) emojis

-<h2>Installation </h2>

npm install --save emoji-component


-<h2>Configuration</h2>


<h3>emojis</h3>
This component requires you to structure your emojis in a array , for example

Sample emoji list

```
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
  ```
  
<h3>recently_used</h3>
Same as emojis

<h3>onEmojiClicked</h3>
This callback method returns the selected emoji object

   
 <h3>background</h3>
Sets the background of the component




<h3>Usage</h3>
  
  ```<template>
  <div>
    <Emoji :emojis='emoji_list' :recently_used='recently_used' 
    @onEmojiClicked="getSelected" background=grey />
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
                emoji_list:[{
                                "id":"555",
                                "tag": "::happy::",
                                "keywords": ["Happy","Elated"],
                                "source": "1.svg",
                                "category": "Good Mood"},
                                {
                                "id":"555",
                                "tag": "::happy::",
                                "keywords": ["Happy","Elated"],
                                "source": "1.svg",
                                "category": "Good Mood"},
                            ],
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
    ```
