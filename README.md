Hola amigos de la #nerdytud

Cuando utilizamos frameworks o librerías de javascript como ser React, Angular, Vue, etc. realmente podemos moldear el DOM de una manera muy flexible.

Hoy les comparto un ejemplo realizado en react para escuchar radios online.

Crear aplicación
```bash
npx create-react-app radioplayer
```

Instalar dependencias
```bash
npm install @material-ui/core

npm install @material-ui/icons

npm i react-player
```

Código (App.js)
```javascript
import { useState } from 'react';
import ReactPlayer from 'react-player'
import { makeStyles } from '@material-ui/core/styles';
import { IconButton, Slider, Grid } from '@material-ui/core';
import PlayArrowIcon from '@material-ui/icons/PlayArrow';
import StopIcon from '@material-ui/icons/Stop';
import VolumeDownIcon from '@material-ui/icons/VolumeDown';
import VolumeUpIcon from '@material-ui/icons/VolumeUp';
import VolumeOffIcon from '@material-ui/icons/VolumeOff';

const useStyles = makeStyles({
  root: {
    width: 200,
  },
});

function App() {
  const classes = useStyles();

  const url = 'https://s6.stweb.tv/radio10/live/playlist.m3u8';

  const [radio, setRadio] = useState({ play: false, volume: 0.5, mute: false });

  const handlePlay = () => {
    setRadio({ ...radio, play: !radio.play });
  }

  const handleVolume = (event, newValue) => {
    setRadio({ ...radio, volume: newValue });
  };

  const handleMute = () => {
    setRadio({ ...radio, mute: !radio.mute });
  }

  return (
    <div className={classes.root}>
      {radio.play ?
        <>
          <IconButton color="secondary" onClick={handlePlay}>
            <StopIcon />
          </IconButton>

          <IconButton color="primary" onClick={handleMute}>
            {radio.mute ? <VolumeUpIcon /> : <VolumeOffIcon />}
          </IconButton>
        </>
        :
        <IconButton color="primary" onClick={handlePlay}>
          <PlayArrowIcon />
        </IconButton>
      }

      <Grid container spacing={2}>
        <Grid item>
          <VolumeDownIcon />
        </Grid>
        <Grid item xs>
          <Slider
            value={radio.volume}
            onChange={handleVolume}
            step={0.1}
            min={0}
            max={1} />
        </Grid>
        <Grid item>
          <VolumeUpIcon />
        </Grid>
      </Grid>

      <ReactPlayer
        url={url}
        playing={radio.play}
        volume={radio.volume}
        muted={radio.mute}
      />
    </div>
  );
}

export default App;
```

Comprobar funcionamiento
```bash
npm start
```
[localhost](http://localhost:3000)