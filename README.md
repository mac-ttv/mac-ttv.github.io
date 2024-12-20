# OVERLAYS WOO

## Github Initial setup
* Create an account on https://github.com (it's free)
* Create a repository in github using your username in the name of the repository: username.github.io
Github lets their users host a project as long as the name follows that convention, which lets us host files there. https://mac-ttv.github.io is my base url, and yours should be the same but with your username. The image below is both an example and hosted on that repository [here](https://github.com/mac-ttv/mac-ttv.github.io/blob/main/images/Capture.PNG).
![example](https://mac-ttv.github.io/images/Capture.PNG)
* Click on Add File, then Create New File, and on the next page your cursor will be in a text box for the file's name and path (path references the folders it's in)  ![example](https://mac-ttv.github.io/newfolder/addfile.PNG). 
* I recommend entering a name for a new folder followed by / which will create a new folder, then enter a filename like ReadMe.md and put some text in the file like ![example](https://mac-ttv.github.io/newfolder/im43.PNG)
* Then you will **commit** the file which is essentially just saving the entire project after any changes. You won't have to know anything about how it works aside from just understanding that it saves the entire project and any changes to it. ![commits](https://mac-ttv.github.io/newfolder/commit.PNG)
* Now you have a folder to hold the image assets and the css file we'll be creating. We'll eventually be adding files to this folder using github's file upload: ![upload](https://mac-ttv.github.io/newfolder/upload1.png) ![dragndrop](https://mac-ttv.github.io/newfolder/dragndrop.png)

## Controller assets setup
* We'll be *borrowing* assets from https://gamepadviewer.com/, which will also be hosting a lot of the functionality for us. Navigate to https://gamepadviewer.com/ and select the controller you want to use as the base controller (black xbox 1, white ps4, etc) and press buttons on your controller to link - note PS5 controllers are more unique but this link should work https://gamepadviewer.com/?p=1&s=5 (once ready to use, add &editcss=your_css_url to this link).
* We'll be borrowing both the images for the controller and the css used as well.
  * Images: 
    * Firefox: Press Alt to show the top menu (File, Edit, etc), click Page Info, and then the media tab. Here you can select all the images and save: ![firefox](https://mac-ttv.github.io/newfolder/firefoxmedia.PNG)
    * Chrome: Right click anywhere on the image and click "Inspect", or press F12 to bring up Chrome DevTools. Then find the Sources tab at the top, and download all of the assets appropriate to your controller (there will be only one, in this example xbox) and we can also download the css file here called "style.css": ![Chrome](https://mac-ttv.github.io/newfolder/chromesources.PNG)
  * CSS:
    * Firefox: Right click anywhere on the image and "Inspect", then select the "{} Style Editor" tab at the top. Scroll down until you see style.css, and save it. ![example](https://mac-ttv.github.io/newfolder/firefoxcss.PNG)
* We'll want to use an image editor to customize our controller and a text editor to work with the css (tho notepad will work if you prefer). For image editing, I recommend [GIMP](https://www.gimp.org/downloads/) and for a text editor I recommend [VSCode](https://code.visualstudio.com/).

### Customizing the image
* This will be brief because I'm certainly not an expert in image editing. First, convert any .svg files to .png by opening them in gimp, then File > Export As > filename.png.  Please use the original filename for naming consistency (easier for future you). You can close the original, and please note that "saving" in gimp will save a gimp project, not an image file :roll_eyes:
* Once you have the png files you can start to open them up and play with them. Every button has 2 images, off and on, but note the bumper and trigger images are a little unique as they only include the 'on' version. The off version is on the controller base image itself. Gamepad Viewer's code will handle the rotation of the joysticks so we just really need to add whatever color we want and then upload all of the images to our github repository.

### Customizing the css
* If you already opened the file and noticed the 4,000+ lines, sorry for the scare but we'll only be using a small portion of it. There are sections wrapped in comments that designate which controller it's being used for, you want to scroll through to find the controller you want, then copy the css and paste it into a new file. If you plan on using multiple controllers or making overlays for multiple controllers, might be a good idea to separate a few of them while we're here. Example:

```css
.xbox-old.half {
    margin-top: -272px;
}

/*END Xbox 360 Controller Styling*/

/*BEGIN Xbox One Controller Styling*/   <----------------------------------------------------------- look for this
.controller.xbox {
    background: url(xbox-assets/base.svg);
    height: 630px;
    width: 750px;
    /*    margin-left: -375px;
        margin-top: -285px;*/
}

.xbox.white {
    background: url(xbox-assets/base-white.svg);  /* <-------------------------- this references an image */
}

.xbox.disconnected {
    background: url(xbox-assets/disconnected.svg); /* <------------------------- this references an image */
}

.xbox.disconnected div {
    display: none;
} ```

* CSS references the image files through what's called a "relative path", which simply means that it's looking for the images starting from where this css file is located in the file structure. I uploaded this css file to the same level as the images in this example, so you can delete the `xbox-assets/` from the `background: url(base-custom.png)`. Also note I changed the file extension to .png instead of .svg. If you prefer, you can add a folder where the css file is located to host imasges and keep the file types more organized. Quick example of that: 
![folderpath](https://mac-ttv.github.io/newfolder/optional/folderpath.png)
![optionalfolder](https://mac-ttv.github.io/newfolder/optional/optionalfolder.png)

In these images you can see the css file in the /newfolder folder, so our reference to this file will be to first include our repository's name as the url: https://mac-ttv.github.io/newfolder/xb1.css . What the *relative path* does is simply assume the files will be in the same folder or further down the folder structure, saves having to type it all out. Here's the difference in css between a separate folder for images or keeping them in the same folder as the css:

```css 
/* everything on same level */
.xbox.white {
    background: url(base-white.png);
}

/* separate folder alongside the css file, which holds the images */
.xbox.white {
    background: url(optional/base-white.png);
}
```

You will want to go through your css file and change every url for every asset you are using, so they all pull from your images, not the default on gamepadviewer.

## Putting everything together
* Once you have all of your images edited and uploaded, and the css refencing the images correctly, you'll want to copy the path to your css file. Open the css file and you can copy the path by clicking the copy button (don't) or highlighting it all (do). The difference is a relative vs absolute path: `newfolder/xb1.css` with the button and `mac-ttv.github.io/newfolder/xb1.css` by highlighting it: ![copy](https://mac-ttv.github.io/newfolder/copypath.PNG). Then just add https:// for the full path to your css file: https://mac-ttv.github.io/newfolder/xb1.css
* Go back to https://gamepadviewer.com/ and select player 1 and your base controller again, then open the menu on the left and Generate URL: ![gpviewerurl](https://mac-ttv.github.io/newfolder/gamepadviewer.PNG)

That will generate a url like this: https://gamepadviewer.com/?p=1&editcss=https%3A%2F%2Fmac-ttv.github.io%2Fnewfolder%2Fxb1.css which you can copy/paste into a new tab to test.

### Troubleshooting
* Errors are practically guaranteed because it's a long process and you're bored, everyone will get them. Error messages are our friend
* If you're having issues with images / assets loading, right click anywhere on the page and inspect, then open the console: ![console](https://mac-ttv.github.io/newfolder/errorexample.PNG)
  I included 2 errors on this project... *totally intentionally..* so we could practice together of course. The first error is for our disconnected file - it's referencing a .svg but our project has the image in a .png. We simply forgot to edit the css file properly, changing that line in the css file to a .png should fix it. 
  The 2nd error is for the dpad.png which we labeled correctly in the css file, but forgot to upload. Uploading the file to the same folder as our css fixes that issue.
* Those are the main errors you should get, anything beyond that... google is your friend. If I'm your friend feel free to dm me :sweat_smile:
