# Electron-Builder-DMG-Tutorial (MacOS)
A step by step tutorial on builder DMG installers for ElectronJS applications using Electron Builder.

Files required to make DMG installer
- App icon [.icns]
- DMG installer background image [.tiff]


### Step 1: Generating Application Icon (.icns) File

| Example: App Icon |
|---|
|<p align = "center"> <img src = "Example Images/App_Icon.png" width = "100px"> <br> <b> 1024px by 1024px </b> </p> |

Create a PNG image of size 1024px by 1024px. <br>
Open a new terminal window and cd into the directory where the PNG image is saved. <br>
Rename the PNG image to ```App_Icon.png``` then copy/paste the commands below into the terminal window and run.

```
mkdir MacOS_Icon.iconset
sips -z 16 16     App_Icon.png --out MacOS_Icon.iconset/icon_16x16.png
sips -z 32 32     App_Icon.png --out MacOS_Icon.iconset/icon_16x16@2x.png
sips -z 32 32     App_Icon.png --out MacOS_Icon.iconset/icon_32x32.png
sips -z 64 64     App_Icon.png --out MacOS_Icon.iconset/icon_32x32@2x.png
sips -z 128 128   App_Icon.png --out MacOS_Icon.iconset/icon_128x128.png
sips -z 256 256   App_Icon.png --out MacOS_Icon.iconset/icon_128x128@2x.png
sips -z 256 256   App_Icon.png --out MacOS_Icon.iconset/icon_256x256.png
sips -z 512 512   App_Icon.png --out MacOS_Icon.iconset/icon_256x256@2x.png
sips -z 512 512   App_Icon.png --out MacOS_Icon.iconset/icon_512x512.png
cp App_Icon.png MacOS_Icon.iconset/icon_512x512@2x.png
iconutil -c icns MacOS_Icon.iconset
rm -R MacOS_Icon.iconset
```

### Step 2: Generating DMG Installer Background Image (.tiff) File

| Example: DMG_Background.png | Example: DMG_Background_Large.png |
|---|---|
|<p align = "center"> <img src = "Example Images/DMG_Background.png" width = "400px"> <br> <b> 544px by 408px </b> </p> |<p align = "center"> <img src = "Example Images/DMG_Background_Large.png" width = "400px"> <br> <b> 1088px by 816px </b> </p>|




Create another PNG image of abitrary size, for this demo a size of 1088px by 634px will be used. <br>
Copy the PNG image and then open in preview. <br>
Resize the image to be 50% smaller by going to ```Tools > Adjust Size``` in Preview's menu bar as shown below. <br>
Rename the images ```DMG_Background.png``` and ```DMG_Background_Large.png```.<br>
Open a new terminal window and cd into the directory where the PNG image is saved. <br>
Copy/paste the commands below into the terminal window and run.

```
tiffutil -cathidpicheck "DMG_Background.png" "DMG_Background_Large.png" -out DMG_Background.tiff
```
### Step 3: Creating an Assets Folder
Create a folder named ```assets``` in your project directory where the ```package.json``` file resides <br>
Copy the generated files ```MacOS_Icon.icns``` and ```DMG_Background.tiff``` to the ```assets``` folder.


### Step 4: Configuring "package.json" File


```
{
  "name": "connect-four",
  "productName": "Simple Connect4",
  "version": "1.0.1",
  "description": "Minimalist Connect4 game",
  "main": "App.js",
  "author": "MichaelTr7",
  "license": "MIT",
  "homepage": "Simple_Connect4.com",
  "build": {
    "appId": "com.simpleconnect4.app",
    "icon": "assets/MacOS_Icon.icns",
    "directories": {
      "output": "build"
    },
    "productName": "Simple Connect4",
    "mac": {
      "target": ["dmg"],
      "identity": null,
      "category": "public.app-category.board-games"
    },
    "dmg": {
      "background": "assets/DMG_Background.tiff",
      "icon": "assets/MacOS_Icon.icns",
      "iconSize": 75,
      "window": {
        "width": 544,
        "height": 408
      },

      "contents": [
        {
          "x": 450,
          "y": 280
        },
        {
          "x": 450,
          "y": 170,
          "type": "link",
          "path": "/Applications"
        }
      ]
    }
  },
  "scripts": {
    "start": "electron .",
    "pack": "electron-builder --dir",
    "dist": "electron-builder",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "dependencies": {},
  "devDependencies": {
    "electron": "^9.2.0",
    "electron-builder": "^22.8.0"
  }
}

```








