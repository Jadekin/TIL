# Loading Images Dynamically 

You cannot load image paths dynamically on React Native. Unlike web development, where you can dynamically load images by specifying a URL, React Native requires images to be bundled and packaged with the app during the build process. Metro is a JavaScript bundler that is responsible for transforming and bundling the source code and assets of a React Native app.

During the development process, Metro scans your code for asset references and includes those assets in the bundle that is served to the app. And It needs to know about the assets during the build process.

``` typescript
// IconText.tsx
interface IconTextProps {
  iconName: string;
  title: string;
}

const IconText = (props: IconTextProps) => {
  const { container, icon, title } = styles;
  return (
    <View style={container}>
      <Image
        style={icon}
        source={require(`../assets/Icons/${iconName}`)}  // <==== Wrong
      />
      <Text style={title}>{props.title}</Text>
    </View>
  );
};

```

The above will return an error. Instead, one alternative is to create a file to export the images, referencing them using the ``require()`` statement,

``` typescript

// index.ts [Added on the Icons folder]

const sunrise = require('./sunrise.png');
const sunset = require('./sunset.png');
const group = require('./group.png');
const weather = require('./cloudy.png');
const city = require('./cityscape.png');
const upcomingWeather = require('./next-week.png');

export { sunrise, sunset, group, weather, city, upcomingWeather };

```

And then, based on the logic within your app, pass the dynamically determined image source as a prop to the component:

``` typescript
// IconText.tsx 
interface IconTextProps {
  icon: any;
  title: string;
}

const IconText = (props: IconTextProps) => {
  const { container, icon, title } = styles;
  return (
    <View style={container}>
      <Image
        style={icon}
        source={props.icon}
      />
      <Text style={title}>{props.title}</Text>
    </View>
  );
};
```