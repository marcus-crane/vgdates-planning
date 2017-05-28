# How are titles stored?

## What are the main problems with game release dates

Part of the issue with keeping a calendar for game releases is that there's so many possible combinations!

A game can have release dates that differ:
  * Per region
    - Usually mid-level games will release in the US on a Tuesday and then in the EU on a Friday purely for boring historical reasons
    - Big AAA games like Pokemon or Grand Theft Auto tend to have a unified worldwide release date
    - Japanese developed titles may have a lengthy delay coming over to the West due to localization or just plain lack of interest. Yakuza, Persona and Danganronpa are popular series that are examples of this happening.
  * Per platform
    - On the odd occasion, a PC port may be delayed intentionally by ~ 2 weeks to give it extra polish
    - While we've transitioned to the PS4/Xbox One generation for the most part, there may still be releases for eg; PS3/Xbox 360 or handhelds that are delayed
  * Per episode
    - Telltale games are a good example of this. A 5 episode series releasing monthly is considered 5 different entries but the completed on disc/Season X release is also considered its own entry as far as retail goes.
  * Early Access
    - When is a game considered "released". If there's an anticipated Early Access title, the initial release date may be worth listing on top of the actual final release date
  * Alpha / Betas
    - An upcoming, usually AAA release, will often have a public beta or "network test" which is considered its own title and those too may differ across platforms
    - It also would need to be listed based on a time span as it's not a product that is either Released or Unreleased.

While not necessarily a comprehensive list, I believe that covers most of the combinations that are likely to pop up plus a few edge cases I hadn't considered until now.

Things like Early Access and Alphas/Betas wouldn't be listed until much later on but it's still useful to note them down.

## What are some examples of release calendaring that already exists

We'll mainly be looking at game databases/game release charts/game stores in this instance.

### Publishers

Presumably, publishers don't have to worry as much seeing as they only need to keep track of their upcoming releases and all public information is generally just text based (marketing posters, investor releases etc) so that's not very useful.

### Game stores

Game stores assign every platform variation its own SKU (stock keeping unit) and tie the release date to it. Since game stores are regionalised, they don't have to worry about differing release dates at all.

### Giant Bomb

This is probably the most useful out of any of the existing resources in terms of how the data might end up structured

Games are stored roughly like so using Metroid Prime (2002) as an example:

```json
// Note: This is a fictional object that represents the page layout
// It is not an excerpt from the Giant Bomb API

{
  "name": "Metroid Prime",
  "released": "2002-11-18",
  "platforms": [
    "Gamecube",
    "Wii"
  ],
  "releases": [
    {
      "name": "Metroid Prime",
      "platform": "Gamecube",
      "region": "United States",
      "date": "2002-11-18"
    },
    {
      "name": "Metroid Prime",
      "platform": "Gamecube",
      "region": "Japan",
      "date": "2003-02-28"
    },
    {
      "name": "Metroid Prime",
      "platform": "Gamecube",
      "region": "United Kingdom",
      "date": "2003-03-21"
    },
    {
      "name": "Metroid Prime (Player's Choice)",
      "platform": "Gamecube",
      "region": "United States",
      "date": "2003-09-25"
    }
  ]
}
```

It's a decent example and there's definitely some ups and downs to this approach.

Pros:

  - I like the idea that the game itself is a single entity with releases underneath it. This is essentially what I was headed towards anyway.
  - It should allow for individual game pages should I choose to have those but would probably require that I do have an overview outside of releases with an array of platforms and what not
  - Grouping the release dates with the platforms themselves will probably be the best way to keep track of everything. 

Cons:

  - For the model that the site would be using, it's a bit redundant listing the name with each entry. It makes total sense for localised names (primarily Japan) but I don't feel I would have an accurate enough source. As a Westerner, I would struggle to find a list of upcoming Japanese titles (that aren't just releases of Western titles) and have enough context to know if the dates are accurate or how to search for a better copy of the cover art
  - The "overview" release date shown is simply the first release date (United States on the Gamecube in this case) which can be confusing without it being outright stated and has a bias towards the United States by default.
  - Each "release" is essentially just every possible combination of region and platform and is probably just reflecting every possible SKU which I feel wouldn't be the most efficient way of storing all this information. I also won't be storing variations like "Player's Choice" which that style is more suited towards.
  - Most of this information will realistically be discarded by an end user. I imagine a user would be prompted to choose their region (or it would be inferred from their timezone) and as such, any releases in Japan or the US won't be visible in the first place.

## Proposed JSON formats

Here are some examples of how I could model information for a game.

* Store each platform/date combination as an object within a regional array:

```json
{
  "name": "Grand Theft Auto V"
  "releases": [{
    "US": [{
      "platform": "PS3",
      "date": "2013-09-17"
    },
    {
      "platform": "X360",
      "date": "2013-09-17"
    },
    {
      "platform": "PS4",
      "date": "2014-11-18"
    },
    {
      "platform": "XONE",
      "date": "2014-11-18"
    }
    {
      "platform": "PC",
      "date": "2015-04-14"
    }],
    "EU": [{
      "platform": "PS3",
      "date": "2013-09-17"
    },
    {
      "platform": "X360",
      "date": "2013-09-17"
    },
    {
      "platform": "PS4",
      "date": "2014-11-18"
    },
    {
      "platform": "XONE",
      "date": "2014-11-18"
    }
    {
      "platform": "PC",
      "date": "2015-04-14"
    }] 
  }]
}
```

This format works for the most part and matches how a user will view the site. An EU user will only want dates relevant to their region.

In the above case, all the dates are identical however and as we move more and more towards digital, this will become the case where there's a lot of duplicated information.