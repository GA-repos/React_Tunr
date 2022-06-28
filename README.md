# Review Create React App and Static Views

## Learning Objectives

- Review Create React App
- Review all the React we learned yesterday by rebuilding a new app

## Let's get started

Let's build a playlist maker called Tunr

[Create React Docs](https://github.com/facebook/create-react-app)

- `npx create-react-app tunr_app`
- `cd tunr_app`
- open a new tab in terminal
- `npm start`
- in the other open tab `code .`

![](https://i.imgur.com/AlBJBso.png)

Let's look at our folders

![](https://i.imgur.com/ovMXd4n.png)

We will be working in the `src` folder. All the code in that folder will get compiled into the react app.

Code outside of the `src` folder will NOT be compiled into the react app. You can put more folders inside the `src` folder for organizational purposes.

The `public` folder is the actual html file that gets loaded into the browser. You can change the details in this file to match your app (app name, different favicon, update the manifest.json)

## Make This App Our Own

Let's remove all the create react app showcase stuff in `src/App.js` and rewrite the component into the same syntax we've been practicing.

We can also get a little fancy and use destructuring to pull out the `Component` object out of React:

![](https://i.imgur.com/ZNF5QX5.png)

Our component, now should look familiar to yesterday. Check your browser - no errors is good.

In Chrome Dev tools Elements tab:

![](https://i.imgur.com/zLIKAkH.png)

We see some extra stuff like `noscript` - that is coming from `public/src/index.html`. You can customize this for your projects but you don't need to do anything for your labs and hw.

Remember, React uses `import` `export` portions of code. This is conceptually the same as `require()` and `module.exports()` we saw in our node apps in the previous units.

## Creating our Static App first

Here is our mockup

![](https://i.imgur.com/mjp850l.png)

- We have an `App` component and inside it we have a
- a header
- form component
- two playlist components
  - playlist components are made up of
    - a table with a header
    - table cells for each song
- a footer

We added a click event that allowed us to click on the h1 and change the h2 below it

- `mkdir src/components`
- `touch src/components/Footer.js`
- `touch src/components/Header.js`
- `touch src/components/Playlist.js`
- `touch src/components/Song.js`

- `touch src/data.js` (we'll add some 'data' a bit later)

- Copy the `copy_this.css` code in instructor notes and paste it in `index.css`

### Build out our components

**Footer.js**

```js

const Footer = ()=> {
	return <footer>Footer</footer>
}

export default Footer;

```

**Header.js**

```js

const Header = ()=> {
	return <header>Header</header>
}

export default Header;

```

##### Add a Form below the header

**App.js**

```js
<form>
  <label htmlFor="title">
    Song
    <input type="text" id="title" />
  </label>
  <label htmlFor="artist">
    Artist
    <input type="text" id="artist" />
  </label>
  <label htmlFor="time">
    Time
    <input type="text" id="time" />
  </label>
  <label>
    <input type="submit" />
  </label>
</form>
```

##### Add a Main tag that will hold one div for playlist info

**App.js**

```js
<main>
  <div>
    <h3>Playlist 1</h3>
    <table>
      <thead>
        <tr>
          <th>Song</th>
          <th>Arist</th>
          <th>Time</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>Song</td>
          <td>Artist</td>
          <td>Time</td>
        </tr>
        <tr>
          <td>Song</td>
          <td>Artist</td>
          <td>Time</td>
        </tr>
        <tr>
          <td>Song</td>
          <td>Artist</td>
          <td>Time</td>
        </tr>
        <tr>
          <td>Song</td>
          <td>Artist</td>
          <td>Time</td>
        </tr>
      </tbody>
    </table>
  </div>
</main>
```

Our app should look like this:

![](https://i.imgur.com/ydz1AnP.png)

Hrrrmmm - this looks like a lot of code in one file... I wonder if we'll learn how to split up our code into smaller components soon...


## Let's add some 'data'

We'll be getting data out of a file and

- `touch src/data.js`
- copy paste the following

```js
const playlist = [
  {
    artist: 'Talking Heads',
    title: 'Once in a Lifetime',
    time: '3:37'
  },
  {
    artist: 'The Clash',
    title: 'Lost in the Supermarket',
    time: '3:44'
  },
  {
    artist: 'Peter Gabriel',
    title: 'Shaking the Tree',
    time: '7:24'
  },
  {
    artist: 'Slowdive',
    title: "Don't Know Why",
    time: '4:42'
  },
  {
    artist: 'Joanna Serrat',
    title: "Keep on Fallin'",
    time: '4:47'
  },
  {
    artist: 'Wolf Parade',
    title: 'Little Golden Age',
    time: '3:44'
  },
  {
    artist: 'Dead Sara',
    title: 'Something Good',
    time: '4:39'
  },
  {
    artist: 'Chaka Khan',
    title: 'Like Sugar',
    time: '4:01'
  },
  {
    artist: 'Alvvays',
    title: 'Lollipop (Ode to Jim)',
    time: '4:39'
  },
  {
    artist: 'Mazzy Star',
    title: 'Flowers in December',
    time: '4:23'
  }
]

export default playlist
```

- add `export default playlist` at the bottom of this file

- in `App.js` add

```js
import playlist from './data.js'
console.table(playlist)
```

Thought question: where will we see this console log?

Thought question: does this app component have state yet? Let's check our dev tools

![](https://i.imgur.com/FUpgqbP.png)

Too add state to our app. We must import the hook useState from react

```js
import { useState } from 'react'
import playlist from './data.js'

const App = () => {
  const [playlist, setPlaylist] = useState(playlist)
  
  return (..... 
  
}
```

check your browser's React dev tools console to see the 'data' in state

![](https://i.imgur.com/wAxMORz.png)

Looking at our mockup we want to put this data in our table. Remove all but one `tr` in the `tbody`

Let's loop through our playlist and add rows for each song

```js
<tbody>
  {playlist.map(song => {
    return (
      <tr>
        <td>Song</td>
        <td>Artist</td>
        <td>Time</td>
      </tr>
    )
  })}
</tbody>
```

Uh-oh we get an error:

![](https://i.imgur.com/RjCFPbe.png)

Create React App is going to keep giving us errors and warnings to be sure we're following best practices. Let's do what it says this time and add a (not really reliable) unique key. Since this is fake data from an array we can just use the array index position for now - when you use data you could use the `id`. This isn't a foolproof way to add a unique key because index positions can change. Again, once we start using real data we can use the `id`. It is ok to not fix this since it is a warning. You can keep building the app.

Let's fix the warning and update our data to now show the actual song info

```js
<tbody>
  { playlists.songs.map((song, index) => {
    return (
      <tr key={index}>
        <td>{song.title}</td>
        <td>{song.artist}</td>
        <td>{song.time}</td>
      </tr>
    )
  })}
</tbody>
```


Let's add our inputs to state 

```js
const [formData,setFormData] = useState()
```

Let's add value to all three input fields

```js
<form>
  <label htmlFor="song">
    Song
    <input type="text" id="song" value={this.state.title} />
  </label>
  <label htmlFor="artist">
    Artist
    <input type="text" id="artist" value={this.state.artist} />
  </label>
  <label htmlFor="time">
    Time
    <input type="text" id="time" value={this.state.time} />
  </label>
```

Now when we type in the input fields, they won't change.

Let's handle the input

```js
const handleChange =  (event) => {
  setFormData({...formData, [event.target.id]: event.target.value })
}
```

Add the event listener

```js
<label htmlFor="song">
  Song
  <input
    type="text"
    id="song"
    value={ formData.title }
    onChange={ handleChange}
  />
</label>
<label htmlFor="artist">
  Artist
  <input
    type="text"
    id="artist"
    value={ formData.artist }
    onChange={ handleChang}
  />
</label>
<label htmlFor="time">
  Time
  <input
    type="text"
    id="time"
    value={ formData.time}
    onChange={ handleChange }
  />
</label>
```

### Get Submit functionality Working

Write our submit function, remember, submit's default behavior is to refresh the page. Let's be sure to prevent that default.

We should not ever mutate state directly. We must update state with `setPlayList()`

First, we're going to create a new object with our state we collected from our inputs.

Then we are going to make a new array, using the destructuring spread operator so that we don't alter state outside of `setPlayList`.

Finally, inside of setState, we'll update our songs array to our new array

```js
const handleSubmit = (event) =>{
  event.preventDefault()
  const newSong = {
    title: formData.title,
    artist: formData.artist,
    time: formData.time
  }

  const updatedSongs = [ ...playlist, newSong ]
  
  setPlayList(updatedSongs)

  //It would be nice to clear the fields. We can do this by updating state a bit more

  setFormData({
    name: '',
    artist: '',
    time: '0:00'
  })
}
```

Bonus:
Can you figure out how you would delete a song?

Your final `App.js` should look something like this:

```js
import { useState } from 'react'
import Footer from './components/Footer'
import Header from './components/Header'
import playlists from './data.js'

const App = () => {
  const [playlist, setPlayList] = useState(playlists)
  const [formData, setFormData] = useState({
    title: '',
    artist: '',
    time: '0:00'
  })


  const handleChange = (event) => {
    setFormData({ ...formData, [event.target.id]: event.target.value })
  }

  const handleSubmit = (event) => {
    event.preventDefault()
    const newSong = {
      title: formData.title,
      artist: formData.artist,
      time: formData.time
    }

    const updatedSongs = [...playlist, newSong]

    setPlayList(updatedSongs)

    //It would be nice to clear the fields. We can do this by updating state a bit more

    setFormData({
      title: '',
      artist: '',
      time: '0:00'
    })
  }

  return (
    <div>
      <Header />
      <form onSubmit={handleSubmit}>
        <label htmlFor="song">
          Song
          <input
            type="text"
            id="title"
            value={formData.title}
            onChange={handleChange}
          />
        </label>
        <label htmlFor="artist">
          Artist
          <input
            type="text"
            id="artist"
            value={formData.artist}
            onChange={handleChange}
          />
        </label>
        <label htmlFor="time">
          Time
          <input
            type="text"
            id="time"
            value={formData.time}
            onChange={handleChange}
          />
        </label>
        <label>
          <input type="submit" />
        </label>
      </form>
      <main>
        <div>
          <h3>Playlist 1</h3>
          <table>
            <thead>
              <tr>
                <th>Song</th>
                <th>Arist</th>
                <th>Time</th>
              </tr>
            </thead>
            <tbody>
              {playlist.map((song, index) => {
                return (
                  <tr key={index}>
                    <td>{song.title}</td>
                    <td>{song.artist}</td>
                    <td>{song.time}</td>
                  </tr>
                )
              })}
            </tbody>
          </table>
        </div>
      </main>
      <Footer />
    </div>
  )

}

export default App
```


# Intro to React Props

## Learning Objectives

- Learn about props
- Learn how to pass props
- Learn difference between props and state
- Be able to create a component with no state and no props (Header, Footer)
- Be able to create a component with only state (App)
- Be able to create a component with only props (Playlist)
- Be able to create a component with props and state (Song)

## Props

Props is short for properties. We know that a component can have state (a view based on data). If we think back to our React Store, we had just one component. It was a pretty small app, so one component was fine. But as we would continue to build out functionality, our one component would get very complex and the code could expand to hundreds or thousands of lines. Maintaining such a large component would be really hard.

## Data flows down

- In React data only flows down
- You can pass data from a top component down to its children.
- The way you pass them is that you create a custom property and then you can access this data through props in the child component
- the properties that are passed down can be strings, numbers, booleans, arrays, objects, functions etc.

![](UnidirectionalDataFlow.png)

Let's continue to build our app by making a new component Playlist and moving our code into it. Then we'll learn how to pass our playlist data down from the `App` component into the Playlist component.

## Add a New Component

if you haven't already:

- make sure you are on the same level as `package.json`
- `mkdir src/components`
- `touch src/components/PlayList.js`

**src/components/PlayList.js**

```js
import React from 'react'

const PlayList = () => {
    return <h3> All the Songs</h3>
}

export default PlayList
```

## Import and render it in our `App.js`

```js
import PlayList from './components/PlayList.js'
```

Between our form and main tags:

![](https://i.imgur.com/uhWpLPz.png)

Let's **MOVE** our song list to our new component (the main tag and everything inside)

From **App.js**

```js
 <main>
        <div>
          <h3>Playlist 1</h3>
          <table>
            <thead>
              <tr>
                <th>Song</th>
                <th>Arist</th>
                <th>Time</th>
              </tr>
            </thead>
            <tbody>
              {playlist.map((song, index) => {
                return (
                  <tr key={index}>
                    <td>{song.title}</td>
                    <td>{song.artist}</td>
                    <td>{song.time}</td>
                  </tr>
                )
              })}
            </tbody>
          </table>
        </div>
      </main>
```

To **src/components/PlayList**

Right now, we should be getting an error that says `TypeError: Cannot read property 'playlist' of null`. Why is that? Remember, we're referring to `state` but there is no state in this component. Instead, we should be getting that information from our parent component, which in this case is our `<App />`. When we are in a child component (`Playlist`) we access information from the parent using `props`. Because of this we would access our songs in our `<Playlist>` component using `props.playlists.songs`. Update your component so that it looks so:

```js

const PlayList = ({playlist}) => { 
  ....

  <tbody>
    { playlist.map((song, index) => {
      return (
        <tr key={index}>
          <td>{song.title}</td>
          <td>{song.artist}</td>
          <td>{song.time}</td>
        </tr>
      )
    })}
  </tbody>

  ...
```

Now we are getting a new error `TypeError: Cannot read property 'songs' of undefined`. This means that we are trying to access playlists in our props, but we don't have a playlists key in our `this.props` object. Why? Because we never passed it down from the parent!

Modify our `<Playlist />` in our `<App />` so that we pass down a value. It should look like below:

**App component**

```js
</form>
<Playlist playlist={playlist} />
<Footer />
```

Now we can access the data we're passing down in our `PlayList` component

## A Component that Has Props and State

First let's practice making a new component

- `touch src/components/Song.js`

```js
import React, { Component } from 'react'

const Song = () => {
    return 'Song'
  
}
export default Song
```

Import this component into the `PlayList`

**Playlist.js**

```
import Song from './Song.js'
```

Let's move our `tr`s into this new component

**Song.js**

```js

const Song = () => {
    return (
      <tr key={index}>
        <td>{song.title}</td>
        <td>{song.artist}</td>
        <td>{song.time}</td>
      </tr>
    )
  
}
export default Song
```

Update our **PlayList.js** so that we are passing properties down to our Song components.

```js
import Song from './Song.js'

const Playlist = ({playlists}) => {
    return (
      <ul>
        { playlists.songs.map((song, index) => {
          return <Song song={song} key={index} />
        })}
      </ul>
    )
  }
}
export default PlayList
```

Update our Song component (we can remove the key property from the `tr` too) so we are rendering our view based on the component's properties.

```js
const Song = ({song}) => {
    return (
      <tr key={index}>
        <td>{song.title}</td>
        <td>{song.artist}</td>
        <td>{song.time}</td>
      </tr>
    )
  
}
export default Song
```

Let's say we want a user to be able to love a song by clicking on a song. If the song is liked, a heart will appear.

Remember, if we want a component to have state we must add the constructor function

Donst forget to import the useState hook

```js
import { useState } from 'react'

const Song = ({song}) => {
  const [love, setLove] = useState(false)

    return (
      <tr key={this.props.index}>
        <td>{this.props.song.title}</td>
        <td>{this.props.song.artist}</td>
        <td>{this.props.song.time}</td>
      </tr>
    )
  
}
```

Now we can conditionally render a heart whether or not an song is loved

```js
return (
  <tr key={index} onClick={toggleLove}>
    <td>{song.title}</td>
    <td>{song.artist}</td>
    <td>{song.time}</td>
    {love ? <td>&hearts;</td> : <td></td>}
  </tr>
)
```

Let's add a function to allow us to toggle the value

```js
let toggleLove = () => {
  setLove(!love)
}
```

Finally, let's add an `onClick` that will allow us to toggle the value of `love` for each song - let's put it on the whole row so our user can click anywhere on the row

```js
<tr onClick={toggleLove}>
```

Now, we should be able to click on the item and toggle whether or not we see the message that the item is in the shopping cart.

## Extra Challenges

- double click the song name to delete it from the list
- add functionality that lets you click on an icon (arrow?) of two songs and then swaps their order
- Allow for multiple playlists to be rendered, when adding a new song, let a user select a playlist to add to or to create a new playlist
- make form into its own component
- Add some sweet sweet css style!
