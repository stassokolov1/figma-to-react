# Figma to React Converter

This demonstrates using the Figma REST API to convert a Figma document to React Components.
Disclaimer: this code is likely incomplete, and may have bugs. It is not intended to be used
in production. This is simply a proof of concept to show what possibilities exist.

## API Usage

We use 2 endpoints in this project:

- `GET /v1/files/:file_key` - Get the JSON tree from a file. This is the main workhorse of this project and lays the skeleton of the React Components.
- `GET /v1/images/:file_key` - When we identify nodes that are vectors or other nodes that can't directly be represented by `div`s, we have to render them as svgs.

## Set up

1. Install [Node](https://nodejs.org/). You'll need a recent version that supports `async / await`
2. In this directory, run `npm install`
3. Run the converter per instructions below

## Usage

By default this project comes with a prerendered component in `src/figmaComponents.js`. You can see a page that uses this component if you
run `npm start`. This will start a React server and a webpage will open to the root page. This webpage will automatically refresh as
you make changes to the source documents. To follow along with the example component, the source Figma file is located [here](https://www.figma.com/file/VGULlnz44R0Ooe4FZKDxlhh4/Untitled).

When we run the converter, we will convert any *top level frames* in the document to React Components *as long as their name starts with `#`*.
In the example document you can see that we have one top level frame named `#Clock`. The component resulting from this will be exported in
`src/figmaComponents.js` as `MasterClock`, a `React.PureComponent`.

In addition, *any* node with a name starting with a `#` will have a code stub generated for it in `src/components`. These code stubs can be
modified to affect the rendering of those components as well as modifying variables within the component (see variables section below).

To run the converter on a file, you will need a personal access token from Figma. Refer to the [Figma API documentation](https://www.figma.com/developers/docs)
for more information on how to obtain a token. The other piece of information you will need is the file key of the file you wish to convert,
which is located in the file's URL (for example, this is `VGULlnz44R0Ooe4FZKDxlhh4` for the example file). So, an example conversion would look
like:

```
node main.js VGULlnz44R0Ooe4FZKDxlhh4 <API_TOKEN_HERE>
```

where `<API_TOKEN_HERE>` would be repaced with your developer token.

You can also change the .env file and insert your token there

```
//.env  
DEV_TOKEN=<YOUR_TOKEN>
```
then you only need to pass the project id
```
node main.js VGULlnz44R0Ooe4FZKDxlhh4
```



*IMPORTANT*: The index.css file is required to be included for components to render completely.
